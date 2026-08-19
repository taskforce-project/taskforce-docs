---
id: dpia-analyse-prealable
title: DPIA — Analyse préalable de nécessité (RGPD Art. 35)
doc_type: rgpd
statut: valide
version: 1.0
date: "16/08/2026"
auteur: Pierre MICHEL
tags: [rgpd, dpia, aipd, art35, profilage, smart-assign, memoire, rncp]
---

# 🧭 DPIA — Analyse préalable de nécessité (Art. 35)

> Détermine, traitement par traitement, si une **analyse d'impact relative à la protection des données**
> (AIPD / DPIA) est **requise** pour TaskForce, selon l'**Art. 35 RGPD** et les **critères EDPB (WP248)**.
> Conclut par une **mini-AIPD ciblée** sur le seul traitement déclenchant des critères : le **Smart Assign**.
> Comble le gap **« DPIA absente »** de l'inventaire sécurité/RGPD.
>
> **Méthode** : un traitement « susceptible d'engendrer un risque élevé » nécessite une DPIA. L'EDPB
> retient **9 critères** ; **≥ 2 critères** remplis → DPIA en principe requise.

---

## 1. Les 9 critères EDPB (grille de lecture)

1. Évaluation / **scoring** (dont profilage) · 2. **Décision automatisée** à effet juridique/significatif
(Art. 22) · 3. **Surveillance systématique** · 4. Données **sensibles** (Art. 9) ou hautement personnelles ·
5. **Grande échelle** · 6. **Croisement** de jeux de données · 7. Personnes **vulnérables** ·
8. Usage **innovant** / nouvelle techno · 9. Traitement **empêchant l'exercice d'un droit**.

---

## 2. Screening des traitements TaskForce

Traitements issus du [[Registre_Traitements_RGPD]].

| Traitement | Critères déclenchés | DPIA requise ? |
|---|---|---|
| T1 Comptes utilisateurs | — | ❌ Non (Art. 6.1.b classique) |
| T2 Facturation / Stripe | — (sous-traitant certifié, pas de carte stockée par nous) | ❌ Non |
| T3 Données métier (issues, pages, chat) | — | ❌ Non |
| **T4 Profils de compétences + Smart Assign** | **#1 scoring**, **#8 usage innovant (IA/embeddings)** ; frôle #3 | ⚠️ **Oui → mini-AIPD §3** |
| T5 Journal d'audit | #3 partiel (mais finalité = sécurité/preuve, minimisé) | ❌ Non (obligation légale + intérêt légitime) |
| T6 Leads Enterprise | — (chiffré) | ❌ Non |

**Conclusion du screening** : seul **T4 (Smart Assign)** remplit **2 critères** (scoring + innovant) → il
justifie une **AIPD ciblée**. Les autres traitements sont des opérations B2B standard, **sans** critère de
risque élevé (ni Art. 9, ni grande échelle, ni décision automatisée) → **AIPD non requise**, décision motivée
et tracée ici (conforme à la logique CNIL : documenter aussi les traitements pour lesquels on conclut à la
non-nécessité).

---

## 3. Mini-AIPD ciblée — Smart Assign (T4)

### 3.1 Description
Le Smart Assign suggère un **assigné** pour une tâche à partir de : `member_skill_profiles` (compétences
**déclaratives**, capacité, séniorité, mode montée-en-compétence), **charge** (issues ouvertes) et
**disponibilité** (`member_leaves`). Un **LLM** (local Ollama, ou Groq si configuré) et des heuristiques
produisent un score ; la **décision finale revient à un humain** (manager/OWNER-ADMIN qui confirme).
Preuve : `core/service/SmartAssignService.java`.

### 3.2 Nécessité & proportionnalité
- **Finalité légitime** (Art. 6.1.f, intérêt légitime B2B) : bonne allocation du travail, montée en compétence.
- **Minimisation** : n'utilise que des attributs professionnels **pertinents** (compétences/charge/dispo) ;
  pas de données personnelles hors sphère professionnelle, pas de donnée Art. 9.
- **Base déclarative & opt-in** : les compétences sont **saisies par le membre** (onboarding), modifiables ;
  la disponibilité est déclarée. Pas de collecte cachée.

### 3.3 Risques & mesures (le point clé)
| Risque | Niveau brut | Mesure en place | Résiduel |
|---|---|---|---|
| **Décision automatisée** (Art. 22) discriminante | Moyen | **Humain dans la boucle** : le smart-assign **suggère**, un manager **confirme** → pas de décision « fondée exclusivement sur un traitement automatisé » | **Faible** |
| Profilage perçu comme notation des salariés | Moyen | Transparence (l'UI affiche skills/charge/dispo + une **raison** en clair) ; pas de score de « performance » caché ; finalité limitée à l'affectation | Faible |
| Biais du modèle (LLM) | Moyen | Score = **mélange** heuristiques déterministes (skills/charge) + LLM **borné** (shortlist, reranking) ; pas d'apprentissage sur données perso ; réversible (le manager tranche) | Faible |
| Exactitude | Faible | Données déclaratives tenues à jour par le membre ; droit de rectification | Faible |
| Confidentialité des profils | Faible | Chiffrement au repos des PII sensibles ; RBAC (visibilité intra-workspace) | Faible |

### 3.4 Droits des personnes
- **Information** : finalité du profilage documentée (registre + politique de confidentialité).
- **Accès / portabilité** : `GET /api/gdpr/export` inclut les `member_skill_profiles` (`GdprService`).
- **Rectification** : édition des compétences/disponibilité par le membre.
- **Opposition / effacement** : le profil de compétences est **facultatif** ; suppression via l'effacement
  du compte (anonymisation). *(À exposer : un réglage « ne pas utiliser mon profil pour le Smart Assign ».)*

### 3.5 Conclusion
Le traitement **ne relève pas** de l'Art. 22 (décision **non exclusivement** automatisée : validation
humaine) et **n'est pas** à grande échelle. Compte tenu des **mesures** (humain dans la boucle, minimisation,
opt-in déclaratif, transparence, chiffrement, droits effectifs), le **risque résiduel est acceptable**. Une
DPIA formelle complète **n'est pas obligatoire** en l'état, mais cette **mini-AIPD** en tient lieu et **doit
être ré-examinée** si : (a) la décision devenait automatique (sans humain), (b) passage à grande échelle,
(c) ajout de données sensibles ou d'un scoring de performance.

---

## 4. Actions de suivi (roadmap)
- [ ] Exposer un **opt-out explicite** « profil non utilisé par le Smart Assign » (renforce Art. 21).
- [ ] Mentionner le profilage Smart Assign dans la **politique de confidentialité** (finalité + base légale).
- [ ] Revoir cette AIPD à chaque évolution matérielle du moteur d'affectation.

---
**Références** : [[Registre_Traitements_RGPD]] · [[Audit_RGPD_Conformite]] · [[Procedure_Violation_Donnees]] ·
RGPD Art. 35 + Art. 22 · EDPB WP248 (critères DPIA) · liste CNIL des traitements soumis/exemptés.
