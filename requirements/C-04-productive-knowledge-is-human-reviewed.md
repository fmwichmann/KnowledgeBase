---
id: C-04
title: Productive knowledge is human-reviewed
type: constraint
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [constraints, review, governance, quality]
related: [P-01, P-02, C-02, ADR-001]
supersedes: []
---

## Statement

Nur Dokumente, die von einem Menschen reviewed wurden (`reviewed: true` **und** `status: active`), dürfen in den produktiven Vector Store geladen werden. Entwürfe und Notes bleiben außen vor.

## Rationale

- Die LLM gibt Inhalte ohne Disclaimer als verbindliches Wissen wieder; ungeprüfte Inhalte würden das Vertrauen untergraben.
- Review ist die einzige Schicht, die Widerspruchsfreiheit ([[P-02]]) und Explizitheit ([[P-01]]) tatsächlich durchsetzt.
- Trennung zwischen "draft" und "active" schützt die Produktion vor halb fertigen Gedanken.

## Implications

- Sync-Skripte filtern strikt: `reviewed == true AND status == active`.
- Notes (`notes/`) und Drafts werden nie in den produktiven Vector Store geladen, optional aber in einen separaten **Staging**-Store ([[HOWTO-vector-store]]).
- Review = jemand außer dem Autor liest, prüft Frontmatter und Inhalt, und setzt `reviewed: true`.
- Bei substanziellen Änderungen wird `reviewed` zurück auf `false` gesetzt, bis ein neuer Review stattgefunden hat.
