# Anforderungen

## MVP

Das System muss lokale Markdown-Dateien einlesen und deren Inhalte in ChromaDB indexieren.

Das System muss, wenn eine Nutzerfrage eingeht, relevante Textabschnitte aus ChromaDB abrufen.

Das System muss auf Basis der abgerufenen Textabschnitte und der Nutzerfrage eine Antwort über das LLM generieren.

Das System muss dem Nutzer die Möglichkeit bieten, Fragen per Telegram zu stellen und Antworten zu empfangen.

## Mittelfristig

Das System soll dem Nutzer die Möglichkeit bieten, Arbeitsanweisungen per Telegram zu übergeben und auszuführen.

## Rahmenbedingungen

Das System muss das LLM über LiteLLM ansprechen, sodass der Anbieter per Konfiguration gewechselt werden kann.

Das System muss die Wissensbasis lokal in ChromaDB speichern, ohne Abhängigkeit zu einem Cloud-Dienst.
