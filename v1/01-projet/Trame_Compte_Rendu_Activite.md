---
id: trame-compte-rendu-activite
title: Trame type de compte rendu d'activite (E6)
doc_type: methode
statut: valide
version: 1.0
date: "23/07/2026"
auteur: Pierre MICHEL
tags: [agile, compte-rendu, e6, methode, memoire, rncp, scrum, kanban]
---

# Trame type de compte rendu d'activite

> Livrable **E6** du referentiel : « une trame type de compte rendu d'activite correspondant a la
> methode projet retenue lors de l'evaluation E5 ». La methode retenue en E5 est decrite dans
> [[Note_Methode_Agile]] : Scrum allege combine a un Kanban, adapte a un projet mono-acteur.

## 1. Pourquoi cette trame a cette forme

Une trame de compte rendu n'a de valeur que si elle epouse la methode qu'elle sert. Celle-ci derive
donc point par point des adaptations decidees en E5, et non d'un modele generique de reunion
d'equipe.

| Ceremonie Scrum standard | Adaptation retenue en E5 | Section correspondante ici |
| --- | --- | --- |
| Sprint planning | Priorisation hebdomadaire (matrice Eisenhower) | 2. Objectifs fixes |
| Daily standup | Auto-revue quotidienne (carnet de bord) | 3. Activites realisees |
| Definition of Done | Checklist en 6 points | 4. Controle de la Definition of Done |
| Sprint review | Validation de jalon par demonstration locale | 5. Indicateurs mesures |
| Retrospective | Bilan de fin de phase | 8. Bilan |

Deux consequences directes du contexte mono-acteur. D'abord, il n'y a **ni participants ni releve de
decisions collectives** : le compte rendu ne rapporte pas ce qui s'est dit, il rapporte ce qui a ete
fait et ce qui a ete mesure. Ensuite, la fonction de controle habituellement portee par l'equipe
doit etre remplacee par des **preuves verifiables**, d'ou l'exigence de reference tracable en
section 3 et de valeurs datees en section 5.

## 2. Cadence d'emploi

Le compte rendu se remplit **chaque semaine**, la priorisation etant hebdomadaire, et se consolide
en fin de cycle (2 a 4 semaines) pour la validation de jalon. Les sections 1 a 6 sont renseignees
chaque semaine ; les sections 7 a 9 le sont en fin de cycle, ou plus tot si un fait le justifie.

## 3. Regles de remplissage

Trois regles rendent la trame operationnelle plutot que decorative.

1. **Toute activite porte une reference verifiable** : numero d'issue, empreinte de commit, ou nom
   de branche. Une ligne sans reference n'est pas un compte rendu, c'est une declaration.
2. **Tout indicateur porte sa date et son perimetre de mesure.** Un pourcentage sans date se perime
   en quelques jours et finit par contredire un autre document.
3. **Les ecarts se declarent, ils ne se rattrapent pas au cycle suivant en silence.** La section 6
   existe pour cela : un objectif non atteint et explique vaut mieux qu'un objectif discretement
   redefini.

---

# Trame

## En-tete

| Champ | Valeur |
| --- | --- |
| Periode couverte | du JJ/MM/AAAA au JJ/MM/AAAA |
| Cycle | nom du cycle et numero |
| Jalon vise | J1 a J6, cf. [[Gantt_Planning]] |
| Phase du plan projet | cf. [[Plan_Projet]] |
| Redacteur | |
| Date de redaction | |

## 1. Contexte du cycle

Trois a cinq lignes : d'ou l'on part, ce qui conditionne ce cycle, ce qui a change depuis le
precedent. Sert a rendre le compte rendu lisible isolement, sans avoir a relire les precedents.

## 2. Objectifs fixes a la priorisation

Issus de la priorisation hebdomadaire. Le quadrant Eisenhower justifie l'ordre retenu.

| # | Objectif | Quadrant Eisenhower | Critere de reussite | Reference |
| --- | --- | --- | --- | --- |
| | | Important et urgent / Important non urgent / Non important urgent / A eliminer | observable et verifiable | issue, lot, jalon |

## 3. Activites realisees

Une ligne par activite significative. La colonne de reference est obligatoire.

| Objectif | Activite | Reference verifiable | Etat |
| --- | --- | --- | --- |
| | | issue, commit, branche | Terminee / En cours / Abandonnee |

## 4. Controle de la Definition of Done

Reprise de la checklist de [[Note_Methode_Agile]] §4. A renseigner pour les livraisons du cycle.

- [ ] Code implemente et compilant
- [ ] Tests unitaires et d'integration ecrits et passants
- [ ] Chaine d'integration continue verte
- [ ] Aucune regression sur les tests existants
- [ ] Code fusionne
- [ ] Documentation du Brain OS mise a jour si l'architecture est touchee

Toute case non cochee doit etre justifiee en section 6.

## 5. Indicateurs mesures

Remplace la revue de sprint : ce que l'on montrerait a une equipe, on le mesure et on le date.

| Indicateur | Valeur | Mesure le | Perimetre ou reserve |
| --- | --- | --- | --- |
| Couverture de tests front | | | |
| Couverture de tests back | | | |
| Suite de tests | | | |
| Analyse statique | | | |
| Securite (dependances, images, pentest) | | | |
| Accessibilite | | | |
| Autre indicateur du cycle | | | |

## 6. Ecarts par rapport aux objectifs

| Objectif concerne | Ecart constate | Cause | Traitement retenu |
| --- | --- | --- | --- |

## 7. Obstacles et risques

Obstacles rencontres, et risques ouverts ou refermes pendant le cycle. Renvoyer au
[[Registre_Risques]] plutot que de dupliquer.

| Obstacle ou risque | Effet sur le projet | Reference registre | Action |
| --- | --- | --- | --- |

## 8. Bilan

Retrospective adaptee au contexte mono-acteur. Deux questions seulement, mais repondues
serieusement.

- **Ce qui a fonctionne et doit etre reconduit.**
- **Ce qui a mal fonctionne et ce que je change concretement au cycle suivant.** Une intention sans
  changement de pratique n'est pas une retrospective.

## 9. Decisions engageantes

Toute decision qui contraint la suite du projet. Si elle est structurante, elle donne lieu a une
entree dans le [[Journal_Decisions_ADR]] et cette section n'en porte que le renvoi.

| Decision | Motif | Consequence | ADR |
| --- | --- | --- | --- |

## 10. Objectifs du cycle suivant

Report des objectifs non atteints, plus les nouveaux. Alimente la priorisation de la semaine
suivante.

---

> Voir aussi : [[Note_Methode_Agile]] (methode E5) · [[Plan_Projet]] · [[Gantt_Planning]] ·
> [[Registre_Risques]] · [[Journal_Decisions_ADR]].
> Exemple rempli : [[CR_2026-S30_Cloture_V1]].
