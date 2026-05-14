---
id: HOWTO-add-document
title: How to add a document to the knowledge base
type: how-to
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [how-to, workflow, authoring, review]
related: [C-01, C-02, C-03, C-04, HOWTO-vector-store]
supersedes: []
---

## Ziel

Neues Wissen so anlegen, dass es ohne Reibung in den produktiven Vector Store fließen kann.

## Schritte

1. **Typ und Verzeichnis wählen**
   - Grundsatz → `principles/` (`P-`)
   - Constraint → `requirements/` (`C-`)
   - Entscheidung → `decisions/` (`ADR-`)
   - Anleitung oder operationale Regel → `how-to/` (`HOWTO-` oder `O-`)
   - Entwurf / Recherche → `notes/` (`N-`)

2. **Nächste freie ID bestimmen**
   - Höchste vergebene Nummer des Präfix ermitteln, +1 nehmen ([[C-03]]).

3. **Datei anlegen**
   - Dateiname: `<ID>-<kebab-case-titel>.md`, z. B. `P-05-prefer-small-files.md`.
   - Frontmatter gemäß [[C-02]] ausfüllen.
   - Initial: `status: draft`, `reviewed: false`.

4. **Inhalt schreiben**
   - Ein Thema pro Datei ([[P-03]]).
   - Struktur: kurze Statement-Section, dann Rationale, dann Implications/Beispiele.
   - Verwandte Dokumente per `[[ID]]` verlinken.

5. **Commit & Push**
   - Konvention aus `CLAUDE.md`: einzelner Commit pro Änderung, sofort pushen.
   - Commit-Message: `add <ID>: <titel>` bzw. `update <ID>: <kurzbeschreibung>`.

6. **Review**
   - Zweite Person liest Inhalt + Frontmatter.
   - Bei OK: `reviewed: true` und `status: active` setzen, `updated`-Datum aktualisieren, erneut committen.

7. **In Vector Store überführen**
   - Siehe [[HOWTO-vector-store]].

## Edge Cases

- **Bestehendes Dokument inhaltlich überarbeiten:** `version` erhöhen, `updated` aktualisieren, ggf. `reviewed: false` setzen, neuen Review durchlaufen.
- **Dokument ablösen:** neues Dokument mit eigener ID anlegen, altes auf `status: superseded` setzen und in `supersedes` des neuen Dokuments eintragen ([[P-02]]).
- **Reine Typo-Fixes:** kein Versionssprung, kein neuer Review nötig.
