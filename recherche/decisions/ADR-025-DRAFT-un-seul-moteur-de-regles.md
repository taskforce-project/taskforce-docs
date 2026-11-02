---
id: adr-025-un-seul-moteur-de-regles
title: "ADR-025 (à promouvoir) : un seul moteur de règles, écrit en Java, compilé en JavaScript pour le runner"
doc_type: adr
statut: active
version: 1.0
date: "02/11/2026"
auteur: Pierre MICHEL
review_cycle: annual
tags: [adr, architecture, regles, harnais, runner, teavm, conseil]
related:
  - "../experiences/Experiences.md"
  - "../conseil/seances/2026-11-01-feuille-de-route.md"
  - "../../v1/road_to_v2/Specification_V2_Harnais.md"
  - "../../v1/12-decisions/Journal_Decisions_ADR.md"
---

# ADR-025 (à promouvoir) : un seul moteur de règles, écrit en Java, compilé en JavaScript pour le runner

> **Décidé par la Présidence le 02/11/2026** : « on adopte R90 (b) ». Il entre dans
> [`v1/12-decisions/Journal_Decisions_ADR.md`](../../v1/12-decisions/Journal_Decisions_ADR.md) sous le n° 025 dès que
> l'index est libre : une autre session y a des modifications en cours.

## Statut

Accepté le 02/11/2026. Mise en œuvre en J1 (TF-J1-1).

## Contexte

- `[ÉTABLI]` Le moteur de règles existe deux fois : en Java pour Cortex et le serveur, en TypeScript dans le runner, qui
  décide chaque action de Claude Code sur la machine. Les cas partagés (`contracts/rules/cases.json`, 84 au 02/11) les
  gardent égaux.
- `[ÉTABLI]` La Présidence, le 01/11/2026 : « pas de duoplication stp », puis « faut voir [...] c'est vrai que c est lourd
  d'appeler Java a chaque fois ». R90 est passée à l'essai, avec E16.
- `[ÉTABLI]` E16 (02/11/2026, [résultats](../experiences/Experiences.md)) :
  - demander chaque décision au backend de la machine tient le seuil de latence, mais laisse l'agent sans aucune décision
    pendant 20 à 23 secondes à chaque redémarrage du backend : réfuté ;
  - le moteur Java compilé en JavaScript par TeaVM 0.16 passe les 84 cas, donne les mêmes décisions que le runner sur 43
    actions réelles, décide en quelques microsecondes et pèse 126 Ko compressé : non réfuté.

## Décision

1. Le moteur de règles s'écrit une seule fois, en Java.
2. Le runner l'embarque compilé en JavaScript par TeaVM : aucune décision ne dépend d'un aller-retour vers le backend.
3. La copie TypeScript du moteur disparaît du runner. Ce qui décrit une action de Claude Code en faits (`facts.ts`)
   reste dans le runner : c'est son adaptateur, pas le moteur.
4. Le fichier compilé est versionné avec le runner, qui se construit sans JDK ; la CI le régénère depuis Java et refuse
   un écart.
5. Les cas partagés restent la garde : ils se rejouent contre Java et contre le module compilé.

## Conséquences

- Une règle ou un motif change en un seul endroit.
- La construction gagne une étape : TeaVM, avec deux remplacements pour les classes du JDK qu'il n'a pas
  (`MessageDigest`, `HexFormat`).
- Le risque : TeaVM est un outil peu répandu. S'il ne suit pas une version future de Java, le repli est un second moteur
  gardé par les cas partagés, la situation d'avant cette décision.

---

**Points d'entrée :** [Décisions du labo](./) · [📓 Journal](../Journal.md) · [Expériences](../experiences/Experiences.md)

**Dernière mise à jour :** 02/11/2026 · **v1.0** · Projet Taskforce
