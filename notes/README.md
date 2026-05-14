---
id: N-readme
title: Notes — purpose and scope
type: note
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [notes, scratchpad, drafts]
related: [C-04, P-04]
supersedes: []
---

## Zweck

`notes/` ist der Bereich für **Entwürfe, Recherchen und Ideen**, die noch nicht den Reife- oder Review-Grad eines produktiven Dokuments haben.

## Regeln

- IDs beginnen mit `N-` (`N-01`, `N-02`, …).
- Frontmatter ist auch hier Pflicht ([[C-02]]); `status` darf `draft` sein, `reviewed` darf `false` sein.
- Notes werden **nicht** in den produktiven Vector Store `kb-prod` geladen ([[C-04]]).
- Wenn eine Note reif wird, wird sie in den passenden Zielordner verschoben — dabei eine **neue** ID gemäß Zieltyp vergeben (`P-`, `C-`, …); die ursprüngliche `N-`-Note wird auf `status: superseded` gesetzt oder gelöscht.
