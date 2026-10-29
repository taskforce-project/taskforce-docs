# Data Flywheel & Apprentissage — RAG aujourd'hui, LoRA demain (sur TON corpus)

> **Principe** : on **n'entraîne rien aujourd'hui**. On fait du **RAG** (meilleur ROI) et on **collecte
> le bon corpus** pour, plus tard, un **LoRA de préférences** spécifique au produit. Le LLM local
> (Qwen) ne battra jamais les modèles frontière — inutile de viser ça. Le moat = l'**orchestration**
> (Brain OS) + un **corpus produit** que personne d'autre n'a.

Lié à : [[Moteur_IA_World_Model_OODA]] (jambe *feedback/reflect*) · [[Roadmap_Consolidee]] (Phase B/C).

## 1. Le constat (pourquoi on ne fine-tune pas maintenant)

Un modèle comme Claude/GPT est bon parce qu'après le pré-entraînement (prédire le mot suivant), il subit
un **SFT** (réponses de référence écrites par des humains) puis un **RLHF** (les humains classent A vs B →
le modèle apprend une **préférence**, pas juste du texte). On ne reproduira pas ça à la main. **Mais** on
peut fabriquer, au fil de l'usage, exactement le carburant d'un RLHF/LoRA : des paires *(généré, corrigé)*
avec un **signal de préférence**.

## 2. L'échelle (du moins cher au plus cher)

| Niveau | Quoi | Coût | Statut |
|---|---|---|---|
| **1 — RAG** | Aucun entraînement ; on donne un meilleur **contexte** via retrieval (Brain OS bge-m3). | ~0 | ✅ **en place** — meilleur ROI |
| **2 — LoRA** | Petit **adaptateur** entraîné sur TON corpus (le style « spec BrainOS », le niveau de détail que TES users préfèrent). | GPU cloud / bonne machine | 🔜 **quand le corpus existe** |
| **3 — Full fine-tuning** | Tous les poids réécrits. | dizaines de GPU, cher | ❌ hors scope projet |

**Le LoRA n'a d'intérêt qu'avec un corpus réel** (sinon on apprend du bruit). D'où : **collecter d'abord**.

## 3. Le flywheel : ce qu'une capture garderait

À **chaque point human-in-the-loop**, une capture garderait le quintuplet :

1. **Requête** utilisateur (l'issue, le prompt, la question) ;
2. **Contexte retrieved** (les nodes Brain OS servis par le retriever) ;
3. **Réponse générée** (le *draft* Qwen) ;
4. **Réponse finale réellement utilisée** (après édition humaine) ;
5. **Signal** : `accepté` | `édité` | `rejeté` (+ *edit distance* draft→final).

> **1er point de collecte = la génération de spec** (déjà construite, Phase B) : on a **déjà** le draft
> (`IssueSpecDraft`) *et* le contenu final approuvé (`ApproveSpecRequest`). La **trace** a été construite puis
> retirée (§5). Points suivants : réponses de l'agent (`AssistantAnswer`), smart-assign, décisions OODA.

## 4. La boucle auto-améliorante (le vrai potentiel)

En étendant le signal au **downstream** du prompt d'exécution :

```
Issue → Qwen propose spec+prompt → l'humain édite/valide (signal 1)
      → Claude Code implémente → PR → l'humain accepte/réécrit (signal 2)
      → mesures : temps gagné ? bug introduit ? réécriture ? → score
```

Après quelques mois : **des dizaines de milliers d'exemples** où l'on sait *ce qui a été accepté, édité,
rejeté, corrigé*. C'est **exactement** un dataset de **préférences** (type DPO) — le carburant d'un LoRA
qui apprend « chez BrainOS, une bonne spec ressemble à ça ».

## 5. Concret : la première brique, construite puis retirée (`ai_generations`)

> ⚠️ **Retirée le 18/10/2026** (`taskforce-fullstack`, commit `5700e4b1`, « refactor(ai): remove the ai_generations
> capture »). La capture du 02/09/2026 (`TF-FLYWHEEL-01`, migration V81) ne s'écrivait que pour un espace où
> `ai_learning_enabled` était vrai, et rien ne pouvait le mettre à vrai : ni route, ni écran. La table est restée vide
> et rien ne la lisait.

- **Ce qui a été retiré** : le service de capture, son entité, ses enums, son dépôt, et leurs appels dans l'IA des
  issues, l'analyse, Smart Assign et le service des issues (les trois gates HITL : spec, décision, smart-assign).
- **Ce qui reste en base** : la table `ai_generations` et la colonne `workspaces.ai_learning_enabled` (défaut
  `false`), qu'aucun code n'écrit ni ne lit. `ai_runs` (V35) reste : Smart Assign l'écrit, les métriques produit la
  lisent.
- **Ce qui reprend la boucle** : R61 du Conseil d'Avenir (séance n°10 du 29/10/2026, retenue) : la banque
  d'évaluations de l'espace nourrie par les dossiers, le registre des modèles par tâche, puis l'export en formats
  ouverts. Aucun entraînement dans TaskForce cette année.
- **RGPD / multi-tenant**, pour toute capture à venir : corpus **par workspace**, jamais de cross-tenant, un
  interrupteur visible, effaçable.

> La leçon : une capture qu'on ne peut ni activer ni lire meurt vide. Le LoRA vient **plus tard**, quand un corpus
> existe et qu'on le lit, **on ne l'invente pas avant**.

## 6. En une phrase

**On ne rend pas Qwen plus intelligent aujourd'hui — on rend TaskForce capable de fabriquer, tout seul,
le corpus qui rendra un petit modèle excellent *pour ce produit* demain.**
