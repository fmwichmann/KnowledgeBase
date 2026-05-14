# Knowledge Base

LLM-zentrierte Wissensbasis. Quellen sind Markdown-Dateien mit YAML-Frontmatter und stabilen IDs; die LLM lädt sie über File Search auf einem Vector Store.

## Verzeichnisse

| Ordner          | Inhalt                                      | ID-Präfix |
|-----------------|---------------------------------------------|-----------|
| `principles/`   | Grundsätze (langlebig, selten geändert)     | `P-`      |
| `requirements/` | Constraints / Anforderungen                 | `C-`      |
| `decisions/`    | Architectural Decision Records (ADRs)       | `ADR-`    |
| `how-to/`       | Operationale Regeln und Handlungsanleitungen| `O-`, `HOWTO-` |
| `notes/`        | Entwürfe, Recherchen, noch nicht reviewed   | `N-`      |

Nur Dokumente mit `status: active` und Review (`reviewed: true`) gelangen in den produktiven Vector Store ([[C-04]]).

## Pflicht-Frontmatter

```yaml
---
id: P-01                       # stabil, niemals umbenennen
title: Knowledge must be explicit
type: principle                # principle | constraint | decision | how-to | operational | note
status: active                 # active | draft | deprecated | superseded
reviewed: true                 # true erst nach menschlichem Review
version: 1                     # bei inhaltlicher Änderung erhöhen
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [knowledge, principles]
related: [P-02, C-02]          # IDs anderer Dokumente
supersedes: []                 # IDs ersetzter Dokumente
---
```

## ID-Konvention ([[C-03]])

- Format: `<PRÄFIX>-<laufende Nummer mit 2 Stellen>`, z. B. `P-01`, `C-04`, `ADR-001`.
- IDs sind **stabil**: bei inhaltlicher Überarbeitung wird die Version erhöht, nicht die ID.
- Wird ein Dokument abgelöst: alter Eintrag bekommt `status: superseded` und verweist via `supersedes` auf den Nachfolger.

## Klassifikation der Regeln

- **P (Principles)** – Grundsätze, die das Verhalten der LLM und der Wissensbasis langfristig prägen.
- **C (Constraints)** – Harte Anforderungen an Form, Speicherung und Review.
- **O (Operational rules)** – Konkrete Verhaltensregeln, die die LLM zur Laufzeit lädt.

## Retrieval-Pipeline

1. Markdown-Dateien werden mit ihrem Frontmatter (als Klartext-Header) in einen Vector Store geladen.
2. Die LLM nutzt **File Search**, um relevante Dokumente per Embedding-Suche auszuwählen.
3. Operationale Regeln (`type: operational`, `status: active`) werden **immer** in den System-Kontext geladen — unabhängig von der Query (siehe [[ADR-001]]).
4. Principles und Constraints werden bei Bedarf nachgeladen; sie fungieren als Leitplanken.

## Workflow

Siehe [[HOWTO-add-document]] zum Anlegen neuer Wissensdokumente und [[HOWTO-vector-store]] zum Synchronisieren mit OpenAI File Search.
