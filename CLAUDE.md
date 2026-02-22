# 📋 Instructions Claude — Rédaction de Documentation Officielle Taskforce

Ce fichier fournit à Claude les directives pour rédiger, mettre à jour ou réviser toute documentation officielle du projet **Taskforce**.  
Toutes les règles ci-dessous sont **obligatoires** sauf mention contraire.

---

## 1. Identité visuelle & logos

### 1.1 Logos disponibles

| Fichier | Usage |
|---|---|
| `assets/images/logo_taskforce.png` | Logo principal du projet |
| `assets/images/logo_taskforce_tp.png` | Logo compact (entêtes, petits espaces) |
| `assets/images/logo_metz_numeric_school.svg` | Logo de l'établissement |

### 1.2 Placement dans les documents

- **Entête de document** : placer un commentaire HTML réservant l'espace logo en toute première ligne du fichier, **avant** le titre `h1` :

  ```markdown
  <!--
  Logo établissement : assets/images/logo_metz_numeric_school.svg
  Logo projet        : assets/images/logo_taskforce.png
  -->
  ```

- Ne jamais intégrer les logos directement en Markdown `![...]()` dans les documents de la section `projet/` ou `technique/` ; utiliser uniquement le commentaire HTML placeholder ci-dessus.
- Dans les documents développeur (`developpeur/`) ou utilisateur (`utilisateur/`), l'intégration directe est autorisée si elle améliore la lisibilité :

  ```markdown
  ![Logo Taskforce](../assets/images/logo_taskforce.png)
  ```

---

## 2. Structure obligatoire d'un document officiel

Chaque nouveau document doit respecter l'ordre suivant :

```
1. Commentaire HTML logos (voir §1.2)
2. Titre H1 — nom court du document
3. Métadonnées (Version, Date, Auteur(s))
4. Séparateur ---
5. Badges shields.io (Type, Statut, Année académique)
6. Séparateur ---
7. Section "Liens rapides"
8. Séparateur ---
9. Tags inline
10. Séparateur ---
11. Table des matières (si document > 3 sections)
12. Séparateur ---
13. Corps du document (sections numérotées)
14. Séparateur ---
15. Pied de page (date de mise à jour + version)
```

### 2.1 Métadonnées

```markdown
**Version :** X.Y  
**Date :** JJ/MM/AAAA  
**Auteur(s) :** Prénom NOM
```

- Utiliser `1.0` pour un premier jet, `1.x` pour des révisions mineures, `2.0` pour une refonte majeure.
- Toujours utiliser le format de date `JJ/MM/AAAA`.
- Indiquer tous les auteurs séparés par une virgule si plusieurs.

### 2.2 Badges shields.io

Format standard :

```markdown
[![Type: <NomType>](https://img.shields.io/badge/Type-<NomType>-<couleur>?style=for-the-badge)]()
[![Statut: <Statut>](https://img.shields.io/badge/Statut-<Statut>-<couleur>?style=for-the-badge)]()
[![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()
```

**Couleurs recommandées par type de document :**

| Type de document | Couleur badge Type | Badge Statut : couleur |
|---|---|---|
| Dossier Projet | `blue` | Draft → `yellow` / Final → `brightgreen` |
| CdCF | `green` | Draft → `yellow` / Final → `brightgreen` |
| CdCT | `orange` | Draft → `yellow` / Final → `brightgreen` |
| Architecture | `purple` | Draft → `yellow` / Final → `brightgreen` |
| API | `cyan` | Draft → `yellow` / Final → `brightgreen` |
| Sécurité | `red` | Draft → `yellow` / Final → `brightgreen` |
| Tests / Recettes | `teal` | Draft → `yellow` / Final → `brightgreen` |
| Manuel Utilisateur | `blue` | Draft → `yellow` / Final → `brightgreen` |
| Quickstart / Guide | `blueviolet` | Draft → `yellow` / Final → `brightgreen` |
| DevOps / CI-CD | `darkgrey` | Draft → `yellow` / Final → `brightgreen` |

### 2.3 Liens rapides

Toujours inclure, après les badges, une section `## Liens rapides` pointant vers les documents principaux de la même catégorie :

```markdown
## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Documentation GitHub](https://github.com/...) <!-- À compléter -->
- [Repository GitHub](https://github.com/...)
```

### 2.4 Tags

Sur une seule ligne, en backticks, juste avant la table des matières :

```markdown
**Tags :** `#gestion-de-projet` `#documentation` `#erp` `#saas`
```

Choisir des tags pertinents parmi : `#gestion-de-projet` `#documentation` `#webapp` `#architecture` `#erp` `#saas` `#api` `#sécurité` `#tests` `#devops` `#utilisateur` `#développeur` `#ci-cd` `#docker` `#backend` `#frontend`.

### 2.5 Table des matières

Obligatoire pour tout document de plus de 3 sections. Utiliser des listes numérotées avec des ancres Markdown :

```markdown
## Table des matières

1. [Introduction](#1-introduction)
   - 1.1 [Objet du document](#11-objet-du-document)
   - 1.2 [Périmètre](#12-périmètre)
2. [Corps principal](#2-corps-principal)
```

### 2.6 Pied de page

À la toute fin de chaque document :

```markdown
---

**Dernière mise à jour :** JJ/MM/AAAA  
**Version :** X.Y  
**Projet :** Taskforce — Metz Numeric School 2025-2026
```

---

## 3. Ton et style rédactionnel

### 3.1 Langue

- **Toujours rédiger en français**, y compris les titres de sections et les commentaires.
- Exception : les termes techniques qui n'ont pas d'équivalent français établi restent en anglais (`backend`, `frontend`, `build`, `pipeline`, `commit`, etc.) sans italique ni guillemets.
- Les noms propres de technologies s'écrivent tels quels : `Spring Boot`, `Next.js`, `Keycloak`, `Docker`, `GitHub Actions`.

### 3.2 Registre

- **Registre professionnel et neutre** : éviter le familier, les abréviations non définies, les tournures orales.
- Préférer la voix active à la voix passive lorsque c'est possible.
- Bannir les formules vagues : «&nbsp;etc.&nbsp;», «&nbsp;et ainsi de suite&nbsp;», «&nbsp;entre autres&nbsp;» — lister exhaustivement ou indiquer une référence.
- Utiliser «&nbsp;le système&nbsp;», «&nbsp;la plateforme&nbsp;», «&nbsp;l'application&nbsp;» pour désigner Taskforce selon le contexte, jamais «&nbsp;le truc&nbsp;», «&nbsp;le machin&nbsp;».

### 3.3 Longueur et densité

- Chaque section doit apporter une valeur informative réelle ; éviter le remplissage.
- Un paragraphe = une idée principale. Maximum 5 à 6 lignes par paragraphe.
- Préférer les listes à puces pour les énumérations de 3 éléments ou plus.
- Utiliser des tableaux pour comparer des options ou récapituler des données structurées.

### 3.4 Titres de sections

- Toujours numéroter les sections du corps (`## 1.`, `### 1.1`, `#### 1.1.1`).
- Les titres de niveau H1 (`#`) sont réservés au titre principal du document (un seul par fichier).
- Les titres ne se terminent pas par un point.
- Capitaliser uniquement le premier mot du titre (sauf noms propres).

### 3.5 Mise en valeur

- **Gras** (`**texte**`) : termes clés, valeurs importantes, noms de produits.
- _Italique_ (`_texte_`) : citations, définitions introduites pour la première fois.
- `Code inline` : noms de fichiers, chemins, commandes, valeurs de configuration, noms de variables.
- Blocs de code (` ``` `) : exemples de code, commandes multi-lignes, configurations YAML/JSON.
- > Citations/notes (blockquote `>`) : informations contextuelles, renvois, avertissements mineurs.
- ⚠️ **Avertissement** / ℹ️ **Note** / ✅ **Succès** : emojis autorisés uniquement en début de ligne pour signaler le type d'information, pas dans le corps du texte courant.

---

## 4. Conventions de formatage Markdown

- Utiliser **un seul espace** après `#`, `-`, `1.` etc.
- Séparer chaque section principale (`##`) par une ligne de séparation `---` au-dessus et en-dessous.
- Les tableaux doivent toujours avoir un en-tête.
- Les blocs de code doivent spécifier le langage : ` ```bash `, ` ```yaml `, ` ```java `, ` ```json `, ` ```markdown `.
- Ne jamais utiliser de HTML brut sauf pour les commentaires de logos (voir §1.2) et les espaces insécables si nécessaire.
- Limiter la profondeur d'indentation des listes à 3 niveaux maximum.

---

## 5. Conventions de nommage et organisation des fichiers

### 5.1 Nommage des fichiers

| Contexte | Convention | Exemple |
|---|---|---|
| Documents projet | `NN_Titre_Document.md` (préfixe numérique 2 chiffres) | `02_CdCF.md` |
| Documents technique | `Titre_Document.md` (PascalCase avec underscores) | `Architecture.md` |
| Documents développeur | `kebab-case.md` ou `README.md` | `docker-setup.md` |
| Documents utilisateur | `Titre_Document.md` | `Manuel_Utilisateur.md` |

### 5.2 Organisation des dossiers

```
taskforce-docs/
├── CLAUDE.md               ← ce fichier (instructions Claude)
├── README.md               ← point d'entrée principal
├── assets/
│   ├── images/             ← logos et images
│   ├── maquettes/          ← captures d'écran UI/UX
│   └── diagrammes/         ← diagrammes techniques
├── projet/                 ← documents de gestion de projet
├── technique/              ← documentation technique
├── utilisateur/            ← documentation utilisateur final
└── developpeur/            ← documentation développeur
```

- Placer chaque nouveau document dans le dossier correspondant à son audience cible.
- Ne jamais placer de fichiers binaires (images, PDF) à la racine ou dans les dossiers de documentation ; les mettre dans `assets/`.

---

## 6. Checklist avant de livrer un document

Vérifier systématiquement les points suivants avant de soumettre un document :

- [ ] Commentaire HTML logos présent en première ligne
- [ ] Titre H1 présent et unique
- [ ] Métadonnées complètes (Version, Date, Auteur(s))
- [ ] Badges shields.io présents (Type, Statut, Année académique)
- [ ] Section "Liens rapides" présente et liens vérifiés
- [ ] Tags pertinents présents
- [ ] Table des matières présente (si > 3 sections) et ancres fonctionnelles
- [ ] Sections numérotées correctement
- [ ] Aucune section vide ou contenant uniquement un placeholder non rempli
- [ ] Pied de page présent avec date, version et mention du projet
- [ ] Langue française respectée
- [ ] Ton professionnel et neutre
- [ ] Nommage du fichier conforme à la convention (§5.1)
- [ ] Fichier placé dans le bon dossier (§5.2)

---

## 7. Exemple de document minimal conforme

```markdown
<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Titre du Document

**Version :** 1.0  
**Date :** 22/02/2026  
**Auteur(s) :** Prénom NOM

---

[![Type: NomType](https://img.shields.io/badge/Type-NomType-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

---

## Liens rapides

- [Dossier Projet](../projet/Dossier_Projet.md)
- [Repository GitHub](https://github.com/...)

---

**Tags :** `#documentation` `#erp` `#saas`

---

## Table des matières

1. [Introduction](#1-introduction)
2. [Corps principal](#2-corps-principal)
3. [Conclusion](#3-conclusion)

---

## 1. Introduction

Présentation du document et de son objet.

---

## 2. Corps principal

Contenu du document.

---

## 3. Conclusion

Synthèse et prochaines étapes.

---

**Dernière mise à jour :** 22/02/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
```

---

**Dernière mise à jour :** 22/02/2026  
**Version :** 1.0  
**Projet :** Taskforce — Metz Numeric School 2025-2026
