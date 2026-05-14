---
id: P-01
title: Knowledge must be explicit
type: principle
status: active
reviewed: true
version: 1
created: 2026-05-14
updated: 2026-05-14
owner: felix-manuel.wichmann@t-online.de
tags: [principles, knowledge, explicitness]
related: [P-02, P-03, C-01, C-02]
supersedes: []
---

## Statement

Wissen, das von der LLM verwendet werden soll, muss **explizit** in der Wissensbasis abgelegt sein. Implizites Wissen (mündliche Absprachen, Slack-Threads, Köpfe einzelner Personen) ist für die LLM nicht existent.

## Rationale

- LLMs können nur abrufen, was als Token im Kontext landet. Stilles Wissen ist nicht retrievable.
- Explizite Dokumente sind versionierbar, reviewbar und auditierbar.
- Reduziert das Risiko von Halluzinationen, weil die LLM auf belegbare Quellen verweisen kann.

## Implications

- Jedes Faktum, jede Regel und jede Entscheidung erhält ein Dokument mit stabiler ID ([[C-03]]).
- Antworten der LLM dürfen nicht auf vermuteten oder ungeschriebenen Konventionen basieren.
- Wenn die LLM ein benötigtes Wissen nicht findet, gibt sie das offen zu, statt zu raten.
