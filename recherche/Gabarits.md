---
id: recherche-gabarits
title: Gabarits — fiches standard du laboratoire
doc_type: reference
statut: active
version: 1.0
date: "31/07/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, gabarits, templates, laboratoire]
related:
  - "./README.md"
  - "./CLAUDE.md"
---

# 🧰 Gabarits — les formes standard du labo

> **Copier, ne pas improviser le format.** Un labo tient parce que chaque fiche a la même forme : on
> compare, on retrouve, on ne réinvente pas la structure à chaque fois. Chaque gabarit impose la
> **discipline épistémique** de [`CLAUDE.md`](./CLAUDE.md) — marqueurs `[ÉTABLI]`/`[DÉDUIT]`/`[HYPOTHÈSE]`
> et, pour tout ce qui est spéculatif, **un test de falsification**.

## 1. Fiche axiome → [`theorie/Axiomes.md`](./theorie/Axiomes.md)

```
### A<n> — <nom court>
- Énoncé             : la proposition, en une phrase.
- Formalisation      : l'objet mathématique. TOUJOURS (consigne : « traduire en math à chaque fois »).
- Couche             : NOYAU (grounded) | FRONTIÈRE (hypothèse).
- Pour               : ce qui plaide pour.
- Contre             : où ça casse. Opposer C1–C4.
- Axe d'amélioration : la version plus forte, ou la condition qui le sauverait.
- Test (repro)       : la requête/mesure qui tranche → renvoie à experiences/Experiences.md.
- Calculable en l'état ? : ✅ / 🟡 / ❌ sur la base dev actuelle.
```

## 2. Fiche expérience → [`experiences/Experiences.md`](./experiences/Experiences.md)

```
## E<n> — <question, en une phrase>
`[statut:: proposée|en-cours|validée|réfutée|abandonnée]` · date

- Hypothèse       : `[HYPOTHÈSE]` ce qu'on croit, formulé de façon RÉFUTABLE.
- Falsification   : L'OBSERVATION PRÉCISE qui prouverait qu'on a tort. (sans ça → pas une expérience)
- Schéma réel     : `[ÉTABLI]` tables/colonnes vérifiées (migration à l'appui) + pièges.
- Protocole       : la requête / la mesure. SQL exact si possible. Aucun LLM si évitable.
- Métrique        : comment on lit le résultat (corrélation, score de Brier, biais…).
- Limite          : n, biais du seed, ce que le run NE tranche pas. À annoncer AVANT de lancer.
- Coût            : en jours + ce qu'on ne fait pas pendant ce temps.
```

## 3. Fiche revue → [`revues/`](./revues/)

```
# Revue — <artefact source> (dump, brainstorm, papier interne)
> Objet + date. Verdict court en 2 lignes (ce qui tient / ce qui casse).

## Ce qui tient (à banquer)     → table : idée | pourquoi | déjà dans le code ?
## Ce qui casse (⚠️)            → une section par faille, opposer C1–C4, nommer le contre-exemple
## Ce que je ferais à la place  → l'ordre honnête, chiffré, faisable ici
```

## 4. Entrée de journal → [`Journal.md`](./Journal.md)

```
## AAAA-MM-JJ — <titre de session>
**Fait**         : ce qui a été produit (avec les liens vers les fiches).
**Trouvé**       : les constats, étiquetés `[ÉTABLI]`/`[DÉDUIT]`/`[HYPOTHÈSE]`.
**Décidé**       : les arbitrages (marquer « en attente de ratification » si humain requis).
**Prochain coup**: la prochaine action concrète, et si elle exige un passage en mode dev.
```

## 5. Fiche question → [`Questions-ouvertes.md`](./Questions-ouvertes.md)

```
## Q<n> — <question>
`[statut:: ouverte|en-cours|tranchée|abandonnée]` · `[prio:: P0..P3]` · date

- La question    : le problème, net.
- Pourquoi ça compte : ce que ça bloque ou oriente.
- Position actuelle  : `[HYPOTHÈSE]` mon inclinaison, sans autorité.
- Ce qu'il faut pour trancher : expérience, ADR, ou lecture.
```

## 6. Brouillon d'ADR → [`decisions/`](./decisions/)

Suivre le template du vault [`templates/TPL_ADR.md`](../templates/TPL_ADR.md) (Contexte · Décision ·
Alternatives · Conséquences · Plan). **Préfixer le fichier `ADR-<n>-DRAFT-…`** tant qu'il vit ici ;
il n'a **aucune autorité** avant promotion (ratification humaine → `v1/12-decisions/`).

---

**Points d'entrée :** [🔬 Labo](./README.md) · [📋 Protocole](./CLAUDE.md) · [📓 Journal](./Journal.md)

**Dernière mise à jour :** 31/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
