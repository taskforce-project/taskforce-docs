---
id: soutenance-plan-minute
title: Plan minuté de la soutenance (étape 1)
doc_type: soutenance
statut: a-valider
version: 1.0
date: "21/07/2026"
auteur: Pierre MICHEL
tags: [soutenance, rncp, oral, plan, timing, bc02, bc03]
---

# Plan minuté de la soutenance

> Étape 1 de la méthode définie dans `.ai/soutenance-brief.md`. **À valider avant toute rédaction
> du texte oral.** Cadre officiel : 20 minutes de présentation démonstration comprise, puis 15
> minutes de questions. Ordre imposé : bloc BC02 (front) puis bloc BC03 (back).

## 1. La décision de densité

Le deck actuel `TaskForce_Soutenance_v3.pptx` compte **32 diapositives**, soit 37 secondes chacune
si la démonstration ne prenait aucun temps. C'est intenable.

**Proposition retenue : 23 diapositives principales**, dont 2 séparateurs de partie et 2 cartons de
démonstration. Il reste donc **19 diapositives parlées** pour 15 minutes de discours, soit environ
48 secondes chacune, et **4 minutes 10 de démonstration live** répartie en deux temps.

La démonstration est coupée en deux volontairement : un passage côté utilisateur dans la partie
front, un passage sur le smart-assign dans la partie back. Cela sert les deux blocs au lieu d'un
seul, et évite le trou de 5 minutes sans slide qui casserait le minutage.

## 2. Le plan, diapositive par diapositive

Le fond indiqué renvoie au gabarit existant : T1 titre, T2 T3 T4 fonds sombres, T5 T6 fonds clairs,
T7 séparateur de section, T8 pleine page orange.

### Ouverture (2 min 30)

| # | Fond | Message unique | Durée | Compétence |
|---|---|---|---|---|
| 1 | T1 | Qui je suis, mon parcours, et TaskForce en une phrase | 0:45 | Introduction imposée |
| 2 | T2 | Le problème client, et ce que le cahier des charges demandait | 0:45 | Contexte, C2 |
| 3 | T2 | L'architecture d'ensemble et les choix de stack, écart au CDC assumé | 1:00 | Motivation des choix |

La diapositive 3 porte le premier point sensible : le CDC impose PHP ou Node, le projet est en Java
Spring Boot. L'écart est annoncé **par moi, en 30 secondes**, pas subi en questions.

### Partie 1, front-end, bloc BC02 (8 min 05)

| # | Fond | Message unique | Durée | Compétence |
|---|---|---|---|---|
| 4 | T7 | Séparateur, Partie 1 Front-end | 0:10 | |
| 5 | T6 | La technologie front retenue et pourquoi elle | 0:50 | C16 |
| 6 | T5 | De la maquette à l'écran livré, et la position honnête sur les wireframes | 0:50 | C13 |
| 7 | T5 | Le design system et la charte, 165 composants sur base accessible | 0:45 | C14 |
| 8 | T6 | Le style, des tokens au CSS purgé et minifié | 0:45 | C14, C16 |
| 9 | T7 | **Démonstration côté utilisateur**, un parcours réel de bout en bout | 2:10 | C15 |
| 10 | T6 | Consommer l'API de façon sécurisée depuis le client | 0:45 | C17 |
| 11 | T5 | Accessibilité, performances et SEO, ce qui est mesuré et ce qui ne l'est pas | 0:50 | C15, C20 |
| 12 | T6 | Tester et industrialiser le front, du linter au cahier de recette | 0:55 | C18, C19 |

### Partie 2, back-end, bloc BC03 (7 min 25)

| # | Fond | Message unique | Durée | Compétence |
|---|---|---|---|---|
| 13 | T7 | Séparateur, Partie 2 Back-end | 0:10 | |
| 14 | T2 | Une architecture en couches, isolée workspace par workspace | 0:50 | C22, C21 |
| 15 | T3 | Le modèle de données, versionné et protégé | 0:50 | C21 |
| 16 | T4 | Une API REST documentée et sécurisée | 0:55 | C24 |
| 17 | T7 | **Démonstration du smart-assign**, le différenciateur, avec son explication | 2:00 | C24 en action |
| 18 | T4 | Le moteur IA, local, gratuit et sobre | 0:45 | C22 écoconception |
| 19 | T6 | Le paiement et la monétisation | 0:45 | C23 |
| 20 | T3 | Tester et industrialiser le back, et la dette que j'ai corrigée | 1:10 | C25, C26 |

### Conclusion (1 min 30)

| # | Fond | Message unique | Durée | Compétence |
|---|---|---|---|---|
| 21 | T3 | Bilan, ce que j'assume et ce que j'ai déjà corrigé | 0:50 | Esprit critique |
| 22 | T8 | Ce que je ferais ensuite, les améliorations possibles | 0:25 | Conclusion imposée |
| 23 | T1 | Merci, questions | 0:15 | |

**Total : 19 minutes 30.** Marge de 30 secondes, plus 20 secondes de coussin dans chaque
démonstration. Répartition front 8:05 contre back 7:25, soit 52 contre 48, cohérent avec le retour
du professeur qui jugeait la partie front trop faible.

## 3. Couverture du référentiel

Les huit compétences du bloc BC02 et les six du bloc BC03 sont couvertes, chacune par une
diapositive dédiée ou par la démonstration.

| Bloc | Compétence | Portée par |
|---|---|---|
| BC02 | C13 concevoir l'interface | 6 |
| BC02 | C14 éléments graphiques et charte | 7, 8 |
| BC02 | C15 UX, parcours, accessibilité | 9, 11 |
| BC02 | C16 langage front, qualité, sécurité, écoconception | 5, 8 |
| BC02 | C17 consommer une API de façon sécurisée | 10 |
| BC02 | C18 tester le front | 12 |
| BC02 | C19 industrialiser le front | 12 |
| BC02 | C20 performances SEO | 11 |
| BC03 | C21 couche de persistance | 14, 15 |
| BC03 | C22 langage back, qualité, sécurité, écoconception | 14, 18 |
| BC03 | C23 paiement et monétisation | 19 |
| BC03 | C24 API sécurisée | 16, 17 |
| BC03 | C25 tester le back | 20 |
| BC03 | C26 industrialiser le back | 20 |

## 4. Ce qui sort du deck actuel

Neuf diapositives quittent le corps de la présentation. Aucune n'est supprimée, toutes basculent en
annexe et restent disponibles pendant les 15 minutes de questions.

| Diapositive v3 | Sort parce que | Devient |
|---|---|---|
| 03 Gestion de projet | Non notée sur BC02 et BC03 | Annexe |
| Production, prêt à déployer | Bloc 4, évalué séparément le 05/10 | Annexe |
| Transverse RGPD et observabilité | Une ligne suffit sur la diapositive 20 | Annexe |
| Contexte et Solution, deux diapositives | Fusionnées | Diapositive 2 |
| Moteur IA détaillé, isolation détaillée | Trop fin pour l'exposé | Annexes déjà prévues |
| Vision v2 « AI Delivery OS » | Hors périmètre noté, consomme du temps | Réduite à 25 secondes sur la 22 |

## 5. Ce qui entre et qui manquait

| Apport | Raison |
|---|---|
| Diapositive 11 étendue au **SEO** | C20 n'était couverte nulle part dans le deck v3 |
| Deux cartons de **démonstration** | La démonstration n'était pas minutée du tout |
| Diapositive 19 **paiement** conservée en corps | C23 est une compétence notée, pas un bonus |
| Écart au CDC annoncé en diapositive 3 | Vaut mieux assumé que subi en questions |
| Position honnête sur les maquettes en 6 | C13 exige des maquettes « précédemment validées » |

## 6. Visuels à produire

| Diapositive | Visuel | État |
|---|---|---|
| 3 | Diagramme C4, vue conteneurs | À exporter |
| 6 | Maquette Figma et écran réel côte à côte | À capturer |
| 7 | Planche de composants du design system | À capturer |
| 11 | Rapport Lighthouse, accessibilité et SEO | **À mesurer**, lot `C3` |
| 15 | Modèle de données | À exporter |
| 16 | Swagger UI | À capturer |
| 17 | Écran Smart Assign avec son explication | À capturer |

## 7. Points bloquants avant la rédaction du texte

1. **Les chiffres divergent selon la source.** La matrice de compétences annonce 92 % et 746 tests
   au front, 78 % et 670 tests au back. Le deck v3, construit sur une lecture du code, annonce 706
   tests au front et 692 tests pour environ 72 % au back. Aucun script oral ne doit être écrit avant
   la re-mesure du lot `C3`.
2. **La matrice revendique des éléments que le code ne démontre pas** : Virtual Threads,
   Testcontainers, scans Semgrep et Trivy en intégration continue. Le jury lit le dossier. À
   trancher dans le chat projet.
3. **C20 est en jaune** : Lighthouse n'est pas mesuré. Soit on mesure avant le 25/09, soit la
   diapositive 11 assume la mesure manquante.
4. **C23 est en jaune** : les webhooks Stripe sont partiellement simulés (PC-005). Cela conditionne
   ce que la diapositive 19 peut affirmer.
5. **Le parcours professionnel de la diapositive 1** doit être fourni, je ne l'invente pas.

## 8. Suite

Une fois ce plan validé : rédaction du texte oral complet, puis scénario de démonstration avec plan
de repli, puis liste de questions probables, puis report dans le PowerPoint.

> Voir aussi : [[Plan_Soutenance]] pour l'architecture détaillée du deck v3, et
> [[README|Matrice des 32 compétences]] pour les critères d'évaluation littéraux.
