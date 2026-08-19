---
id: procedure-violation-donnees
title: Procédure de gestion des violations de données (RGPD Art. 33/34)
doc_type: rgpd
statut: valide
version: 1.0
date: "16/08/2026"
auteur: Pierre MICHEL
tags: [rgpd, violation, breach, notification, cnil, art33, art34, procedure, memoire, rncp]
---

# 🚨 Procédure de gestion des violations de données personnelles

> Procédure interne de détection, qualification, notification et documentation des **violations de
> données à caractère personnel** au sens de l'**Art. 4.12 du RGPD**. Elle couvre les obligations
> **Art. 33** (notification à la CNIL sous 72 h) et **Art. 34** (information des personnes concernées).
> Chaque mesure s'appuie sur des contrôles **réellement implémentés** dans TaskForce (référencés).
>
> **Cadre** : RGPD (UE 2016/679) · lignes directrices EDPB 9/2022 sur la notification de violations · guide CNIL.
> **Responsable de traitement** : TaskForce (Pierre MICHEL). Comble le gap **TF-RGPD-009** ([[Problemes_Connus]]).

---

## 1. Définition — qu'est-ce qu'une violation ?

Une **violation de données** est un incident de sécurité entraînant, de manière accidentelle ou illicite :

| Type (Art. 32.2) | Description | Exemple TaskForce |
|---|---|---|
| **Confidentialité** | Accès ou divulgation non autorisés | Fuite de la base, IDOR inter-tenant, token volé |
| **Intégrité** | Altération non autorisée | Modification frauduleuse d'issues / de profils |
| **Disponibilité** | Perte, destruction, indisponibilité | Suppression de base, ransomware, panne prolongée |

⚠️ Un incident de sécurité **sans** donnée personnelle impactée (ex. défiguration d'une page marketing
statique) **n'est pas** une violation au sens RGPD, mais suit la même chaîne de détection.

**Facteur atténuant structurel de TaskForce** : les mots de passe ne sont **jamais** stockés côté
TaskForce (auth déléguée à **Keycloak/OIDC**), et 4 colonnes PII sensibles sont **chiffrées au repos**
(AES-256-GCM, [[Chiffrement_Au_Repos]]) → une exfiltration de la base seule laisse ces données
inexploitables sans la clé (variable d'environnement, hors base).

---

## 2. Détection — sources d'alerte

| Source | Mécanisme (implémenté) | Fichier de preuve |
|---|---|---|
| Journal d'audit immuable | `AuditService` trace accès sensibles + `GDPR_EXPORT`/`GDPR_DELETE` | `core/service/AuditService.java`, table `audit_logs` |
| Limitation de débit | `RateLimitFilter` (Bucket4j) — pics d'auth/API = signal brute-force | `shared/security/RateLimitFilter.java` |
| Authentification | Logs Keycloak (échecs, connexions anormales) | Keycloak (IdP) |
| Erreurs applicatives | Logs serveur, `ClientLogController` (erreurs front remontées) | `core/api/ClientLogController.java` |
| Scans de sécurité | Trivy / Semgrep / ZAP (CVE, secrets, DAST) | `scripts/security-scan.ps1` |
| Signalement | Utilisateur, chercheur (contact `privacy@taskforce.dev`), sous-traitant | — |

> **À renforcer (roadmap)** : alerting automatisé (seuils sur les métriques de supervision) —
> aujourd'hui la détection combine journalisation + revue. Cf. [[Observabilite]].

---

## 3. Chaîne de responsabilité

| Rôle | Titulaire (projet) | Responsabilité |
|---|---|---|
| **Point de contact incident** | Référent sécurité | Reçoit l'alerte, ouvre la fiche, déclenche la procédure |
| **Responsable de traitement** | TaskForce (Pierre MICHEL) | Décide de la notification CNIL / personnes ; signe |
| **DPO / relais RGPD** | (à désigner ; par défaut le responsable) | Qualifie le risque, rédige la notification, tient le registre |
| **Technique** | Développeur d'astreinte | Contient, corrige, préserve les preuves (logs) |

*(Sur un proto RNCP à équipe réduite, ces rôles peuvent être portés par la même personne ; ils sont
distingués pour la traçabilité et la montée en charge.)*

---

## 4. Processus (du T0 à la clôture)

```
T0 Détection ──► Confinement immédiat ──► Qualification ──► Évaluation du risque
                                                                   │
                        ┌──────────────────────────────────────────┤
                        ▼                                           ▼
             Risque pour les personnes ?                 Registre des violations
             (probable)                                  (TOUTES, même non notifiées)
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                 ▼
   Notif. CNIL      Risque ÉLEVÉ ?    Correctifs +
   ≤ 72 h (Art.33)  → Info personnes  retour d'expérience
                     sans délai (Art.34)
```

### 4.1 Confinement immédiat (T0 → T0+quelques heures)
Révoquer les sessions/tokens compromis (Keycloak), couper l'accès de l'acteur, isoler le composant,
**préserver les journaux** (`audit_logs`, logs serveur) sans les altérer. Ne pas détruire de preuve.

### 4.2 Qualification (≤ 24 h)
Confirmer qu'il s'agit bien de **données personnelles** ; déterminer le **type** (§1), les **catégories**
et le **volume** de personnes/enregistrements, la **cause** et la **fenêtre temporelle**.

### 4.3 Évaluation du risque pour les personnes
Grille inspirée **ENISA / CNIL** (croiser 3 axes) :

| Axe | Faible | Moyen | Élevé |
|---|---|---|---|
| **Nature des données** | Données publiques/pro basiques | Identité + contenu métier | Données sensibles, mots de passe (n/a ici), financières |
| **Facilité d'identification** | Pseudonymisée/chiffrée | Identifiable indirectement | Directement nominative |
| **Gravité des conséquences** | Négligeable | Désagrément/limité | Préjudice significatif (usurpation, discrimination) |

**Le chiffrement au repos** (AES-256-GCM) et l'**anonymisation à l'effacement** font **baisser** l'axe
« facilité d'identification » pour les colonnes concernées → une violation portant uniquement sur des
champs chiffrés, la clé restant sûre, peut relever de l'**exemption Art. 34.3.a** (données rendues
incompréhensibles).

### 4.4 Notification CNIL (Art. 33) — **≤ 72 h** après la prise de connaissance
Obligatoire **sauf si** la violation est « peu susceptible d'engendrer un risque » pour les personnes.
Si les 72 h ne peuvent être tenues, notifier de façon **échelonnée** en justifiant le retard.
Contenu minimal → voir modèle §6.1.

### 4.5 Information des personnes (Art. 34) — **sans délai injustifié**
Obligatoire **uniquement** si la violation est susceptible d'engendrer un **risque ÉLEVÉ**.
**Exemptions (Art. 34.3)** : (a) données rendues incompréhensibles (chiffrement) ; (b) mesures
ultérieures écartant le risque élevé ; (c) effort disproportionné → communication publique équivalente.
Modèle → §6.2.

### 4.6 Clôture
Correctif déployé et vérifié (test de non-régression) ; entrée finalisée au **registre des violations** ;
**retour d'expérience** (cause racine, action préventive) reporté au [[Problemes_Connus]] / roadmap.

---

## 5. Registre des violations (Art. 33.5)

**Toute** violation est consignée, **qu'elle soit notifiée ou non**. Emplacement : registre interne
sécurisé (accès restreint responsable/DPO). Modèle de fiche :

| Champ | Contenu |
|---|---|
| ID / date de découverte | `VIOL-AAAA-NN` / horodatage |
| Nature | Confidentialité / Intégrité / Disponibilité |
| Données & personnes concernées | Catégories + volume estimé |
| Cause & chronologie | T0, cause racine, fenêtre |
| Conséquences probables | Évaluation du risque (§4.3) |
| Mesures prises | Confinement, correctif |
| Notifiée ? | CNIL (O/N + date) · Personnes (O/N + date) · Justification si non |
| Statut | Ouverte / Contenue / Clôturée |

---

## 6. Modèles de notification

### 6.1 Notification CNIL (Art. 33.3)
- **Nature** de la violation + catégories et **nombre approximatif** de personnes et d'enregistrements.
- **Coordonnées** du DPO / point de contact.
- **Conséquences probables**.
- **Mesures** prises ou proposées (dont atténuation).

### 6.2 Information des personnes (Art. 34.2) — langage clair
- Description de la violation en **termes simples**.
- Coordonnées du point de contact.
- Conséquences probables.
- Mesures prises + **recommandations** aux personnes (ex. changer le mot de passe **côté Keycloak**,
  vigilance hameçonnage).

---

## 7. Sous-traitants (Art. 33.2)

Un sous-traitant qui subit une violation doit **informer TaskForce sans délai**. TaskForce reste
responsable de la notification CNIL/personnes. La liste des sous-traitants et les clauses associées
vivent au [[Registre_Traitements_RGPD]] (à réconcilier — cf. gap ouvert sur l'incohérence
sous-traitants IA/hébergeur).

---

## 8. Tests & preuves associés

- **IDOR inter-tenant** (confidentialité) : corrigés et **testés** (PC-021/PC-034) — `ProjectVisibilityGuard`,
  tests de contrôle d'accès (403) → réduit la surface de violation de confidentialité.
- **Signature webhook** (intégrité) : rejet 400 sur signature invalide — `StripeWebhookServiceTest`.
- **Effacement/anonymisation** : `GdprServiceIntegrationTest` (droit à l'effacement).
- **Chiffrement** : `EncryptedStringConverterTest` (11 cas).

> **À produire pour compléter** : un **exercice de simulation** (table-top) documenté d'une violation
> fictive rejouant cette procédure, à joindre au dossier comme preuve d'opérationnalité.

---
**Références** : [[Audit_RGPD_Conformite]] · [[Registre_Traitements_RGPD]] · [[Chiffrement_Au_Repos]] ·
[[PSSI]] · [[Threat_Model_STRIDE]] · RGPD Art. 33/34 · EDPB Guidelines 9/2022.
