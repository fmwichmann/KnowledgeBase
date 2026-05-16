---
id: ADR-001
title: Nutzung der Claude API über LiteLLM als generisches LLM-Interface
status: aktiv
date: 2026-05-15
links:
  - REQ-006
  - REQ-007
---

## Kontext

Für den Telegram Bot wird ein LLM benötigt, das programmatisch aufgerufen werden kann. Die Wissensbasis-Chunks aus ChromaDB müssen in den Prompt eingebettet und die Antwort maschinell weiterverarbeitet werden. Langfristig soll ein Anbieterwechsel ohne Codeänderungen möglich sein, um Kosten zu optimieren und nicht von einem Anbieter abhängig zu sein.

## Alternativen

**Claude.ai / Claude Pro (Weboberfläche):** Kein programmatischer Zugriff. Ausschließlich für manuelle Nutzung im Browser konzipiert. Nicht geeignet.

**Claude Code CLI (`claude -p`):** Technisch als Unterprozess aufrufbar, aber nicht für automatisierten Einsatz gebaut. Kein strukturierter Output (kein JSON), kein natives Kontextmanagement, Prompt-Zusammensetzung mit Sonderzeichen fehleranfällig. Würde eine unnötige Zwischenschicht einführen.

**Direkte Claude API ohne Abstraktionsschicht:** Funktioniert, bindet jedoch den gesamten Code an Anthropic. Ein späterer Anbieterwechsel erfordert Code-Änderungen an allen API-Aufrufstellen.

**Anthropic File Search (Vector Stores):** Proprietäre Vektorsuche innerhalb der Anthropic-Infrastruktur. Daten liegen in der Cloud, Speicherkosten fallen an, kein Zugriff ohne Internet. Macht einen späteren Anbieterwechsel deutlich aufwendiger, da Vektordatenbank und LLM-Anbindung gemeinsam migriert werden müssten.

## Entscheidung

Claude API wird über **LiteLLM** als generisches Interface angesprochen. LiteLLM bietet eine einheitliche API für 100+ Anbieter. Das verwendete Modell wird per Konfiguration gesteuert, nicht im Code fest verdrahtet.

Modellstrategie:
- Entwicklung: kostengünstiges oder kostenloses Modell (z.B. Groq/Llama)
- Produktion einfache Abfragen: `claude-haiku-4-5`
- Produktion komplexe Aufgaben: `claude-sonnet-4-6`

Als Vektordatenbank wird **ChromaDB** lokal betrieben — anbieterneutral, keine Cloud-Abhängigkeit.

## Konsequenzen

**Positiv:**
- Anbieterwechsel per Konfigurationszeile, ohne Codeänderung
- Kostenoptimierung durch Modellwahl je Aufgabentyp
- Strukturierter JSON-Output ermöglicht Fehlerbehandlung und Token-Monitoring
- Prompts können programmatisch mit Wissensbasis-Chunks zusammengesetzt werden

**Negativ:**
- Zusätzliche Abhängigkeit (litellm als Bibliothek)
- Claude API Key erforderlich (separate Registrierung auf api.anthropic.com, ~$5 Startguthaben)

**Neutral:**
- Pay-per-use Abrechnung statt Flatrate
