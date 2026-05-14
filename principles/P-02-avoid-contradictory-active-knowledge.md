---
id: P-02
title: Avoid contradictory active knowledge
type: principle
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [principles, consistency, governance]
related: [P-01, C-03, C-04]
supersedes: []
---

## Statement

Zwei aktive Dokumente (`status: active`) dürfen sich nicht widersprechen. Wird eine Regel ersetzt, erhält das alte Dokument `status: superseded` und verlinkt via `supersedes` auf den Nachfolger.

## Rationale

- Widersprüche im Retrieval-Korpus führen zu instabilen, nicht-deterministischen Antworten.
- Embedding-Suche kann nicht zwischen "gültig" und "veraltet" unterscheiden — die Statusfelder müssen das tun.
- Eine eindeutige Quelle pro Aussage ist Voraussetzung für vertrauenswürdige Antworten.

## Implications

- Vor jedem Merge: prüfen, ob bestehende aktive Dokumente betroffen sind.
- Veraltete Inhalte werden **nicht gelöscht**, sondern auf `superseded` gesetzt, damit historischer Kontext erhalten bleibt.
- Nur Dokumente mit `status: active` werden in den produktiven Vector Store geladen ([[HOWTO-vector-store]]).
