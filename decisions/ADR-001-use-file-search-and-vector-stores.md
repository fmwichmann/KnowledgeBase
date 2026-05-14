---
id: ADR-001
title: Use OpenAI File Search and a Vector Store as the LLM knowledge backend
type: decision
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [decision, architecture, retrieval, openai, vector-store]
related: [P-01, P-03, P-04, C-01, C-02, C-04, O-01, HOWTO-vector-store]
supersedes: []
---

## Context

Es wird eine LLM benötigt, die

- vordefinierte operationale Regeln (z. B. Antwortstil [[O-01]]) **automatisch** lädt und
- Wissen aus einer kuratierten, versionierten Quelle ausliefert.

Die Quelle ist ein Git-Repo aus Markdown-Dateien mit YAML-Frontmatter ([[C-01]], [[C-02]]).

## Decision

Die Architektur basiert auf zwei OpenAI-Bausteinen:

1. **Vector Store** (`kb-prod`) — enthält alle reviewten, aktiven Markdown-Dokumente inkl. Frontmatter.
2. **File Search Tool** auf einem Assistant bzw. der Responses-API — übernimmt Embedding-Suche und Kontextinjektion.

Operationale Regeln (`type: operational`, `load_always: true`) werden **zusätzlich** als statischer Bestandteil der `instructions` mitgegeben, damit sie nicht von der semantischen Suche abhängen.

## Alternatives considered

| Alternative                      | Verworfen, weil … |
|----------------------------------|-------------------|
| Eigene RAG-Pipeline (LangChain/Haystack + eigene Vector-DB) | Mehr Pflegeaufwand, verstößt gegen [[P-04]]. |
| Reines System-Prompting (alle Dokumente immer mit übergeben) | Skaliert nicht; Token-Limit; teuer. |
| Wiki / Notion als Quelle         | Nicht git-versionierbar, schlecht reviewbar, verstößt gegen [[C-01]]. |
| Nur Stichwortsuche                | Findet semantisch ähnliche, aber wortverschiedene Inhalte nicht ([[P-03]]). |

## Consequences

**Positiv**
- Kein eigener Server, keine eigene Vector-DB.
- Frontmatter wird gleichzeitig zu Filter- und Retrieval-Material ([[P-03]]).
- Saubere Trennung zwischen Quelle (Git) und Index (Vector Store).

**Negativ / Risiken**
- Bindung an OpenAI als Anbieter.
- Sync-Mechanismus muss explizit gepflegt werden ([[HOWTO-vector-store]]).
- Operationale Regeln müssen doppelt aktiv sein (File **und** System-Prompt), sonst greift `load_always` nicht zuverlässig.

## Follow-ups

- Sync-Skript automatisieren (Git-Hook oder GitHub Action).
- Evaluations-Set anlegen, das `O-01`-Stil und Quellenangabe prüft.
- Re-Evaluation, sobald die Wissensbasis > ~500 Dokumente überschreitet.
