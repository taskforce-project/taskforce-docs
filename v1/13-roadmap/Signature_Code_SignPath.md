---
id: signature-code-signpath
title: Signature de l'app desktop (SignPath Foundation)
doc_type: procedure
statut: active
version: 1.0
date: "20/10/2026"
auteur: Pierre MICHEL
review_cycle: on-change
tags: [desktop, signature, windows, signpath, release, securite]
related:
  - "../03-architecture/Specification_App_Desktop.md"
  - "./Plan_Release_Open_Source.md"
---

# Signature de l'app desktop (SignPath Foundation)

**Version :** 1.0
**Date :** 20/10/2026
**Auteur(s) :** Pierre MICHEL

## 1. Pourquoi signer

Un installeur signé dit à Windows qui l'a publié et prouve qu'il n'a pas été modifié depuis. Sans signature :
SmartScreen affiche « Windows a protégé votre ordinateur » au premier lancement, et des antivirus bloquent un fichier
inconnu par réputation. C'est arrivé le 20/10 : McAfee a classé `TaskForce-Setup-1.0.0.exe` comme virus ou programme
indésirable sur le poste du CEO (fichier non signé, jamais vu par VirusTotal).

## 2. Ce que la SignPath Foundation engage

- **Gratuit** pour les projets open source, sans contrat payant.
- **Le certificat est au nom de « SignPath Foundation »** : c'est l'éditeur que Windows affiche, pas TaskForce. La
  fondation se porte garante que le fichier vient bien de notre dépôt public.
- La clé reste chez eux (module matériel) : personne ne peut la copier, nous non plus.
- On ne signe que ce que GitHub Actions construit depuis le dépôt public, et **chaque release attend ton approbation**
  dans SignPath (avec double authentification).
- Règles (`signpath.org/terms`) : licence open source sans composant propriétaire, pas de programme malveillant,
  projet maintenu et déjà publié, page « Code signing policy » sur le site, double authentification pour toute
  l'équipe (GitHub et SignPath), confidentialité décrite. En cas de manquement, la fondation peut suspendre le
  service et révoquer le certificat.

### Quitter

- **À tout moment, sans frais** : on retire la variable et le secret SignPath de GitHub, les releases suivantes
  sortent non signées (ou signées par un autre moyen). On peut demander la fermeture du compte.
- Les installeurs déjà signés **restent signés** (signature horodatée), sauf révocation du certificat pour
  non-respect des règles.
- La réputation acquise auprès de SmartScreen et des antivirus est attachée à leur certificat : en passant à notre
  propre certificat, elle repart de zéro.

### Autres voies (si refus, ou plus tard)

- **Certum, certificat « Open Source Developer »** : à ton nom, de l'ordre de 25 à 70 € par an selon les sources,
  carte à puce ou signature dans le cloud. Vérifier sur la page de Certum le prix et la prise en charge
  d'Authenticode (signature Windows) avant d'acheter : les sources se contredisent.
- **Azure Artifact Signing** (Microsoft) : environ 10 $ par mois ; en Europe, réservé aux entreprises (pas aux
  personnes).

## 3. Prérequis

| Prérequis | État |
| --- | --- |
| Licence open source sans composant propriétaire | Fait (AGPL-3.0 ; Electron, Java, PostgreSQL gardent leurs licences libres) |
| Une version déjà publiée | Fait (`desktop-v1.0.0`, `1.0.1` et `1.0.2`) |
| Build automatisé depuis le dépôt | Fait (workflow `Desktop - Release`) |
| Page « Code signing policy », liée depuis l'accueil et le téléchargement | Faite le 20/10 (`/code-signing-policy`, pied de page et page de téléchargement) |
| Politique de confidentialité | Faite (`/legal/privacy`, décrit ce que l'app envoie) |
| Double authentification GitHub pour chaque membre | Faite le 20/10 : exigée dans l'organisation (Miche1-Pierre, spykernv et Alizee-Huot l'avaient déjà). L'option « Only allow secure two-factor methods » reste désactivée : elle demande de retirer le SMS du compte du CEO, ce que SignPath n'exige pas |
| Réputation du projet | **Point faible** : dépôt public depuis octobre 2026, 1 étoile, app tout juste publiée |

Avant d'exiger la double authentification dans l'organisation (Settings, Authentication security, « Require
two-factor authentication »), vérifier que chaque membre l'a activée : GitHub retire de l'organisation ceux qui ne
l'ont pas.

## 4. Le formulaire (`signpath.org/apply`)

Formulaire en anglais, avec un CAPTCHA : rempli par le CEO, **dossier déposé le 20/10, en revue** (mail de SignPath reçu). Réponses préparées :

| Champ | Réponse |
| --- | --- |
| Project Name | TaskForce |
| Repository URL | https://github.com/taskforce-project/taskforce-fullstack |
| Homepage URL | https://taskforce-project.fr |
| Download URL | https://taskforce-project.fr/download (elle mentionne la SignPath Foundation et mène à la Code signing policy) |
| Privacy Policy URL | https://taskforce-project.fr/legal/privacy |
| Wikipedia URL | (vide) |
| Tagline | Open source desktop app to plan your work, keep a project memory and hand tasks to AI coding agents. |
| Category | La plus proche de « Productivity » ou « Developer tools » |
| Description | TaskForce is a free, open source (AGPL-3.0) work management app for Windows and Linux. It plans projects and issues, keeps a project memory (Brain OS) and lets people hand tasks to AI coding agents such as Claude Code, which work on the person's own computer and open pull requests on GitHub. Projects stay on the computer; a free TaskForce account is used to sign in. The same code also runs as a self-hosted web app. |
| Reputation | Honnête : public depuis octobre 2026 ; site, documentation (https://docs.taskforce-project.fr), releases GitHub et leurs téléchargements ; projet né comme projet de fin d'études en développement logiciel, devenu open source. Ajouter toute mention publique (post LinkedIn, articles) quand elle existe. |
| Maintainer Type | Individual (ou small team) |
| Build System | GitHub Actions |
| First Name / Last Name / Email | Les tiens : ce sera ton compte SignPath, avec double authentification |
| Company Name | (vide) |
| Primary Discovery Channel | Ce qui est vrai (par exemple un assistant IA) |
| Case « Code of Conduct… certificates are issued in SignPath Foundation's name… » | À cocher après lecture (obligatoire) |
| Case « store and process my personal data » | À cocher (obligatoire) |
| Case « receive other communications » | Facultative, à laisser décochée |

## 5. Après l'acceptation

1. **Dans SignPath** (avec moi, en partage d'écran ou en me donnant la main sur le navigateur) :
   - connecter le système de build de confiance **GitHub.com** à l'organisation et au projet ;
   - projet `taskforce`, lié au dépôt ;
   - configuration d'artefact : l'artefact GitHub (un zip) contient `TaskForce-Setup-<version>.exe`, à signer en
     Authenticode ; SignPath demande aussi de fixer le nom de produit (`TaskForce`) ;
   - politique de signature `release-signing`, approbateur : toi ;
   - un utilisateur CI avec un jeton d'API, autorisé à soumettre sur cette politique.
2. **Dans GitHub** (Settings, Secrets and variables, Actions) : variable `SIGNPATH_ORGANIZATION_ID`, secret
   `SIGNPATH_API_TOKEN` ; facultatif : `SIGNPATH_PROJECT_SLUG`, `SIGNPATH_SIGNING_POLICY_SLUG` si les noms diffèrent.
3. **Chaque release** : on lance `Desktop - Release` comme d'habitude. Le job Windows s'arrête sur « Sign the
   installer », SignPath t'envoie la demande, tu l'approuves (6 h au plus), puis le job reprend : installeur signé,
   `latest.yml` et carte des blocs recalculés (`desktop/scripts/signed-installer.mjs`), publication.
4. Je passe `SIGNED_BUILDS.windows` à `true` (`landing-page/src/lib/release.ts`) : le site dit que les builds sont
   signés et la Code signing policy affiche la mention de SignPath au présent.

La CI est prête depuis le 20/10 : ces étapes ne s'exécutent que lorsque `SIGNPATH_ORGANIZATION_ID` existe ; d'ici là,
les releases sortent comme avant, non signées.

## 6. Ce que je ne peux pas faire

Le dossier est à ton nom : remplir et envoyer le formulaire (CAPTCHA, acceptation des conditions), créer ton compte
SignPath et sa double authentification, approuver chaque signature. Tout le reste est fait ou se fait avec moi.

## 7. En attendant : faux positifs des antivirus

- VirusTotal partage les fichiers qu'on lui envoie avec les éditeurs d'antivirus, dont McAfee : y envoyer chaque
  installeur publié, celui que le site propose. L'envoi d'un fichier sans compte passe par un reCAPTCHA au moment de
  confirmer : c'est au CEO de le faire (le 20/10, l'envoi automatisé de la 1.0.2 s'est arrêté là). Empreinte SHA-256
  de `TaskForce-Setup-1.0.2.exe` : `67d6e77e27ffa7e6909ab066d493833b5d9f86c6f5c9568e8b2d853841ccc6c0`.
- McAfee : un fichier de plus de 50 Mo ne passe pas par l'e-mail de signalement ; la voie connue est de publier le
  lien VirusTotal sur leur forum communautaire (compte McAfee requis) en demandant le retrait du faux positif.
