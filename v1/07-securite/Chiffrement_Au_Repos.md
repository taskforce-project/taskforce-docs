---
id: chiffrement-au-repos
title: Chiffrement au repos des données sensibles
doc_type: reference
statut: active
version: 1.0
date: "24/07/2026"
auteur: Pierre MICHEL
tags: [securite, chiffrement, rgpd, c24, c11, aes, memoire, rncp]
---

# Chiffrement au repos

> **Répond à C24** (« les données sensibles sont chiffrées ») et à **C11.2** (RGPD). Ce document dit
> **exactement** ce qui est chiffré, ce qui ne l'est pas, et pourquoi. La formulation compte : annoncer
> « toutes les données personnelles sont chiffrées » serait faux et vérifiable en une requête SQL.

## 1. La phrase juste

> **Les secrets sont chiffrés en base. Les identifiants qui servent de clés de recherche ne le sont
> pas : ils sont protégés par le contrôle d'accès applicatif et par le chiffrement disque de l'hôte.**

C'est la formulation à employer dans le dossier et à l'oral. Elle est défendable parce qu'elle est
vraie, et elle survit à un jury qui ouvre la base.

## 2. Ce qui est chiffré

**Quatre colonnes**, toutes via `@Convert(converter = EncryptedStringConverter.class)`.

| Table | Colonne | Contenu | Pourquoi |
|---|---|---|---|
| `connector_connections` | `config` | JSON des identifiants de connexion à un outil tiers | Secrets d'accès à des systèmes externes |
| `integrations` | `access_token` | Jeton OAuth GitHub / Slack | Un jeton volé donne accès au compte tiers |
| `enterprise_inquiries` | `message` | Texte libre écrit par un prospect | Donnée personnelle non structurée |
| `enterprise_inquiries` | `notes` | Notes internes de l'équipe commerciale | Appréciations sur des personnes identifiées |

**Algorithme** : AES-256-GCM. La clé est dérivée par SHA-256 de la valeur configurée — c'est donc une
**phrase secrète**, pas une clé base64 (un point que la documentation d'exemple annonçait à tort).

**Format en base** : `enc:base64(IV(12 octets) || chiffré+tag)`. Le vecteur d'initialisation est tiré
aléatoirement à chaque écriture : deux chiffrements du même clair produisent des sorties différentes,
ce qui interdit toute corrélation par comparaison de colonnes.

## 3. Ce qui n'est PAS chiffré, et pourquoi

### 3.1 Les identifiants servant de clés de recherche

`users.email`, `users.keycloak_id` — non chiffrés, **délibérément**.

GCM est non déterministe : la même adresse chiffrée deux fois donne deux valeurs différentes. Un
`WHERE email = ?` ne peut donc plus fonctionner. Chiffrer ces colonnes exigerait soit un chiffrement
déterministe (qui réintroduit la corrélation qu'on cherchait à éviter), soit un *blind index* — une
colonne de hachage dédiée, avec sa propre gestion de sel et de rotation.

**Le compromis est assumé** : la complexité ajoutée dépasserait le gain, l'adresse de courriel étant de
toute façon connue de l'infrastructure de messagerie.

### 3.2 Les codes OTP

`otp_verifications.otp_code` est stocké **en clair**, non haché. Trois propriétés limitent la portée :

- **durée de vie de 15 minutes** (`OtpService.OTP_EXPIRY_MINUTES`) ;
- **5 tentatives maximum**, au-delà desquelles le code passe en `EXPIRED` ;
- **usage unique** — `canBeValidated()` exige l'état `PENDING`, donc un code consommé ne se rejoue pas.

Un attaquant capable de lire cette table a déjà un accès en base, c'est-à-dire un niveau de compromission
où le code OTP n'est pas le maillon faible. Hacher le code resterait néanmoins une amélioration bon
marché, et figure à ce titre dans les pistes du §6.

### 3.3 ⚠️ Une incohérence à connaître

`otp_verifications` porte aussi `phone_number`, `company_name` et `enterprise_message` **en clair** —
alors que le **même message** est chiffré dans `enterprise_inquiries.message`.

Ces colonnes servent de zone de transit : elles portent les informations saisies pendant l'inscription
Enterprise, avant que le compte n'existe. La donnée finit chiffrée dans sa table de destination, mais
transite en clair. La purge de rétention limite l'exposition dans le temps, elle ne la supprime pas.

C'est une **incohérence réelle**, énoncée ici plutôt que découverte par le jury. Correction possible :
appliquer le même convertisseur à ces trois colonnes, sans aucune contrainte technique puisqu'aucune
n'est utilisée comme clé de recherche.

## 4. ⚠️ Le défaut trouvé et corrigé le 24/07/2026

**En production, le chiffrement au repos aurait été silencieusement inactif.** Trois maillons cassés,
indépendants, chacun suffisant à provoquer la panne :

| Maillon | État avant | Conséquence |
|---|---|---|
| `application-prod.yml` | Ne déclarait **pas** `security.encryption-key` | La valeur par défaut de `@Value` étant vide, le convertisseur devenait un passe-plat |
| `docker-compose.prod.yml` | Transmettait `ENCRYPTION_KEY` | L'application lit `TF_ENCRYPTION_KEY` : **la variable n'était lue par personne** |
| `.env.prod.example` | Proposait `ENCRYPTION_KEY=` | Un opérateur remplissant scrupuleusement le fichier n'aurait **toujours** pas de chiffrement |

Résultat : jetons OAuth et identifiants de connecteurs écrits **en clair**, sans erreur, sans
avertissement, sans ligne de journal.

**Ce qui rend ce défaut instructif** : le convertisseur était **correctement testé**. Dix tests
couvrent le round-trip, l'aléa du vecteur d'initialisation, la lecture tolérante — **dont un test qui
vérifie explicitement que l'absence de clé produit un passe-plat**. Ce comportement de repli était donc
documenté, testé, et considéré comme correct. Ce que personne n'avait vérifié, c'est que la
configuration de production menait **systématiquement** dans cette branche. Une suite verte prouve que
le code fait ce qu'on lui demande, jamais qu'on lui demande la bonne chose.

**Les corrections apportées :**

1. `application-prod.yml` déclare `security.encryption-key: ${TF_ENCRYPTION_KEY}`.
2. `docker-compose.prod.yml` et `.env.prod.example` transmettent désormais `TF_ENCRYPTION_KEY`.
3. **`EncryptionKeyHolder` refuse le démarrage** quand le profil `prod` est actif et que la clé est
   vide, et **journalise son état** dans tous les cas — `INFO` actif, `WARN` inactif. L'état cesse
   d'être invisible.

> ⚠️ **Pourquoi une garde en Java plutôt qu'un simple placeholder sans valeur par défaut.** La
> première version du correctif s'appuyait sur `${TF_ENCRYPTION_KEY}` sans repli, en pariant que
> Spring refuserait de démarrer. **Ce raisonnement est faux** : Spring n'échoue que si la propriété
> est **absente**, jamais si elle est **vide**. Or Docker Compose transmet `TF_ENCRYPTION_KEY: ""`
> dès que la variable existe sans valeur — c'est-à-dire exactement ce que produit un `.env.prod`
> recopié depuis l'exemple et rempli à moitié, le scénario le plus probable. Le placeholder se serait
> résolu sans erreur et le chiffrement serait retombé en silence sur le passe-plat, **reproduisant
> le défaut que le correctif prétendait éliminer**.
>
> Vérifié en rendant la configuration : `docker compose config` produit bien `TF_ENCRYPTION_KEY: ""`.
> La seule garde fiable teste **la valeur**, pas sa présence. Elle est figée par
> `EncryptedStringConverterTest` — trois cas (`null`, `""`, `"   "`) sous profil `prod`.

## 5. Les autres couches

Le chiffrement applicatif n'est qu'une couche. Le dispositif complet :

| Couche | Mécanisme | État |
|---|---|:--:|
| Transport | TLS 1.3, terminaison nginx | ✅ configuré |
| Colonnes sensibles | AES-256-GCM applicatif | ✅ 4 colonnes |
| Mots de passe | Jamais stockés — délégués à Keycloak (bcrypt) | ✅ |
| Disque de l'hôte | Chiffrement au niveau du volume | ⚠️ **dépend de l'hébergeur, non tranché** |
| Sauvegardes | Dumps `backup.ps1` | ⚠️ **non chiffrés** — voir §6 |

> Le chiffrement disque relève du fournisseur d'hébergement, question encore ouverte
> ([[Strategie_Hebergement]]). C'est lui qui couvre `users.email` et les codes OTP, d'où l'importance
> de ne pas le présenter comme acquis.

## 6. Pistes non retenues à ce stade

Aucune n'est requise par une compétence, toutes sont défendables à l'oral comme axes d'amélioration :

1. **Chiffrer les trois colonnes de transit** d'`otp_verifications` — la plus simple, elle supprime
   l'incohérence du §3.3.
2. **Hacher les codes OTP** plutôt que les stocker en clair.
3. **Chiffrer les dumps de sauvegarde**, aujourd'hui produits en clair par `backup.ps1`.
4. **Blind index sur `users.email`**, pour chiffrer l'adresse sans perdre la recherche — de loin le
   plus coûteux, et le moins rentable des quatre.

> 🔗 Voir aussi : [[Auth_Autorisation]] · [[Registre_Traitements_RGPD]] · [[Audit_RGPD_Conformite]] ·
> [[PSSI]] · [[Diagramme_Etats_UML]] §7 (cycle de vie du code OTP).
