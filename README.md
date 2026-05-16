# KnowledgeBase

Persönliche Wissensbasis — LLM-gestützt gepflegt und abgefragt.

## Verzeichnisse

### decisions/
Architekturentscheidungen (ADRs): was wurde entschieden, warum, mit welchen Konsequenzen.
Eine Datei pro Entscheidung — jede hat einen eigenen Lebenszyklus (Status, Nachfolger).

Frontmatter: `id`, `title`, `status` (aktiv | ersetzt durch ADR-XXX), `date`, `links`
Abschnitte: Kontext, Alternativen, Entscheidung, Konsequenzen

### requirements/
Anforderungen an die Anwendung — minimal, priorisiert, erweiterbar.
Eine Datei pro Anforderung.

Frontmatter: `id`, `title`, `priority` (mvp | mittelfristig | rahmenbedingung), `status` (aktiv | ersetzt durch REQ-XXX), `links`
Inhalt: Eine Anforderung im SOPHIST MASTeR-Stil.

### how-to/
Schritt-für-Schritt-Anleitungen für wiederkehrende Aufgaben.
Eine Datei pro Thema.

Frontmatter: `id`, `title`, `links`
Abschnitte: Ziel, Voraussetzungen, Schritte

### notes/
Lose Notizen, Rechercheergebnisse, Zwischenstände.
Eine Datei pro Thema oder alles in einer Datei — nach Bedarf.

### principles/
Grundsätze zur Organisation und Pflege der Wissensbasis.
Alle Grundsätze in einer Datei: `principles/principles.md`

Frontmatter: `id`, `title`
Abschnitte: Grundsatz, Begründung, Anwendung

## Dateiorganisation

Jedes Dokument mit eigenem Lebenszyklus oder Verlinkungsbedarf erhält eine eigene Datei. Das stellt sicher, dass jedes Dokument als vollständiger, in sich geschlossener Chunk indexiert wird und gezielt verlinkt werden kann.

- **Wartbarkeit:** Änderungen an einem Dokument betreffen nur seine eigene Datei. Das LLM kann Dokumente gezielt aktualisieren, ohne andere zu berühren.
- **Zugriff:** Einzeldateien erzeugen saubere Chunks beim Indexieren — kein Inhalt wird durch Fragmentierung vom zugehörigen Kontext getrennt.
- **Lesbarkeit:** Klare Benennung (`REQ-001-wissensaufnahme.md`) macht Inhalt ohne Öffnen der Datei erkennbar.

| Verzeichnis    | Granularität              | Begründung                                                  |
|----------------|---------------------------|-------------------------------------------------------------|
| `decisions/`   | Eine Datei pro ADR        | Eigener Lebenszyklus je Entscheidung (Status, Ersatz)       |
| `requirements/`| Eine Datei pro Anforderung| Saubere Chunks, gezielte Verlinkung, eigener Lebenszyklus   |
| `principles/`  | Eine Datei gesamt         | Wenige, stabile Grundsätze ohne eigenen Lebenszyklus        |
| `how-to/`      | Eine Datei pro Thema      | Anleitungen sind thematisch unabhängig                      |
| `notes/`       | Nach Bedarf               | Lose Notizen, kein festes Schema                            |

## Verlinkung

Dokumente verweisen auf verwandte Dokumente über das `links`-Feld im YAML-Frontmatter. Links werden in beide Richtungen gepflegt. Das LLM aktualisiert beim Anlegen oder Verknüpfen von Dokumenten stets beide Seiten.

```yaml
links:
  - ADR-001
  - HOW-002
```
