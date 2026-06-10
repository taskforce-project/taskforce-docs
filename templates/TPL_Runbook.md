---
id: <% tp.file.title.toLowerCase().replace(/\s+/g, '-') %>
title: <% tp.file.title %>
doc_type: runbook
statut: active
category: deployment
date: <% tp.date.now("DD/MM/YYYY") %>
auteur: Pierre MICHEL
review_cycle: quarterly
tags: [runbook, ops]
related: []
---
<!-- Template Runbook — Templater. category: deployment/incident/maintenance/recovery/security. -->

# <% tp.file.title %>

## Objectif
> Quand utiliser ce runbook ? Quel problème résout-il ?

## Prérequis
- [ ] Accès requis :
- [ ] Outils requis :

## Symptômes / déclencheurs
> Comment reconnaît-on que ce runbook s'applique ?

## Étapes
### 1.
### 2.

## Vérification
> Comment confirmer que c'est résolu ?

## Rollback
> Comment revenir en arrière si ça empire ?

## Escalade
| Si | Contacter | Canal |
| -- | --------- | ----- |

## Liens
- [Architecture §5 (infra)](../v1/03-architecture/Architecture.md)
- [PS/PCA/PRA](../v1/11-pca-pra/PS_PCA_PRA.md)
