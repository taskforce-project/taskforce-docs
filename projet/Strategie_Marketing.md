<!--
Logo établissement : assets/images/logo_metz_numeric_school.svg
Logo projet        : assets/images/logo_taskforce.png
-->

# Stratégie Marketing & Commerciale

**Version :** 1.0  
**Date :** 27/02/2026  
**Auteur(s) :** Pierre MICHEL

[![Type: Stratégie](https://img.shields.io/badge/Type-Strat%C3%A9gie-purple?style=for-the-badge)]() [![Statut: Draft](https://img.shields.io/badge/Statut-Draft-yellow?style=for-the-badge)]() [![Année académique: 2025-2026](https://img.shields.io/badge/Année%20académique-2025--2026-lightgrey?style=for-the-badge)]()

## Liens rapides

- [Dossier Projet](./Dossier_Projet.md)
- [CdCF – Cahier des Charges Fonctionnel](./02_CdCF.md)
- [CdCT – Cahier des Charges Technique](./03_CdCT.md)
- [Business & Analyse de marché](./Etude_business.md)
- [Stratégie Marketing & Commerciale](./Strategie_Marketing.md)

**Tags :** `#marketing` `#commerciale` `#pricing` `#strategie` `#go-to-market` `#chatbot-ia` `#marketplace`

<div class="section-intro">

## Sommaire

1. [Positionnement et proposition de valeur](#1-positionnement-et-proposition-de-valeur)
2. [Segmentation et cibles](#2-segmentation-et-cibles)
3. [Plans tarifaires et pricing](#3-plans-tarifaires-et-pricing)
   - 3.1 [Grille tarifaire Application Core (4 plans)](#grille-tarifaire-détaillée-application-core)
   - 3.2 [Stratégie Pricing Chatbot IA - Wallet Compute](#stratégie-pricing-chatbot-ia-wallet-compute)
   - 3.3 [Marketplace de Modules - Écosystème étendu](#marketplace-de-modules-écosystème-étendu)
4. [Stratégie d'acquisition](#4-stratégie-dacquisition)
5. [Canaux de distribution](#5-canaux-de-distribution)
6. [Stratégie de communication](#6-stratégie-de-communication)
7. [Parcours client et onboarding](#7-parcours-client-et-onboarding)
8. [Indicateurs de performance (KPIs)](#8-indicateurs-de-performance-kpis)

</div>

> **Sections complétées** : Grille tarifaire 4 plans (Student gratuit, Individual 8€, Pro 13€, Enterprise sur devis), Pricing Chatbot IA (wallet compute), Marketplace modules  
> **Sections en construction** : Acquisition, Communication, KPIs (à compléter ultérieurement)

<div class="section-positioning">

## 1. Positionnement et proposition de valeur

### Proposition de valeur unique

**À compléter** : Value proposition principale de Taskforce (Assignation automatique intelligente + ERP modulaire + Conformité secteurs réglementés)

### Différenciateurs clés

**À compléter** : Comparaison avec concurrents (Jira, Asana, Monday.com, ClickUp)

### Positionnement prix

**À compléter** : Positionnement premium, milieu de gamme, ou value

</div>

<div class="section-segments">

## 2. Segmentation et cibles

### Segments de marché

**À compléter** :

- TPE/PME (5-50 employés)
- Moyennes entreprises (50-250 employés)
- Grandes entreprises (250+ employés)
- Secteurs spécifiques (pharma, laboratoires, industrie réglementée)

### Personas cibles

**À compléter** : Définition des personas acheteurs (CEO, CTO, Chef de projet, RH)

</div>

<div class="section-pricing">

## 3. Plans tarifaires et pricing

### Grille tarifaire détaillée - Application Core

Modèle freemium avec **4 plans** adaptés aux différents segments de marché.

| Fonctionnalité              | **Student (Gratuit)** | **Individual**     | **Pro**          | **Enterprise**         |
| --------------------------- | --------------------- | ------------------ | ---------------- | ---------------------- |
| **Prix**                    | **0€** (Gratuit)      | **8€/user/mois**   | **13€/user/mois** | **Sur devis** (18-25€) |
| **Cible**                   | Étudiants certifiés   | Freelances, petites équipes | PME/Professionnels | Grandes organisations |
| **Utilisateurs**            | 5 max                    | 10 max             | Illimité         | Illimité               |
| **Projets**                 | 3 actifs                 | 10 actifs          | Illimité         | Illimité               |
| **Période d'essai**         | - (gratuit permanent)    | **14 jours gratuits** | 14 jours gratuits | Sur demande demo     |
| **Modules sectoriels**      | 0                        | 1 inclus           | 2 inclus         | Tous inclus            |
| **Stockage**                | 2GB total                | 10GB/user          | 50GB/user        | Illimité ou dédié      |
| **Support**                 | Communautaire            | Email sous 48h     | Email sous 24h   | SLA 99.9% + CSM dédié  |
| **Assignation automatique** | Basic                    | Standard           | Avancée          | ML sur-mesure          |
| **API**                     | 100 calls/j              | 500 calls/j        | Illimitée + webhooks | Illimitée + priorité |
| **SSO**                     | Non                      | Google/M365 basic  | SAML             | SAML + SCIM            |
| **Audit logs**              | 7 jours                  | 30 jours           | 90 jours         | 1 an + export conformité |
| **Chatbot IA (compute)**    | 2$/mois inclus           | 5$/mois inclus     | 10$/mois inclus  | Custom compute pool    |

**Conditions plan Student (Gratuit)** :
- **Gratuit permanent** avec justificatif étudiant (carte, certificat scolarité)
- Validité 1 an renouvelable tant que statut étudiant actif
- Upgrade automatique vers Individual à expiration avec **-20% première année**
- Limité aux usages académiques et projets étudiants (non commercial)
- Pas de carte bancaire requise

### Stratégie Pricing Chatbot IA - Wallet Compute

Le chatbot IA Taskforce adopte un **système de wallet compute flexible** inspiré de GitHub, évitant la complexité des "tokens" pour l'utilisateur final.

#### Modèle économique

**Principe** : L'utilisateur achète du **"crédit de requêtes"** (compute wallet) au lieu de tokens LLM bruts.

| **Plan**                  | **Crédit inclus/mois** | **Prix**   | **Équivalent requêtes** | **Compute rate**      |
| ------------------------- | ---------------------- | ---------- | ----------------------- | --------------------- |
| **Student (Gratuit)**     | 2$ compute             | 0€       | ~40 requêtes standard   | Inclus dans plan      |
| **Individual**            | 5$ compute             | 8€       | ~100 requêtes           | Inclus dans plan      |
| **Pro**                   | 10$ compute            | 13€      | ~200 requêtes           | Inclus dans plan      |
| **Enterprise**            | Custom pool            | Sur devis  | Illimité avec fair use  | Pool dédié + SLA      |
| **Add-on compute (tous)** | Flexible               | À la carte | Variable                | 1$ = ~20 req standard |

#### Fonctionnement wallet compute (modèle adaptatif)

**Exemple pratique** :

```
1. Utilisateur Individual : 5$ compute/mois inclus (plan de base)
   ou
   Utilisateur Pro : 10$ compute/mois inclus (plan de base)

2. Ajout adaptatif en cours de mois :
   - Besoin ponctuel → achète +5$ compute → total 15$ disponible
   - Consomme 12$ effectivement → reste 3$

3. Fin de mois :
   - Compute consommé : 12$
   - Compute non utilisé : 3$ → récupéré par Taskforce
   - Mois suivant : retour au plan de base (10$ compute inclus)

4. Ajout flexible :
   - L'utilisateur peut ajouter 5$, 10$, 50$, ou 1000$ selon besoin
   - Aucun engagement : consommation à la demande
   - Si sous-consommation : Taskforce récupère le surplus (pas de report)
```

**Avantages utilisateur** :

- **Pas de jargon technique** : "crédit de requêtes" au lieu de "tokens"
- **Flexibilité totale** : ajout de compute à la demande en un clic
- **Prévisible** : estimation requêtes restantes en temps réel dans l'UI
- **Sans engagement** : retour au plan de base chaque mois
- **Fair use** : pas de restriction arbitraire, paiement à l'usage

**Mécanisme de tarification** :

| **Type requête**               | **Coût compute** | **Description**                               |
| ------------------------------ | ---------------- | --------------------------------------------- |
| Question simple (50 tokens)    | 0.05$            | "Résume cette tâche"                          |
| Requête standard (200 tokens)  | 0.10$            | "Analyse ce projet et propose optimisations"  |
| Requête complexe (500 tokens)  | 0.25$            | "Génère rapport complet avec recommandations" |
| Requête avancée (1000+ tokens) | 0.50$+           | "Analyse prédictive multi-projets avec ML"    |

**UI/UX Wallet** :

```
┌─────────────────────────────────────────┐
│  Crédit Requêtes IA                     │
│                                         │
│  Disponible : 7.50$ / 10.00$            │
│  ▓▓▓▓▓▓▓▓▓░░░░░░ 75%                    │
│                                         │
│  ~150 requêtes restantes ce mois        │
│                                         │
│  [+ Ajouter crédit] [Historique]        │
└─────────────────────────────────────────┘
```

**Stratégie commerciale** :

1. **Inclusion dans plans** : Chaque plan inclut du compute de base → exposure maximale chatbot IA
2. **Upsell naturel** : Notification intelligente quand 80% compute consommé (non intrusif)
3. **Packages prédéfinis** : +5$, +10$, +20$, +50$, +100$ en un clic (pas de formulaire complexe)
4. **Volume discounts** : >100$ d'ajout → -10%, >500$ → -15% (encourage gros utilisateurs)
5. **Facturation simplifiée** : Ajout compute apparaît comme ligne séparée sur facture mensuelle

**Revenue model** :

- **Marge compute** : Coût LLM réel ~0.40$/1000 tokens → prix utilisateur 1.00$/1000 tokens → **marge 60%**
- **Surplus non consommé** : 100% récupéré par Taskforce → **revenu additionnel pur** (15-20% compute acheté non utilisé en moyenne)
- **Prévision Y1** : 20% users dépassent compute inclus → 15$ add-on moyen → +3$/user/mois ARPU additionnel

### Marketplace de Modules - Écosystème étendu

Taskforce intègre une **marketplace in-app** type App Store permettant extensions tierces et modules premium.

#### Architecture marketplace

**3 catégories de modules** :

| **Type**                   | **Fournisseur** | **Prix**          | **Commission Taskforce** | **Exemples**                                    |
| -------------------------- | --------------- | ----------------- | ------------------------ | ----------------------------------------------- |
| **Modules officiels**      | Taskforce       | 3-9€/user/mois    | 100% revenus             | LIMS Labo, Qualité ISO, GED Réglementaire       |
| **Modules certifiés**      | Partenaires     | Variable          | 30%                      | Intégrations ERP (SAP, Oracle), BI avancée      |
| **Modules communautaires** | Développeurs    | Gratuit ou payant | 20% si payant            | Templates workflows, scripts automation, themes |

#### Fonctionnement marketplace

**Installation modules** :

```
1. Parcourir marketplace depuis interface Taskforce
2. Aperçu module : description, prix, avis, screenshots
3. Installation en 1 clic (avec période essai 14j si payant)
4. Facturation automatique intégrée à l'abonnement principal
5. Désinstallation instant (prorata si désinstallation <30j)
```

**Pricing modules officiels** :

| **Module**             | **Prix**       | **Plan requis** | **Description**                                         |
| ---------------------- | -------------- | --------------- | ------------------------------------------------------- |
| **LIMS Laboratoires**  | 7€/user/mois   | Pro ou +        | Gestion échantillons, traçabilité, conformité BPL/GLP   |
| **Qualité ISO**        | 5€/user/mois   | Pro ou +        | Audits, non-conformités, CAPA, docs qualité             |
| **GED Réglementaire**  | 6-9€/user/mois | Pro ou +        | Signatures électroniques, versioning, conformité 21 CFR |
| **Advanced Analytics** | 4€/user/mois   | Pro ou +        | BI, dashboards custom, exports avancés                  |
| **Time Tracking Pro**  | 3€/user/mois   | Tous plans      | Suivi temps détaillé, facturation client                |
| **Custom Workflows**   | 8€/user/mois   | Enterprise      | Workflows sur-mesure avec règles métier complexes       |

**Modules certifiés partenaires** (exemples) :

- **SAP Integration** (partenaire SAP) : 15€/user/mois → sync bidirectionnelle ERP
- **Power BI Connector** (partenaire Microsoft) : 8€/user/mois → dashboards intégrés
- **DocuSign Integration** : 5€/user/mois → signatures électroniques natives
- **Zapier Premium** : 6€/user/mois → 1000+ intégrations automatisées

**Modules communautaires** :

- **Templates sectoriels** : Gratuit (pharma, construction, conseil, IT)
- **Custom reports** : Gratuit ou 1-3€/mois
- **Themes UI** : Gratuit (dark mode, high contrast, custom branding)
- **Automation scripts** : Gratuit (contributed by community)

#### Modèle économique marketplace

**Revenus Taskforce** :

1. **Modules officiels** : 100% revenus → 5-9€/user/mois × 25% adoption base Enterprise = **+1.25€ ARPU moyen**
2. **Commission partenaires** : 30% sur modules certifiés → 15€ × 30% × 10% adoption = **+0.45€ ARPU moyen**
3. **Commission communauté** : 20% sur modules payants → revenus marginaux mais écosystème valorisé

**Total ARPU additionnel marketplace** : **+1.70€/user/mois** (projections conservatrices)

**Stratégie go-to-market marketplace** :

- **Lancement** : Q2 2027 (après consolidation produit core Y1)
- **Phase 1** : 3 modules officiels (LIMS, Qualité ISO, GED) → capture secteurs réglementés
- **Phase 2** : Ouverture partenaires certifiés (5-10 partenaires stratégiques) → intégrations ERP/BI
- **Phase 3** : SDK communautaire public → écosystème développeurs tiers

**Programme développeurs** :

- **SDK gratuit** : API complète + documentation + sandbox
- **Certification module** : Processus review sécurité/qualité (3-5 jours review)
- **Revenue share** : 70% développeur, 30% Taskforce (ou 80/20 si module gratuit avec donations)
- **Promotion** : Featured modules dans marketplace (top downloads, trending, editor's choice)

#### KPIs marketplace

| **Métrique**                  | **Objectif Y2** | **Objectif Y3** | **Objectif Y5** |
| ----------------------------- | --------------- | --------------- | --------------- |
| Modules officiels disponibles | 3               | 5               | 10              |
| Modules partenaires certifiés | 5               | 15              | 40              |
| Modules communautaires        | 20              | 100             | 500+            |
| Taux adoption modules (users) | 15%             | 25%             | 40%             |
| ARPU additionnel marketplace  | +0.80€          | +1.20€          | +2.50€          |

### Stratégie de pricing

**Modèle adopté** : Freemium multicanal avec monétisation progressive

1. **Par utilisateur/mois** : Pricing linéaire 0€ (Student gratuit) → 8€ (Individual) → 13€ (Pro) → 18-25€ (Enterprise)
2. **Période d'essai** : **14 jours gratuits** sur plans Individual et Pro (carte bancaire optionnelle)
3. **Rabais annuel** : -20% si engagement 12 mois (ex: Pro 13€ → 10.40€/mois facturé annuellement)
4. **Garantie** : Satisfait ou remboursé 30 jours (tous plans payants)

**Monétisation additionnelle** :

- **Chatbot IA** : Wallet compute flexible (2-10$ inclus selon plan + add-ons à la demande)
- **Modules marketplace** : 3-9€/user/mois pour modules officiels, 20-30% commission modules tiers
- **Services professionnels** : Formation on-site, migration données, consulting (Enterprise uniquement)

### Pricing psychologique

**Stratégies appliquées** :

1. **Anchor pricing** : Plan Enterprise "Sur devis" ancre la valeur perçue élevée, rendant Pro (13€) attractif
2. **Good-Better-Best** : 4 plans optimaux pour conversion (Student gratuit → Individual essai → Pro standard → Enterprise premium)
3. **Prix psychologiques** : 8€ et 13€ (vs 10€/15€ arrondis) → perception "prix juste sous seuil psychologique"
4. **Décoy effect** : Plan Individual (8€) avec essai rend Pro (13€) plus attractif pour professionnels (+62% valeur perçue)

### Politique commerciale

**Remises et programmes** :

- **Remises volume** :
  - 50-100 utilisateurs : -10% sur plan Pro
  - 100-250 utilisateurs : -15%
  - 250+ utilisateurs : négociation Enterprise avec tarifs dégressifs
- **Tarifs spéciaux** :
  - **Éducation** : Plan Student **gratuit permanent** (0€) avec justificatif + upgrade vers Individual -20% première année post-études
  - **Associations/ONG** : -30% sur tous plans payants (justificatif requis)
  - **Startups (<2 ans)** : -25% première année (via partnerships Station F, French Tech, BPI)
- **Programme partenaires/revendeurs** :
  - Commission 15% sur ventes apportées (récurrente)
  - Accès démo illimité et bac à sable dédié
  - Co-marketing et leads partagés
- **Upsell/cross-sell marketplace** :
  - Recommandations modules selon secteur détecté automatiquement
  - Bundles sectoriels : LIMS + Qualité ISO + GED = -15% vs achat séparé
  - Trial automatique 14j sur modules premium pour users Pro/Enterprise

</div>

<div class="section-acquisition">

## 4. Stratégie d'acquisition

### Objectifs d'acquisition

**À compléter** :

- Année 1 : X clients, Y MRR/ARR
- CAC (Customer Acquisition Cost) cible
- LTV (Lifetime Value) cible
- Ratio LTV/CAC > 3

### Canaux d'acquisition

**À compléter** :

**Inbound Marketing** :

- SEO (blog technique, guides, études de cas)
- Content marketing (livres blancs, webinaires)
- Marketing automation (lead nurturing)

**Outbound Marketing** :

- LinkedIn Ads ciblés décideurs
- Google Ads (mots-clés métier)
- Cold outreach (email, LinkedIn)

**Partnerships** :

- Intégrateurs systèmes ERP
- Consultants en transformation digitale
- Revendeurs sectoriels (pharma, industrie)

**Viral/Referral** :

- Programme de parrainage (1 mois offert)
- Intégrations tierces (Slack, Teams, GitHub)

</div>

<div class="section-distribution">

## 5. Canaux de distribution

### Vente directe

**À compléter** : Self-service via site web + Sales team pour Enterprise

### Marketplaces

**À compléter** : Présence sur marketplaces SaaS (Capterra, G2, GetApp)

### Partenaires

**À compléter** : Réseau de revendeurs et intégrateurs

</div>

<div class="section-communication">

## 6. Stratégie de communication

### Messaging clés

**À compléter** :

- Message principal (tagline)
- Messages par segment
- Objections et réponses

### Canaux de communication

**À compléter** :

- Site web vitrine + landing pages
- Blog technique
- Réseaux sociaux (LinkedIn prioritaire)
- Newsletter
- Webinaires et démos
- Salons et événements métier

### Content marketing

**À compléter** :

- Études de cas clients
- Tutoriels et documentation
- Comparatifs concurrents
- Livres blancs sectoriels

</div>

<div class="section-customer-journey">

## 7. Parcours client et onboarding

### Funnel de conversion

**À compléter** :

```
Visiteur → Lead → MQL → SQL → Trial → Customer → Power User
```

### Onboarding

**À compléter** :

- Email de bienvenue
- Tutoriel interactif
- Quick wins (premières tâches assignées automatiquement en <5min)
- Suivi personnalisé (support proactif J+3, J+7, J+14)

### Rétention

**À compléter** :

- Suivi d'usage (adoption features)
- Customer success proactif
- Webinaires clients
- Programme de feedback continu

</div>

<div class="section-kpis">

## 8. Indicateurs de performance (KPIs)

### KPIs d'acquisition

**À compléter** :

- Trafic site web (visiteurs uniques/mois)
- Taux de conversion visiteur → trial
- Taux de conversion trial → payant
- CAC (Customer Acquisition Cost)
- Coût par lead qualifié

### KPIs de revenus

**À compléter** :

- MRR (Monthly Recurring Revenue)
- ARR (Annual Recurring Revenue)
- ARPU (Average Revenue Per User)
- Churn rate (taux d'attrition mensuel)
- Net Revenue Retention (NRR)

### KPIs d'engagement

**À compléter** :

- Taux d'activation (users actifs / users inscrits)
- DAU/MAU (Daily/Monthly Active Users)
- Feature adoption (% utilisant assignation auto)
- NPS (Net Promoter Score)
- CSAT (Customer Satisfaction Score)

</div>

## Conclusion

**À compléter** : Synthèse de la stratégie go-to-market et prochaines étapes

**Dernière mise à jour :** 27/02/2026  
**Version :** 1.0  
**Projet :** Taskforce - Metz Numeric School 2025-2026
