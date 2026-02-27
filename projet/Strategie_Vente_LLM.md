<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Stratégie Vente LLM & Chatbot IA

**Version :** 1.0  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Stratégie](https://img.shields.io/badge/Type-Strat%C3%A9gie-blue?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [Business & Analyse de marché](./Etude_business.md)
- [Stratégie Marketing & Commerciale](./Strategie_Marketing.md)

**Tags :** `#llm` `#chatbot-ia` `#wallet-compute` `#pricing` `#monetisation` `#ai-strategy`

## Sommaire

1. [Vue d'ensemble](#1-vue-densemble)
2. [Modèle économique wallet compute](#2-modèle-économique-wallet-compute)
3. [Architecture technique](#3-architecture-technique)
4. [Stratégie de pricing](#4-stratégie-de-pricing)
5. [Revenue model & projections](#5-revenue-model--projections)
6. [Go-to-market & adoption](#6-go-to-market--adoption)
7. [Optimisation & scaling](#7-optimisation--scaling)
8. [KPIs & monitoring](#8-kpis--monitoring)

## 1. Vue d'ensemble

### 1.1. Positionnement stratégique

Le **Chatbot IA Taskforce** représente un **avantage concurrentiel majeur** dans le secteur du Project Management Software :

**Différenciateurs clés** :

- **Terminologie accessible** : "Crédit de requêtes" au lieu de "tokens" techniques
- **Modèle adaptatif** : Ajout flexible de compute à la demande selon besoin
- **Revenue optimization** : Récupération des crédits non utilisés = profit pur
- **Intégration native** : Dans chaque plan (pas d'add-on optionnel séparé)
- **Fair use intelligent** : Pas de restriction arbitraire, tarification transparente

### 1.2. Cas d'usage principaux

| **Cas d'usage**                   | **Valeur utilisateur**                                              | **Type compute**       |
| --------------------------------- | ------------------------------------------------------------------- | ---------------------- |
| Résumé automatique tâches/projets | Gain temps management, vision synthétique instantanée               | Simple (0.05$/requête) |
| Assignation intelligente          | Optimisation charge équipe, prévention burnout                      | Standard (0.10$)       |
| Analyse prédictive risques        | Détection anticipée problèmes, recommandations proactives           | Complexe (0.25$)       |
| Génération rapports exécutifs     | Reporting automatisé, dashboards narratifs pour C-level             | Complexe (0.25$)       |
| Optimisation workflows            | Suggestions amélioration processus, best practices selon historique | Avancé (0.50$+)        |
| Analyse multi-projets & tendances | Insights stratégiques, patterns cachés, prévisions budget/délais    | Avancé (0.50$+)        |

## 2. Modèle économique wallet compute

### 2.1. Principe fondamental

**Système de wallet compute flexible** inspiré de GitHub Copilot et AWS Credits :

```
┌──────────────────────────────────────────────────────────┐
│  UTILISATEUR                                             │
│                                                          │
│  1. Plan de base : 10$ compute/mois (Pro)               │
│                                                          │
│  2. Besoin ponctuel → achat +20$ compute                │
│     → Total disponible : 30$ pour le mois               │
│                                                          │
│  3. Consommation réelle : 18$                           │
│                                                          │
│  4. Fin de mois :                                       │
│     - Utilisé : 18$ (facturé à l'utilisateur)           │
│     - Non utilisé : 12$ → RÉCUPÉRÉ PAR TASKFORCE        │
│                                                          │
│  5. Mois suivant : retour plan de base (10$ compute)    │
└──────────────────────────────────────────────────────────┘
```

**Avantages business** :

- **Revenue additionnel pur** : 15-20% compute acheté jamais consommé
- **ARPU uplift** : +3$/user/mois en moyenne (20% users dépassent base)
- **Upsell naturel** : Notification quand 80% consommé (non intrusif)
- **Pas de report** : Crédits non utilisés = profit Taskforce (reset mensuel)

### 2.2. Grille tarifaire compute inclus par plan

| **Plan**       | **Crédit inclus/mois** | **Prix plan** | **Équivalent requêtes** | **Valeur compute** |
| -------------- | ---------------------- | ------------- | ----------------------- | ------------------ |
| **Student**    | 2$ compute             | 0€ (gratuit)  | ~40 requêtes standard   | Inclus             |
| **Individual** | 5$ compute             | 8€            | ~100 requêtes           | Inclus             |
| **Pro**        | 10$ compute            | 13€           | ~200 requêtes           | Inclus             |
| **Enterprise** | Custom pool            | Sur devis     | Illimité fair use       | Pool dédié + SLA   |

**Add-on compute** (tous plans) :

- Flexible : 5$, 10$, 20$, 50$, 100$, 500$, 1000$+
- Taux : 1$ = ~20 requêtes standard
- Activation instantanée (pas de validation manuelle)

### 2.3. Tarification par type de requête

| **Type requête** | **Tokens LLM** | **Coût compute** | **Cas d'usage typiques**                                    |
| ---------------- | -------------- | ---------------- | ----------------------------------------------------------- |
| Question simple  | ~50 tokens     | 0.05$            | Résumé tâche, statut projet, question rapide                |
| Requête standard | ~200 tokens    | 0.10$            | Analyse projet, suggestions optimisation, assignation auto  |
| Requête complexe | ~500 tokens    | 0.25$            | Génération rapport, analyse multi-critères, recommandations |
| Requête avancée  | 1000+ tokens   | 0.50$ - 1.00$    | Analyse prédictive, ML patterns, insights stratégiques      |

**Note** : Tarif affiché utilisateur = "crédit de requêtes", pas "tokens" (simplification UX)

## 3. Architecture technique

### 3.1. Stack LLM

**Modèles utilisés** (multi-LLM strategy) :

| **Tâche**           | **Modèle**        | **Coût API**      | **Justification**                       |
| ------------------- | ----------------- | ----------------- | --------------------------------------- |
| Questions simples   | GPT-3.5 Turbo     | 0.0015$/1K tokens | Rapide, économique, qualité suffisante  |
| Analyse standard    | GPT-4 Turbo       | 0.01$/1K tokens   | Meilleur raisonnement, contexte long    |
| Analyse avancée     | GPT-4 ou Claude 3 | 0.03$/1K tokens   | Qualité maximale, raisonnement complexe |
| Embeddings (search) | text-embedding-3  | 0.0001$/1K tokens | Recherche sémantique, classification    |

**Optimisations coûts** :

- **Routing intelligent** : Requête simple → GPT-3.5, complexe → GPT-4
- **Cache réponses** : Requêtes identiques (<5min) → cache Redis (coût 0)
- **Truncation contexte** : Limiter tokens input selon type requête
- **Rate limiting** : Fair use par plan (éviter abus)

### 3.2. Infrastructure backend

```
┌─────────────────────────────────────────────────────────────┐
│  TASKFORCE BACKEND (Spring Boot)                           │
│                                                             │
│  ┌─────────────────┐    ┌──────────────────┐               │
│  │  Wallet Service │───▶│  Billing Service │               │
│  └────────┬────────┘    └──────────────────┘               │
│           │                                                 │
│           ▼                                                 │
│  ┌─────────────────────────────────────────┐               │
│  │  LLM Router Service                     │               │
│  │  - Analyse requête (simple/complexe)    │               │
│  │  - Sélection modèle optimal             │               │
│  │  - Calcul coût compute                  │               │
│  │  - Rate limiting + fair use             │               │
│  └─────────┬───────────────────────────────┘               │
│            │                                                │
│            ▼                                                │
│  ┌─────────────────────────────────────────┐               │
│  │  LLM Provider Adapters                  │               │
│  │  - OpenAI API                           │               │
│  │  - Anthropic Claude API (backup)        │               │
│  │  - Fallback strategy si downtime        │               │
│  └─────────────────────────────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

**Sécurité & conformité** :

- **Pas de stockage données sensibles** dans prompts LLM
- **Anonymisation** : Données projet anonymisées avant envoi API
- **RGPD compliance** : Pas de training modèles sur données clients
- **Audit logs** : Toutes requêtes LLM trackées (qui, quand, coût)

## 4. Stratégie de pricing

### 4.1. Positionnement prix vs concurrence

| **Concurrent**   | **Modèle IA**                     | **Prix**                 | **Limites**                                      |
| ---------------- | --------------------------------- | ------------------------ | ------------------------------------------------ |
| **Notion AI**    | Add-on obligatoire                | +10$/user/mois           | Flat fee, pas de granularité                     |
| **Asana AI**     | Inclus Enterprise uniquement      | (plan à partir de 25$)   | Pas accessible PME                               |
| **ClickUp AI**   | Add-on                            | +5$/user/mois            | Simple, mais requêtes limitées                   |
| **Taskforce AI** | Inclus tous plans (2-10$ compute) | 0€ (Student) à 13€ (Pro) | Flexible, ajout à la demande, pas de limite fixe |

**Avantage compétitif Taskforce** :

- **Inclus dans tous les plans** (pas d'add-on séparé)
- **Flexible** : Acheter seulement si besoin ponctuel
- **Transparent** : Coût par requête affiché
- **Fair use** : Pas de limite arbitraire mensuelle

### 4.2. Packages add-on compute

**Tarifs add-on** (tous plans) :

| **Package** | **Prix**  | **Équiv. requêtes standard** | **Use case**                      |
| ----------- | --------- | ---------------------------- | --------------------------------- |
| Small       | 5$        | ~100 requêtes                | Freelance besoin ponctuel         |
| Medium      | 10$       | ~200 requêtes                | Pic activité mensuelle            |
| Large       | 20$       | ~400 requêtes                | Équipe 5-10 users besoin régulier |
| XL          | 50$       | ~1000 requêtes               | Équipe >10 users, usage intensif  |
| XXL         | 100$      | ~2000 requêtes               | Entreprise multi-projets          |
| Custom      | Sur devis | Variable                     | Enterprise avec volume garantie   |

**Remises volume** :

- ≥100$ : -10%
- ≥500$ : -15%
- ≥1000$ : -20% (négociation Enterprise)

### 4.3. UI/UX Wallet (mockup frontend)

```
┌────────────────────────────────────────────────────────────────┐
│  Chatbot IA - Wallet Compute                               │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  Crédit disponible ce mois                                 │
│  ━━━━━━━━━━━━━━━━━━━━  75%                                    │
│  7.50$ / 10.00$                                               │
│                                                                │
│  Estimation : ~150 requêtes restantes                      │
│                                                                │
│  ┌──────────────────┐  ┌──────────────────┐                  │
│  │  + Ajouter crédit │  │  Historique      │                  │
│  └──────────────────┘  └──────────────────┘                  │
│                                                                │
│  Tip : Vous utilisez régulièrement le chatbot IA.          │
│     Ajouter +5$ pourrait éviter limitation en fin de mois.    │
│     [Ajouter 5$] [Ignorer]                                    │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

**Notifications intelligentes** :

- **80% consommé** : "Bientôt à court de crédit IA, ajouter ?"
- **95% consommé** : "Plus que 0.50$ crédit IA restant" (urgent)
- **100% consommé** : "Crédit épuisé, ajouter pour continuer"

**Pas de blocage brutal** : L'utilisateur peut ajouter crédit en 1 clic même à 100%

## 5. Revenue model & projections

### 5.1. Calcul marges LLM

**Exemple requête standard (200 tokens)** :

| **Poste**               | **Coût réel** | **Prix facturé** | **Marge** |
| ----------------------- | ------------- | ---------------- | --------- |
| Input API (100 tokens)  | 0.001$        | -                | -         |
| Output API (100 tokens) | 0.002$        | -                | -         |
| **Total coût LLM**      | **0.003$**    | -                | -         |
| Infrastructure          | 0.002$        | -                | -         |
| **Coût total**          | **0.005$**    | **0.10$**        | **95%**   |

**Note** : Marge exceptionnellement élevée car coûts LLM en baisse constante (-50% en 2024)

**Marge moyenne tous types requêtes** : **60-70%** (après infra, support, R&D)

### 5.2. Revenue additionnel par plan

| **Plan**   | **Compute inclus** | **% users dépassant base** | **Add-on moyen** | **Revenue add./user/mois** |
| ---------- | ------------------ | -------------------------- | ---------------- | -------------------------- |
| Student    | 2$                 | 5% (usage léger)           | 5$               | +0.25$                     |
| Individual | 5$                 | 15% (freelances actifs)    | 10$              | +1.50$                     |
| Pro        | 10$                | 25% (équipes intensives)   | 15$              | +3.75$                     |
| Enterprise | Custom pool        | 40% (volume garanti)       | 50$              | +20.00$                    |

**ARPU additionnel moyen pondéré** : **+3.00$/user/mois** (tous plans confondus)

### 5.3. Profit sur crédits non utilisés

**Hypothèse conservatrice** : 15% compute acheté jamais consommé

| **Plan**     | **Users Y1** | **Compute acheté total/mois** | **Non utilisé (15%)** | **Profit pur/mois** |
| ------------ | ------------ | ----------------------------- | --------------------- | ------------------- |
| Student      | 500          | 2$ × 500 = 1,000$             | 150$                  | **150$**            |
| Individual   | 300          | (5$ + 1.50$) × 300 = 1,950$   | 293$                  | **293$**            |
| Pro          | 200          | (10$ + 3.75$) × 200 = 2,750$  | 413$                  | **413$**            |
| Enterprise   | 50           | Custom pool (~50k$/mois)      | 7,500$                | **7,500$**          |
| **Total Y1** | **1,050**    | **~55k$/mois**                | **~8.3k$/mois**       | **~100k$/an**       |

**Profit pur Y1 sur non-consommé** : **~100k$/an** (15% crédits achetés)

### 5.4. Projections 5 ans

| **Année** | **Users actifs** | **ARPU base** | **ARPU IA add.** | **MRR total** | **ARR** | **Profit IA pur** |
| --------- | ---------------- | ------------- | ---------------- | ------------- | ------- | ----------------- |
| Y1        | 1,050            | 11€           | +3$              | 14.5k€        | 174k€   | ~100k€            |
| Y2        | 2,300            | 12€           | +3.5$            | 35.6k€        | 427k€   | ~250k€            |
| Y3        | 4,800            | 13€           | +4$              | 81.6k€        | 979k€   | ~600k€            |
| Y4        | 9,200            | 14€           | +4.5$            | 170k€         | 2.04M€  | ~1.2M€            |
| Y5        | 15,500           | 15€           | +5$              | 310k€         | 3.72M€  | ~2.1M€            |

**Note** : ARPU IA augmente avec maturité produit (plus de cas d'usage, meilleure adoption)

## 6. Go-to-market & adoption

### 6.1. Roadmap déploiement

**Phase 1 : MVP Chatbot IA (Q3 2026)** :

- Questions simples (résumé tâches, statut projets)
- Assignation automatique intelligente
- Wallet compute inclus dans tous plans (2-10$)
- Add-on 5-100$ en 1 clic
- Routing GPT-3.5/GPT-4 selon complexité

**Phase 2 : Analyse avancée (Q1 2027)** :

- Génération rapports exécutifs
- Analyse prédictive risques projets
- Suggestions optimisation workflows
- Intégration Claude 3 (backup + qualité)

**Phase 3 : Intelligence stratégique (Q3 2027)** :

- Analyse multi-projets & tendances
- Prévisions budget/délais ML-powered
- Détection patterns cachés
- Recommandations C-level automatisées

### 6.2. Stratégie adoption

**Leviers activation** :

1. **Onboarding interactif** :
   - Tutorial guidé chatbot IA sur premier projet
   - 3 requêtes gratuites offertes (hors wallet) pour découverte
   - "Quick wins" : Résumé projet instantané, assignation 1-click

2. **Gamification** :
   - Badge "AI Power User" si >50 requêtes/mois
   - Leaderboard usage IA par équipe (opt-in)
   - Débloquer cas d'usage avancés après X requêtes

3. **Social proof** :
   - Témoignages clients : "Le chatbot IA a réduit notre temps de reporting de 70%"
   - Case studies sectoriels (pharma, construction, IT)
   - Webinars démo chatbot IA (1x/mois)

4. **Incentives conversion** :
   - Student → Individual : +5$ compute offert premier mois
   - Individual → Pro : +10$ compute offert + unlock cas d'usage avancés
   - Pro → Enterprise : POC personnalisé avec custom pool

### 6.3. KPIs adoption

| **Métrique**                   | **Objectif Y1** | **Objectif Y2** | **Objectif Y5** |
| ------------------------------ | --------------- | --------------- | --------------- |
| % users activant chatbot IA    | 60%             | 75%             | 85%             |
| Requêtes moyennes/user/mois    | 25              | 40              | 60              |
| % users dépassant compute base | 20%             | 30%             | 40%             |
| NPS chatbot IA                 | 50              | 60              | 70              |
| Taux retention users IA actifs | 85%             | 90%             | 95%             |

## 7. Optimisation & scaling

### 7.1. Réduction coûts LLM

**Leviers court terme (Y1-Y2)** :

1. **Cache Redis stratégique** :
   - Requêtes identiques <5min → cache → économie 20-30%
   - Réponses FAQ projets → cache persistant → économie 10%

2. **Fine-tuning modèles** :
   - GPT-3.5 fine-tuné sur cas d'usage Taskforce → qualité GPT-4 à coût GPT-3.5
   - Économie potentielle : 40-50% sur requêtes standard

3. **Prompt engineering** :
   - Prompts optimisés → moins de tokens input
   - Chain-of-thought sélectif (uniquement si nécessaire)
   - Économie : 15-20% tokens

**Leviers long terme (Y3-Y5)** :

1. **Modèle propriétaire** :
   - Fine-tune Llama 3 ou Mistral sur données Taskforce
   - Hébergement on-premise → coût marginal quasi-nul après investissement initial
   - Économie potentielle : 70-80% vs API externe

2. **Hybrid approach** :
   - Modèle propriétaire requêtes simples/standard (80% volume)
   - API externe (GPT-4) requêtes complexes uniquement (20% volume)
   - Économie globale : 60-70%

### 7.2. Scaling infrastructure

**Capacité cible Y5** :

- 15,500 users actifs
- ~930,000 requêtes/mois (60 req/user/mois)
- ~186M tokens/mois

**Infrastructure nécessaire** :

| **Composant**        | **Y1**        | **Y5**             | **Coût mensuel Y5** |
| -------------------- | ------------- | ------------------ | ------------------- |
| API LLM externe      | OpenAI Tier 1 | OpenAI Tier 4      | ~75k$               |
| Cache Redis          | 1GB           | 50GB               | ~200$               |
| Compute backend      | 2 instances   | 10 instances (k8s) | ~2k$                |
| Load balancer        | Basic         | Advanced + CDN     | ~300$               |
| Monitoring (Datadog) | Basic         | APM complet        | ~500$               |
| **Total infra Y5**   | **~5k$/mois** | **~78k$/mois**     | **~78k$/mois**      |

**Marge Y5** : 310k€ MRR - 78k$ infra (~70k€) = **240k€ MRR net** (77% marge)

## 8. KPIs & monitoring

### 8.1. KPIs business

| **KPI**                     | **Formule**                                       | **Objectif Y1** | **Objectif Y5** |
| --------------------------- | ------------------------------------------------- | --------------- | --------------- |
| **ARPU IA additionnel**     | Revenue IA add-ons / Total users                  | +3$/user        | +5$/user        |
| **Taux adoption chatbot**   | Users avec ≥1 requête/mois / Total users          | 60%             | 85%             |
| **Revenue IA/MRR total**    | Revenue IA / MRR total                            | 20%             | 25%             |
| **Profit pur non-consommé** | Compute acheté non utilisé / Total compute acheté | 15%             | 15%             |
| **Conversion add-on**       | Users achetant add-on / Total users               | 20%             | 40%             |

### 8.2. KPIs techniques

| **KPI**                     | **Cible** | **Alert si** |
| --------------------------- | --------- | ------------ |
| **Latence moyenne requête** | <3s       | >5s          |
| **Taux erreur API LLM**     | <1%       | >3%          |
| **Coût moyen/1000 tokens**  | <0.015$   | >0.025$      |
| **Cache hit rate**          | >25%      | <15%         |
| **Uptime chatbot IA**       | >99.5%    | <99%         |

### 8.3. Dashboards monitoring

**Dashboard business (Metabase/Looker)** :

- Revenue IA jour/semaine/mois (évolution)
- ARPU IA par plan (Student, Individual, Pro, Enterprise)
- Top users IA (>100 requêtes/mois)
- Taux adoption par cohorte (mois d'inscription)
- Compute non-consommé (profit pur) tracking

**Dashboard technique (Datadog/Grafana)** :

- Requêtes/seconde (pic heures)
- Latence P50/P90/P99
- Coût LLM temps réel (budget alert)
- Cache hit rate
- Erreurs API (par provider : OpenAI, Claude)

## Conclusion & recommandations

### Points clés stratégie LLM

**Modèle économique robuste** :

- ARPU additionnel +3-5$/user/mois
- Marges 60-70% sur compute
- Profit pur 15% sur non-consommé
- Scaling économiquement viable (77% marge Y5 après infra)

**Différenciation concurrentielle** :

- Inclus tous plans (vs add-on séparé concurrents)
- Terminologie accessible ("crédit requêtes" vs tokens)
- Flexible sans engagement (achat à la demande)
- Fair use intelligent (pas de limite arbitraire)

**Adoption facilitée** :

- Onboarding interactif avec quick wins
- Notifications intelligentes non intrusives
- Social proof & case studies
- Gamification & incentives

### Prochaines étapes

1. **Q2 2026** : Finaliser intégration OpenAI API + wallet service backend
2. **Q3 2026** : Beta privée chatbot IA (50 users early adopters)
3. **Q4 2026** : Launch public chatbot IA (MVP phase 1)
4. **Q1 2027** : Analyse performance + itération features (phase 2)
5. **Q3 2027** : Intelligence stratégique avancée (phase 3)

**Projet :** Taskforce - Metz Numeric School 2025-2026  
**Contact :** Pierre MICHEL
