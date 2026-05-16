# KnowledgeBase

Persönliche Wissensbasis — LLM-gestützt gepflegt und abgefragt.

## Verzeichnisse

### decisions/
Architekturentscheidungen (ADRs): was wurde entschieden, warum, mit welchen Konsequenzen.
Eine Datei pro Entscheidung.

Abschnitte: Kontext, Alternativen, Entscheidung, Konsequenzen

### requirements/
Anforderungen an die Anwendung — minimal, priorisiert, erweiterbar.
Eine Datei pro Anforderung. Inhalt: eine Anforderung im SOPHIST MASTeR-Stil.

### how-to/
Schritt-für-Schritt-Anleitungen für wiederkehrende Aufgaben.
Eine Datei pro Thema.

Abschnitte: Ziel, Voraussetzungen, Schritte

### notes/
Lose Notizen, Rechercheergebnisse, Zwischenstände.
Eine Datei pro Thema oder alles in einer Datei — nach Bedarf.

### principles/
Grundsätze zur Organisation und Pflege der Wissensbasis.
Alle Grundsätze in einer Datei: `principles/principles.md`

Abschnitte: Grundsatz, Begründung, Anwendung

## Frontmatter

Jede Datei enthält einen YAML-Header mit Metadaten. Nicht alle Felder sind für jeden Dokumenttyp relevant — siehe Spalte "Verwendet in".

| Feld       | Werte / Format                              | Verwendet in                  | Bedeutung                                                                 |
|------------|---------------------------------------------|-------------------------------|---------------------------------------------------------------------------|
| `id`       | `ADR-001`, `REQ-001`, …                     | Alle                          | Stabile, eindeutige Kennung. Basis für Verlinkung.                        |
| `title`    | Freitext                                    | Alle                          | Menschenlesbare Bezeichnung des Dokuments.                                |
| `status`   | `aktiv` \| `ersetzt durch XXX`              | decisions, requirements       | Zeigt an, ob das Dokument noch gültig ist oder durch ein anderes ersetzt wurde. |
| `date`     | `YYYY-MM-DD`                                | decisions                     | Datum der Entscheidung.                                                   |
| `priority` | `muss` \| `soll` \| `kann`                    | requirements                | Spiegelt das Modalverb im Anforderungssatz: **muss** = zwingend, **soll** = gefordert aber kein Blocker, **kann** = optional. |
| `links`    | Liste von IDs: `[ADR-001, REQ-002]`         | Alle                          | Verweise auf inhaltlich verwandte Dokumente. Werden in beide Richtungen gepflegt. |

## Dateiorganisation

Jedes Dokument mit eigenem Lebenszyklus oder Verlinkungsbedarf erhält eine eigene Datei. Das stellt sicher, dass jedes Dokument als vollständiger, in sich geschlossener Chunk indexiert wird und gezielt verlinkt werden kann.

- **Wartbarkeit:** Änderungen an einem Dokument betreffen nur seine eigene Datei.
- **Zugriff:** Einzeldateien erzeugen saubere Chunks beim Indexieren — kein Inhalt wird durch Fragmentierung vom zugehörigen Kontext getrennt.
- **Lesbarkeit:** Kurze ID-basierte Dateinamen (`REQ-001.md`), Titel im Frontmatter.

| Verzeichnis    | Granularität               | Begründung                                                |
|----------------|----------------------------|-----------------------------------------------------------|
| `decisions/`   | Eine Datei pro ADR         | Eigener Lebenszyklus je Entscheidung (Status, Ersatz)     |
| `requirements/`| Eine Datei pro Anforderung | Saubere Chunks, gezielte Verlinkung, eigener Lebenszyklus |
| `principles/`  | Eine Datei gesamt          | Wenige, stabile Grundsätze ohne eigenen Lebenszyklus      |
| `how-to/`      | Eine Datei pro Thema       | Anleitungen sind thematisch unabhängig                    |
| `notes/`       | Nach Bedarf                | Lose Notizen, kein festes Schema                          |

## Verlinkung

Dokumente verweisen auf verwandte Dokumente über das `links`-Feld im YAML-Frontmatter. Links werden in beide Richtungen gepflegt. Das LLM aktualisiert beim Anlegen oder Verknüpfen von Dokumenten stets beide Seiten.

```yaml
links:
  - ADR-001
  - REQ-002
```
