---
id: plan-soutenance
title: Plan de soutenance — TaskForce (15-20 min + Q&A)
doc_type: soutenance
statut: en-cours
version: 1.0
date: "06/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, plan, slides, script, demo, qa, rncp, dfs, couverture]
---

# 🗺️ Plan de soutenance — TaskForce

> **Format** : 15–20 min de présentation + ~10 min de questions. Cible : **~17 min**.
> **Ce que l'école évalue à l'oral** (README mémoire §1) : la soutenance = **démonstration de
> l'application front-end (bloc 2) + back-end (bloc 3)** + présentation de synthèse. Les blocs 1
> (conception) et 4 (déploiement) sont surtout évalués par le **dossier écrit** et la **mise en
> situation** ; ils servent ici de **cadrage** (contexte + crédibilité), pas de cœur.
>
> 👉 Conséquence : **le pic de la soutenance = la démo front puis la partie back (code + API +
> sécurité + tests).** Ce plan est calibré ainsi.

---

## 0. Règle d'or

Trois messages, quoi qu'il arrive :
1. **Le produit marche** et résout un vrai problème (démo front + Smart Assign).
2. **Le back est solide et maîtrisé** : API sécurisée, persistance, paiement, tests (démo/code back).
3. **Je prends du recul** : je nomme les limites et ce que j'ai corrigé (ex. migration auth OIDC).

---

## 1. Structure & timing (calibrée blocs 2 & 3)

| Bloc | Partie | Slides | Durée | Rôle |
|:-:|-------|:------:|:----:|------|
| — | **A. Cadrage** (contexte, solution, archi) | 1–4 | ~3:00 | Poser le décor (bloc 1 léger) |
| **2** | **B. ⭐ Démo FRONT-END** | 5–8 | ~5:30 | **Cœur évalué** — C13→C20 |
| **3** | **C. ⭐ BACK-END (démo + code)** | 9–13 | ~5:30 | **Cœur évalué** — C21→C26 |
| — | **D. Qualité / Sécu / RGPD / Prod** | 14–15 | ~1:30 | Transverse + bloc 4 (léger) |
| — | **E. Distance critique + conclusion** | 16–17 | ~1:30 | Recul + fin |

**≈ 17 min.** Si tu débordes, coupe dans A et D — **jamais** dans B et C.

---

## 2. Script slide par slide (ce que tu dis)

### Partie A — Cadrage (~3 min)

**Slide 1 — Titre (0:20)**
> « Bonjour, je suis Pierre Michel. Je présente TaskForce, un ERP SaaS de gestion de projet avec
> assignation intelligente des tâches, développé comme fil rouge du titre Développeur Full Stack. »
Logos école + projet.

**Slide 2 — Le problème (0:50)** · *C1*
> « Dans une équipe, répartir les tâches à la main crée des surcharges, un manque de visibilité, et des
> affectations sous-optimales. Le manager doit croiser mentalement compétences, charge et disponibilités
> à chaque tâche. » → Poser la problématique d'usage.

**Slide 3 — La solution & le périmètre livré (1:00)** · *C1–C3*
> « TaskForce automatise cette répartition. Périmètre V1 livré : workspaces multi-tenant, projets, issues
> avec Kanban, **Smart Assign par IA**, chat temps réel, facturation Stripe, RGPD. » Dire 1 phrase sur le
> hors-périmètre (honnêteté). Mentionner la **méthode agile** (Scrum allégé, cycles) → *C4*.

**Slide 4 — Architecture & stack (1:00)** · *C7–C10, C22*
> Montrer le **diagramme C4 (conteneurs)**. « Next.js en front, Spring Boot 4 / Java 21 en back,
> PostgreSQL + pgvector, Keycloak pour l'identité, Groq pour l'IA, RabbitMQ pour le temps réel, le tout
> conteneurisé. Architecture en couches, multi-tenant. » Rester bref — le détail vient en partie C.

---

### Partie B — ⭐ Démo FRONT-END (bloc 2, ~5:30) — *le cœur n°1*

> **Écran = live app.** Parle en montrant. Objectif : démontrer C13→C17 par le parcours, C18–C19 par
> un aparté « voici la CI/couverture », C20 par la landing.

**Slide 5 — Interface & parcours (démo, 2:00)** · *C13, C15*
> Connexion (Keycloak) → dashboard workspace. « Interface pensée mobile-first, sombre/clair, composants
> Radix accessibles (WCAG 2.1 AA, audit axe-core en CI). » Créer une issue (raccourci `C`), montrer le
> Kanban drag-and-drop. Insister : **parcours fluide, states de chargement/erreur, accessibilité**.

**Slide 6 — ⭐ Smart Assign (démo, 1:45)** · *C15 + différenciateur*
> Sur l'issue → « Suggérer un assigné ». Montrer les **candidats classés**, les **5 signaux** (sémantique
> pgvector, charge, historique, dispo, labels) et l'**explication en langage naturel** (Groq). « Ce n'est
> pas une boîte noire : chaque suggestion est justifiée. » Accepter → feedback stocké.

**Slide 7 — Charte & consommation d'API sécurisée (0:50)** · *C14, C17*
> « Design system cohérent (tokens partagés). Côté données, tout passe par un client Axios centralisé qui
> injecte le **JWT**, gère le **refresh automatique** sur 401, et redirige proprement. API tierces : Stripe
> (paiement, iframe PCI-DSS), Dicebear (avatars). » → *C12 = API tierce consommée*.

**Slide 8 — Tests & industrialisation front (0:55)** · *C16, C18, C19, C20*
> « Front testé : **92 % de couverture Vitest** (746 tests) + **E2E Playwright** (auth, routes,
> accessibilité). Qualité : TypeScript strict, ESLint bloquant, en-têtes de sécurité (CSP/HSTS). CI
> GitHub Actions qui build et gate la couverture. » Montrer le badge/rapport. Une phrase SEO (Astro SSG,
> landing) → *C20*.

---

### Partie C — ⭐ BACK-END : démo + code (bloc 3, ~5:30) — *le cœur n°2*

> **Ici on montre du code / Swagger / l'archi**, pas seulement l'UI. C'est ce que l'école attend
> (« prototype/démo/**code** »).

**Slide 9 — Persistance & modèle de données (1:00)** · *C21*
> Montrer le **MCD/MLD** (ou l'ERD). « ~50 tables, migrations **Flyway** versionnées, PostgreSQL 18 +
> **pgvector** (index HNSW pour la recherche sémantique). Sécurité en profondeur : contrôle d'accès au
> niveau service, `AuditableEntity`, chiffrement **AES-256-GCM** des PII. »

**Slide 10 — API sécurisée (démo Swagger + sécurité, 1:30)** · *C24*
> Ouvrir **Swagger UI**. « API REST documentée (OpenAPI auto-généré). Sécurité : Keycloak émet des tokens
> **OIDC RS256**, l'API est un Resource Server (validation JWK). Validation `@Valid` sur tous les DTOs,
> rate limiting Bucket4j, isolation multi-tenant anti-IDOR. » *Raconter la migration JWT HS512→OIDC comme
> preuve de recul et de maîtrise.*

**Slide 11 — Paiement & monétisation (0:50)** · *C23*
> « Stripe : Checkout + 5 webhooks signés (idempotence `stripe_event_id`), portail de facturation, machine
> à états d'abonnement. Le back ne voit jamais un numéro de carte. Modèle freemium FREE/PRO/ENTERPRISE. »

**Slide 12 — Code & organisation (0:50)** · *C22*
> Montrer l'arborescence `shared / core / modules`. « Architecture en couches, dépendances
> unidirectionnelles, un module métier isolé par domaine. Java 21 + Virtual Threads pour la scalabilité
> I/O. Composants à jour, scannés (Trivy/Semgrep). »

**Slide 13 — Tests & industrialisation back (1:00)** · *C25, C26*
> « Back testé : **78 % JaCoCo** (658 tests), avec **Testcontainers** — vrai Postgres + pgvector + vraies
> migrations, **pas de mock de base**. CI : Checkstyle, tests, gate de couverture, build image Docker →
> GHCR, scans sécurité. » Montrer le rapport JaCoCo ou le workflow.

---

### Partie D — Transverse & production (~1:30)

**Slide 14 — Sécurité, RGPD & observabilité (0:50)** · *C11, C27, C32*
> « OWASP couvert (headers, RBAC, chiffrement, pentest ZAP). RGPD : export + effacement (avec suppression
> de l'identité Keycloak), registre Art. 30. Observabilité : OTel → SigNoz, 9 alertes Prometheus dont deux
> orientées sécurité. » (bloc 4 = surtout évalué en mise en situation → rester synthétique).

**Slide 15 — Déploiement & CI/CD (0:40)** · *C28–C31*
> « 7 workflows GitHub Actions, images versionnées sur GHCR. Deux cibles de déploiement documentées (VM
> école / Render Frankfurt), nginx TLS, rate limiting distribué Redis pour le multi-instances. »

---

### Partie E — Recul & conclusion (~1:30)

**Slide 16 — Distance critique (0:50)**
> « Ce qui n'est pas parfait et que j'assume : pas de tests de charge, DAST pas encore bloquant en CI, DPA
> Groq à formaliser, app monolingue. Et ce que j'ai **corrigé** en durcissement : la dette JWT (→ OIDC),
> le rate limiting mono-instance (→ Redis), l'effacement RGPD Keycloak. » → montre la maturité d'analyse.

**Slide 17 — Ce que j'ai appris + merci (0:40)** · *C12*
> « Montée en compétence : IA/embeddings, sécurité OIDC, observabilité, et une discipline de documentation
> (le Brain OS). Merci — je suis à vous pour les questions. »

---

## 3. Script de démo (détail, à répéter et sécuriser)

> **Vidéo de secours obligatoire** (screencast) si réseau / Keycloak / Groq flanche.
> Jeu de données **seed** préparé, workspace de démo, `GROQ_API_KEY` valide, onglets pré-ouverts.

**Front (partie B)** : login → créer issue (`C`) → Kanban → **Smart Assign** (score + signaux +
explication) → accepter → (bonus) chat temps réel dans une 2ᵉ fenêtre.

**Back (partie C)** : Swagger UI (montrer un endpoint sécurisé + le schéma) → un bout de code clé
(`SecurityConfig` décodeur RS256, ou `SmartAssignService`) → le rapport JaCoCo / un workflow CI.

---

## 4. Matrice de couverture — chaque compétence a son moment

> **Checklist anti-oubli.** Tant qu'une compétence n'a pas un slide/moment, le passage à l'oral ne la
> démontre pas. (Le **dossier écrit** couvre tout ; ici on s'assure que l'**oral** touche l'essentiel,
> avec priorité aux blocs 2 & 3.)

### Bloc 1 — Conception (cadrage oral, détail dans le dossier)
| C | Compétence | Où à l'oral |
|:-:|---|---|
| C1 | Analyser la demande | Slides 2–3 |
| C2 | Expertise / préconisations | Slide 4 + Q&A (choix stack) |
| C3 | Caractéristiques (public/sécu/budget) | Slide 3 |
| C4 | Agile | Slide 3 (méthode) |
| C5 | Env. de dev collaboratif | Q&A / dossier (Docker, Git) |
| C6 | Wireframes | Dossier (montrer si question) |
| C7 | STB → conception | Slide 4 |
| C8 | Modélisation (classes/MCD) | Slide 9 (MCD) |
| C9 | Architecture BDD / persistance | Slide 9 |
| C10 | Architecture logicielle | Slides 4, 12 |
| C11 | RGPD/CNIL | Slide 14 (+ mise en situation) |
| C12 | Veille | Slide 17 + Q&A |

### Bloc 2 — Front-end ⭐ (démontré à l'oral)
| C | Compétence | Où à l'oral |
|:-:|---|---|
| C13 | Concevoir l'UI | Slide 5 (démo) |
| C14 | Éléments graphiques / charte | Slide 7 |
| C15 | UX / parcours / accessibilité | Slides 5–6 (démo) |
| C16 | Langage front (qualité/sécu) | Slide 8 |
| C17 | Consommer une API sécurisée | Slide 7 |
| C18 | Tester le front (≥ 50 %) | Slide 8 (92 %) |
| C19 | Industrialiser le front | Slide 8 (CI) |
| C20 | SEO | Slide 8 (Astro) |

### Bloc 3 — Back-end ⭐ (démontré à l'oral)
| C | Compétence | Où à l'oral |
|:-:|---|---|
| C21 | Persistance (sécu en profondeur) | Slide 9 |
| C22 | Langage back (qualité/écoconc.) | Slides 4, 12 |
| C23 | Paiement + monétisation | Slide 11 |
| C24 | API sécurisée | Slide 10 (Swagger + OIDC) |
| C25 | Tester le back (≥ 50 %) | Slide 13 (78 %) |
| C26 | Industrialiser le back | Slide 13 (CI/CD) |

### Bloc 4 — Déploiement (cadrage oral, cœur = mise en situation)
| C | Compétence | Où à l'oral |
|:-:|---|---|
| C27 | Doc technique + changelog | Slide 14 (Brain OS) |
| C28 | Domaine / DNS / TLS | Slide 15 |
| C29 | Choix hébergement | Slide 15 |
| C30 | Administrer l'hébergement | Slide 15 |
| C31 | Déploiement automatisé | Slide 15 |
| C32 | Supervision / journalisation | Slide 14 (SigNoz/alertes) |

> ✅ **Les 32 compétences ont un point d'ancrage.** Les blocs 2 & 3 (C13–C26) sont **démontrés
> activement** ; les blocs 1 & 4 sont **cités et pointés vers le dossier/la mise en situation**.

---

## 5. Préparation Q&A (~10 min) — questions anticipées

> Répondre **court, honnête, avec une preuve**. Ne pas savoir = le dire + où on chercherait.

**Architecture / choix**
- *Pourquoi Spring Boot 4 / Java 21 ?* → Virtual Threads (scalabilité I/O sans réécriture), écosystème sécu mature. ADR-001.
- *Pourquoi pgvector, pas Pinecone ?* → une seule base, données UE, HNSW < 10 ms p95. ADR-005.
- *Pourquoi Groq, pas OpenAI ?* → latence (~150 vs ~30 tok/s) → UX interactive ; fallback Java si indispo. ADR-004.
- *Multi-tenant, isolation ?* → `WorkspaceAccessInterceptor` + contrôle rôle service + filtrage `workspace_id` (anti-IDOR).

**Front (bloc 2)**
- *Accessibilité prouvée ?* → axe-core en CI (E2E `a11y.spec.ts`), Radix ARIA natif, focus/contrastes WCAG AA.
- *Sécurité côté API front ?* → JWT en header, refresh auto sur 401, refresh token en cookie HttpOnly.

**Back (bloc 3)**
- *Authentification ?* → Keycloak émet des tokens **OIDC RS256** ; l'API est Resource Server (JWK + issuer). *Raconter la migration depuis HS512 : dette identifiée (veille ANSSI) → corrigée → 658 tests verts.*
- *Injection / validation ?* → JPA paramétré + `@Valid` sur tous les DTOs + chiffrement AES-256-GCM.
- *Tests d'intégration fiables ?* → Testcontainers (vrai Postgres+pgvector, vraies migrations), pas de mock DB. 78 %.
- *Sécurité du paiement ?* → délégation Stripe (iframe PCI-DSS), webhooks signés + idempotents.

**Recul**
- *Le plus difficile ?* → (réponse sincère préparée : ex. observabilité OTel, ou migration auth).
- *Que feriez-vous différemment ?* → formaliser les ADR **avant** de coder (le JWT HS512 est né d'un glissement) ; tests de charge plus tôt.
- *Ça passe à l'échelle ?* → back stateless → scale-out ; rate limiting déjà distribué (Redis) ; limite : mono-instance en V1.

---

## 6. Logistique & conseils

- **Répéter chronométré** 2–3 fois ; couper ce qui déborde (dans A et D, jamais B/C).
- **Slides sobres** : 1 idée / slide, un visuel fort (réutiliser C4, MCD, séquences du Brain OS).
- **Preuves à portée** : Brain OS + repo + Swagger + rapports de tests ouverts (« montrez-moi »).
- **Plan B démo** : screencast enregistré.
- **Ne pas survendre** : nommer les limites avant le jury = crédibilité.

---

> 🔗 [[README|Matrice des 32 compétences]] · [[Architecture_C4]] · [[Modele_Donnees_MCD_MLD]] ·
> [[Diagrammes_Sequence_UML]] · [[Note_Innovation_Distance_Critique]] · [[Journal_Decisions_ADR]] ·
> [[Bloc2_Frontend]] · [[Bloc3_Backend]] · [[Release_Notes]]

**Dernière mise à jour :** 06/07/2026 · **Version :** 1.0 (calibrée blocs 2 & 3 + matrice de couverture)
