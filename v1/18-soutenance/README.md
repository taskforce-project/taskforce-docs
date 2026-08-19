---
id: soutenance-hub
title: Dossier de soutenance — TaskForce (RNCP DFS)
doc_type: soutenance
statut: en-cours
version: 0.1
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, presentation, rncp, dfs, oral, jury, demo]
---

# 🎓 Dossier de soutenance — TaskForce

> Hub de préparation de l'**oral RNCP** « Développeur Full Stack » (Metz Numeric School 2025-2026).
> Format visé : **présentation 15–20 min + questions ~10 min**.

## Contenu du dossier

- [⏱️ Plan minuté](./Plan_Minute.md) — **document de travail actif** : 23 diapositives pour 20 min
  démo comprise, couverture C13→C20 puis C21→C26, ce qui bascule en annexe. À valider.
- [🗺️ Plan de soutenance](./Plan_Soutenance.md) — architecture de la présentation slide-par-slide,
  timing, arc narratif, script de démo, préparation Q&A.
- `assets/` — captures d'écran, exports de diagrammes, PDF des slides (à déposer).

## Ce qu'il reste à produire

- [x] Slides (support visuel) — **v3 générée, ancrée sur le code réel** : `TaskForce_Soutenance_v3.pptx` (27 slides + 5 annexes, notes intégrées, sans caractères IA, chiffres vérifiés contre le dépôt). Voir [[Plan_Soutenance#⭐ Architecture v2 (deck généré, post-retour prof du 14/07)]]. Reste : insérer les 7 visuels (C4, MCD, Swagger, écran Smart Assign, composants, maquette vs réel, Lighthouse) et mesurer le Lighthouse de l'app.
- [ ] Répétition chronométrée (viser 17 min pour garder une marge).
- [ ] Environnement de démo stable (jeu de données seed, workspace de démo, secours vidéo si réseau HS).
- [ ] Export PDF des slides (annexe obligatoire du dossier de validation).

## Principe

Le jury retient **la démo** et **la clarté des choix techniques**, pas l'exhaustivité. Le plan est
construit pour : (1) montrer vite le produit qui marche, (2) prouver la maîtrise des 4 blocs par des
**preuves concrètes**, (3) assumer une **distance critique** (les limites + comment on les a traitées —
ex. migration JWT→OIDC).

> 🔗 S'appuie sur : [[README|Matrice des 32 compétences]] · [[Architecture_C4]] · [[Note_Innovation_Distance_Critique]] ·
> [[Journal_Decisions_ADR]] · [[Release_Notes]].
