# Roadmap consolidée — TaskForce (v2 en tête, solde v1 à la fin)

> **Master roadmap** post-pivot (07/07/2026). Séquence le **pivot v2 « AI Delivery OS »** ([[IDEA]], [[Moteur_IA_World_Model_OODA]]) **devant**, et repousse le **backlog v1** ([[Roadmap_Backlog]]) à la fin — **sauf le socle RNCP, non négociable** (voir ⚠️).
> Détail v2 par épic : [[Roadmap_v2]]. Détail v1 : [[Roadmap_Backlog]].

---

## Vue d'ensemble (phases)

| Phase | Contenu | Sortie |
|---|---|---|
| **0. Spécification** *(quasi finie)* | Vision + moteur + agents + benchmark + contrat API + données (les docs `v2/`) | Spec exécutable ✅ |
| **1. Socle IA** | **IA-1** retrieval Brain OS · **IA-5** `ai-service` dockerisé · **contrat API** backend↔ai-service | Le cerveau branché |
| **2. Flow AI-native = 🎯 tranche PFR** | **P1** (projet→cycles, issue→spec/prompt) · **IA-2** modèles · **IA-3 min** (1 boucle predict/reflect) · **1 agent COO** · **P4** human-in-the-loop · **P2** cockpit GitHub (lecture) | La démo qui prouve la thèse |
| **3. Extension IA** | **IA-4** (3 agents complets CPO/CTO/COO) · boucle World Model complète · **P3** runs/checkpoints · **P5** chat-as-app | Produit riche |
| **4. Reste v2** | GitHub 2-way/push · Slack sortant · fine-tune LoRA · Events API | Vision étendue |
| **5. Solde backlog v1** | Les `TF-*` restants (finition pro, ★) | Nettoyage |

> **Dépendance racine** : tout le track IA repose sur **IA-1 (retrieval)** → Phase 1 d'abord, toujours.

---

## ⚠️ Le socle RNCP ne se décale PAS (PFR)

Le backlog v1 est mappé au **référentiel RNCP** (c'est le *socle minimal* du diplôme). On repousse la **finition pro** (★, P2/P3), **mais** ces items restent **obligatoires pour la soutenance** et tournent **EN PARALLÈLE** des phases 1-2, pas « à la toute fin » :

| Item v1 | Pourquoi non négociable |
|---|---|
| **TF-TEST-001** — couverture front ≥ 50 % | exigence référentiel (back déjà ✅ 86 %) |
| **TF-SEC-*** P1 (OWASP, secrets, en-têtes, accès) | bloc sécurité RNCP |
| **TF-INFRA-001→006** (hébergement, TLS, prod durcie, CD, backup) | bloc déploiement RNCP |
| **TF-DOC-001** — **mémoire** (rédaction continue) | c'est le livrable noté |
| **TF-DOC-004/005** (diagrammes conception, wireframes) | bloc conception |

> Règle : **le v2 est la vitrine différenciante ; le socle RNCP est le passage obligé.** On mène les deux de front — le v2 fournit d'ailleurs de la matière au mémoire (innovation, veille IA, ADRs).

---

## Ordre d'exécution conseillé (macro)

1. **Finir Phase 0** (ADRs : Brain OS interne, World Model×OODA, contrat inter-services).
2. **Phase 1** — IA-1 + contrat API + `ai-service` dockerisé.
3. **Phase 2** — la tranche PFR (démontrable de bout en bout).
4. **En parallèle 1→2** — socle RNCP (tests front, sécu P1, déploiement, mémoire).
5. **Phases 3-4** — extension (post-démo).
6. **Phase 5** — solde des `TF-*` restants.

---

## Threads « Phase 0 » restants
- [ ] ADR « Brain OS interne, non exposé » · ADR « World Model × OODA » · ADR « contrat backend↔ai-service » (→ `v1/12-decisions/`)
- [ ] Mesurer le benchmark sur un golden set ([[Benchmark_Modeles_IA]] §5)
- [ ] Choix embeddings (bge-m3 local par défaut)

**Dernière MAJ :** 07/07/2026 · Master roadmap post-pivot.
