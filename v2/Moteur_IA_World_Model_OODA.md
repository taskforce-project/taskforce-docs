# Moteur IA — World Model × OODA (v2)

> **Statut : conception (v2, non implémenté).** Étend la vision [[IDEA]] (« AI Delivery Operating System ») avec l'architecture du **moteur de décision IA**. Rien ici n'est codé — c'est la cible. Format Obsidian, à démontrer avant de marquer « fait ».
> Issu du brainstorm du 07/07/2026.

---

## 1. Principe fondateur : l'orchestration est le moat

Reprise de [[IDEA]] : l'avantage concurrentiel ne dépend **pas du modèle** (Claude/GPT/Gemini/open source = commodité interchangeable) mais du **moteur d'orchestration piloté par le [[Brain_OS]]**. Le modèle exécute ; TaskForce oriente, découpe, décide, valide, mémorise.

Conséquence directe sur l'archi : **on investit dans l'indexation du Brain OS et la boucle de décision, pas dans la taille du modèle.**

---

## 2. Retrieval-first : petit modèle + Brain OS ultra-indexé

- Un petit modèle (7–14B) est **faible en connaissance**, **moyen en raisonnement**.
- Le Brain OS (knowledge graph + embeddings) **injecte exactement le bon contexte** → le petit modèle « sait » sur *notre* domaine.
- **« Contexte élevé » = retrieval + compression intelligente**, PAS une grosse fenêtre (une fenêtre pleine de bruit rend un petit modèle *plus* bête).
- Limite honnête : le retrieval ne règle pas le **raisonnement multi-étapes complexe** → on **décompose** la tâche (graph d'étapes simples) ou on **monte en modèle** pour ces étapes (cf. §3).

> C'est **le** levier : un 7B bien nourri par le Brain OS sort du travail de 70B sur notre périmètre.

---

## 3. Modèles : stratégie hybride (⚠️ benchmark à faire)

| Usage | Modèle | Pourquoi |
|---|---|---|
| Volume (extraction, routing, résumé, tags, embeddings) | **petit** (Groq / local) | rapide, quasi gratuit |
| Raisonnement dur (découpage projet, décisions C-level) | **fort** (hosted) | qualité de raisonnement |
| « Notre modèle » (étape 2) | **fine-tune LoRA/QLoRA** d'un petit open model sur notre domaine | différenciant, GPU modeste |

- ⚠️ **« Gratuit » = pas de coût d'API**, mais **coût GPU** si self-host (VRAM). Groq est déjà branché (`GROQ_API_KEY`) → point de départ sans hardware.
- ❌ Foundation from-scratch = hors sujet. ❌ JEPA entraîné = recherche (cf. §4).
- ▶ **TODO** : `Benchmark_Modeles_IA.md` (coût / latence / qualité sur nos tâches réelles).

---

## 4. La boucle de décision : World Model × OODA

Deux cadres **complémentaires**, pas concurrents :
- **OODA** (Boyd) = le **tempo** : Observe → Orient → Decide → Act. Décision rapide + feedback actif ; qui cycle plus vite « prend l'ascendant ».
- **World Model** (esprit LeCun, version pragmatique) = l'**intelligence dans `Orient`** + l'**apprentissage** qui améliore chaque cycle.

### Couplage
| Phase OODA | Ce qui s'y passe | World Model |
|---|---|---|
| **Observe** | signaux : état projet, GitHub (PR/CI), Brain OS | — |
| **Orient** ⭐ | synthèse des observations via le modèle prédictif **+ expériences passées** | **le monde-modèle vit ici** |
| **Decide** | l'agent propose une décision **assortie d'une prédiction des conséquences** | **Predict** |
| **Act** | exécution — **human-in-the-loop = le gate** (Approve/Reject/Retry) | Act |
| *(bouclage)* | observer le **résultat réel** → comparer à la prédiction → stocker l'**écart** | **Observe + Reflect** |

### Ce que ça donne
1. **Predict** : avant d'agir, prédire ("créer ces 5 issues → +2 sem sur le jalon, dépendance sur X, risque Y"), en sortie structurée.
2. **Act** : exécuter (validation humaine).
3. **Observe + Reflect** : comparer prédit vs réel, **stocker l'écart dans le Brain OS** comme *expérience*.
4. Les `Orient`/`Predict` futurs **retrouvent** ces écarts → l'agent devient **« habile »**.

→ World model **basé mémoire/retrieval** (lignée *Reflexion / Voyager / Generative Agents*), **sans gradient**. Capture ~80 % de l'idée de LeCun sans rien entraîner.
→ **Tempo (OODA) + apprentissage (World Model) = rapide ET qui s'améliore.**

---

## 5. Agents C-level

- Chaque agent = **rôle** (CTO / CFO / COO / …) + **outils** + **accès Brain OS scopé**, qui tourne la boucle §4.
- Émet une **liste de décisions** à chaque granularité : **issue → projet → entreprise**.
- ⚠️ Les multi-agents **dérapent** (boucles, décisions hallucinées, coût). Garde-fous :
  - décisions **proposées, jamais auto-exécutées** sur le critique,
  - **human-in-the-loop**,
  - **commencer avec 3 agents** (CPO / CTO / COO), pas 8.
- ▶ **Définis en détail dans [[Agents_C_Level]]** (rôles, observe/décide/prédit, outils, garde-fous).

---

## 6. Human-in-the-loop

- Le **gate** est à `Act` : `Approve / Reject / Retry / Edit Prompt` (cf. [[IDEA]] « Validation »).
- Doit être **rapide** pour ne pas casser le tempo OODA (validation en un clic, résumé + risques pré-calculés).

---

## 7. Accès au Brain OS — **DÉCIDÉ (07/07) : personne ne le voit**

Le **Brain OS est un moteur interne, invisible à l'utilisateur.** Pas de « vue Brain OS » dans le produit.
- Ce qu'il contient (embeddings, délibérations d'agents, *expériences*/écarts de prédiction, world-model mémoire) = **cuisine interne** → jamais exposé. Protège le moat **et** évite tout risque de fuite inter-workspace / de « raisonnement à moitié cuit » montré à l'utilisateur.
- **L'explicabilité passe par les objets produit**, pas par le Brain : l'utilisateur voit des **décisions**, des **specs**, des **docs générées**, un **résumé + risques** au moment du human-in-the-loop. Ce sont des objets produit *dérivés* du Brain, avec leur propre cycle de vie — pas le Brain lui-même.
- **Isolation interne** quand même stricte : le moteur scope tout par workspace (1 workspace = 1 brain) pour ne pas contaminer le raisonnement d'un workspace avec un autre.

> Formule : *le Brain OS est le moteur ; l'utilisateur voit la route, jamais le moteur.*
▶ **ADR à écrire** dans `v1/12-decisions/` (« Brain OS interne, non exposé »).

---

## 8. TODO / threads ouverts

- [ ] `Benchmark_Modeles_IA.md` (§3)
- [ ] ADR « World Model × OODA » + ADR « Accès Brain OS » (§7)
- [ ] Refonte agents C-level + indexation Brain OS (§5)
- [ ] Schéma DB des « expériences » (reflect) : format d'une prédiction, d'un écart, rattachement aux nodes Brain OS
- [ ] Voir [[Roadmap_v2]] pour le séquencement et la tranche PFR
