---
id: C-02
title: YAML frontmatter is mandatory
type: constraint
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [constraints, metadata, frontmatter, yaml]
related: [C-01, C-03, C-04, P-03]
supersedes: []
---

## Statement

Jedes Markdown-Dokument in der Wissensbasis beginnt mit einem YAML-Frontmatter-Block. Dokumente ohne Frontmatter werden **nicht** in den Vector Store aufgenommen.

## Required Fields

| Feld       | Typ              | Beschreibung                                              |
|------------|------------------|-----------------------------------------------------------|
| `id`       | string           | Stabile ID gemäß [[C-03]] (`P-01`, `C-02`, `ADR-001`, …). |
| `title`    | string           | Aussagekräftiger Titel.                                   |
| `type`     | enum             | `principle` \| `constraint` \| `decision` \| `how-to` \| `operational` \| `note`. |
| `status`   | enum             | `active` \| `draft` \| `deprecated` \| `superseded`.      |
| `reviewed` | boolean          | `true` erst nach menschlichem Review ([[C-04]]).          |
| `version`  | integer          | Wird bei inhaltlicher Änderung erhöht.                    |
| `created`  | date (ISO 8601)  | Erstellungsdatum.                                         |
| `updated`  | date (ISO 8601)  | Letztes inhaltliches Update.                              |
| `owner`    | string           | Verantwortliche Person (E-Mail).                          |
| `tags`     | list[string]     | Suchbegriffe für Retrieval ([[P-03]]).                    |
| `related`  | list[id]         | Verwandte Dokumente.                                      |
| `supersedes` | list[id]       | Dokumente, die durch dieses ersetzt werden ([[P-02]]).    |

## Rationale

- Frontmatter macht Metadaten für Pre-Filter und Routing maschinell zugänglich.
- File Search indexiert auch den Header — Frontmatter-Begriffe verbessern Retrieval.
- Pflicht-Schema verhindert unklare/halbfertige Einträge.

## Implications

- Validierung erfolgt vor jedem Sync ([[HOWTO-vector-store]]).
- Optionale Felder dürfen ergänzt, aber nicht ohne Begründung eingeführt werden ([[P-04]]).
