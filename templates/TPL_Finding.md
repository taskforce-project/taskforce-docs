---
id: <% tp.file.title.toLowerCase().replace(/\s+/g, '-') %>
title: <% tp.file.title %>
doc_type: finding
statut: open
severity: sev3
domain: backend
date: <% tp.date.now("DD/MM/YYYY") %>
auteur: Pierre MICHEL
tags: [finding, audit]
related: []
---
<!-- Template Finding (constat d'audit) — Templater. severity: sev1..sev4 ; domain: backend/frontend/api/infra/securite. -->

# <% tp.file.title %>

## Preuve (evidence)
> Code, logs, captures, traces montrant le problème.

## Impact
> Conséquence concrète si non résolu.

## Cause racine
> Cause identifiée.

## Plan de remédiation
1.
2.

## Critères de vérification
> Comment valider que c'est résolu ?

## Liens
- [Dette technique](../v1/09-audits/Dette_Technique.md)
- [Problèmes connus](../v1/09-audits/Problemes_Connus.md)
- [Backlog](../v1/13-roadmap/Roadmap_Backlog.md)
