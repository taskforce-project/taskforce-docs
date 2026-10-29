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

---

**Points d'entrée :** [🔬 R&D](../README.md) · [🤖 Mode recherche](../CLAUDE.md) · [❓ Questions](../Questions-ouvertes.md) · [📖 Notes critiques](../revues/World-Model.md)

**Dernière mise à jour :** 29/10/2026 · **v1.1** · Projet Taskforce, Metz Numeric School 2025-2026
