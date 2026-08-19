# Système d'intégrations — Catalogue déclaratif + connecteurs

> **Problème** : un fichier / un écran **spécifique par outil** (Plane, GitHub, Asana…) ne scale pas à
> 50+ intégrations. **Solution** : **un catalogue déclaratif** (le « pool ») + une **UI/API générique**
> pilotée par ce catalogue. Ajouter un outil = **une ligne**. L'implémenter = un **connecteur**.

Lié à : [[Moteur_IA_World_Model_OODA]] (les connecteurs alimentent la jambe *observe*) · [[Data_Flywheel_et_Apprentissage]].

## 1. Architecture (additive — ne casse pas l'existant)

```
ConnectorCatalog (déclaratif, ~47 outils)      ← LA source des configs (le pool)
   └─ ConnectorDescriptor{ key, name, category, authType, fields[], capabilities[], status }
GET /integrations/catalog  → pool groupé par catégorie + statut de connexion du workspace
Integration (entité)       → credentials chiffrés (par workspace + provider)   [inchangé]
Connecteurs (comportement) → Plane / GitHub / Slack  (services dédiés, réutilisés)
```

- **On n'a pas refactoré** l'enum `IntegrationProvider` (11 fichiers, dont 4 tests GitHub/Slack) : la
  couche catalogue est **purement additive**. L'enum ne grandit que d'**une valeur par connecteur
  réellement implémenté**.
- Le catalogue est la **source unique de vérité** de « quels outils existent et comment ils se
  configurent ». L'UI n'a plus besoin d'un écran par outil : elle **rend le catalogue**.

## 2. Le descripteur (la « fiche » d'un outil)

| Champ | Rôle |
|---|---|
| `key` | slug stable (`plane`, `github`, `stripe`) |
| `category` | 16 catégories (Gestion de projet, Dev & CI/CD, Infra, DB, Ads, Analytics, Paiements, CRM, Comm, Auth, Sécu, Productivité, Design, E-commerce, Automatisation, Modèles IA) |
| `authType` | `OAUTH2` (redirection) · `API_KEY` · `TOKEN` · `CONFIG` (multi-champs) · `NONE` — **pilote le formulaire** |
| `fields[]` | champs de connexion (clé/secret/…) rendus par l'UI (vide pour OAuth) |
| `capabilities[]` | `observe` (→ Brain OS) · `act` (écrire/pousser) · `metrics` |
| `status` | `AVAILABLE` (connectable) · `PLANNED` (dans le pool, pas encore implémenté) |

## 3. Le pool (état 09/07/2026)

- **47 outils / 16 catégories**. **AVAILABLE** : `plane` (API key → ingestion Brain OS), `github`
  (OAuth), `slack` (OAuth). Le reste = **PLANNED** (roadmap visible) : Linear, Asana, ClickUp, Jenkins,
  Docker, Kubernetes, Vercel, Render, Cloudflare, AWS, VPS, Supabase, Neon, MongoDB Atlas, Redis Cloud,
  Google/Meta/LinkedIn Ads, Google Analytics, PostHog, Clarity, Stripe, HubSpot, Salesforce, Zoho,
  Intercom, Twilio, Resend, Mail/SMTP, Clerk, Keycloak, Bitwarden, Notion, Google Workspace, Microsoft
  365, Granola, Raycast, Canva, Figma, ElevenLabs, Shopify, n8n, Zapier, Groq.

## 4. Ajouter un outil

1. **Le rendre visible** : une ligne `planned(key, name, category, authType, description)` dans
   `ConnectorCatalog`. → apparaît immédiatement dans le pool (UI générique).
2. **Le rendre connectable** : implémenter un connecteur (validation creds + éventuel `sync` d'ingestion),
   ajouter la valeur d'enum `IntegrationProvider`, passer l'entrée en `available(...)` avec ses `fields`.

## 5. UI générique · ✅ **fait (09/07)**

- Section **« Catalogue d'intégrations »** dans les settings workspace (`IntegrationsCatalog`,
  `components/integrations/integrations-catalog.tsx`) : rend `GET /integrations/catalog` — cartes groupées
  par catégorie, badges *connecté / bientôt*, résumé (total/connectés/disponibles).
- **Connexion adaptative** : OAuth (`github`/`slack`) = bouton **Connecter** 1-clic (redirection) ; clé/config
  (`plane`) = **dialog piloté par `fields`** (formulaire déclaratif) → connect → choix du projet → **Synchroniser → Brain OS**.
- **Tooltip d'aide** (`setupHint`) : quand ce n'est pas du 1-clic, une bulle ⓘ explique **où récupérer la clé**
  (+ lien `docsUrl`), sur la carte et dans le dialog. (Ex. Plane : « avatar → Settings → Personal access tokens → Add token ; le slug est dans l'URL ».)
- **Vérifié** : TS clean, route settings compile 200, catalogue renvoie fields+setupHint+docsUrl.

## 6. Reste à faire

- **Dispatch générique** (SPI `IntegrationConnector` + registry) : `POST /integrations/{key}/connect|sync`
  unifiés (aujourd'hui Plane a ses endpoints dédiés ; GitHub/Slack gardent l'OAuth, spécifique).
- **Prochains connecteurs** (jambe *observe* OODA) : Linear, puis Stripe / Google Ads / PostHog / Resend…
