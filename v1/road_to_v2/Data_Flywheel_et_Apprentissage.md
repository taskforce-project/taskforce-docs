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

## 3. Le flywheel — ce qu'on capture, dès maintenant

À **chaque point human-in-the-loop**, on enregistre le quintuplet :

1. **Requête** utilisateur (l'issue, le prompt, la question) ;
2. **Contexte retrieved** (les nodes Brain OS servis par le retriever) ;
3. **Réponse générée** (le *draft* Qwen) ;
4. **Réponse finale réellement utilisée** (après édition humaine) ;
5. **Signal** : `accepté` | `édité` | `rejeté` (+ *edit distance* draft→final).

> **1er point de collecte = la génération de spec** (déjà construite, Phase B) : on a **déjà** le draft
> (`IssueSpecDraft`) *et* le contenu final approuvé (`ApproveSpecRequest`). Il ne manque que la **trace**.
> Points suivants : réponses de l'agent (`AssistantAnswer`), smart-assign, décisions OODA.

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

## 5. Concret - la première brique EST FAITE (`ai_generations`)

> ✅ **Implémenté le 02/09/2026** (`TF-FLYWHEEL-01`, migration V81) : la table de capture + le câblage aux
> 3 gates HITL (spec, décision, smart-assign). Cf. `.ai/roadmap.md` et `v1/02-produit/IA.md` (`IA-FLYW-001`).
> Reste en aval : l'export JSONL et le LoRA/DPO.

- ✅ **Trace de génération** : table `ai_generations` `(workspace_id, kind, request_ref, context_refs[],
  draft, final, signal, edit_distance, model, latency_ms, created_by, created_at)`. `kind` (VARCHAR) et
  `final` (jsonb) restent extensibles → accueillir l'outcome d'exécution d'un agent en V2, sans migration.
- ✅ **Alimentée par les 3 gates** : SPEC (`generateSpec` draft → `approveSpec` final + signal +
  edit_distance), DECISION (`accept` → ACCEPTED, `dismiss` → REJECTED), SMART_ASSIGN (`recommend` reco →
  `updateIssue` assigné réel). Best-effort (ne casse jamais le flux), corpus distinct d'`assignment_events`.
- **Export** (à venir) : un dump JSONL par workspace, prêt pour un entraînement LoRA/DPO ultérieur.
- **RGPD / multi-tenant** : corpus **par workspace**, jamais de cross-tenant ; **opt-in**
  (`ai_learning_enabled`, défaut OFF), effaçable (`purgeWorkspace` + CASCADE workspace).

> Tant que le volume est faible, la table ne sert « qu'à » l'observabilité et à la jambe *feedback* de
> l'OODA. Le LoRA vient **plus tard**, quand le corpus est mûr — **on ne l'invente pas avant**.

## 6. En une phrase

**On ne rend pas Qwen plus intelligent aujourd'hui — on rend TaskForce capable de fabriquer, tout seul,
le corpus qui rendra un petit modèle excellent *pour ce produit* demain.**
