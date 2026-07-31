---
id: recherche-experiences
title: Registre des expériences falsifiables — R&D Brain OS
doc_type: register
statut: active
version: 1.0
date: "17/07/2026"
auteur: Pierre MICHEL
review_cycle: monthly
tags: [recherche, register, experiences, falsification, brain-os]
related:
  - "./CLAUDE.md"
  - "./Open_Questions.md"
  - "./World_Model_Notes.md"
---

# 🧪 Registre des expériences

> **Règle d'entrée** — une hypothèse n'entre ici que si elle vient avec **l'observation qui la tuerait**.
> Pas de critère de falsification → ce n'est pas une expérience, c'est une croyance
> ([`CLAUDE.md`](../CLAUDE.md) §4.6).
>
> **Ce registre ne déclenche rien tout seul.** Le mode recherche **n'autorise pas à coder**
> ([`CLAUDE.md`](../CLAUDE.md) §9). Une expérience s'exécute en mode développement, sous
> [`AGENTS.md`](../../AGENTS.md), après arbitrage de priorité — et la priorité au 17/07/2026 est la
> **clôture V1 + soutenance**. Tout ce qui suit est donc **post-V1**.

## Format

| Champ | Sens |
| --- | --- |
| **Hypothèse** | Ce qu'on croit, formulé de façon **réfutable** |
| **Falsification** | **L'observation précise qui prouverait qu'on a tort** |
| **Protocole** | Ce qu'on fait, avec quelles données réelles |
| **Coût** | En jours, et **ce qu'on ne fait pas pendant ce temps** |
| **Statut** | `[statut:: proposée|en-cours|validée|réfutée|abandonnée]` |

## Vue d'ensemble

| ID | Expérience | Coût | LLM ? | Statut |
| --- | --- | :--: | :--: | :--: |
| [E1](#e1--nos-prédictions-sont-elles-calibrées-) | Calibrer les prédictions déjà faites | ~2 j | non | proposée |
| [E2](#e2--la-dérivée-ẋ-apporte-t-elle-de-linformation-) | La dérivée $\dot x$ | ~1 j | non | proposée |
| [E3](#e3--la-classe-de-référence-bat-elle-le-llm-) | Classe de référence vs LLM | ~1 j | oui (comparaison) | proposée |
| [E4](#e4--un-llm-peut-il-produire-une-dynamique-non-triviale-) | Un LLM sait-il faire de la dynamique ? | ~1 j | oui | proposée |

> **L'ordre compte.** E1 avant tout le reste : sans mesure de calibration, **aucune** des autres n'est
> interprétable. C'est l'inversion proposée dans [`World_Model_Notes.md`](../revues/World-Model.md) §10 —
> **mesurer avant de simuler**.

---

## E1 — Nos prédictions sont-elles calibrées ?

`[statut:: proposée]` · **La plus importante.** Ouverte le 17/07/2026

**Hypothèse** `[HYPOTHÈSE]` — Les prédictions que le système produit **déjà** sont mal calibrées, et on
n'en sait rien parce qu'on ne les a jamais confrontées au réel.

**Le point clé, souvent manqué** — `[ÉTABLI]` **TaskForce fait déjà des prédictions.** La Phase 4 lot 2b
fait générer par le LLM les **story points**, la **priorité** et le **type** d'une issue à l'approbation
d'une spec. **Un story point est une prédiction d'effort.** Elles ne sont comparées à **rien**.

**Falsification** — Si l'erreur des points prédits vs réels est **sans biais et de faible variance**
(sur les issues clôturées du scénario + du seed), alors le système prédit **déjà** correctement, et
l'urgence d'un world model tombe. Inversement, un biais fort valide qu'il faut mesurer avant de
construire.

**Protocole** — Aucune ligne de code produit. Requête sur `issues` clôturées : `storyPoints` (prédit,
IA) vs durée réelle (`completedAt − createdAt`, ou passage `IN_PROGRESS → DONE`). Calculer biais,
dispersion, et une **courbe de calibration**. `[ÉTABLI]` Les données existent : 267 issues au seed.

⚠️ **Limite à annoncer d'emblée** — le seed est **synthétique** ; ses story points ne viennent pas d'un
vrai travail. La mesure est donc valable comme **plomberie** (« le pipeline de scoring fonctionne »),
**pas** comme vérité sur la qualité prédictive. La vraie mesure demande des cycles réels → **C3**.

**Ce que ça débloque** — La table des écarts prédit/réel de
[Moteur_IA_World_Model_OODA](../../v1/road_to_v2/Moteur_IA_World_Model_OODA.md) §4, `[ÉTABLI]` **spécifiée
et jamais construite**. C'est le chaînon manquant entre les deux documents.

**Coût** — ~2 j. Pendant ce temps : pas de clôture V1. → **post-V1**.

---

## E2 — La dérivée $\dot x$ apporte-t-elle de l'information ?

`[statut:: proposée]` · Ouverte le 17/07/2026 · **protocole précisé le 31/07/2026 (schéma vérifié)**

**Hypothèse** `[HYPOTHÈSE]` — La **tendance** ($\dot x$) prédit mieux qu'un état absolu ($x$). Deux
projets à 70 % d'avancement, l'un qui accélère et l'autre qui décélère, ne finissent pas pareil.
C'est **la meilleure idée** de [`World Model.md`](../../World%20Model.md) ([`World_Model_Notes.md`](../revues/World-Model.md) T3).
Formalisée en **[Axiome A3](../theorie/Axiomes.md#a3--le-rythme--ẋ)**.

**Falsification** — Si, sur les cycles clôturés, l'avancement au **premier tiers** de la fenêtre **ne
classe pas** les cycles selon leur complétion finale (corrélation de rang $\rho \leq 0$), alors $\dot x$
n'apporte rien **ici** et sort du modèle.

**Schéma réel (vérifié 31/07)** `[ÉTABLI]` — migrations V16 / V23 / V38 :

| Donnée | Où | Piège |
| --- | --- | --- |
| Fenêtre du cycle | `cycles.start_date`, `cycles.end_date` (DATE) | **Pas de `completed_at` sur `cycles`** → la clôture réelle n'est pas datée ; fenêtre = dates planifiées |
| Lien cycle→issue | table de jonction **`cycle_issues`** `(cycle_id, issue_id)` | **pas** de `issues.cycle_id` |
| Issue terminée | `issues.completed_at IS NOT NULL` + `issue_statuses.category = 'COMPLETED'` | exclure `category = 'CANCELLED'` |
| Effort | `issues.story_points` (INTEGER) | **nullable** → repli sur le comptage |

**Protocole** — SQL pur, **aucun LLM**, aucune migration. Extraction par cycle clôturé : complétion
finale (en points *et* en comptage) + complétion atteinte à la **mi-fenêtre** :

```sql
WITH w AS (
  SELECT id, name, start_date, end_date,
         (start_date + (((end_date - start_date) * 0.5)::int)) AS mid_date
  FROM cycles WHERE status = 'COMPLETED'
),
s AS (
  SELECT ci.cycle_id,
         COUNT(*)                                                       AS n_tot,
         COUNT(*) FILTER (WHERE st.category = 'COMPLETED')              AS n_done,
         COALESCE(SUM(i.story_points), 0)                              AS p_tot,
         COALESCE(SUM(i.story_points) FILTER (WHERE st.category='COMPLETED'), 0) AS p_done,
         COALESCE(SUM(i.story_points) FILTER (
             WHERE st.category='COMPLETED' AND i.completed_at::date <= w.mid_date), 0) AS p_done_mid
  FROM cycle_issues ci
  JOIN issues         i  ON i.id = ci.issue_id
  JOIN issue_statuses st ON st.id = i.status_id
  JOIN w                 ON w.id = ci.cycle_id
  WHERE st.category <> 'CANCELLED'
  GROUP BY ci.cycle_id
)
SELECT w.name,
       s.n_done || '/' || s.n_tot                                       AS count_final,
       ROUND(100.0*s.p_done     / NULLIF(s.p_tot,0), 1)                 AS pct_final_points,
       ROUND(100.0*s.p_done_mid / NULLIF(s.p_tot,0), 1)                 AS pct_at_mid   -- proxy de ẋ
FROM w JOIN s ON s.cycle_id = w.id
ORDER BY w.name;
```

**Métrique** — corrélation de rang **Spearman** $\rho$ entre `pct_at_mid` (précurseur) et
`pct_final_points` (résultat), sur l'ensemble des cycles clôturés. Le `completed_at` par issue permet,
si besoin, une **courbe de burn-up** par cycle (pente = $\dot x$ vrai) plutôt qu'un seul point à mi-fenêtre.

⚠️ **Limite dominante, à annoncer avant de lancer** — `[ÉTABLI]` le seed met **~8 issues sur 267 dans
des cycles** (« 259 hors cycle », roadmap Phase 4bis) et le scénario produit **~4 cycles clôturés**.
Donc $n \approx 4$, ~2 points de burn-up par cycle : **statistiquement dérisoire**. Ce run **valide que
la mesure se calcule sur le vrai schéma** (plomberie), il ne **tranche pas** l'hypothèse. Le vrai test
exige des **cycles réels** → **C3** (~20/an). Et le seed est **synthétique** : ses story points ne
viennent pas d'un vrai effort (cf. E1).

**Coût** — ~1 j. **Le meilleur rapport valeur/risque du dossier** : zéro invention possible (la requête
ne touche que des colonnes vérifiées), et ça sert le produit (afficher une tendance de cycle) même si
l'hypothèse théorique tombe.

---

## E3 — La classe de référence bat-elle le LLM ?

`[statut:: proposée]` · Ouverte le 17/07/2026

**Hypothèse** `[HYPOTHÈSE]` — Un **taux de base** trivial (« les sprints comme celui-ci ont fini à 80 % »)
prédit **au moins aussi bien** qu'un LLM qui raisonne sur le contexte. C'est le résultat classique du
*reference class forecasting* (Kahneman & Tversky, Flyvbjerg — [`References.md`](../references/Bibliotheque.md) §5).

**Falsification** — Si le LLM bat significativement le taux de base sur les cycles clôturés, alors le
raisonnement contextuel **apporte** quelque chose et la piste « moteur » se défend. Sinon, `[DÉDUIT]`
la bonne architecture est **une requête SQL**, pas un world model — et il faut l'admettre.

**Protocole** — Deux prédicteurs sur les mêmes cycles : (A) moyenne historique de complétion ;
(B) LLM Qwen avec le contexte RAG. Comparer par **score de Brier**. ⚠️ Métré `AiMeter` (**C4**).

**Coût** — ~1 j, dépend de **E1** (il faut le scoring d'abord).

> **Pourquoi cette expérience mérite d'être faite même si elle « perd »** — un résultat négatif
> (« le SQL suffit ») **économise des mois**. C'est le meilleur usage possible d'une journée.

---

## E4 — Un LLM peut-il produire une dynamique non triviale ?

`[statut:: proposée]` · Ouverte le 17/07/2026

**Hypothèse** `[HYPOTHÈSE]` — Un LLM interrogé sur $P(G_{t+1} \mid G_t, a)$ produit de l'**intuition
naïve**, pas de la dynamique. Il répondra que recruter augmente la vélocité.

**Falsification** — **Le test de Brooks.** Demander à Qwen l'effet de « embaucher 2 développeurs sur un
projet en retard ». S'il répond spontanément que la vélocité **baisse d'abord** (formation +
communication en $O(n^2)$), qu'il **chiffre le délai**, et qu'il tient ce raisonnement de façon
**stable** sur des variantes du prompt, alors l'option **(b)** de [Q2](../Questions-ouvertes.md#q2--doù-vient-f-)
est plus solide que je ne le crois, et il faut le reconnaître.

**Pourquoi ce test précis** — `[ÉTABLI]` `World Model.md` utilise **exactement cet exemple**
(`Hire → Velocity +30`) pour illustrer son moteur, et c'est le **contre-exemple canonique** du domaine
depuis 1975. Si le LLM reproduit l'erreur du document, ça démontre le mode d'échec **(a)/(b)** sur le
cas le plus favorable qui soit — un effet publié, célèbre, sûrement dans ses données d'entraînement.

⚠️ **Biais à contrôler** — la loi de Brooks est **si connue** qu'un LLM peut la réciter sans la
« comprendre ». Le test ne vaut que sur des variantes **moins canoniques** (« doubler le périmètre à
mi-cycle », « remplacer le lead 3 semaines avant la livraison »). C'est **la** partie difficile du
protocole, et elle décide de la validité de l'expérience.

**Coût** — ~1 j. Métré `AiMeter` (**C4**).

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [❓ Questions](../Questions-ouvertes.md) · [📖 Notes critiques](../revues/World-Model.md)

**Dernière mise à jour :** 17/07/2026 · **v1.0** · Projet Taskforce — Metz Numeric School 2025-2026
