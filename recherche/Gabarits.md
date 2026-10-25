---
id: recherche-gabarits
title: Gabarits — fiches standard du laboratoire
doc_type: reference
statut: active
version: 1.1
date: "21/10/2026"
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [recherche, gabarits, templates, laboratoire]
related:
  - "./README.md"
  - "./CLAUDE.md"
  - "./conseil/README.md"
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

## 7. Fiche membre du Conseil → [`conseil/membres/`](./conseil/membres/)

Un fichier par membre, `<prenom-nom>.md`. Règles : [charte du Conseil](./conseil/README.md) §8 et §9.

```
---
id: conseil-<slug>
title: "Conseil d'Avenir : <Nom>"
doc_type: fiche-membre
pole: Impulsion | Pont | Harmonie | Science
statut_personne: en vie | décédé en <année>
derniere_mise_a_jour: "JJ/MM/AAAA"
tags: [recherche, conseil, membre]
related:
  - "../README.md"
---

# <Nom>
> Siège : <titre court> · Pôle : <pôle>
> Personnage simulé à partir de positions publiques sourcées (charte §8).

## Qui                           → fonctions à la date de mise à jour, `[ÉTABLI]` + source
## Ce que cette personne défend  → 4 à 8 positions publiques, `[ÉTABLI]` + (source, date) ; paraphrase
## Décisions et prises de position récentes → « mois année : fait » + source (siège historique : décisions marquantes)
## Au Conseil `[HYPOTHÈSE]`      → angle d'attaque · questions qu'elle pose · ce qui la fait bondir
                                   · tensions avec d'autres membres · ce qu'elle apporterait à TaskForce
## Limites de la simulation      → angles morts, positions manquantes ou changées, caricatures à éviter
## Sources                       → [titre](url), date de publication, date de consultation
```

## 8. Procès-verbal de séance du Conseil → [`conseil/seances/`](./conseil/seances/)

Un fichier par séance, `AAAA-MM-JJ-<sujet>.md`. Déroulé : [charte du Conseil](./conseil/README.md) §6.

```
---
id: conseil-seance-AAAA-MM-JJ-<sujet>
title: "Conseil d'Avenir : séance du JJ/MM/AAAA"
doc_type: pv-seance
statut: active
date: "JJ/MM/AAAA"
auteur: Pierre MICHEL
formation: restreinte | plénière | duel | audition
tags: [recherche, conseil, seance]
related:
  - "../README.md"
---

# Séance du JJ/MM/AAAA : <sujet>
> Simulation : les membres sont des personnages simulés. Aucune phrase n'est une citation de la personne réelle.

- Saisine         : la question de la Présidence, et l'horizon (prochaine version, 3 ans, 10 ans).
- Formation       : les membres présents, le contradicteur, l'ordre de parole tiré au sort.
- Fiches          : celles rafraîchies avant la séance, et ce qui a changé.

## Dossier          → 5 à 10 faits `[ÉTABLI]` sourcés : état réel du produit, marché, règles, positions récentes
## Tour de table    → une intervention par membre, 5 à 8 lignes, `[HYPOTHÈSE]`
## Confrontation    → chaque désaccord : qui contre qui, sur quoi, le meilleur argument de chaque camp
## Recommandations  → table : # | recommandation | pour | contre | preuve en 10 jours | signal d'arrêt
## Décision         → par recommandation : retenue | à l'essai | écartée | reportée, et la raison de la Présidence
## Notes du secrétariat → corrections factuelles, écarts à la fiche, anachronismes, sources manquantes
## Suites           → où chaque résultat est rangé (expérience, question, brouillon d'ADR, Journal)
```

---

**Points d'entrée :** [🔬 Labo](./README.md) · [📋 Protocole](./CLAUDE.md) · [📓 Journal](./Journal.md) · [🏛️ Conseil](./conseil/README.md)

**Dernière mise à jour :** 21/10/2026 · **v1.1** · Projet Taskforce
