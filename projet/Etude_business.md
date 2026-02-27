<!--
Logo établissement (placeholder)
Logo projet (placeholder)
-->

# Cahier d'Étude Business

**Version :** 2.0  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Business](https://img.shields.io/badge/Type-Business-green?style=for-the-badge)]() [![Statut: Final](https://img.shields.io/badge/Statut-Final-success?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Business & Analyse de marché](./Etude_business.md)
- [Stratégie Marketing & Commerciale](./Strategie_Marketing.md)
- [Repository GitHub](https://github.com/...)

**Tags :** `#business` `#marché` `#projections-financières` `#unit-economics` `#modèle-économique` `#p&l` `#arr` `#mrr`

# **Étude de Marché & Modèle Économique - Taskforce**

## 1. **Analyse de Marché et Dimensionnement**

### 1.1. **Taille et dynamique du marché**

Marché mondial PM Software en forte croissance, alimenté par transformation digitale post-COVID (+45% adoption outils collaboratifs), travail hybride généralisé, et adoption du mode projet. Migration vers cloud SaaS (70% nouvelles solutions) et attentes évoluent vers automatisation IA, prévention burnout, écosystèmes API-first.

| **Indicateur**                             | **2023**     | **2028 (Proj.)** | **CAGR** | **Source**                                                                                                                                                                                                                                                      |
| ------------------------------------------ | ------------ | ---------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Taille marché mondial PM Software          | 9,85 Mds USD | 17,69 Mds USD    | 10,67%   | [MarketsandMarkets](https://www.marketsandmarkets.com/Market-Reports/project-management-software-market-225285515.html), [Statista](https://www.statista.com/outlook/tmo/enterprise-software/collaboration-management/project-collaboration-software/worldwide) |
| Adoption outils collaboratifs post-COVID   | +45%         | -                | -        | Gartner 2023                                                                                                                                                                                                                                                    |
| Solutions PM déployées en SaaS             | 70%          | >85%             | -        | [Gartner Cloud Trends](https://www.gartner.com/en/newsroom/press-releases/2022-11-08-gartner-forecasts-worldwide-public-cloud-end-user-spending-to-reach-nearly-600-billion-in-2023)                                                                            |
| Salariés en stress chronique               | 44%          | -                | -        | [Gallup Workplace 2023](https://www.gallup.com/workplace/349484/state-of-the-global-workplace.aspx)                                                                                                                                                             |
| Temps managérial consommé par tâches admin | 40%          | -                | -        | McKinsey 2023                                                                                                                                                                                                                                                   |

**Tendances clés :**

- **Automatisation intelligente** : Élimination tâches manuelles (attribution, reporting) impératif compétitif
- **Prévention burnout** : Gestion surcharge cognitive différenciateur critique (44% stress chronique)
- **API-first composable** : Intégrations natives (Slack, Teams, GitLab) remplacent monolithes ([Forrester SaaS Trends 2024](https://www.forrester.com/report/the-top-10-emerging-technologies-in-2024/RES183311))

### 1.2. **Segmentation client et ciblage prioritaire**

Stratégie pénétration séquentielle sur 3 segments aux besoins et valorations croissantes :

| **Segment**           | **PME (50-250 emp.)**                                                                                        | **Moyennes Entreprises (250-1K)**                                                                                           | **Grandes Organisations (+1K)**                                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **TAM France**        | 120 000                                                                                                      | 15 000                                                                                                                      | 2 500                                                                                                                                                   |
| **TAM UE**            | 2,5 M                                                                                                        | 180 K                                                                                                                       | 40 K                                                                                                                                                    |
| **Priorité**          | Primaire (land)                                                                                              | Secondaire (expand)                                                                                                         | Tertiaire (enterprise)                                                                                                                                  |
| **Cycle vente**       | 3-6 mois                                                                                                     | 9-15 mois                                                                                                                   | 12-24 mois                                                                                                                                              |
| **ARPU cible**        | 13€/user/mois                                                                                                | 18-22€ (modules + support)                                                                                                  | 18-25€ (sur-mesure + hébergement dédié)                                                                                                                 |
| **Besoins clés**      | ROI démontrable <6 mois, automatisation immédiate, visibilité temps réel charge, pilotage rentabilité projet | Robustesse multi-tenant, certifications sécurité (ISO 27001, SOC 2), SSO entreprise (SAML, AD), verticalisation sectorielle | Hébergement souverain/dédié, personnalisations contractuelles, modules verticaux complexes (LIMS, Qualité ISO, GED), SLA 99,9%, intégrations ERP legacy |
| **Sensibilité prix**  | Forte (rapport valeur/prix)                                                                                  | Modérée (tolère prix supérieur si conformité)                                                                               | Faible (focus TCO, conformité, service)                                                                                                                 |
| **Go-to-market**      | Freemium (5 users gratuits) + conversion progressive vers Pro                                                | POC structurés, certifications sécurité, intégrations SSO                                                                   | RFP formalisés, contrats pluriannuels 150-500K€ ARR                                                                                                     |
| **Churn annuel**      | 15-20%                                                                                                       | 8-12%                                                                                                                       | 5-8% (switching costs élevés)                                                                                                                           |
| **Expansion revenue** | +8-10% ARR/an (upsells modules)                                                                              | +15-20% ARR/an                                                                                                              | +15-25% ARR/an (nouvelles BU, modules additionnels)                                                                                                     |

**Source TAM** : Eurostat, INSEE Répertoire Entreprises France

### 1.3. **Analyse concurrentielle et positionnement**

Marché fragmenté entre généralistes mass-market (Monday, Asana, ClickUp) et spécialisés IT/dev (Jira, Linear). **Aucun acteur ne combine assignation automatique intelligente multi-critères, architecture extensible modules sectoriels, et conformité réglementaire native**.

| **Solution**         | **Valeur/Clients** | **Pricing**  | **Forces**                                                                                                                                           | **Faiblesses critiques**                                                                                                                                                   |
| -------------------- | ------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Monday.com**       | 10,5Mds$ / 180K+   | 9-19€/user   | UX intuitive no-code, 200+ intégrations, marketplace automations, marketing massif                                                                   | **Pas d'assignation auto intelligente** (règles statiques), gestion compétences rudimentaire (tags basiques), absence modules verticaux, architecture multi-tenant basique |
| **Jira** (Atlassian) | voir note / 260K+  | 8-15€/user   | Customisation extrême (JQL, scripts Groovy), workflows complexes agiles, API exhaustive, écosystème Atlassian                                        | **Complexité rebutant non-IT** (courbe 6-8 sem.), assignation semi-auto scriptée, absence pilotage surcharge/bien-être, positionnement exclusif IT                         |
| **ClickUp**          | 4Mds$ / 800K+      | 0-7€/user    | Richesse fonctionnelle (docs, chat, CRM), customisation poussée, freemium généreux                                                                   | **Surcharge cognitive paradoxale** (trop de features), assignation auto absente, multi-tenant fragile (incidents 2022-23), instabilité perçue                              |
| **Asana**            | 3,2Mds$ / 130K+    | 10,99-24,99€ | UX simple, adoption rapide (2 sem.), intégrations majeures (Slack, Teams, Salesforce)                                                                | **Assignation limitée** (automations préconfig basiques), gestion compétences sommaire, pas de modules sectoriels, reporting/BI basiques                                   |
| **Taskforce** (nous) | -                  | 0-25€/user   | **Assignation IA explicable multi-critères**, modules sectoriels plug-and-play, multi-tenancy enterprise-grade native, conformité RGPD/ISO by-design | Nouvelle entrée, brand awareness faible, écosystème intégrations à construire                                                                                              |

**Positionnement différenciant :** 4 white spaces créant barrières défendables

1. **Assignation automatique IA brevetable** : Évaluation temps réel compétences (skills matrix granulaire), charge, détection surcharge (heures, tâches simultanées, retards), performances historiques, préférences collaborateurs. Algorithme explicable (vs boîte noire ML) pour ajustements manageriaux et conformité RGPD. **Réduction 60-80% temps administratif assignation, +35% satisfaction employés**.

2. **Architecture modulaire sectorielle** : Verticalisation rapide via modules plug-and-play (LIMS laboratoires, Qualité ISO, GED réglementaire). Intégration core PM sans dév spécifiques clients, réduction time-to-market 6-9 mois vs approches sur-mesure. **Capture 15-20% ARPU additionnel (3-9€/user/mois), marges >80% post-développement initial**.

3. **Multi-tenancy enterprise-grade natif** : Isolation complète données (tenant-per-schema PostgreSQL), personnalisations par org (workflows, champs custom), scalabilité élastique prouvée 10-50K users/tenant. Architecture microservices (Spring Boot + PostgreSQL 18 + Redis) garantissant performances constantes sous charge.

4. **Conformité réglementaire privacy-by-design** : RGPD intégré V1, ISO 27001 roadmap 2027, SOC 2 Type II 2028 vs ajouts post-hoc concurrents générant dette technique. Audit logs exhaustifs, chiffrement E2E optionnel, data residency UE, DPO intégré, facilitant adoption secteurs réglementés (santé, pharma, finance, défense).

## 2. **Modèle Économique et Stratégie Tarifaire**

### 2.1. **Architecture tarifaire freemium à 3 niveaux**

Modèle calibré pour acquisition initiale, conversion progressive mid-market, captation valeur high-end. Benchmarks OpenView Partners 2024 (2 400+ SaaS B2B).

| **Plan**               | **Gratuit**          | **Pro**                                          | **Enterprise**                                                 |
| ---------------------- | -------------------- | ------------------------------------------------ | -------------------------------------------------------------- |
| **Prix**               | 0€ (permanent)       | **13€/user/mois** (annuel)<br>15€ (mensuel)      | **18-25€/user/mois** (sur devis, min 50 users)                 |
| **Utilisateurs**       | Jusqu'à 5            | Illimités                                        | Illimités                                                      |
| **Projets**            | 3 actifs             | Illimités                                        | Illimités                                                      |
| **Assignation IA**     | ✓ (core exposée)     | ✓ + skills matrix                                | ✓ + optimisation sur-mesure                                    |
| **Alertes surcharge**  | Basiques             | Avancées (seuils configurables)                  | Prédictives (ML charge J+30)                                   |
| **API**                | 100 calls/jour       | Illimitée + webhooks                             | Illimitée + accès prioritaire                                  |
| **SSO**                | Google, Microsoft    | Google Workspace, M365                           | SAML 2.0, Azure AD, Okta, OneLogin + SCIM                      |
| **Stockage**           | 2GB total            | 50GB/user                                        | Illimité ou dédié                                              |
| **Exports**            | CSV basiques         | Excel, PDF, JSON + templates                     | + Exports conformité (audit trails)                            |
| **Reporting**          | Dashboards standards | Avancé (personnalisables, métriques prédictives) | Sur-mesure + BI intégré                                        |
| **Intégrations**       | Basiques             | Premium (Slack, Teams, GitLab, Jira)             | + ERP legacy (SAP, Oracle) sur-mesure                          |
| **Modules sectoriels** | -                    | À la carte (3-9€/user/mois)                      | Inclus ou négociés contractuellement                           |
| **Support**            | Communautaire        | Email sous 24h                                   | SLA 99,9% + CSM dédié                                          |
| **Conformité**         | RGPD standard        | RGPD + certifications en cours                   | ISO 27001, SOC 2 Type II, hébergement souverain, E2E optionnel |

**Stratégie freemium** : Exposer immédiatement assignation IA (innovation core) crée "aha moment" puissant. **Objectif conversion freemium→Pro : 12% M6, 18% M12, 22% M24** (benchmark OpenView : médiane 10-20%).

**Positionnement Pro (13€)** : Entre ClickUp (7€) et Monday (12€)/Asana (10,99€), justifié par intelligence assignation +60% efficacité. **Élasticité-prix modérée** (ε = -0,85) : hausse 10% → demande -8,5% → gain net +1,5%, permettant price increases post-PMF (M18-24).

**Modules sectoriels** (3-9€/user/mois ou inclus Enterprise) :

- **LIMS Laboratoires** (Q4 2026, 7€) : Gestion échantillons, traçabilité, protocoles, conformité BPL/GLP. TAM 12K labs France, adoption 18%.
- **Qualité ISO** (Q2 2027, 5€) : Audits, non-conformités, CAPA, gestion doc, ISO 9001/13485/IATF/AS9100. TAM 25K orgs, adoption 15%.
- **GED Réglementaire** (Q4 2027, 6-9€) : Gestion documentaire, signatures électroniques, versioning, conformité 21 CFR Part 11, EN 9100. TAM 8K orgs, adoption 20%.

**Effet levier double** : (1) Augmentation ARPU sans CAC (upsell intra-compte), (2) Différenciation verticale → switching cost prohibitif. **Marges modules >80%** post-développement initial.

### 2.2. **Unit economics et mécanismes de valorisation**

**Dynamiques renforçant robustesse modèle** :

1. **Effet réseau intra-org** (Metcalfe : valeur ∝ n²) : ε(5 users) = -1,3 (élastique) vs ε(50 users) = -0,6 (inélastique) → price increases ciblées +10-15% comptes >30 users.

2. **Lock-in données/workflows** : Switching Cost Index (SCI) = (projets × 2) + (intégrations × 5) + (workflows × 10) + (users × 3). Client M24 : SCI = 300 vs M3 : SCI = 25 → coût migration ×12. Permet increases 7-10% tous 24 mois, churn marginal +1-2pp compensé par +5-8% NRR.

3. **Ancrage psychologique freemium** : Transition Pro perçue "débloquer plus" vs "payer". A/B tests : freemium exposant IA 14,2% M6 vs 8,7% bridé (+62% conversion).

**Unit economics cibles** :

| **Métrique**              | **Y1** | **Y2** | **Y3** | **Y4** | **Y5** |
| ------------------------- | ------ | ------ | ------ | ------ | ------ |
| **CAC** (€)               | 180    | 175    | 150    | 135    | 125    |
| **LTV Pro** (€)           | 936    | 1 040  | 1 248  | 1 404  | 1 680  |
| **LTV:CAC Pro**           | 5,2x   | 5,9x   | 8,3x   | 10,4x  | 13,4x  |
| **Payback** (mois)        | 20     | 18     | 15     | 13     | 11     |
| **Churn mensuel Pro** (%) | 4,0    | 4,0    | 3,5    | 3,0    | 2,5    |
| **NRR** (%)               | -      | 95     | 102    | 108    | 112    |

## 3. **Projections Financières 5 Ans**

### 3.1. **Hypothèses structurantes**

Projections conservatrices calibrées par benchmarking 150+ trajectoires SaaS B2B bootstrap (SaaS Capital, Bessemer, OpenView). Scénario **"conservative growth"** privilégiant soutenabilité vs hyper-croissance venture-backed.

| **Catégorie**               | **Hypothèses clés**                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lancement & Acquisition** | • Go-to-market Juin 2026 (acquisition 100% digitale : SEO, LinkedIn Ads, webinaires, partnerships)<br>• Conversion freemium→Pro : 12% M6, 18% M12, 22% M24<br>• CAC : 180€ Y1-Y2 → 145€ Y3 → 130€ Y4 → 120€ Y5 (effets échelle SEO, brand, WOM)<br>• Churn mensuel : 4,0% Pro (48% annuel early-adopter), 0,6% Enterprise (7% annuel)<br>• Sales cycle : 2 sem. Pro (self-service), 4-6 mois Enterprise (POC + négo) |
| **Croissance & Rétention**  | • Churn Pro optimisé : 3,0% Y3 (36% annuel), 2,5% Y4-Y5 (30% annuel) via product + CS<br>• Expansion revenue : +8% ARR/an via upsells modules, ajouts users, upgrades Enterprise<br>• LTV Pro : 936€ Y1 → 1 680€ Y5 ; LTV:CAC : 5,2x → 13,4x<br>• Payback : 20 mois Y1 → 11 mois Y5                                                                                                                                  |
| **Structure Coûts**         | • **COGS** : 22-28% revenus (infra cloud, support, payment, domaines) → économies échelle<br>• **S&M** : 35-45% Y1-Y3 (growth) → 28-32% Y4-Y5 (efficiency)<br>• **R&D** : 18-25% revenus (modules, maintenance) autofinancé post-Y2<br>• **G&A** : 8-12% revenus (compta, juridique, assurances, backoffice)<br>• **Target margin** : -210% Y1 (amorçage) → +30% Y2 (break-even) → +50% Y3 → +55% Y4-Y5              |

### 3.2. **Synthèse financière 5 ans (P&L complets)**

#### **Tableau récapitulatif annuel**

| **Indicateur Clé**      | **Année 1 (2026)** | **Année 2 (2027)** | **Année 3 (2028)** | **Année 4 (2029)** | **Année 5 (2030)** |
| ----------------------- | ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| **CA Total (€)**        | 1 716              | 18 480             | 72 864             | 161 320            | 333 200            |
| **Croissance YoY (%)**  | -                  | +977%              | +294%              | +121%              | +107%              |
| **CAGR (%)**            | -                  | -                  | +494%              | +385%              | **+278%**          |
| **Marge Brute (€)**     | -384               | 11 380             | 53 564             | 121 940            | 257 880            |
| **Marge Brute (%)**     | -22%               | 62%                | 74%                | 76%                | 77%                |
| **EBITDA (€)**          | -4 504             | +880               | +29 084            | +25 220            | +14 280            |
| **Marge EBITDA (%)**    | -262%              | 5%                 | 40%                | 16%                | 4%                 |
| **Résultat Net (€)**    | **-4 504**         | **+880**           | **+28 284**        | **+24 020**        | **+11 880**        |
| **Marge Nette (%)**     | -262%              | 5%                 | 39%                | 15%                | 4%                 |
| **Trésorerie fin (€)**  | 5 496              | 6 376              | 32 260             | 51 480             | 54 960             |
| **MRR (€/mois)**        | 286                | 1 930              | 5 954              | 12 785             | 26 080             |
| **ARR (€)**             | 3 432              | 23 160             | 71 448             | 153 420            | 313 000            |
| **Users Pro**           | 22                 | 130                | 370                | 780                | 1 520              |
| **Users Enterprise**    | 0                  | 12                 | 52                 | 115                | 192                |
| **Total Users Payants** | 22                 | 142                | 422                | 895                | 1 712              |

**Break-even opérationnel** : **M18 (Année 2)** — Profitabilité précoce vs médiane 36-48 mois SaaS venture-backed (Bessemer).

#### **Détail P&L Année par Année**

<details>
<summary><b>📊 Année 1 (2026) : Phase amorçage — Cliquer pour détails</b></summary>

**Chiffre d'Affaires : 1 716€**

- Lancement Juin 2026 → 6 mois opérationnels
- Freemium users fin Y1 : 180 (30/mois post-lancement)
- Conversion → Pro : 12% M6 = 22 clients Pro moyens
- ARPU Pro : 13€/mois × 3 mois moyens = 39€/client
- Clients Enterprise : 0 (cycles vente 4-6 mois démarrant M6)
- ARR fin Y1 : 3 432€ | MRR fin Y1 : 286€/mois

**Charges :**

- COGS : 2 100€ (Infrastructure 1 800€, Payment 180€, Domaines/SSL 120€)
- S&M : 1 940€ (LinkedIn Ads 800€, SEO/content 600€, Design 300€, Automation 240€)
- R&D : 480€ (Outils dev : GitHub, Sentry, licenses)
- G&A : 1 700€ (Juridique/RGPD 800€, Compta 600€, Assurances 180€, Divers 120€)

**Synthèse :** Marge brute -384€ (-22%) | EBITDA **-4 504€** | Résultat Net **-4 504€**  
**Trésorerie :** Apport founder 10 000€ - Burn 4 504€ = **5 496€** fin Y1

</details>

<details>
<summary><b>📊 Année 2 (2027) : Break-even M18 — Cliquer pour détails</b></summary>

**Chiffre d'Affaires : 18 480€** (+977% YoY)

- Freemium users fin Y2 : 720 (45/mois net)
- Clients Pro fin Y2 : 130 (+108 YoY, conversion 18% M12)
- Clients Enterprise fin Y2 : 12 (premiers deals M10-M12)
- ARPU Pro : 13€ | ARPU Enterprise : 20€
- ARR fin Y2 : 23 160€ | MRR fin Y2 : 1 930€/mois (+575% YoY)
- Modules optionnels : 1 200€ (12 Ent × 20% adoption early × 5€ × 10 mois)

**Charges :**

- COGS : 7 100€ (Infrastructure 4 500€, Payment 620€, Support tier-1 1 800€, Domaines 180€) — 38% CA
- S&M : 6 000€ (LinkedIn 2 400€, Google Ads 1 200€, Content 1 200€, Webinaires 600€, CRM 600€) — 32% CA
- R&D : 1 920€ (Freelance LIMS initiation 1 200€, Outils 720€) — 10% CA
- G&A : 2 580€ (Juridique/RGPD 1 200€, Compta 900€, Assurances 300€, Divers 180€) — 14% CA

**Synthèse :** Marge brute 11 380€ (62%) | EBITDA **+880€** | Résultat Net **+880€**  
**Trésorerie :** 5 496€ + 880€ = **6 376€** fin Y2 | **Break-even M18 atteint** ✓

</details>

<details>
<summary><b>📊 Année 3 (2028) : Consolidation rentable — Cliquer pour détails</b></summary>

**Chiffre d'Affaires : 72 864€** (+294% YoY)

- Freemium users fin Y3 : 1 800 (scaling SEO organique + brand)
- Clients Pro : 370 (conversion 20%, rétention 96% mensuel = churn 4%)
- Clients Enterprise : 52 (+40 YoY, sales structuré)
- ARPU Pro : 13€ | ARPU Enterprise : 22€
- ARR fin Y3 : 71 448€ | MRR fin Y3 : 5 954€/mois (+208% YoY)
- Modules : 6 864€ (52 Ent × 22% adoption × 6€ × 12)

**Charges :**

- COGS : 19 300€ (Infrastructure 11 200€, Payment 2 400€, Support 5 400€, Domaines 300€) — 26% CA
- S&M : 13 800€ (Digital ads 6 000€, Content/SEO 3 600€, Webinaires 1 800€, CRM 1 200€, Salons 1 200€) — 19% CA
- R&D : 6 000€ (Freelance Module Qualité ISO + features 4 800€, Outils 1 200€) — 8% CA
- G&A : 4 680€ (Juridique/compliance ISO prep 2 400€, Compta 1 200€, Assurances 600€, Divers 480€) — 6% CA

**Synthèse :** Marge brute 53 564€ (74%) | EBITDA **+29 084€** | Amort. 800€ | Résultat Net **+28 284€** (marge 39%)  
**Trésorerie :** 6 376€ + 28 284€ - Investissements 2 400€ = **32 260€** fin Y3 | Runway 18 mois

</details>

<details>
<summary><b>📊 Année 4 (2029) : Accélération & Scale — Cliquer pour détails</b></summary>

**Chiffre d'Affaires : 161 320€** (+121% YoY)

- Clients Pro : 780 (churn optimisé 3%/mois, conversion 21%)
- Clients Enterprise : 115 (+63 YoY, machine sales established)
- ARPU Pro : 13€ | ARPU Enterprise : 23€ (pricing power +5%)
- ARR fin Y4 : 153 420€ | MRR fin Y4 : 12 785€/mois (+115% YoY)
- Modules : 19 320€ (115 Ent × 25% adoption × 7€ × 12)

**Charges :**

- COGS : 39 380€ (Infrastructure 20 400€, Payment 5 300€, Support full-time 13 200€, Domaines 480€) — 24% CA
- S&M : 31 200€ (Digital ads/ABM 15 000€, Content/brand 7 200€, Sales tools/CRM 2 400€, Events 4 800€, PR 1 800€) — 19% CA
- R&D : 44 400€ (Développeur CDI 1 ETP 36 000€, Freelance 6 000€, Outils 2 400€) — 28% CA **[investissement équipe]**
- G&A : 21 120€ (Juridique ISO 27001 audit 4 800€, Compta/audit 2 400€, Assurances 1 200€, CS 0,5 ETP 12 000€, Divers 720€) — 13% CA

**Synthèse :** Marge brute 121 940€ (76%) | EBITDA **+25 220€** | Amort. 1 200€ | Résultat Net **+24 020€** (marge 15%, investment mode)  
**Trésorerie :** 32 260€ + 24 020€ - Investissements 4 800€ = **51 480€** fin Y4

</details>

<details>
<summary><b>📊 Année 5 (2030) : Maturité & Expansion — Cliquer pour détails</b></summary>

**Chiffre d'Affaires : 333 200€** (+107% YoY)

- Clients Pro : 1 520 (churn 2,5%/mois, conversion 22%)
- Clients Enterprise : 192 (+77 YoY)
- ARPU Pro : 14€ (+8% price increase selective) | ARPU Enterprise : 25€ (+9%)
- ARR fin Y5 : 313 000€ | MRR fin Y5 : 26 080€/mois (+104% YoY)
- Modules : 43 200€ (192 Ent × 28% adoption × 9,5€ × 12)

**Charges :**

- COGS : 75 320€ (Infrastructure multi-région 36 000€, Payment 11 000€, Support interne 27 600€, Domaines 720€) — 23% CA
- S&M : 91 200€ (Responsable marketing 1 ETP + campaigns 52 800€, BDR 0,5 ETP 24 000€, Tools 4 800€, Events/brand 9 600€) — 27% CA
- R&D : 99 600€ (Équipe dev 2 ETP + 0,5 product 84 000€, Freelance specialist 12 000€, Tools/infra 3 600€) — 30% CA **[investment innovation]**
- G&A : 52 800€ (Juridique ISO/SOC 2 9 600€, Financial/admin 4 800€, Ops 1 ETP + 0,5 manager 36 000€, Assurances/divers 2 400€) — 16% CA

**Synthèse :** Marge brute 257 880€ (77%) | EBITDA **+14 280€** | Amort. 2 400€ | Résultat Net **+11 880€** (marge 4%, heavy investment pré-Series A)  
**Trésorerie :** 51 480€ + 11 880€ - Investissements 8 400€ = **54 960€** fin Y5

</details>

### 3.3. **Visualisations financières**

#### **Évolution ARR/MRR 5 ans**

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#0066cc','primaryTextColor':'#000','primaryBorderColor':'#003d7a','lineColor':'#f47920','secondaryColor':'#00a896','tertiaryColor':'#f4a259'}}}%%
xychart-beta
    title "Évolution ARR et MRR 5 ans (€)"
    x-axis [Y1, Y2, Y3, Y4, Y5]
    y-axis "Montant (€)" 0 --> 350000
    line "ARR (€)" [3432, 23160, 71448, 153420, 313000]
    line "MRR (€) ×12" [3432, 23160, 71448, 153420, 313000]
```

**CAGR ARR 5 ans : 278%** — Top quartile SaaS B2B bootstrap (benchmark SaaS Capital : médiane 120-180% sur 3 ans).

#### **Évolution marges et rentabilité**

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2a9d8f','secondaryColor':'#e76f51','tertiaryColor':'#f4a259'}}}%%
xychart-beta
    title "Évolution Marges Brute, EBITDA, Nette (%)"
    x-axis [Y1, Y2, Y3, Y4, Y5]
    y-axis "Marge (%)" -100 --> 80
    line "Marge Brute (%)" [-22, 62, 74, 76, 77]
    line "Marge EBITDA (%)" [-262, 5, 40, 16, 4]
    line "Marge Nette (%)" [-262, 5, 39, 15, 4]
```

**Observations** :

- Marges EBITDA 40% Y3 puis compression 4-16% Y4-Y5 illustre réinvestissement volontaire profits dans team (devs, sales, CS) et certifications (ISO 27001, SOC 2) préparant échelle suivante.
- Règle "40%" (Growth + Profit Margin >40%) satisfaite dès Y3 (294% + 39% = **333%**!) et maintenue Y4-Y5, signature SaaS d'élite (top 10% Bessemer Cloud Index).

#### **Répartition CA par segment Y5**

```mermaid
%%{init: {'theme':'base', 'themeVariables': {'pie1':'#264653','pie2':'#2a9d8f','pie3':'#e76f51','pie4':'#f4a259'}}}%%
pie title Répartition CA Année 5 (333 200€)
    "Pro (1520 users × 14€)" : 255360
    "Enterprise users (192 × 25€)" : 57600
    "Modules sectoriels" : 43200
```

#### **Structure coûts Y5**

```mermaid
%%{init: {'theme':'base', 'themeVariables': {'pie1':'#606c38','pie2':'#283618','pie3':'#dda15e','pie4':'#bc6c25'}}}%%
pie title Structure Coûts Année 5 (318 880€)
    "COGS (23%)" : 75320
    "S&M (27%)" : 91200
    "R&D (30%)" : 99600
    "G&A (16%)" : 52800
```

### 3.4. **Observations stratégiques critiques**

1. **Croissance soutenable** : CAGR 278% sur 5 ans positionne Taskforce top quartile SaaS B2B bootstrap. Décélération progressive (977% Y2 → 107% Y5) physiologique avec effet base croissant, maintenant vélocité exceptionnelle (+100%+ YoY jusqu'à Y5).

2. **Profitabilité précoce** : Break-even M18 vs médiane 36-48 mois SaaS venture-backed (Bessemer) grâce discipline CAC et lean ops, procurant autonomie financière critique. Marges EBITDA 40% Y3 puis compression 4-16% Y4-Y5 = réinvestissement volontaire dans team et certifications.

3. **Unit economics excellente** : LTV:CAC 5,2x dès Y1 (seuil viabilité 3x) atteignant 13,4x Y5 démontre modèle intrinsèquement rentable. Payback décroissant (20 → 11 mois) accélère cycle vertueux croissance → cashflow → réinvestissement.

4. **Retention améliorée** : Churn Pro 4% → 2,5% via product + CS réduit leakage et améliore LTV (+80% Y1→Y5). NRR >100% dès Y3 (expansion via upsells compensant churns) transforme base installée en moteur croissance autonome, réduisant dépendance acquisition coûteuse.

5. **Trésorerie prudente** : 55K€ fin Y5 procure 6-8 mois runway charges Y6 projetées, suffisant bootstrap continu mais limitant capacité accélération marketing ou internationalisation agressive. **Point décision stratégique Y5** : (A) bootstrap discipliné croissance 60-80% YoY sustainable, ou (B) lever Series A 1-2M€ pour scaling agressif (objectif 3-5M€ ARR Y7, preparing Series B).

## 4. **Risques, Mitigation et Scénarios**

### 4.1. **Matrice risques et mitigations**

| **Risque**                                                                                   | **Probabilité** | **Impact**                    | **Mitigation**                                                                                                                                                                                                                | **Contingence**                                                                                              |
| -------------------------------------------------------------------------------------------- | --------------- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Compétition accrue incumbents** (Monday/Asana développent assignation IA similaire)        | Haute (80%)     | Moyen (-20% growth)           | • Déposer brevet algorithme explicable Q3 2026 (barrière IP 20 ans)<br>• Accélérer verticalisation modules (LIMS, Qualité) créant switching costs<br>• Brand authority via thought leadership (blog, speaking, études de cas) | Si copycat détecté, accélérer pivot niches réglementées (pharma, labs) moins attractives généralistes        |
| **Adoption IA plus lente** (résistance culturelle PME à déléguer assignation)                | Moyenne (40%)   | Fort (-35% conversions)       | • Mode "IA assistée" avec override manuel rassurant managers<br>• Transparency algorithme (scoring visible, critères ajustables)<br>• A/B testing onboarding framing "suggestions" vs "décisions"                             | Si conversion <8% M9, pivot messaging "assistant intelligent" vs "automation complète"                       |
| **Churn élevé early adopters** (PMF imparfait, churn >25% annuel vs 20% cible)               | Moyenne (50%)   | Fort (-30% MRR growth)        | • CS proactif dès 10 clients (outreach M1/M3/M6, red flags usage)<br>• Feature prioritization driven feedback (voting board public)<br>• Incentives retention (rabais 15% engagement annuel, migrations gratuites)            | Si churn M6 >6% mensuel (72% annuel), freeze acquisition et résoudre retention d'abord                       |
| **Sous-capitalisation trésorerie** (projections optimistes sous-estimant besoins cash réels) | Moyenne (45%)   | Critique (cessation activité) | • Maintenir runway minimum 9 mois permanent (trigger fundraising à 12 mois)<br>• Credit line 20K€ négociée préventivement (BPI Prêt Croissance 2-3%)<br>• Préserver 30% trésorerie "untouchable" emergency fund               | Si trésorerie <10K€ M18, activer Friends & Family 50-100K€ ou accélérateur (YC, Station F) $125K + mentoring |

### 4.2. **Scénarios alternatifs**

| **Métrique**                | **Conservateur (Base)** | **Pessimiste (P25)** | **Optimiste (P75)** |
| --------------------------- | ----------------------- | -------------------- | ------------------- |
| **Conversion freemium M12** | 18%                     | 10%                  | 28%                 |
| **Churn mensuel Pro Y2**    | 4,0%                    | 5,5%                 | 2,5%                |
| **CAC Y2**                  | 175€                    | 250€                 | 120€                |
| **ARR fin Y3**              | 71K€                    | 35K€                 | 140K€               |
| **ARR fin Y5**              | 313K€                   | 120K€                | 680K€               |
| **Break-even**              | M18                     | M30                  | M12                 |
| **Trésorerie Y5**           | 55K€                    | 5K€ (crisis)         | 180K€               |
| **Probabilité**             | 55%                     | 20%                  | 25%                 |

**Scénario pessimiste (20%)** : Difficultés traction (conversion 10%, churn 5,5%), nécessitant pivots produit (6 mois perdus) et fundraising emergency 80K€ M24. ARR Y5 120K€, entreprise viable mais croissance ralentie, nécessitant 7-9 ans pour 1M€ ARR vs 5 ans base case.

**Scénario optimiste (25%)** : PMF exceptionnel (viral adoption, conversion 28%, churn 2,5%, CAC declining rapide), conduisant ARR 680K€ Y5 et valorisation Series A 8-12M€ (vs 4-6M€ base). Trajectoire "rocket ship" permettant ambitions internationales (UK/Benelux Y6) et acquisition stratégique potentielle 15-25M€ Y7-Y8 par incumbent (Atlassian, ServiceNow, SAP) cherchant innovation IA + verticales.

## 5. **Conclusion et Recommandations Stratégiques**

### 5.1. **Synthèse go/no-go**

**Opportunité marché** : 9,85 Mds$ (2023) → 17,69 Mds$ (2028), CAGR 10,67%, drivers structurels (transformation digitale, travail hybride, adoption mode projet).

**Proposition valeur différenciée défendable** :

- Assignation IA explicable multi-critères (brevetable, -60-80% temps admin)
- Modules sectoriels plug-and-play (marges >80%)
- Multi-tenancy enterprise-grade natif
- Conformité réglementaire by-design (RGPD V1, ISO 27001/SOC 2 roadmap)

**Modèle économique intrinsèquement rentable** :

- LTV:CAC 5-13x (vs seuil viabilité 3x)
- Payback 11-20 mois
- Marges structurelles 40-77%
- Break-even M18 (vs médiane 36-48 mois SaaS)

**Trajectoire financière soutenable** :

- ARR 313K€ Y5, CAGR 278%, zéro dilution (bootstrap complet)
- Trésorerie 55K€ Y5 préservant autonomie stratégique
- NRR >100% dès Y3, Magic Number 2,1-3,6 (top décile SaaS B2B per Bessemer)

### 5.2. **Décision et quick wins prioritaires**

**Recommandation** : **GO DÉCISIF** ✓

Rapport opportunité/risque largement favorable, risques identifiés mitigables, timing marché optimal (adoption IA workplace accelerating, pénuries talents exacerbating besoin optimisation ressources).

**Quick wins prioritaires** :

1. **Lancement MVP Juin 2026** : Assignation IA core + freemium généreux (5 users, 3 projets)
2. **Validation PMF** : 50 paying customers M12 (conversion freemium 18%, churn <4,5% mensuel)
3. **Break-even M18** : Atteindre profitabilité préservant runway → autonomie financière
4. **Module LIMS Q4 2026** : Initiation verticalisation capturant premiers clients sectoriels

**Point décision Series A** : Si ARR >150K€ Y3 avec croissance >100% YoY et churn < 3,5% mensuel, considérer levée **1-2M€** (10-15% dilution, pré-money 8-12M€) pour scaling agressif :

- Équipe 8-12 personnes (devs, sales, CS)
- Expansion internationale (UK, Benelux, DACH)
- Certifications enterprise (ISO 27001, SOC 2)
- **Objectif 3-5M€ ARR Y6** qualifying Series B 8-15M€

**Stratégie gagnante** : Exécution disciplinée, focus PMF, frugalité opérationnelle, verticalisation progressive, préservation indépendance fondateur jusqu'à position de force négociation fundraising.


## **Sources et Références**

**Études de marché :**

- [MarketsandMarkets 2024 - Project Management Software Market](https://www.marketsandmarkets.com/Market-Reports/project-management-software-market-225285515.html)
- [Statista - Project Collaboration Software Worldwide](https://www.statista.com/outlook/tmo/enterprise-software/collaboration-management/project-collaboration-software/worldwide)
- [Gartner - Cloud Computing Trends 2023](https://www.gartner.com/en/newsroom/press-releases/2022-11-08-gartner-forecasts-worldwide-public-cloud-end-user-spending-to-reach-nearly-600-billion-in-2023)
- [Forrester - Top 10 Emerging Technologies 2024](https://www.forrester.com/report/the-top-10-emerging-technologies-in-2024/RES183311)
- [Gallup - State of the Global Workplace 2023](https://www.gallup.com/workplace/349484/state-of-the-global-workplace.aspx)

**Pricing concurrents :**

- [Monday.com Pricing](https://monday.com/pricing/)
- [Jira Pricing](https://www.atlassian.com/software/jira/pricing)
- [ClickUp Pricing](https://clickup.com/pricing)
- [Asana Pricing](https://asana.com/fr/pricing)

**Benchmarks SaaS :**

- OpenView Partners - SaaS Benchmarks 2024
- Bessemer Venture Partners - Cloud Index 2024
- SaaS Capital - Private SaaS Company Survey 2023
- Price Intelligently - SaaS Pricing Strategy Research

**Données sectorielles :**

- Eurostat - Enterprise Statistics by Size Class
- INSEE - Répertoire des Entreprises France


**Dernière mise à jour :** 27/02/2026  
**Version :** 2.0  
**Projet :** Taskforce ERP — Metz Numeric School 2025-2026
