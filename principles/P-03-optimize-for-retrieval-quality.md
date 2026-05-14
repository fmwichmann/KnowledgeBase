---
id: P-03
title: Optimize for retrieval quality
type: principle
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [principles, retrieval, embeddings, chunking]
related: [P-01, C-01, C-02, ADR-001]
supersedes: []
---

## Statement

Dokumente werden so geschrieben, dass eine semantische Suche sie zuverlässig findet und ein LLM sie ohne Zusatzkontext verstehen kann.

## Rationale

- File Search basiert auf Embedding-Ähnlichkeit; verstreute oder vage Inhalte verschlechtern die Trefferqualität.
- Ein Chunk muss eigenständig lesbar sein, weil im Retrieval oft nur Ausschnitte zurückkommen.

## Implications

- **Ein Thema pro Datei.** Kein Sammelsurium, keine "Misc"-Dateien.
- **Self-contained Sections.** Jede Überschrift wiederholt den Kontext (z. B. "Die Wissensbasis nutzt …" statt "Sie nutzt …").
- **Aktive Sprache, eindeutige Begriffe.** Synonyme nur, wenn sie tatsächlich verwendet werden sollen.
- **Frontmatter-Tags** spiegeln Suchbegriffe, die ein Nutzer plausibel verwendet.
- **Kurze Absätze (≤ 5 Zeilen)** verbessern die Chunk-Granularität.
- Verlinkung anderer Dokumente per `[[ID]]` macht semantische Beziehungen explizit.
