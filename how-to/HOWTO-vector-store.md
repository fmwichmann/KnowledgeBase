---
id: HOWTO-vector-store
title: How to sync the knowledge base with OpenAI File Search
type: how-to
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [how-to, vector-store, file-search, openai, sync]
related: [C-02, C-04, ADR-001, O-01]
supersedes: []
---

## Ziel

Die Markdown-Wissensbasis als **Vector Store** für **OpenAI File Search** bereitstellen, sodass die LLM zur Laufzeit Wissen abrufen und operationale Regeln ([[O-01]]) automatisch laden kann.

## Architektur

```
┌─────────────────────────┐    sync   ┌──────────────────────────┐
│  Repo (Markdown + YAML) │  ───────► │ Vector Store: kb-prod    │
└─────────────────────────┘           │  - nur reviewed + active │
                                      └──────────────────────────┘
                                                 │
                                                 ▼
┌────────────────────┐  File Search  ┌──────────────────────────┐
│  System Prompt     │  ───────────► │  Assistant / Responses   │
│  + alle O-* docs   │               │  API                     │
└────────────────────┘               └──────────────────────────┘
```

Zwei Stores:

- `kb-prod` — alle Dokumente mit `reviewed: true` und `status: active`.
- `kb-staging` (optional) — Drafts und Notes für Tests.

## Sync-Regeln

1. Pre-Filter: nur Dateien aus `principles/`, `requirements/`, `decisions/`, `how-to/`, die `reviewed: true` und `status: active` haben ([[C-04]]).
2. Frontmatter wird **mit** in den Upload aufgenommen (nicht gestrippt) — die Metadaten verbessern Retrieval.
3. Bei Statuswechsel auf `superseded` / `deprecated` wird die Datei aus `kb-prod` entfernt.
4. Operationale Regeln (`type: operational`, `load_always: true`) werden **zusätzlich** als statischer System-Prompt-Anhang im Assistant hinterlegt, damit sie unabhängig vom Retrieval immer aktiv sind.

## Vorgehensweise (OpenAI Platform)

1. Vector Store anlegen: `kb-prod`.
2. Pre-Filter-Skript (Python/Node, später) erzeugt eine Upload-Liste.
3. Über Platform-UI oder API hochladen (`POST /v1/vector_stores/{id}/files`).
4. Assistant / Response konfigurieren:
   - `tools: [{ type: "file_search" }]`
   - `tool_resources.file_search.vector_store_ids: ["<kb-prod-id>"]`
   - `instructions`: Inhalt aller Dokumente mit `type: operational, load_always: true` zusammengefügt.
5. Smoke-Test: Beispiel-Query gegen den Assistant → Antwort muss `O-01`-Stil einhalten und mindestens eine Quelle zitieren.

## Re-Sync

- Bei Merge in `main`: erneuter Sync.
- Geänderte Dateien überschreiben den Vector-Store-Eintrag.
- Entfernte / `superseded` Dateien werden gelöscht.

## Anti-Patterns

- ❌ Frontmatter vor dem Upload entfernen (verringert Retrieval-Qualität, siehe [[P-03]]).
- ❌ Drafts in `kb-prod` laden — verstößt gegen [[C-04]].
- ❌ Operationale Regeln nur als File einspielen, ohne sie ebenfalls in den System-Prompt zu packen — die LLM lädt sie sonst nicht garantiert.
