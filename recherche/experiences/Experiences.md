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
| [E5](#e5--un-llm-est-il-une-fonction-stable-) | Un LLM est-il une fonction stable ? | ~0,5 j | oui | proposée |
| [E6](#e6--le-front-de-pareto-des-cycles-passés-est-il-informatif-) | Le front de Pareto passé informe-t-il ? | ~0,5 j | non | proposée |
| [E7](#e7--quelle-part-de-lattente-humaine-porte-sur-du-réversible-) | Part de l'attente humaine sur du réversible (Conseil, R1) | ~0,5 j + 10 j d'usage | non | proposée |
| [E8](#e8--des-règles-écrites-comme-du-code-sont-elles-relues-) | Règles d'agent écrites comme du code (Conseil, R2) | ~1 j | non | proposée |
| [E9](#e9--le-temps-dattention-par-résultat-accepté-se-mesure-t-il-) | Attention humaine par résultat accepté (Conseil, R3) | ~1 j | non | proposée |
| [E10](#e10--un-relecteur-dédié-trouve-t-il-de-vrais-défauts-) | Relecteur dédié des pull requests (Conseil, R4) | ~0,5 j | oui | proposée |
| [E11](#e11--un-petit-modèle-local-rend-il-une-tâche-en-commentaire-acceptable-) | Un petit modèle local pour les tâches en commentaire (Conseil, R51) | ~1,5 j | oui | proposée |
| [E12](#e12--un-petit-modèle-affiné-bat-il-le-modèle-de-base-avec-recherche-) | Un petit modèle affiné contre le modèle de base avec recherche (Conseil, R62) | ~1,5 j | oui | proposée |
| [E13](#e13--le-spécialiste-gagne-t-il-du-temps-sur-un-vrai-dossier-) | Le temps du spécialiste sur un vrai dossier (Conseil, R63), à J8 | ~1 j | oui | proposée |
| [E14](#e14--la-promesse-se-redit-elle-en-une-phrase-) | La promesse redite en une phrase (Conseil, R65), à J8 | ~2 h | non | proposée |
| [E15](#e15--la-voix-se-transcrit-elle-sur-la-machine-juste-et-vite-) | La voix transcrite sur la machine (Conseil, R80) | ~1 j | oui | proposée |
| [E16](#e16--une-seule-source-pour-le-moteur-de-règles-sans-aller-retour-) | Une seule source pour le moteur de règles (Conseil, R90), en J1 | ~1 j | non | faite : (a) réfutée, (b) tient |
| [E17](#e17--lindice-de-confiance-se-mesure-t-il-et-monte-t-il-) | L'indice de confiance, mesure de départ à J2 (Conseil, R104) | ~1 j | non | proposée |

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

**Raffinement (31/07, issu de [A5-calibration](../theorie/A5-calibration.md))** — E1 n'est pas « une »
calibration mais **trois régimes** :
- **Grain issue** (volume) : mesurer d'abord le **biais** $\mathbb{E}[\hat s - s]$ et la dispersion des
  story points (c'est de la **régression**, pas encore de la calibration). Réel = `SUM(issue_worklogs.minutes)`
  (V47) **si peuplé** ; sinon **latence** `completed_at − created_at`, en **déclarant le biais** (latence ≠ effort).
- **Exiger de battre le taux de base** (décomposition de Murphy : fiabilité **et** résolution — un
  prédicteur « toujours la moyenne » est calibré *et* nul). Sinon le « modèle » ne sert à rien → rejoint [E3](#e3--la-classe-de-référence-bat-elle-le-llm-).
- **Grain cycle** : mesuré **pour mémoire** seulement — ~4 points/bin, **IC de Wilson ≈ [0,30 ; 0,95]** →
  **statistiquement indécidable** (C3).
- **Grain décision** (contrefactuel) : **zone interdite**, on ne score pas (mur C2).
- **Bloqué en amont** : la calibration vraie (couverture d'intervalle) exige que **le produit émette une
  incertitude** (intervalle/proba), pas un point → **E1b**, non lançable en l'état.

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

## E5 — Un LLM est-il une fonction (stable) ?

`[statut:: proposée]` · Ouverte le 31/07/2026 · issue de [A4-dynamique](../theorie/A4-dynamique.md) §6

**Hypothèse** `[HYPOTHÈSE]` — Interrogé comme $f$ (« état + action → état suivant »), un LLM **n'est pas
un opérateur stable** : ses sorties varient avec le prompt/seed, donc $\operatorname{Var}_\omega[f_\omega(G,a)]$
est grande. Un objet qui répond différemment à la même question **n'est pas une fonction**.

**Falsification** — Si, sur $K$ reformulations **sémantiquement équivalentes** du même $(G,a)$, les
prédictions clés (le **signe** et l'**ordre de grandeur** des $\Delta$ sur 3–4 métriques) restent
**stables** (taux d'inversion de signe ≈ 0), alors un LLM peut servir d'opérateur approché et l'option
(b) de A4 est plus solide que je ne le crois.

**Protocole** — 1 couple $(état, action)$ réaliste (réutiliser le cas Brooks d'E4). Générer $K=10$
variantes de prompt (paraphrases, **ordre des faits permuté**, même consigne de sortie structurée).
Mesurer la dispersion des $\Delta$ prédits par métrique. **Deux régimes** : $T=0$ (déterminisme nominal —
isole la **sensibilité au prompt**) et $T>0$ (ajoute la variance d'échantillonnage). Métré `AiMeter` (**C4**).

**Métrique** — taux d'**inversion de signe** des $\Delta$ entre runs ; écart-type relatif des magnitudes ;
accord de rang (Kendall) entre les runs.

**Limite** — $T>0$ gonfle mécaniquement la variance ; c'est le run $T=0$ qui teste vraiment « fonction ou
pas ». Un accord élevé ne prouve pas que $f$ est *juste* (E3/E4 s'en chargent), seulement qu'il est *stable*.

**Coût** — ~0,5 j.

---

## E6 — Le front de Pareto des cycles passés est-il informatif ?

`[statut:: proposée]` · Ouverte le 31/07/2026 · issue de [A8-trajectoires](../theorie/A8-trajectoires.md) · **lançable sans A4/A5**

**Hypothèse** `[HYPOTHÈSE]` — Sur les cycles clôturés, avec **2–3 objectifs** mesurables, une **minorité
nette** domine → le front de Pareto est une **lentille rétrospective utile**. (À 6 objectifs il
dégénérerait — front ≈ tout — mais on n'en mesure que 2–3, ce qui **sauve** l'affaire.)

**Falsification** — Si la **fraction non dominée** (bootstrappée) est **proche de 1**, Pareto n'informe
pas à notre $(m,n)$ ; si une **minorité stable** domine, A8 tient comme lentille descriptive.

**Schéma réel** `[ÉTABLI]` — objectifs calculables : **complétion** (E2), **respect délai**
(`MAX(issues.completed_at)` du cycle vs `cycles.end_date` — ⚠️ pas de `completed_at` sur `cycles`, proxy),
**débit** (`SUM(story_points)` des issues finies). Risque/dette/stress **non mesurés** → exclus (et c'est
tant mieux : ça garde $m$ petit).

**Protocole** — filtre de **dominance** $O(n^2)$ sur les cycles clôturés (trivial à $n{\approx}20$) ;
**bootstrap** : rééchantillonner les cycles, mesurer la **fréquence de non-domination** par cycle. Aucun
LLM, aucune migration.

**Métrique** — fraction non dominée ; **stabilité au bootstrap** (un cycle « vraiment » non dominé l'est
sur ≥ X % des rééchantillons).

**Limite** — $n \approx 4$ (scénario) / peu de cycles au seed → mesure la **plomberie + la forme**, pas une
vérité (C3). Seed **synthétique**.

**Coût** — ~0,5 j (dépend d'E2 pour les objectifs). **Le seul test de frontière lançable sans rien débloquer.**

---

## E7 : Quelle part de l'attente humaine porte sur du réversible ?

`[statut:: proposée]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°1](../conseil/seances/2026-10-26-premiere-regle.md), R1

**Jalon** : J2 de la feuille de route ([séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md)) : la part des
demandes sur du réversible est l'un des signaux de l'indice de confiance (E17).

**Hypothèse** `[HYPOTHÈSE]` : au moins 30 % du temps où un agent attend une décision humaine porte sur des actions
réversibles, celles qui restent dans la branche de travail (lecture, écriture, commit local, tests).

**Falsification** : moins de 30 % de l'attente porte sur du réversible. R1 ne libère alors presque rien ; elle reste un
principe, pas un levier produit.

**Schéma réel** `[ÉTABLI]` : les demandes de validation passent par le hook `PermissionRequest` du runner, servi en
local (`taskforce-runner/src/agent.ts`) ; chaque délégation a sa chronologie dans l'app. À vérifier en mode
développement : ce que la chronologie garde de chaque demande (outil, arguments, heure de la demande, heure de la
décision).

**Protocole** : écrire d'avance la table de réversibilité (réversible : tout ce qui reste dans la branche de travail ;
irréversible : push, fusion, migration d'une base partagée, envoi externe, secret) ; classer chaque demande des
délégations réelles de Pierre pendant 10 jours ; mesurer la part du temps d'attente par classe.

**Métrique** : part du temps d'attente, et du nombre de demandes, qui porte sur du réversible.

**Limite** : une seule personne (C1), peu de délégations en 10 jours ; la table elle-même est un choix, à revoir.

**Coût** : ~0,5 j de développement (horodater les demandes, si ce n'est pas déjà fait) et 10 jours d'usage.

**Premiers relevés** (recette 1.3.2, 29/10/2026, en nombre de demandes et non en durée), d'après le
[Conseil, séance n°8](../conseil/seances/2026-10-29-recette-132.md) :
- `[ÉTABLI]` Une mission de modification d'un fichier a demandé quatre accords : deux commandes de lecture, le commit
  local, le lancement des tests. Trois portaient sur du réversible.
- `[ÉTABLI]` Une mission de recherche a demandé sept accords, tous des recherches ou des lectures d'adresses web. La table
  des règles les classe irréversibles, parce que la requête sort de la machine.
- `[DÉDUIT]` Sur la première mission, la falsification ne tient pas : 3 demandes sur 4 portent sur du réversible. R46
  (retenue le 29/10) en tire la suite : les lectures passent, le web demande un accord par mission. Les missions
  rejouées après R46 sont la mesure suivante.

---

## E8 : Des règles écrites comme du code sont-elles relues ?

`[statut:: proposée]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°1](../conseil/seances/2026-10-26-premiere-regle.md), R2

**Hypothèse** `[HYPOTHÈSE]` : les règles qui encadrent un agent, écrites dans un fichier (qui l'a décidée, pourquoi,
quand la revoir) et comptées, sont relues et ajustées ; dispersées dans le code, elles ne le sont pas.

**Falsification** : en 10 jours, le fichier n'est ni relu ni modifié, ou les compteurs ne changent aucune décision.
C'est alors de la conformité de papier.

**Schéma réel** `[ÉTABLI]` : les règles du runner sont aujourd'hui dans le code : outils autorisés d'avance
(`allowedTools`), outils refusés (`DENIED_TOOLS`), mode de permission manuel et hook de validation
(`taskforce-runner/src/agent.ts`).

**Protocole** : transcrire ces règles dans un fichier daté que le runner lit ; compter, pour chaque règle, les blocages,
les demandes de validation et les autorisations ; revue au dixième jour.

**Métrique** : relectures et modifications du fichier ; part des règles qui ont servi.

**Limite** : 10 jours ne jugent pas une règle rare. Aucune suppression sur cette seule base (charte du Conseil,
décision R2).

**Coût** : ~1 j de développement.

---

## E9 : Le temps d'attention par résultat accepté se mesure-t-il ?

`[statut:: proposée]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°1](../conseil/seances/2026-10-26-premiere-regle.md), R3

**Hypothèse** `[HYPOTHÈSE]` : le temps d'attention humaine par résultat accepté (attente d'une décision, puis relecture,
par pull request acceptée) se mesure sur l'ordinateur, sans rien envoyer, et bouge quand le harnais change. Le temps de
cycle d'une mission se mesure à côté.

**Falsification** : les données locales ne séparent pas le temps d'attention du temps d'absence (la personne est
partie), ou la mesure ne bouge pas quand R1 libère le réversible.

**Schéma réel** `[ÉTABLI]` : l'app n'envoie aucune donnée d'usage (site, `llms.txt`) ; délégations et demandes vivent
dans la base locale du compte.

**Protocole** : sur 10 jours de délégations de Pierre, horodater demande, décision, ouverture et fusion de la pull
request ; calculer les minutes d'attention par résultat accepté, le temps de cycle et les décisions regrettées
(approbations annulées, retours arrière).

**Métrique** : médiane et dispersion des trois mesures.

**Limite** : N ≈ 1 (C1) ; l'attention réelle n'est qu'approchée. L'envoi de données est hors de cette expérience
([Q10](../Questions-ouvertes.md)).

**Coût** : ~1 j de développement.

---

## E10 : Un relecteur dédié trouve-t-il de vrais défauts ?

`[statut:: proposée]` · Ouverte le 27/10/2026 · issue du [Conseil, séance n°1](../conseil/seances/2026-10-26-premiere-regle.md), R4

**Hypothèse** `[HYPOTHÈSE]` : un relecteur dédié, d'un autre fournisseur que l'agent qui a codé, avec une liste de
points à vérifier et une partie libre, trouve de vrais défauts que l'agent n'a pas vus.

**Falsification** : moins d'un défaut utile, confirmé par Pierre, sur 10 pull requests d'agent. Le coût dépasse alors le
gain à ce stade.

**Schéma réel** `[ÉTABLI]` : TaskForce délègue déjà à Claude Code et à GitHub Copilot, qui ouvrent des pull requests
liées aux issues.

**Protocole** : choisir un modèle existant reconnu en analyse (pas d'entraînement, C4) ; liste : sécurité, tests, actions
irréversibles, respect des règles du runner, données personnelles, plus une partie libre ; relecture avant celle de
Pierre sur 10 pull requests ; Pierre classe chaque remarque (vrai défaut ou bruit).

**Métrique** : vrais défauts trouvés, bruit, minutes de relecture humaine gagnées ou perdues.

**Limite** : 10 pull requests ; le jugement de Pierre sert de référence. Entraîner un relecteur maison viendra après,
si le modèle existant montre la valeur.

**Coût** : ~0,5 j de développement, plus les appels au modèle relecteur.

---

## E11 : Un petit modèle local rend-il une tâche en commentaire acceptable ?

`[statut:: proposée]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°8](../conseil/seances/2026-10-29-recette-132.md), R51 (avec R31)

**Hypothèse** `[HYPOTHÈSE]` : un petit modèle à outils, sur l'ordinateur (qwen3:8b), porté par la boucle de Cortex,
rend acceptable au moins trois tâches sur cinq dont le livrable est un commentaire : chercher et résumer, trier, rédiger.

**Falsification** : le petit modèle échoue sur trois tâches sur cinq, avec les critères écrits avant de lancer.
L'hypothèse est alors fausse pour les commentaires, et l'agent local n'est pas proposé.

**Schéma réel** `[ÉTABLI]` : deux agents de délégation existent, Claude Code par le runner local et GitHub Copilot ; aucun
ne délègue à un modèle local. La boucle de Cortex appelle déjà ses outils avec qwen3:8b dans l'app desktop. Dans la
recette 1.3.2, deux missions ont rendu leur résultat en commentaire, sans code.

**Protocole** : cinq tâches, dont les deux missions en commentaire de la recette 1.3.2 ; pour chacune, les critères
d'acceptation écrits avant de lancer ; la même tâche faite par qwen3:8b et par Claude Code ; Pierre juge chaque
résultat sans savoir lequel l'a produit, si c'est possible.

**Métrique** : tâches acceptées sur cinq, pour chaque modèle ; durée ; corrections demandées.

**Limite** : cinq tâches, une personne qui juge (C1) ; un poste avec un GPU portable de 8 Go.

**Coût** : ~1 j de développement (l'agent local comme troisième agent de délégation, par la même porte et le même dossier),
plus une demi-journée de mesure.

**L'essai de J1, écrit le 04/11/2026 avant le lancement** (R113, séance n°16 ; TF-J1-4) : la boucle minimale de
TaskForce sur la passerelle, avec qwen3:8b (Ollama, sur le poste de la Présidence). Elle lit l'issue (description, liste
de contrôle, commentaires), les autres issues de son projet et les notes que la personne peut lire, puis poste sa réponse
en commentaire. Elle n'a ni le web ni dépôt : les tâches des étapes 16 et 23 de la recette 1.3.2, qui cherchaient sur le
web, sont remplacées par deux tâches du même genre dont la matière est dans l'issue (1 et 4). Claude Code ne fait pas les
mêmes tâches dans cet essai, et le juge n'est pas à l'aveugle : c'est l'agent de développement, critère par critère. Une
tâche est réussie quand tous ses critères tiennent ; R51 tient à trois sur cinq.

Les cinq tâches, dans un projet sans dépôt (« Essai R51 ») de l'espace de démo, sur une copie de la base de dev :

1. **Résumer** : la description colle les notes de version 2.3 et 2.4 d'une API fictive. « Résume en cinq points au plus
   ce qui change pour l'équipe mobile, et dis s'il faut modifier l'app avant la mise à jour. » Critères : (a) le
   changement cassant (`/v1/orders` devient `/v2/orders`) est nommé, et la réponse dit qu'il faut modifier l'app ; (b) cinq
   points au plus ; (c) aucun changement absent des notes ; (d) en français.
2. **Trier** : six retours de la bêta, chacun avec sa personne. « Classe ces retours par thème et dis lequel traiter en
   premier, et pourquoi. » Critères : (a) trois thèmes au moins, chacun des six retours rangé ; (b) une seule priorité, la
   perte de données que deux personnes rapportent, avec une raison tirée des retours ; (c) aucun retour inventé ; (d) en
   français.
3. **Rédiger**, en anglais : la liste de contrôle porte quatre éléments faits de la version 2.4. « Write the release note
   for version 2.4 from the checklist, for our users. » Critères : (a) les quatre éléments y sont ; (b) 150 mots au plus ;
   (c) rien au-delà de la liste ; (d) en anglais ; (e) elle ne dit pas avoir publié quoi que ce soit.
4. **Faire le point sur le projet** : « Fais le point : quelles issues du projet sont bloquées, et lesquelles sont
   terminées ? » Critères : (a) les issues de la colonne Blocked, toutes et seulement elles, par leur clé ; (b) les issues
   de la colonne Done, par leur clé ; (c) aucune clé inventée ; (d) en français.
5. **Résumer un fil** : la description colle un fil de quatre messages de trois personnes sur le choix d'une base de
   données ; un commentaire y ajoute une question. « Résume la décision prise et les questions qui restent ouvertes. »
   Critères : (a) la décision du fil (rester sur PostgreSQL, pas de MongoDB) ; (b) les deux questions ouvertes (la date de
   la migration des sauvegardes, et qui la teste) ; (c) aucune décision prêtée à quelqu'un qui ne l'a pas prise ; (d) en
   français.

## E12 : Un petit modèle affiné bat-il le modèle de base avec recherche ?

`[statut:: proposée]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°10](../conseil/seances/2026-10-29-intelligence-possedee.md), R62

**Plateforme** : Kaggle, dans le compte de la Présidence (décision du 30/10/2026).

**Hypothèse** `[HYPOTHÈSE]` : affiné sur le corpus public de la banque de tests (§16.2 de la spécification), un petit
modèle ouvert répond mieux aux questions de ce corpus, avec la bonne source et la citation exacte, que le même modèle de
base avec la recherche de TaskForce.

**Falsification** : le modèle affiné ne bat pas le modèle de base avec recherche sur les évaluations écrites avant, ou il
perd sur les cas de sûreté. L'entraînement n'est alors pas promis : la boucle reste les évaluations et le choix du
modèle.

**Schéma réel** `[ÉTABLI]` : aucun entraînement ni affinage dans TaskForce, pas de GPU au labo (C4). L'app desktop fait
tourner des modèles d'Ollama. La banque de tests prévoit une famille « contexte » sur un corpus public à plusieurs
versions, et une famille « modèles ».

**Protocole** :
- Le secrétariat prépare le carnet et les évaluations ; la Présidence le lance dans son compte d'un GPU gratuit (Kaggle
  ou Colab, quotas à vérifier), puisque l'agent ne crée pas de compte.
- Un petit modèle ouvert, d'une taille que le GPU gratuit accepte, affiné en LoRA ou QLoRA, puis exporté au format
  d'Ollama.
- Trois bras sur les mêmes questions : le modèle de base seul, le modèle de base avec recherche, le modèle affiné avec
  recherche.
- Les questions, leurs sources et les cas de sûreté (demandes hors domaine ou dangereuses) sont écrits avant de lancer.

**Métrique** : réponses avec la bonne source et la citation exacte ; refus corrects sur les cas de sûreté ; durée et
mémoire sur le poste.

**Limite** : un corpus public, pas les données d'un client (C1) ; un seul modèle ; une personne qui juge.

**Coût** : 0 € de calcul ; ~1 j pour préparer le carnet et les évaluations, plus une demi-journée de mesure.

## E13 : Le spécialiste gagne-t-il du temps sur un vrai dossier ?

`[statut:: proposée]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°10](../conseil/seances/2026-10-29-intelligence-possedee.md), R63

**Hypothèse** `[HYPOTHÈSE]` : sur un dossier réel de conformité d'un produit à un standard qui évolue, un spécialiste du
partenaire de conception passe moins de temps avec TaskForce (les règles, les accords, le dossier chaîné) qu'avec sa
méthode actuelle, sans rater un point qu'elle trouve.

**Falsification** : son temps ne baisse pas, ou la revue avec TaskForce rate un point que la méthode actuelle trouve.

**Schéma réel** `[ÉTABLI]` : pas encore de partenaire de conception ; le premier cas d'usage est retenu depuis la séance
n°2 ; aucun connecteur d'outil de conformité.

**Protocole** : un dossier choisi avec le partenaire ; le temps de la méthode actuelle, chronométré ou relevé sur le
dernier dossier comparable ; le même type de dossier dans TaskForce ; les points trouvés de chaque côté, comparés par le
spécialiste.

**Métrique** : le temps du spécialiste ; les points trouvés et ratés ; le nombre de demandes de décision.

**Limite** : un dossier, un spécialiste ; aucun tirage au sort possible (C1, C2).

**Coût** : le temps du partenaire ; ~1 j de préparation.

## E14 : La promesse se redit-elle en une phrase ?

`[statut:: proposée]` · Ouverte le 29/10/2026 · issue du [Conseil, séance n°10](../conseil/seances/2026-10-29-intelligence-possedee.md), R65

**Hypothèse** `[HYPOTHÈSE]` : après la même présentation de deux minutes, au moins trois personnes de la cible sur cinq
redisent la promesse en une phrase juste, pour l'une des deux formules : « posséder son intelligence », ou
« infrastructure de conformité native IA ».

**Falsification** : moins de trois sur cinq, pour les deux formules. Le site ne change pas.

**Schéma réel** `[ÉTABLI]` : aucun entretien mené ; le site ne porte aucune des deux formules. Les mots de la cible,
d'après la Présidence (30/10/2026) : audit, traçabilité, IQ, OQ, PQ, réglementation, référentiel.

**Protocole** : cinq personnes de la cible, dont un spécialiste de la conformité et un responsable ; les deux formules,
dans un ordre tiré au sort ; on note la phrase redite, mot pour mot.

**Métrique** : phrases justes sur cinq, par formule.

**Limite** : cinq personnes, que la Présidence recrute.

**Coût** : ~2 h d'entretiens.

## E15 : La voix se transcrit-elle sur la machine, juste et vite ?

`[statut:: proposée]` · Ouverte le 30/10/2026 · issue du [Conseil, séance n°13](../conseil/seances/2026-10-30-atelier-ecrans-base.md), R80

**Hypothèse** `[HYPOTHÈSE]` : dans l'app desktop, un modèle de transcription qui tourne sur l'ordinateur comprend les
commandes qu'on dit à TaskForce avec moins d'une erreur sur dix mots, et rend le texte en moins de deux secondes après
le second clic sur le micro, sans service en ligne ni coût (R62).

**Falsification** : une erreur ou plus sur dix mots, ou plus de deux secondes, sur la machine de la Présidence. La voix
de l'app desktop passe alors par le navigateur, comme dans la webapp, avec la phrase qui le dit.

**Schéma réel** `[ÉTABLI]` : aucune voix dans le code au 30/10/2026 ; la barre écrite existe (R76, #444). Dans la
webapp, la voix passera par le service de reconnaissance du navigateur : TaskForce n'en reçoit que le texte.

**Protocole** : vingt commandes, dix en français et dix en anglais, prises dans les suggestions de la barre et dans les
demandes gardées aux dossiers (« Create an issue… », « Which issues are blocked? »), dites par la Présidence sur sa
machine ; le texte rendu comparé mot pour mot au texte dit.

**Métrique** : l'erreur par mot (WER) sur les vingt commandes, et le délai entre le second clic et le texte affiché.

**Limite** : une seule voix et une seule machine ; le modèle de transcription reste à choisir.

**Coût** : ~1 j (le modèle sur la machine, puis la mesure).

## E16 : Une seule source pour le moteur de règles, sans aller-retour ?

`[statut:: faite]` · Ouverte le 01/11/2026 · Faite le 02/11/2026 · issue du [Conseil, séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md), R90 (à l'essai) · résultats [plus bas](#résultats-du-02112026)

**Hypothèse** `[HYPOTHÈSE]` : l'une de deux voies supprime le double moteur sans gêner l'agent.
- **(a) Le runner demande chaque décision au backend Java de la machine.** Le surcoût reste sous 10 ms au 95e centile,
  quand une action de Claude Code prend plusieurs secondes.
- **(b) Le moteur Java, compilé en JavaScript** (TeaVM ou J2CL), tourne dans le runner, sans aller-retour, et passe les
  51 cas partagés.

**Falsification** : les deux voies échouent.
- (a) dépasse 10 ms au 95e centile, ou bloque l'agent quand le backend redémarre.
- (b) ne compile pas le moteur, ou échoue à un cas.

Le double moteur reste alors, protégé par les cas partagés, comme la Présidence l'a accepté.

**Schéma réel** `[ÉTABLI]` :
- `RulesEngine`, `Glob` et `RulesDigest` en Java, environ 200 lignes ;
- `rules.ts` et `glob.ts` dans le runner, environ 185 lignes ;
- 51 cas dans `contracts/rules/cases.json`, rejoués par la CI des deux côtés.

Dans l'app desktop, le backend et le runner tournent sur la même machine.

**Protocole** :
1. Une mission réelle de Claude Code, jouée deux fois : décisions prises dans le runner, puis demandées au backend. On
   mesure le délai de chaque décision et la durée totale.
2. Le moteur Java compilé en JavaScript, branché sur les 51 cas.

**Métrique** : le délai de décision (médiane, 95e centile), les cas passés, la taille du code produit.

**Limite** : une machine, une mission ; la version hébergée, avec un serveur distant, n'est pas mesurée.

**Coût** : ~1 j.

### Résultats du 02/11/2026

**Verdict** :
- `[ÉTABLI]` (a) tient le seuil de latence sur la topologie de l'app (Java natif), mais l'agent n'a plus aucune décision
  pendant chaque redémarrage du backend : elle est réfutée par son second critère.
- `[ÉTABLI]` (b) compile le moteur et passe les 84 cas partagés d'aujourd'hui (22 motifs, 60 décisions, 2 empreintes) :
  elle n'est pas réfutée.
- `[ÉTABLI]` Les décisions se compilent sans rien changer ; l'empreinte a demandé trois lignes changées dans
  `EvidenceChain` et deux classes du JDK fournies à TeaVM.
- `[DÉDUIT]` L'hypothèse tient par (b) : une seule source Java, compilée pour le runner, sans aller-retour.

**Décision de la Présidence (02/11/2026)** : « on adopte R90 (b) ». Le moteur Java, compilé en JavaScript, remplace
le moteur TypeScript du runner (TF-J1-1, [ADR-025](../decisions/ADR-025-DRAFT-un-seul-moteur-de-regles.md)).

**Code et machine** `[ÉTABLI]` :
- branche `exp/e16-single-engine` de taskforce-fullstack, sans pull request, partie d'`origin/dev` le 01/11 puis
  fusionnée avec `origin/dev` le 02/11 (`cbf22ac6` : la porte de #467, la table de 36 règles) ; on y trouve l'endpoint
  `POST /api/delivery/runner/rules/decide` (authentifié comme les autres routes du runner), les bancs dans
  `experiments/e16-single-engine/bench`, le module TeaVM dans `experiments/e16-single-engine/teavm` et les chiffres bruts
  dans `experiments/e16-single-engine/results` ;
- Intel Core 7 240H (10 cœurs, 16 fils), 31,6 Go, Windows 11 Home 10.0.26200, sur secteur, mode d'alimentation
  « Équilibré » ;
- Node 24.18.0, TeaVM 0.16.0, Jackson 2.21.4 ;
- le backend de la branche en profil `desktop`, avec les options Java de l'app (`-XX:TieredStopAtLevel=1`,
  `-XX:+UseSerialGC`, `-Xmx768m`), sur sa propre base PostgreSQL 18 (pgvector), à côté du backend de dev ;
- « natif » : le Java de l'app desktop installée (Temurin 21.0.12.1), sur 127.0.0.1, comme dans l'app ;
- « conteneur » : le Java de l'image du backend de dev (Temurin 21.0.13), port publié par Docker Desktop 29.7.2 (WSL2).

**La suite rejouée** `[ÉTABLI]` :
- les 43 lignes « Rule decision » du journal du runner de l'app : trois missions (29/10 à 13:16 et à 13:24, 01/11 à
  14:33), 451 s de travail en tout, une décision toutes les 4 s en médiane (de 0 à 100 s) ;
- le journal garde l'outil, l'effet et la règle, pas l'entrée : chaque entrée est reconstituée, et le runner
  d'aujourd'hui la décide comme le journal, sauf cinq lectures du shell (`ls`, `cat`, `wc`) que la règle `run-reads`,
  ajoutée depuis, autorise au lieu de les demander ;
- sous la table de 36 règles : 27 actions autorisées, 16 demandées, aucune refusée ;
- chaque passe compare le backend et le module JavaScript au runner : aucun écart.

**(a) La décision demandée au backend** `[ÉTABLI]`, en millisecondes sauf mention :

| Mesure | Natif, passe 1 (`a-native`) | Natif, passe 2 (`a-native-2`) | Conteneur (`a-container`) |
| --- | ---: | ---: | ---: |
| Démarrage jusqu'à `/readyz` (3 démarrages) | 19,4 à 21,0 s | 19,2 à 22,8 s | 20,9 à 22,4 s |
| Première décision après un démarrage | 37 à 52 | 43 à 52 | 49 à 57 |
| Premier passage après démarrage, 129 décisions : médiane / 95e centile | 5,2 / 8,0 | 4,9 / 8,4 | 6,6 / 11,7 |
| À chaud, connexion gardée, 8 600 décisions : médiane / 95e / 99e centile | 1,12 / 2,16 / 2,85 | 1,54 / 2,79 / 3,47 | 3,13 / 5,66 / 8,76 |
| À chaud, connexion neuve, 860 décisions : médiane / 95e centile | 2,01 / 3,09 | 2,21 / 3,20 | 3,80 / 5,26 |
| Au rythme du journal (écarts plafonnés à 5 s), 43 décisions : médiane / 95e centile | 1,89 / 2,97 | 2,07 / 3,11 | 3,82 / 29,13 |
| Redémarrage : temps sans décision | 19,9 s | 22,0 s | 22,6 s |
| Redémarrage : décisions refusées (une tentative toutes les 50 ms) | 315 | 347 | 355 |
| Processeur de la machine occupé (tout compris) pendant la passe à chaud | 41 % | 59 % | 69 % |
| Build Maven d'une autre session pendant la passe | non | à la fin | du début à la fin |

Repères, sur la même machine :
- `[ÉTABLI]` Le moteur du runner, en TypeScript, dans trois processus neufs : 0,003 à 0,004 ms en médiane et 0,006 à
  0,008 ms au 95e centile à chaud ; 0,08 à 0,09 ms au 95e centile au premier passage.
- `[ÉTABLI]` Les faits (`toolFacts`), calculés par le runner dans les deux voies : 0,25 à 0,27 ms au 95e centile.
- `[ÉTABLI]` La boucle locale seule (un serveur Node minimal, le même client, mesure du 01/11) : 0,047 ms en médiane et
  0,135 ms au 95e centile, connexion gardée.
- `[ÉTABLI]` Le 01/11, avec la table de 35 règles et une machine moins chargée (48 %), le conteneur restait sous le
  seuil : 6,5 ms au 95e centile au premier passage, 3,4 ms au rythme du journal (historique de la branche, `efb58712`).
- `[ÉTABLI]` Dans l'app desktop installée, le backend a mis 13,4 à 76,2 s à démarrer (19,8 s en médiane, 38,7 s au 95e
  centile), sur 28 démarrages du 19/10 au 02/11/2026 (journal de l'app).

Ce que disent ces chiffres :
- `[ÉTABLI]` En natif, comme dans l'app, le seuil tient partout : le pire 95e centile est de 8,8 ms, sur les 43
  premières décisions après un redémarrage.
- `[ÉTABLI]` En conteneur, sous la charge d'un autre build, il casse : 11,7 ms au premier passage, 29,1 ms au rythme du
  journal.
- `[ÉTABLI]` La toute première décision après chaque démarrage dépasse le seuil partout : 37 à 59 ms.
- `[DÉDUIT]` Sur les trois missions, 43 décisions à environ 5 ms ajoutent 0,2 s à 451 s de travail : l'agent ne le sent
  pas.
- `[ÉTABLI]` Pendant un redémarrage, aucune décision n'arrive pendant 19,9 à 22,6 s ; chaque tentative échoue vite, en
  1,8 à 3,3 ms au 95e centile (connexion refusée, ou coupée par Docker Desktop).
- `[ÉTABLI]` Les jetons du runner ne survivent pas au redémarrage : il en redemande un (une réponse 401 par passe).
- `[DÉDUIT]` Avec la règle de R90 (sans réponse, l'action est refusée), chaque action de l'agent est refusée pendant ce
  temps : c'est le second critère de falsification.
- `[DÉDUIT]` (a) n'est pas seule en cause : 27 des 43 actions passent déjà par le backend (16 demandes d'accord, 11 outils
  TaskForce par son serveur MCP) ; (a) y ajoute les 16 autres (lectures, écriture dans la copie, git, outils internes).
- `[ÉTABLI]` Dans l'app, la coque démarre et arrête le runner avec le backend (`desktop/src/stack.ts`).
- `[DÉDUIT]` Un redémarrage du backend seul, mission en cours, vient donc d'une panne.

**(b) Le moteur Java compilé en JavaScript par TeaVM 0.16.0** `[ÉTABLI]` :

| Mesure | Décisions seules (`decisions.js`) | Moteur entier (`rules-engine.js`) |
| --- | --- | --- |
| Sources du serveur changées | aucune | `EvidenceChain`, trois lignes |
| Classes du JDK fournies à TeaVM | aucune | `MessageDigest` (SHA-256), `HexFormat` |
| Cas passés | 82 sur 82 (sans les 2 empreintes) | 84 sur 84 |
| Taille brute / gzip / brotli | 135 655 / 43 131 / 35 727 octets | 391 527 / 126 215 / 101 098 octets |
| Chargement du module dans Node | 45 ms | 87 ms |
| Décision à chaud : médiane / 95e centile | 0,002 / 0,004 ms | 0,002 / 0,004 ms |
| Premier passage : 95e centile / maximum | 0,18 / 4,0 ms | 0,23 / 4,4 ms |

- `[ÉTABLI]` Le module lit `RulesEngine`, `Glob`, `RulesBundle`, `RulesDigest`, `CanonicalJson` et `EvidenceChain` dans
  `backend/tf-api`, sans copie ; lui sont propres l'adaptateur, qui lit les objets JavaScript (233 lignes), les deux
  classes fournies à TeaVM et leur règle de substitution (183 lignes).
- `[ÉTABLI]` La fusion du 02/11 n'a touché aucune de ces sources : la table et les cas se lisent à l'exécution, le même
  module passe les cas d'hier (71) et ceux d'aujourd'hui (84).
- `[ÉTABLI]` Sans changement, TeaVM refuse l'empreinte : `java.security.MessageDigest` lui manque
  (`EvidenceChain.sha256`), et le champ statique `ObjectMapper` d'`EvidenceChain` construit tout Jackson, qui demande
  `ReentrantLock`, puis `ConcurrentLinkedQueue`.
- `[ÉTABLI]` Aucune de ces classes, ni `HexFormat`, n'est dans la bibliothèque de TeaVM 0.16.0 (1 510 classes).
- `[ÉTABLI]` Le correctif : `EvidenceChain` crée ses événements par `JsonNodeFactory` au lieu d'un `ObjectMapper` (même
  résultat ; les tests du serveur qui touchent la chaîne passent, 271 avant la fusion et 132 après) ; le module fournit
  `MessageDigest` (SHA-256 en Java pur) et `HexFormat` par la substitution de classes de TeaVM.
- `[ÉTABLI]` Compilé, le moteur Java décide en 2 µs en médiane et 4 µs au 95e centile, contre 3 à 4 µs et 6 à 8 µs pour
  celui du runner.
- `[ÉTABLI]` TeaVM ayant abouti, J2CL n'a pas été essayé.

**Contre les critères de falsification** :
- `[ÉTABLI]` (a), sous 10 ms au 95e centile : oui en natif (8,8 ms au pire), non en conteneur sous charge (29,1 ms au
  rythme du journal). Bloque l'agent quand le backend redémarre : oui, 19,9 à 22,6 s sans décision mesurés, pour un
  démarrage de 13,4 à 76,2 s dans l'app. (a) est réfutée.
- `[ÉTABLI]` (b), compile le moteur : oui, après les trois lignes d'`EvidenceChain` et les deux classes fournies ; sans
  elles, les décisions seulement. Échoue à un cas : non, 84 sur 84. (b) n'est pas réfutée.
- `[DÉDUIT]` Les deux voies n'échouent pas ensemble : la condition qui gardait le double moteur n'est pas remplie.

**Ce que la mesure ne dit pas** :
- `[ÉTABLI]` Une machine, chargée par les builds d'autres sessions pendant une partie des passes, et trois missions
  reconstituées, pas rejouées par Claude Code.
- `[ÉTABLI]` Le prototype (a) décide avec la table par défaut et n'écrit pas la chaîne de preuve, que R90 écrivait à
  chaque décision.
- `[DÉDUIT]` Écrire un événement en base à chaque décision ajouterait une transaction PostgreSQL à chaque aller-retour.
- `[ÉTABLI]` (b) n'est pas branché dans le runner : `rules.ts` et `glob.ts` décident toujours.
- `[HYPOTHÈSE]` Une évolution du moteur Java peut appeler une classe que TeaVM n'a pas : la CI devrait compiler le module
  et rejouer les cas sur le JavaScript produit à chaque changement.
- `[HYPOTHÈSE]` Le module contient déjà `CanonicalJson` et l'empreinte SHA-256 de la chaîne : la vérification d'un
  dossier (`evidence.ts`, `verify.ts`) pourrait passer par lui aussi, à essayer.

**Ce que ça change pour R90** :
- `[DÉDUIT]` (b) donne la source unique sans aller-retour que la Présidence cherchait : le runner décide sur place, avec
  le code Java du serveur, et ne dépend du backend que pour ce qui en dépendait déjà.
- `[ÉTABLI]` En échange, une étape de build (Maven et TeaVM : 21 s ici pour les deux modules) et un module de 136 à
  392 Ko dans le runner.
- `[ÉTABLI]` La Présidence tranche R90 sur ces chiffres (séance n°15).

**Coût réel** `[ÉTABLI]` : ~0,6 j, sur deux jours (01/11 puis 02/11, après la fusion de `origin/dev`).

## E17 : L'indice de confiance se mesure-t-il, et monte-t-il ?

`[statut:: proposée]` · Ouverte le 01/11/2026 · issue du [Conseil, séance n°15](../conseil/seances/2026-11-01-feuille-de-route.md), R104

**Hypothèse** `[HYPOTHÈSE]` : les neuf signaux de l'indice de confiance (PV n°15) se mesurent à partir des dossiers et
des journaux, sans questionnaire, sauf le retour des personnes extérieures. Chacun progresse d'un jalon à l'autre à
partir de J2.

**Falsification** : un signal qu'on ne sait pas mesurer à J2, ou un signal qui recule deux jalons de suite (le signal
d'arrêt de R104).

**Schéma réel** `[ÉTABLI]` : les dossiers de mission gardent les décisions, les accords et les tests ; aucun des neuf
signaux n'est calculé aujourd'hui. Depuis TF-J1-8 (R116, `taskforce-fullstack` #483, pas encore fusionnée), chaque
phrase de Cortex que TaskForce remplace, parce qu'elle annonçait une action sans son résultat d'outil, entre au dossier
de la réponse comme incident de confiance : un événement `note` signé du serveur (`incident: trust`, `experiment: E17`),
avec la phrase fausse, ce que TaskForce a montré et les outils du tour. Ces incidents se comptent depuis les dossiers,
sans questionnaire ; la personne, elle, ne voit plus la phrase fausse.

**Protocole** : la mesure de départ à la fin de J2, sur la boucle mince (deux packs), avec les seuils écrits avant
(Duflo) ; puis la même mesure à chaque jalon, publiée au Journal.

**Métrique** : les neuf signaux, chacun avec son seuil.

**Limite** : peu de missions avant J8, et trois personnes extérieures par jalon.

**Coût** : ~1 j pour la mesure de départ, puis ~2 h par jalon.

**Incidents relevés avant la mesure de départ** `[ÉTABLI]` :
- 01/11/2026, mission 6 du rejeu de J0 sur l'app desktop : deux lectures de nodejs.org que la table disait « demander »
  sont passées sans question, la porte laissant la décision aux permissions de Claude Code. Corrigé par R107 et R108,
  publiés avec la 1.8.0 le 02/11/2026 ([séance n°16](../conseil/seances/2026-11-01-revue-j0.md)).
- 02/11/2026, app desktop 1.6.0, Cortex sur qwen3:8b : à « What changed in this project this week? », Cortex répond « La
  carte TESTTA-2 a été supprimée du projet test-taskforce. » alors qu'aucune suppression n'a eu lieu (son seul outil du
  tour : `list_issues`). Une IA qui dit avoir fait ce qu'elle n'a pas fait. Juste avant, sans outil de suppression,
  il avait préparé une carte de création titrée « Supprimer l'issue TESTTA-2 ». Réponse : R116 (séance n°17), dans
  #483 ; les six échanges sont des cas de la banque (R118). Rejoués sur qwen3:8b sur une copie de la base de dev, une
  note dite « créée » sans outil atteignait encore la personne avant R116 ; après, TaskForce la remplace et l'incident
  est au dossier.

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [❓ Questions](../Questions-ouvertes.md) · [📖 Notes critiques](../revues/World-Model.md)

**Dernière mise à jour :** 02/11/2026 · **v1.5** · Projet Taskforce, Metz Numeric School 2025-2026
