---
id: P-04
title: Minimize maintenance overhead
type: principle
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [principles, maintenance, simplicity]
related: [P-01, P-02, C-01]
supersedes: []
---

## Statement

Die Wissensbasis bleibt schlank: nur was aktiv genutzt wird, bleibt aktiv. Werkzeuge, Schemata und Prozesse sind so einfach wie möglich.

## Rationale

- Jede zusätzliche Konvention erzeugt Pflegekosten und damit Drift zwischen Doku und Realität.
- Eine kleine, gepflegte Wissensbasis ist für die LLM wertvoller als eine große, veraltete.
- Markdown + Git + Vector Store reicht; komplexere Systeme (Wikis, Datenbanken) sind explizit nicht vorgesehen.

## Implications

- Keine Tooling-Eigenentwicklung, wenn ein Standardprozess (Git, OpenAI File Search) ausreicht.
- Frontmatter-Felder werden nur ergänzt, wenn sie konkret im Retrieval oder Review verwendet werden.
- Veraltete Inhalte werden regelmäßig auf `superseded` oder `deprecated` gesetzt, statt sie nur stehen zu lassen.
- Notes (`notes/`) sind ausdrücklich erlaubt, müssen aber nicht ans Review-Niveau heran — sie fließen nicht in den produktiven Vector Store ([[C-04]]).
