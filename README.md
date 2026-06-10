# 📚 TaskForce — Documentation (Brain OS)

Base de connaissance complète de TaskForce, organisée comme un **vault Obsidian versionné** (modèle inspiré
du « documentation operating system » de Plania). Conçue pour être navigable par un **humain** et par une **IA**.

> 🧠 **[Brain OS — Hub central](./Brain_OS.md)** : point d'entrée unique (architecture, API, modules, dette,
> problèmes connus, état produit). 🤖 Une IA lit d'abord **[AGENTS.md](./AGENTS.md)**.

---

## 🗂️ Structure du vault

```
taskforce-docs/
├─ Brain_OS.md          ← hub central (carte de contenu)
├─ AGENTS.md            ← contrat d'agent (kernel : orientation + auto-entretien)
├─ v1/                  ← ÉTAT ACTUEL du produit (16 domaines numérotés)  →  v1/README.md
├─ v2/                  ← cible future (vide pour l'instant)
├─ frameworks/          ← SOP & procédures transverses (hors version)
├─ templates/           ← templates de documents (Templater)
└─ assets/             ← images, maquettes, diagrammes, schémas HTML
```

**Versioning :** `v1/` = ce qui existe aujourd'hui ; `v2/` = cible future. On ne mélange jamais les deux
dans un document (cf. [Conventions](./v1/04-engineering/Conventions_Documentation.md)).

## 📖 Accès rapide

- 🧠 **[Brain OS — Hub](./Brain_OS.md)** · 🤖 **[AGENTS.md](./AGENTS.md)** · ⚙️ **[SOP](./frameworks/SOP_Developpement.md)**
- 📦 **[Index v1 — tous les domaines](./v1/README.md)**
- 🏛️ [Architecture](./v1/03-architecture/Architecture.md) · 🔌 [API](./v1/05-api/API.md) · 🧩 [Modules](./v1/03-architecture/Modules.md)
- 🚧 [État Produit](./v1/02-produit/README.md) · 📋 [Backlog](./v1/13-roadmap/Roadmap_Backlog.md) · 🔥 [Problèmes connus](./v1/09-audits/Problemes_Connus.md)
- 🎓 [Mémoire RNCP](./v1/16-memoire-rncp/README.md) · 👥 [Doc utilisateur](./v1/15-utilisateur/Manuel_Utilisateur.md)
- 🗺️ Schémas (PFR) : [flux complet](./assets/brain-os-flow.html) · [architecture technique](./assets/architecture-technique.html) · [boîte à outils infra/sécurité](./assets/infra-toolchain.html) · [système Brain OS](./assets/brain-os-systeme.html)
- 🧰 [Catalogue d'outils infra & sécurité (gratuit/OSS)](./v1/06-infra/Outils_Infra_Securite.md)

## 🚀 Comment l'utiliser

**Obsidian** : ouvrir ce dossier comme vault (config `.obsidian/` fournie ; plugins recommandés dans
[Conventions §7](./v1/04-engineering/Conventions_Documentation.md)). La vue Graphe colore les notes par domaine.

**Contribuer** : dupliquer un [template](./templates/Template_Doc_Technique.md), respecter le front-matter et
le [SOP](./frameworks/SOP_Developpement.md). Commits `docs(scope): …`. Ne jamais supprimer un doc → l'archiver
dans [`v1/20-archive/`](./v1/20-archive/README.md).

## 🔗 Liens utiles

- Code source : [`../taskforce-fullstack`](../taskforce-fullstack) · version compacte IA : `../taskforce-fullstack/.ai/`
- Swagger API : `http://localhost:8080/api/swagger-ui.html` · Keycloak : `http://localhost:8180`

---

**Dernière mise à jour :** 09/06/2026 · **Brain OS v1** · Projet Taskforce — Metz Numeric School 2025-2026
