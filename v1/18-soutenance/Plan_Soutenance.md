---
id: plan-soutenance
title: Plan de soutenance — TaskForce (15-20 min + Q&A)
doc_type: soutenance
statut: en-cours
version: 0.1
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, plan, slides, demo, qa, rncp, dfs]
---

# 🗺️ Plan de soutenance — TaskForce

> **Format** : 15–20 min de présentation + ~10 min de questions.
> **Objectif** : prouver la maîtrise des 4 blocs (32 compétences) par un **produit réel** + des
> **choix techniques justifiés** + une **distance critique** assumée.
> **Cible de durée** : viser **17 min** (marge de sécurité), ~15 slides.

---

## 1. Arc narratif (la ligne directrice)

> « Un problème réel d'équipe → un produit qui l'automatise avec de l'IA → une ingénierie de niveau
> pro (sécurité, tests, RGPD, CI/CD) → une lucidité sur ce qui reste à faire. »

Trois messages à faire passer, quoi qu'il arrive :
1. **Le produit marche et résout un vrai problème** (démo Smart Assign).
2. **Les choix techniques sont justifiés, pas subis** (ADR, distance critique).
3. **La démarche est rigoureuse et honnête** (tests, sécurité, dette tracée puis corrigée).

---

## 2. Découpage slide-par-slide (timing indicatif)

| # | Slide | Durée | Contenu clé | Bloc/compétence |
|:-:|-------|:----:|-------------|-----------------|
| 1 | **Titre** | 0:20 | TaskForce · Développeur Full Stack · nom · date · logos | — |
| 2 | **Le problème** | 1:00 | Répartition manuelle des tâches = surcharge, perte de visibilité. Chiffre/anecdote. | C1 |
| 3 | **La solution + périmètre V1** | 1:30 | ERP modulaire SaaS : workspaces, projets, issues, **Smart Assign IA**, temps réel, billing. Ce qui est livré vs hors-périmètre. | C1–C3 |
| 4 | **Stack & architecture (C4)** | 2:00 | Diagramme C4 conteneurs : Next.js · Spring Boot 4/Java 21 · PostgreSQL+pgvector · Keycloak · Groq · RabbitMQ · MinIO · SigNoz. Multi-tenant. | C7–C10, C22 |
| 5 | **🎬 DÉMO (le cœur)** | 4:30 | Voir §3 (script). Inscription→login→workspace→issue→**Smart Assign**→chat temps réel. | C13–C17, C21–C24 |
| 6 | **Zoom : Smart Assign** | 1:30 | 5 signaux pondérés (sémantique pgvector 0.45 + charge + historique + dispo + labels) + explication LLM Groq + growth mode. Le différenciateur. | C22, innovation |
| 7 | **Sécurité** | 1:30 | OWASP (headers, RBAC anti-IDOR, AES-256-GCM) · **auth OIDC RS256 Keycloak** (histoire de la migration = distance critique + remédiation). | C21, C24 |
| 8 | **Qualité & tests** | 1:15 | 78 % back (JaCoCo, 658 tests, Testcontainers no-mock) · 92 % front (Vitest, 746) · E2E Playwright + axe-core WCAG. | C18, C25 |
| 9 | **RGPD & conformité** | 1:00 | Export/effacement (+ suppression Keycloak) · registre Art.30 · chiffrement PII · notice cookies. | C11 |
| 10 | **CI/CD & observabilité** | 1:15 | 7 workflows GitHub Actions · GHCR · OTel→SigNoz · 9 alertes Prometheus (dont sécu). | C26, C31, C32 |
| 11 | **Déploiement** | 0:45 | 2 options (VM école / Render Frankfurt) · Docker · nginx TLS · rate limiting Redis distribué. | C28–C30 |
| 12 | **Distance critique** | 1:15 | Ce qui n'est pas parfait : tests de charge absents, DAST pas en CI bloquant, DPA Groq, app monolingue. + ce que j'ai corrigé (JWT, rate-limit, RGPD Keycloak). | innovation |
| 13 | **Ce que j'ai appris** | 0:45 | Montée en compétence : IA/embeddings, sécurité OIDC, observabilité, rigueur doc (Brain OS). | C12 |
| 14 | **Roadmap** | 0:30 | Prochaines étapes produit + dette V1.1 tracée (backlog). | C3 |
| 15 | **Conclusion / merci** | 0:20 | Synthèse 1 phrase + ouverture questions. | — |

**Total ≈ 17 min.** Slides 5–6 (démo + Smart Assign) = le pic ; ne pas les sacrifier si on déborde
ailleurs.

---

## 3. Script de démo (4–5 min, répété et sécurisé)

> **Règle d'or** : parcours **court, linéaire, sans surprise**, sur un jeu de données préparé (seed).
> Prévoir une **vidéo de secours** (screencast) si le réseau/Keycloak/Groq flanche le jour J.

1. **Login** (20 s) — montrer la connexion Keycloak (mentionner : tokens OIDC RS256, pas de mot de
   passe stocké côté app). Arriver sur le dashboard workspace.
2. **Créer une issue** (40 s) — raccourci `C`, titre, description, priorité. Montrer la vue Kanban.
3. **⭐ Smart Assign** (90 s) — sur l'issue, cliquer « Suggérer un assigné ». Montrer :
   - les candidats classés avec **score** et **signaux détaillés**,
   - l'**explication en langage naturel** (Groq),
   - accepter une suggestion → feedback stocké.
   *C'est le moment fort : prendre le temps, expliquer les 5 signaux à voix haute.*
4. **Temps réel** (40 s) — ouvrir un canal de chat, envoyer un message (mentionner STOMP/WebSocket +
   fallback SockJS). Idéalement une 2ᵉ fenêtre pour montrer la synchro live.
5. **Bonus si le temps** (30 s) — un cycle (sprint) ou une page wiki, ou l'export RGPD dans les
   paramètres.

**Checklist pré-démo** : seed chargé (`db.ps1 seed`), workspace de démo prêt, GROQ_API_KEY valide,
onglets déjà ouverts, zoom navigateur lisible, mode clair, notifications OS coupées.

---

## 4. Préparation Q&A (~10 min) — questions anticipées

> Répondre **court, honnête, avec une preuve**. Si on ne sait pas : le dire + où on chercherait.

**Architecture & choix techniques**
- *Pourquoi Spring Boot 4 / Java 21 ?* → Virtual Threads (scalabilité I/O sans réécriture), écosystème
  sécurité mature. ADR-001.
- *Pourquoi pgvector et pas Pinecone/Weaviate ?* → une seule base (moins d'ops), données dans l'UE,
  index HNSW < 10 ms p95. ADR-005.
- *Pourquoi Groq et pas OpenAI ?* → latence (~150 vs ~30 tokens/s) → UX interactive ; fallback Java si
  indispo. ADR-004. Limite assumée : dépendance US, DPA à formaliser.
- *Multi-tenant, comment isolez-vous les données ?* → `WorkspaceAccessInterceptor` + contrôle rôle au
  niveau service ; filtrage `workspace_id` systématique (anti-IDOR, OWASP A01).

**Smart Assign / IA**
- *Comment marche le score ?* → 5 signaux pondérés (sémantique 0.45 / charge 0.22 / historique 0.15 /
  dispo 0.10 / labels 0.08) ; embeddings `all-MiniLM-L6-v2` (384d) en pgvector ; explication LLM.
- *Et si Groq est down ?* → dégradation gracieuse : le moteur Java produit un résultat sans
  l'explication en langage naturel.

**Sécurité**
- *Comment gérez-vous l'authentification ?* → Keycloak émet des tokens **OIDC RS256** ; l'API est un
  Resource Server (validation JWK + issuer). *Raconter la migration depuis le JWT HS512 custom : une
  dette que j'ai identifiée (veille ANSSI), documentée, puis corrigée et vérifiée (658 tests).*
- *Injection / validation ?* → Bean Validation `@Valid` sur tous les DTOs ; requêtes JPA paramétrées ;
  chiffrement AES-256-GCM des PII sensibles.

**Tests & qualité**
- *Vos tests d'intégration sont-ils fiables ?* → oui, **Testcontainers** (vrai Postgres+pgvector, vraies
  migrations Flyway), pas de mock DB (ADR-007). 78 % back / 92 % front + E2E Playwright.
- *Couverture ≠ qualité, non ?* → d'accord ; on couvre aussi les cas limites (tests paramétrés) et les
  parcours E2E ; limite reconnue : pas de tests de **charge** (tracé TF-TEST-009).

**RGPD**
- *Droit à l'effacement ?* → anonymisation locale + suppression de l'identité Keycloak (après commit,
  tolérant à l'échec) + journalisation d'audit.

**Recul / posture**
- *Qu'est-ce qui a été le plus difficile ?* → (préparer une réponse sincère : ex. l'observabilité OTel,
  ou la migration auth).
- *Que feriez-vous différemment ?* → formaliser les ADR **avant** de coder (le JWT HS512 est né d'un
  glissement non décidé) ; tests de charge plus tôt.
- *Comment ça passe à l'échelle ?* → backend stateless (tokens auto-suffisants) → scale-out horizontal ;
  rate limiting déjà distribué (Redis) ; limites : mono-instance en V1, pas d'auto-scaling.

---

## 5. Logistique & conseils

- **Répéter à voix haute, chronométré**, 2–3 fois. Couper ce qui fait déborder.
- **Slides sobres** : 1 idée par slide, peu de texte, un visuel/diagramme fort (réutiliser les
  diagrammes du Brain OS : C4, séquences, MCD).
- **Preuves à portée** : garder un onglet Brain OS + le repo ouverts pour répondre « montrez-moi ».
- **Plan B démo** : screencast enregistré de la démo (au cas où).
- **Ne pas survendre** : nommer les limites avant que le jury ne les trouve = crédibilité.

---

> 🔗 [[README|Matrice des 32 compétences]] · [[Architecture_C4]] · [[Diagrammes_Sequence_UML]] ·
> [[Note_Innovation_Distance_Critique]] · [[Journal_Decisions_ADR]] · [[Release_Notes]] · [[Manuel_Utilisateur]]

**Dernière mise à jour :** 05/07/2026 · **Version :** 0.1
