---
id: C-01
title: Markdown is the canonical source format
type: constraint
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [constraints, format, markdown]
related: [C-02, P-03, P-04]
supersedes: []
---

## Statement

Alle Wissensdokumente werden als **Markdown** (`.md`) abgelegt. Andere Formate (PDF, DOCX, Notion-Export) gelten als Sekundärquelle und müssen für die Aufnahme in die Basis nach Markdown konvertiert werden.

## Rationale

- Markdown ist plain-text, git-freundlich und mit File Search direkt indexierbar.
- Binärformate können nicht versioniert und schwer reviewed werden.
- Einheitliches Format reduziert Tooling und Pflegeaufwand ([[P-04]]).

## Implications

- Dateiendung: `.md`, UTF-8, LF-Zeilenenden.
- Tabellen, Code-Blöcke und Listen folgen CommonMark.
- Bilder werden neben dem Dokument abgelegt und relativ verlinkt; bevorzugt SVG/PNG.
- Konvertierungs-Pipelines (z. B. PDF→MD) gehören in [[HOWTO-add-document]], nicht in den Vector Store.
