# Agents C-level (v2)

> **Statut : conception (v2, non implémenté).** Détaille les 3 agents spécialisés qui tournent la boucle [[Moteur_IA_World_Model_OODA]] (§4-5). Décidé le 07/07/2026 : **3 agents** pour le cœur *delivery* ; le « board » est extensible ensuite (CFO, CISO… au niveau entreprise).
> Garde-fou transverse : **décisions PROPOSÉES, jamais auto-exécutées** sur le critique · **human-in-the-loop** au gate `Act` · commencer avec ces 3, pas plus.

---

## Pourquoi ces 3 (et pas 8)

TaskForce = **AI Delivery OS** (livrer un produit logiciel). Le trio couvre les 3 questions de toute livraison : **quoi** (produit), **comment** (technique), **quand/à quel coût/risque** (delivery). Le finance/sécu (CFO/CISO) sont des extensions *entreprise*, pas le cœur du PFR.

Chaque agent :
- observe (`Observe`) un périmètre, s'oriente via le Brain OS (`Orient`),
- **propose** des décisions **assorties d'une prédiction** (`Decide`/Predict) à 3 granularités : **issue → projet → entreprise**,
- ne s'exécute qu'après validation humaine (`Act`), puis on mesure l'écart (`Reflect`).

---

## 🧭 1. CPO — Chief Product Officer (le « quoi »)

| | |
|---|---|
| **Rôle** | Transforme une **intention** en produit découpé : vision → specs → épics → issues, critères d'acceptation, priorisation. |
| **Observe** | intention utilisateur, feedback, état du backlog, specs existantes (Brain OS) |
| **Décide (propose)** | découpage en cycles/jalons/issues · rédaction spec + critères d'acceptation par issue · priorité/valeur · prompt d'exécution IA |
| **Prédit** | « ce découpage → N issues, X j de charge, dépendances Y, valeur métier Z » |
| **Outils** | retrieval Brain OS, génération structurée (spec/issues), lien vers CTO pour la faisabilité |
| **Garde-fous** | ne crée rien sans validation · pas de priorisation « business-critique » auto |

## 🏗️ 2. CTO — Chief Technology Officer (le « comment »)

| | |
|---|---|
| **Rôle** | Faisabilité et cohérence technique : architecture, DB/API design, risques techniques, revue de PR/diff, dette. |
| **Observe** | spec (du CPO), code/état repo GitHub (PR, CI, structure), Architecture/Modules du Brain OS |
| **Décide (propose)** | choix d'archi/pattern · découpage technique d'une issue · alerte dette/risque · verdict de revue (PR : approve/changes) |
| **Prédit** | « ce choix → impact perf/coût/dette X, risque de régression Y, temps Z » |
| **Outils** | retrieval Brain OS (archi/API), lecture GitHub (repos/PR/CI — déjà branché), analyse de diff |
| **Garde-fous** | ne merge/écrit jamais sur GitHub sans validation · signale les risques, ne les tranche pas seul |

## 📦 3. COO — Chief Delivery Officer (le « quand / risque »)

| | |
|---|---|
| **Rôle** | Pilote la **livraison** : planning (cycles/jalons), capacité, dépendances, risque, timeline. **C'est lui qui incarne le plus la boucle World Model × OODA** (prédire les conséquences delivery). |
| **Observe** | vélocité, charge, dépendances inter-issues, blocages, écarts passés (expériences Reflect) |
| **Décide (propose)** | replanification · ré-assignation/rééquilibrage · alerte de dérive de jalon · décision « go/no-go » d'un checkpoint |
| **Prédit** | « si on fait X → +2 sem sur le jalon, goulot sur Y, risque de dérive Z » → **c'est CETTE prédiction qu'on compare au réel pour apprendre** |
| **Outils** | retrieval Brain OS (historique/expériences), données projet (cycles/issues/worklogs), redistribution existante |
| **Garde-fous** | propose la replanif, ne l'impose pas · human-in-the-loop sur tout arbitrage |

---

## Orchestration

- **Séquence type** (création de projet) : CPO découpe → CTO valide la faisabilité + affine le technique → COO planifie + prédit la timeline → **l'humain valide** → exécution (Claude) → Reflect (COO mesure l'écart timeline, CTO l'écart technique).
- **Conflits d'agents** : un **arbitre** (règles simples ou l'humain) tranche ; on ne laisse pas 3 LLM « débattre » en boucle (coût + dérive).
- **Coût** : n'appeler un agent que sur les événements qui le concernent (pas les 3 à chaque micro-action).

## Extensions (post-PFR)
CFO (coût/budget projet & entreprise) · CISO (sécurité/conformité) · agents *métier* injectés selon le domaine du workspace. Voir [[Roadmap_v2]].
