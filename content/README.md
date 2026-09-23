# content/ — Fragen- und Quellenarchiv

Dieser Ordner ist das Archiv für alles, was in die Brandmeister-Quiz-App einfließt: Quellmaterial, Notizen und der gepflegte Master-Fragenbestand. Er liegt bewusst im selben Repo wie die App, damit alles an einem Ort bleibt.

## Struktur

```
content/
├── README.md              ← diese Datei
├── notizen.md              ← offene Ideen, ToDos, Themen für später (Monetarisierung, weitere Berufe, ...)
├── fragen/
│   └── brandmeister_master.json   ← gepflegter Master-Fragenbestand (aktuell 295 Fragen)
└── quellen/
    └── README.md           ← Quellenverzeichnis + Ablage für Rohmaterial (PDFs, Auszüge, Links)
```

## Wie das mit der App zusammenhängt

Die App selbst lädt ihre Fragen **live aus Firestore** (`packs/brandmeister/questions/...`), nicht direkt aus diesem Ordner — das ermöglicht Änderungen ohne App-Update (siehe Admin-Bereich in der App: "Fragen verwalten").

`fragen/brandmeister_master.json` ist trotzdem wichtig als:
- **Referenz/Backup**: der vollständige Fragenbestand als Klartext, unabhängig von Firestore einsehbar und versionierbar (über die Git-Historie nachvollziehbar).
- **Startbestand**: dieselbe Datei ist die Grundlage für den bereits ausgeführten einmaligen "Fragen-Datenbank initialisieren"-Schritt in der App, der den Bestand nach Firestore überträgt.
- **Basis für größere Ergänzungen**: Wer viele neue Fragen auf einmal einpflegen will, kann sie hier vorbereiten (gleiches Format wie unten beschrieben), bevor sie einzeln über den Admin-Bereich übernommen oder in einem Rutsch nach Firestore migriert werden.

Für einzelne, schnelle Änderungen (eine Frage hinzufügen/korrigieren/löschen) ist der Admin-Bereich in der App selbst der direkte Weg — dort landen Änderungen sofort live in Firestore, ohne diesen Ordner anzufassen.

## Frage-Format

Jede Frage ist ein Objekt mit:

```json
{
  "n": "1.1",              // ID: <Bereich-Nr>.<laufende Nr innerhalb des Bereichs>
  "s": "FwDV 1",            // Bereich/Abschnitt
  "q": "Fragetext ...",      // die Frage
  "o": ["Option 1", "Option 2", "..."],  // Antwortoptionen
  "c": [0, 2]                // Indizes der richtigen Optionen (0-basiert, Mehrfachauswahl möglich)
}
```

## Quellen

Fragenkatalog: Institut der Feuerwehr NRW (idf.nrw) · Lernkompass, ergänzt um Fragen zum BHKG NRW. Details und Rohmaterial: siehe `quellen/README.md`.
