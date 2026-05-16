# KnowledgeBase

Persönliche Wissensbasis — LLM-gestützt gepflegt und abgefragt.

## Verzeichnisse

### decisions/
Architekturentscheidungen (ADRs): was wurde entschieden, warum, mit welchen Konsequenzen.
Eine Datei pro Entscheidung — jede hat einen eigenen Lebenszyklus (Status, Nachfolger).

Frontmatter: `id`, `title`, `status` (aktiv | ersetzt durch ADR-XXX), `date`
Abschnitte: Kontext, Alternativen, Entscheidung, Konsequenzen

### requirements/
Anforderungen an die Anwendung — minimal, priorisiert, erweiterbar.
Alle Anforderungen in einer Datei: `requirements/requirements.md`

### how-to/
Schritt-für-Schritt-Anleitungen für wiederkehrende Aufgaben.
Eine Datei pro Thema.

### notes/
Lose Notizen, Rechercheergebnisse, Zwischenstände.
Eine Datei pro Thema oder alles in einer Datei — nach Bedarf.

### principles/
Grundsätze zur Organisation und Pflege der Wissensbasis.
Alle Grundsätze in einer Datei: `principles/principles.md`

Frontmatter: `id`, `title`
Abschnitte: Grundsatz, Begründung, Anwendung

## Dateiorganisation

Die Granularität richtet sich nach Lebenszyklus und Zugriffsmuster des Inhalts:

- **Wartbarkeit:** Inhalte mit eigenem Lebenszyklus (Status, Nachfolger) erhalten eine eigene Datei, damit Änderungen isoliert vorgenommen werden können. Stabile, zusammengehörige Inhalte werden konsolidiert — weniger Dateien bedeuten weniger Pflegeaufwand.
- **Zugriff:** Das LLM findet thematisch fokussierte Dateien zuverlässiger als große Mischdateien. Konsolidierung ist dort sinnvoll, wo Inhalte ohnehin gemeinsam abgefragt werden.
- **Lesbarkeit:** Wenige, klar benannte Dateien sind für Menschen leichter zu überblicken als viele Kleinstdateien.

| Verzeichnis    | Granularität         | Begründung                                              |
|----------------|----------------------|---------------------------------------------------------|
| `decisions/`   | Eine Datei pro ADR   | Eigener Lebenszyklus je Entscheidung (Status, Ersatz)   |
| `requirements/`| Eine Datei gesamt    | Anforderungen gehören zusammen, überschaubares Volumen  |
| `principles/`  | Eine Datei gesamt    | Wenige, stabile Grundsätze                              |
| `how-to/`      | Eine Datei pro Thema | Anleitungen sind thematisch unabhängig                  |
| `notes/`       | Nach Bedarf          | Lose Notizen, kein festes Schema                        |
