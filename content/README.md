# content/ — Fragen- und Quellenarchiv

Dieser Ordner ist das Archiv für alles, was in die Brandmeister-Quiz-App einfließt: Quellmaterial, Notizen und der gepflegte Master-Fragenbestand. Er liegt bewusst im selben Repo wie die App, damit alles an einem Ort bleibt.

## Struktur

```
content/
├── README.md              ← diese Datei
├── notizen.md              ← offene Ideen, ToDos, Themen für später (Monetarisierung, weitere Berufe, ...)
├── fragen/
│   ├── brandmeister_master.json         ← gepflegter Master-Fragenbestand Brandmeister (295 Fragen, live in Firestore)
│   ├── rettungssanitaeter_master.json   ← vorbereiteter Fragenkatalog Rettungssanitäter (90 Fragen, noch nicht importiert)
│   └── notfallsanitaeter_master.json    ← vorbereiteter Fragenkatalog Notfallsanitäter (122 Fragen, noch nicht importiert)
└── quellen/
    ├── README.md                        ← Quellenverzeichnis + Ablage für Rohmaterial (PDFs, Auszüge, Links)
    ├── rettungssanitaeter_quellen.md     ← Quellen für den Rettungssanitäter-Fragenkatalog
    └── notfallsanitaeter_quellen.md      ← Quellen für den Notfallsanitäter-Fragenkatalog
```

## Wie das mit der App zusammenhängt

Die App selbst lädt ihre Fragen **live aus Firestore** (`packs/brandmeister/questions/...`), nicht direkt aus diesem Ordner — das ermöglicht Änderungen ohne App-Update (siehe Admin-Bereich in der App: "Fragen verwalten").

`fragen/brandmeister_master.json` ist trotzdem wichtig als:
- **Referenz/Backup**: der vollständige Fragenbestand als Klartext, unabhängig von Firestore einsehbar und versionierbar (über die Git-Historie nachvollziehbar).
- **Startbestand**: dieselbe Datei ist die Grundlage für den bereits ausgeführten einmaligen "Fragen-Datenbank initialisieren"-Schritt in der App, der den Bestand nach Firestore überträgt.
- **Basis für größere Ergänzungen**: Wer viele neue Fragen auf einmal einpflegen will, kann sie hier vorbereiten (gleiches Format wie unten beschrieben), bevor sie einzeln über den Admin-Bereich übernommen oder in einem Rutsch nach Firestore migriert werden.

Für einzelne, schnelle Änderungen (eine Frage hinzufügen/korrigieren/löschen) ist der Admin-Bereich in der App selbst der direkte Weg — dort landen Änderungen sofort live in Firestore, ohne diesen Ordner anzufassen.

Für einen kompletten neuen Beruf (wie `rettungssanitaeter_master.json` oder `notfallsanitaeter_master.json`) gibt es im Admin-Bereich unter „Berufe/Packs verwalten" einen Weg, ganz ohne Redeploy:
1. „+ Neues Pack anlegen" → Name eingeben (z. B. „Rettungssanitäter"), damit wird automatisch die passende Pack-ID erzeugt.
2. Im Bereich „Fragen verwalten" (zeigt jetzt den neu angelegten Pack) → „Fragen aus JSON importieren" → die passende Datei aus diesem Ordner auswählen.
3. Fertig — die Fragen liegen sofort live in Firestore für diesen Pack, komplett getrennt vom Brandmeister-Bestand, den Lernende sehen.

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
