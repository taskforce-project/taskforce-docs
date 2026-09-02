# Thèse produit — V1 → V2 (clarifiée)

> **Source de vérité de la thèse produit.** Réconcilie le brainstorm de juillet
> (les autres fichiers `road_to_v2/`, désormais contexte historique) avec l'état
> réel du code et le cadrage produit du 02/09/2026. Règle d'or de ce document :
> **distinguer le livré de l'aspirationnel, toujours.** Le plan d'exécution qui fait
> foi reste `Roadmap_Consolidee.md` ; la mécanique de capture, `Data_Flywheel_et_Apprentissage.md`.

## La thèse en une phrase

**TaskForce est la couche qui amène chaque tâche jusqu'au bon exécutant — humain
ou IA — de façon explicable, et qui apprend de chaque décision.**

Ce n'est ni un traceur de tâches de plus, ni un remplaçant des outils d'exécution.
C'est le tissu conjonctif entre le travail à faire et *qui/quoi* le fait, qui ouvre
un chemin vers l'automatisation de bout en bout **sous supervision humaine**.

## V1 — aujourd'hui (le socle réel)

- **Ce que c'est :** le copilote d'affectation. Score déterministe (compétences +
  charge réelle + disponibilité) → un petit modèle **local** reclasse et justifie →
  **l'humain tranche**. Poids visibles, donnée sur l'infra du client.
- **Livré et vérifiable :** smart-assign, graphe Brain OS, inférence locale (Ollama),
  génération de spec + prompt, decision board *one-shot* (observe→reflect→3 priorités),
  hôte MCP + quelques connecteurs (plane, github, slack).
- **Wedge :** les **services professionnels — agences, ESN, cabinets**, là où le
  staffing *est* le P&L. Pas « les PME » (personne n'a mal). Amorçage par **3-5 design
  partners**, expansion par siège.
- **Moat honnête :** pas « l'IA pas chère » (l'avantage coût fond). Le **graphe
  d'organisation** qui se densifie à l'usage + la **localité** (donnée RH/projet qui ne
  sort pas = souveraineté/conformité). Un concurrent ne les copie pas sans les données.

## V2 — le cap (routing vers l'exécutant + apprentissage)

**Le shift :** en V1 on route le travail vers des **humains**. En V2, une tâche peut
être routée vers un **exécutant IA** (Claude Code, GitHub Copilot, autre) : TaskForce
génère la spec + le prompt, l'exécutant produit (une PR), **l'humain valide**. On
n'internalise pas l'exécution — on *amène jusqu'à l'exécutant* et on garde la main au
gate. C'est le chemin vers une **automatisation de bout en bout supervisée**.

**La continuité qui rend V2 défendable :** la V1 installe le **graphe** (qui sait faire
quoi, qui porte quoi, à quelle charge) et la confiance « l'humain décide ». La V2
**route et apprend sur ce graphe**. Un concurrent parti direct sur « l'orchestration
d'agents » n'a pas ce graphe. **V1 = le wedge et le data-moat ; V2 = le prix.**

### Réel vs aspirationnel (à ne jamais confondre en pitch)

| Brique | Statut réel |
|---|---|
| Smart-assign, Brain OS, inférence locale, spec+prompt, decision board one-shot | **Livré** (services Java vérifiés) |
| Hôte MCP + 3 connecteurs (plane/github/slack) | **Livré** ; 44 autres connecteurs = *affichés* « PLANNED », non implémentés |
| **Flywheel de données** (`ai_generations`) | **En cours** — la table n'existait pas ; c'est le lot V1 prioritaire (capture à chaque gate HITL) |
| **Boucle d'apprentissage** (predict→reflect→ré-injection, « l'erreur baisse ») | **Aspirationnel** — c'est le cœur du « World Model » et il n'est *pas* codé |
| **Routing vers exécutant IA** (assigner une tâche à Claude/Copilot) | **Aspirationnel** — la direction ; MVP à cadrer |
| 3 agents C-level (CPO/CTO/COO) | **Aspirationnel** (un `DecisionService` générique existe, pas les 3 personas) |
| Passage à l'échelle (inférence hébergée multi-tenant) | **Non traité** — tout tourne sur un laptop 8 Go VRAM ; le « 0 € » est une contrainte de démo, pas un modèle d'exploitation |

**Moat V2 :** le graphe org **+** le corpus de préférences (dès que `ai_generations`
tourne) **+** la traçabilité/contrôle — qui devient une *exigence réglementaire* dès
qu'un exécutant IA agit à ta place (d'où le beachhead naturel pharma / 21 CFR pour le
« control plane »).

## Ce qui rend la thèse non-fictive — 3 priorités

1. **Le flywheel, maintenant** (`ai_generations`, cf. `Data_Flywheel_et_Apprentissage.md`).
   Sans lui, chaque interaction IA est de la donnée perdue à jamais et le moat ne peut
   pas commencer à s'accumuler. Petit à coder, plus haut levier du plan.
2. **Fermer UNE boucle démontrable** : un cycle predict→reflect avec une métrique
   « l'erreur de prédiction a baissé ». Une boucle fermée > dix features ouvertes.
3. **Un MVP de routing vers exécutant** : assigner une tâche à Claude/Copilot → spec +
   prompt transmis → l'humain valide la PR. Le même `ai_generations` capture alors le
   *downstream* (PR acceptée/réécrite) et ferme la boucle produit.

## Garde-fous honnêtes

- **Le récit a 1-2 ans d'avance sur le code.** Le démontrable aujourd'hui = « génère une
  spec + un prompt à copier sur une issue ». Nommer ce différentiel désarme la due
  diligence (et le piège « c'est bon partout, exceptionnel nulle part »).
- **Discipline avant tout pitch investisseur :** fermer **une** boucle + posséder **un**
  segment. Le plan se prévient lui-même : *« Piège n°1 = le scope. »*
- **« Vérifié e2e » n'est pas une preuve** (cf. l'aveu « le RAG était décoratif jusqu'au
  16/07 » dans `brain-os-roadmap.md`) : exiger une démo *live* en usage réel.
- **Isolation par workspace** (RGPD, opt-in, effaçable) : vertueux, mais fragmente le
  corpus — la mutualisation cross-tenant qui donnerait du volume est exclue par design.

---
*MAJ 02/09/2026. Les fichiers `road_to_v2/*` de juillet restent lisibles comme
historique de conception ; en cas de contradiction, **ce document et
`Roadmap_Consolidee.md` priment**.*
