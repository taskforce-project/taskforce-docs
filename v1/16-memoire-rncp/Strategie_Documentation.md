---
id: strategie-documentation
title: Stratégie de documentation — liste maître des livrables
doc_type: moc
statut: active
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [documentation, livrables, rncp, e1-e29, memoire, strategie]
---

# Stratégie de documentation — liste maître

> **But** : recenser **TOUS** les documents à produire pour couvrir le projet + valider le titre RNCP
> (livrables **E1–E29** / compétences **C1–C32**). Légende : ✅ existe · 🟡 partiel/à finaliser · ⬜ à créer.
> La rédaction du mémoire est **narrative** (cf. `README.md` §4) et chaque affirmation pointe vers une preuve.

## A. Dossier de validation (mémoire) — colonne vertébrale

| Doc | Contenu | Statut |
| --- | --- | :--: |
| `16-memoire-rncp/README.md` | Matrice C1–C32 + livrables E1–E29 (checklist maître) | ✅ |
| `Bloc1_Conception_Modelisation.md` | Rédaction C1–C12 (par compétence : énoncé, preuve, narration) | 🟡 |
| `Bloc2_Frontend.md` | Rédaction C13–C20 | 🟡 |
| `Bloc3_Backend.md` | Rédaction C21–C26 | 🟡 |
| `Bloc4_Deploiement_Production.md` | Rédaction C27–C32 | 🟡 |
| `Strategie_Documentation.md` (ce doc) | Plan de production | ✅ |

## B. Livrables E1–E29 (par bloc)

### Bloc 1 — Conception
| E | Document | Où / à créer | Statut |
| --- | --- | --- | :--: |
| E1 | Reformulation de la demande | `01-projet/Dossier_Projet.md`, `01_CdCF.md` | 🟡 |
| E2 | **Planning + budget prévisionnels** | ⬜ **à créer** : Gantt/jalons DFS + budget (infra + charge×TJM) | ⬜ |
| E3 | Note de préconisations techniques | `01-projet/02_CdCT.md` + `03-architecture/Architecture.md` | 🟡 |
| E4 | Procédure environnement de dev | `15-utilisateur/Guid_Installation.md`, `QUICKSTART.md` | ✅ |
| E5 | **Note justifiant la méthode agile** | ⬜ **à créer** (Scrum/Kanban, cérémonies, outillage) | ⬜ |
| E6 | **Trame de compte-rendu + 1 exemple** | ⬜ **à créer** | ⬜ |
| E7 | **Wireframes annotés** | 🟡 `assets/maquettes/` (images) → **doc annoté** (UC + route) à produire | 🟡 |
| E8 | **Dossier de conception** (cas d'usage, **classes**, **MCD/MLD**, archi) | 🟡 `03-architecture/` → **diagrammes UML + MCD/MLD** à générer depuis le code réel (JPA/Flyway) | 🟡 |
| E9 | **Audit RGPD (cas pro externe)** | ⬜ **à créer** (≠ RGPD de TaskForce, déjà fait) | ⬜ |
| E10 | **Méthodologie de veille** | ⬜ **à créer** (sources/fréquence + ≥3 entrées : Groq, Next, Spring Boot 4…) | ⬜ |

### Bloc 2 — Front-end
| E | Document | Où | Statut |
| --- | --- | --- | :--: |
| E11 | Développement front | `02-produit/Frontend.md`, code | 🟡 |
| E12 | Consommation d'une API tierce | `05-api/API.md`, intégrations (GitHub/Stripe) | 🟡 |
| E13 | Plan de tests front + exécution | `08-operations/Tests.md` | ✅ |
| E14 | Industrialisation front | `.github/workflows/frontend-tests.yml` + CI (gates) | 🟡 |
| — | Accessibilité (C13/C15) | `14-design/Accessibilite.md` | 🟡 |

### Bloc 3 — Back-end
| E | Document | Où | Statut |
| --- | --- | --- | :--: |
| E15 | Couche de persistance | `03-architecture/Architecture.md` (Flyway/JPA) | ✅ |
| E16 | Développement back | `02-produit/Backend.md`, code | 🟡 |
| E17 | **Système de paiement + monétisation** | 🟡 Stripe (`02-produit/*` + code) → à documenter (webhooks, plans) | 🟡 |
| E18 | API sécurisée | `05-api/API.md`, `07-securite/Sécurité.md`, Swagger | ✅ |
| E19 | Plan de tests back | `08-operations/Tests.md` | ✅ |
| E20 | Industrialisation back | `.github/workflows/backend-tests.yml`, `release.yml` | 🟡 |

### Bloc 4 — Déploiement & production
| E | Document | Où / à créer | Statut |
| --- | --- | --- | :--: |
| E21 | **Hébergement + diagramme de déploiement** | ⬜ **à créer** (Guacamole/VM école) | ⬜ |
| E22 | Environnement de production sécurisé | 🟡 `docker-compose.prod.yml`, `06-infra/` → à formaliser (secrets, chiffrement disque, bastion) | 🟡 |
| E23 | **Nom de domaine + DNS + certificats** | ⬜ **à créer** (déploiement) | ⬜ |
| E24 | Déploiement automatisé | 🟡 `08-operations/DevOps.md`, `release.yml` → pipeline de déploiement | 🟡 |
| E25 | Journalisation / audit | ✅ `07-securite/Sécurité.md`, `AuditLog` + OTEL + logs front | ✅ |
| E26 | Supervision + alertes | ✅ `observability/alerts/` + SigNoz | ✅ |
| E27 | Détection de bugs + correctifs | ✅ `09-audits/Problemes_Connus.md` + `qa-findings.md` | ✅ |
| E28 | Détection de failles + correctifs | ✅ `07-securite/Sécurité.md` (pentest ZAP/Semgrep/Trivy) | ✅ |
| E29 | **Génération de doc + changelog** | 🟡 Brain OS + `release.yml` → consolider un CHANGELOG | 🟡 |

## C. Documents utilisateur & support
| Doc | Statut |
| --- | :--: |
| `15-utilisateur/Manuel_Utilisateur.md` | 🟡 à finaliser |
| `15-utilisateur/Guid_Installation.md` | ✅ |
| `15-utilisateur/FAQ.md` | 🟡 |
| `15-utilisateur/Release_Notes.md` | 🟡 |
| `10-runbooks/` (exploitation, incident) | 🟡 |

## D. Récap — ce qu'il RESTE à CRÉER (⬜) ou finaliser en priorité
1. **E8 Dossier de conception** : diagrammes **cas d'usage**, **classes** (reflet JPA ~29 entités), **séquence** (parcours clés), **MCD/MLD** (dérivés Flyway) — *le plus lourd, cœur du Bloc 1*.
2. **E2 Planning + budget** prévisionnels (Gantt/jalons + budget).
3. **E7 Wireframes annotés** (depuis `assets/maquettes/`).
4. **E5 note agile** + **E6 trame CR** + **E10 veille** (courts, documentaires).
5. **E9 audit RGPD cas pro** (sujet externe imposé).
6. **E21 diagramme de déploiement** + **E23 DNS/TLS** (avec le déploiement).
7. **Rédaction narrative** des 4 Blocs (assemblage des preuves).
8. **E29 CHANGELOG** consolidé.

## E. Séquencement conseillé (doc = tout à la fin, cf. décision user)
1. **Diagrammes** (E8) — générables du code (UML/MCD/MLD) → je peux les produire.
2. **Docs courts** (E2, E5, E6, E10) en parallèle.
3. **E9 RGPD cas pro** (sujet à part).
4. **Rédaction des Blocs** (assemblage) + **E29 changelog**.
5. **Déploiement** (E21/E23) une fois les VM prêtes.
