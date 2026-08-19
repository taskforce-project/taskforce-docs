---
id: gantt-planning
title: Planning prévisionnel — Gantt & jalons
doc_type: planning
statut: valide
version: 1.0
date: "05/07/2026"
auteur: Pierre MICHEL
tags: [gantt, planning, jalons, calendrier, chemin-critique, memoire, rncp]
---

# 📊 Planning prévisionnel — Gantt & jalons

> Représentation temporelle du projet (format Gantt Mermaid + tableau jalons).
> Source : [[Plan_Projet]] + dates réelles observées.
> Pour les dépendances entre tâches → [[Diagramme_PERT]].

---

## Diagramme de Gantt

```mermaid
gantt
    title TaskForce — Planning V1 (nov. 2025 → juil. 2026)
    dateFormat  YYYY-MM-DD
    axisFormat  %b %y

    section Cadrage & Conception
    Initialisation & cadrage          :done,    p0, 2025-11-04, 2025-11-15
    Conception fonctionnelle          :done,    p1, 2025-11-18, 2025-11-29
    Conception technique              :done,    p2, 2025-12-02, 2025-12-20

    section Développement
    M1 — Core (auth, multi-tenant, Stripe)       :done,    m1, 2026-01-02, 2026-01-31
    M2 — Métier (projets, issues, smart-assign)  :done,    m2, 2026-02-03, 2026-02-28
    M3 — Enrichissement (chat, Brain OS, RGPD)   :done,    m3, 2026-03-03, 2026-03-28

    section Tests & Qualité
    Tests & validation                :done,    t1, 2026-03-31, 2026-04-26
    Itérations & correctifs           :done,    t2, 2026-05-26, 2026-06-20

    section Déploiement & Docs
    Déploiement prod (VM école)       :active,  d1, 2026-04-28, 2026-05-23
    Documentation finale (~97 docs)   :active,  d2, 2026-06-23, 2026-07-05

    section Jalons clés
    Jalon — Core livré                :milestone, j1, 2026-01-31, 0d
    Jalon — Stripe + SaaS actif       :milestone, j2, 2026-02-28, 0d
    Jalon — RGPD + a11y               :milestone, j3, 2026-03-28, 0d
    Jalon — Tests OK (JaCoCo ≥ 60%)  :milestone, j4, 2026-04-26, 0d
    Jalon — Feature freeze            :milestone, j5, 2026-06-20, 0d
    Soutenance RNCP                   :crit,       j6, 2026-07-05, 0d
```

---

## Jalons clés

| Jalon | Date | Critère de réussite | Statut |
|---|---|---|---|
| **J1 — Core livré** | 31/01/2026 | Auth Keycloak + multi-tenant + CRUD projets/issues | ✅ |
| **J2 — SaaS actif** | 28/02/2026 | Stripe FREE/PRO opérationnel + webhooks | ✅ |
| **J3 — RGPD + a11y** | 28/03/2026 | Export portabilité + axe-core < 10 violations | ✅ |
| **J4 — Tests OK** | 26/04/2026 | JaCoCo ≥ 60 %, Vitest ≥ 70 %, ZAP 0 HIGH | ✅ |
| **J5 — Feature freeze** | 20/06/2026 | Plus de nouvelles features — doc uniquement | ✅ |
| **J6 — Soutenance RNCP** | Juillet 2026 | Bundle PDF + démo + mémoire complet | 🔄 |

---

## Durées et charge estimée

| Phase | Durée calendaire | Charge estimée |
|---|---|---|
| Cadrage & Conception | 7 semaines | 3–4 h/jour |
| Développement (M1–M3) | 12 semaines | 5–7 h/jour |
| Tests & Validation | 4 semaines | 4–5 h/jour |
| Déploiement | 4 semaines | 2–3 h/jour |
| Documentation finale | 2 semaines | 6–8 h/jour |

> **Total estimé** : ~9 mois (nov. 2025 – juil. 2026) · ~1 600 h équivalent temps plein
> (projet en parallèle de la formation).

> 🔗 Voir aussi : [[Plan_Projet]] · [[Diagramme_PERT]] · [[Budget_Previsionnel]] ·
> [[Note_Methode_Agile]].
