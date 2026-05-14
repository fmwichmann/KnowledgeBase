---
id: C-03
title: Stable document IDs are required
type: constraint
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [constraints, ids, identifiers, versioning]
related: [C-02, P-01, P-02]
supersedes: []
---

## Statement

Jedes Dokument hat eine **stabile, eindeutige ID** im Frontmatter (`id:`). Die ID ändert sich über die gesamte Lebensdauer des Dokuments nicht — auch nicht bei Umbenennung, Umordnung oder Inhaltsänderung.

## ID-Format

- Präfix nach Dokumenttyp:
  - `P-` Principle (z. B. `P-01`)
  - `C-` Constraint (z. B. `C-02`)
  - `O-` Operational rule (z. B. `O-01`)
  - `ADR-` Decision Record (z. B. `ADR-001`)
  - `HOWTO-` How-To (z. B. `HOWTO-add-document`)
  - `N-` Note (z. B. `N-01`)
- Laufende Nummer ist 2-stellig (3-stellig bei ADRs), z. B. `P-01`, `ADR-007`.
- ID = exakt der Wert in `id:`. Der Dateiname enthält die ID am Anfang, dient aber nur der Auffindbarkeit.

## Rationale

- Stabile IDs ermöglichen Referenzen (`related`, `supersedes`, `[[ID]]`-Links) ohne Bruch.
- Embeddings ändern sich beim Reupload, aber Verweise im Korpus bleiben gültig.
- Audit und Review-Historie können auf IDs aufbauen.

## Implications

- Bei Umbenennung der Datei bleibt die `id` unverändert.
- IDs werden **nie wiederverwendet**, auch wenn das ursprüngliche Dokument gelöscht würde.
- Wird ein Dokument durch ein neues ersetzt: neues Dokument bekommt eine neue ID, listet das alte unter `supersedes`; altes Dokument wechselt auf `status: superseded`.
