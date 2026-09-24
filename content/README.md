# content/ — Fragen- und Quellenarchiv

Dieser Ordner ist das Archiv für alles, was in die Brandmeister-Quiz-App einfließt: Quellmaterial, Notizen und der gepflegte Master-Fragenbestand. Er liegt bewusst im selben Repo wie die App, damit alles an einem Ort bleibt.

## Struktur

```
content/
├── README.md               ← diese Datei
├── notizen.md               ← offene Ideen, ToDos, Themen für später (Monetarisierung, ...)
├── fragen/
│   ├── brandmeister_master.json        ← gepflegter Master-Fragenbestand Brandmeister (557 Fragen, live in Firestore)
│   ├── new_combined_all.json           ← Rohdatei: die 262 neu ergänzten Brandmeister-Fragen (Stand B1-Ausbildungsunterlagen)
│   ├── rettungssanitaeter_master.json  ← Fragenkatalog Rettungssanitäter (90 Fragen, live in Firestore)
│   └── notfallsanitaeter_master.json   ← Fragenkatalog Notfallsanitäter (122 Fragen, live in Firestore)
└── quellen/
    ├── README.md                        ← Quellenverzeichnis + Ablage für Rohmaterial (PDFs, Auszüge, Links)
    ├── rettungssanitaeter_quellen.md    ← Quellen für den Rettungssanitäter-Fragenkatalog
    └── notfallsanitaeter_quellen.md     ← Quellen für den Notfallsanitäter-Fragenkatalog
```

## Wie das mit der App zusammenhängt

Die App lädt ihre Fragen **live aus Firestore** (`packs/{packId}/questions/...`), nicht direkt aus diesem Ordner — das ermöglicht Änderungen ohne App-Update (siehe Admin-Bereich in der App: "Fragen verwalten"). Alle drei Berufe (Brandmeister, Rettungssanitäter, Notfallsanitäter) sind eigene Packs und für Lernende über den Pack-Umschalter in der App wählbar.

Die JSON-Dateien in `fragen/` sind trotzdem wichtig als:
- **Referenz/Backup**: der vollständige Fragenbestand als Klartext, unabhängig von Firestore einsehbar und versionierbar (über die Git-Historie nachvollziehbar).
- **Startbestand**: Grundlage für den Bulk-Import im Admin-Bereich ("Fragen aus JSON importieren").
- **Basis für größere Ergänzungen**: Wer viele neue Fragen auf einmal einpflegen will, kann sie hier vorbereiten (gleiches Format wie unten beschrieben), bevor sie über den Admin-Bereich importiert werden.

Für einzelne, schnelle Änderungen (eine Frage hinzufügen/korrigieren/löschen) ist der Admin-Bereich in der App selbst der direkte Weg — dort landen Änderungen sofort live in Firestore, ohne diesen Ordner anzufassen.

Für einen kompletten neuen Beruf gibt es im Admin-Bereich unter „Berufe/Packs verwalten" einen Weg, ganz ohne Redeploy:
1. „+ Neues Pack anlegen" → Name eingeben, damit wird automatisch die passende Pack-ID erzeugt.
2. Im Bereich „Fragen verwalten" (zeigt den neu angelegten Pack) → „Fragen aus JSON importieren" → die passende Datei aus diesem Ordner auswählen.
3. Fertig — die Fragen liegen sofort live in Firestore für diesen Pack, komplett getrennt von den übrigen Berufen.

## Frage-Format

Jede Frage ist ein Objekt mit:

```json
{
  "n": "1.1",                              // ID: <Bereich-Nr>.<laufende Nr innerhalb des Bereichs>
  "s": "FwDV 1",                           // Bereich/Abschnitt
  "q": "Fragetext ...",                    // die Frage
  "o": ["Option 1", "Option 2", "..."],    // Antwortoptionen
  "c": [0, 2]                              // Indizes der richtigen Optionen (0-basiert, Mehrfachauswahl möglich)
}
```

## Brandmeister — Themenbereiche (557 Fragen, 17 Bereiche)

FwDV 1 · FwDV 3 · FwDV 7 · Atemschutz · FwDV 10 · Leitern · FwDV 500 · Gefahrstoffe · FwDV 810 · Sprechfunk · Einsatz- & Löschlehre · Fahrzeug- & Gerätekunde · Rechtliche Grundlagen · Wissenschaftliche Grundlagen · BHKG · ABC-Einsatz · Strahlenschutz · Gefahren der Einsatzstelle · Technische Hilfeleistung · Straße · E-/Hybridfahrzeuge · Drehleiter · Staatsbürgerkunde · Vorbeugender Brandschutz

Die letzten sieben Bereiche (ab ABC-Einsatz) sowie Erweiterungen der Bereiche Atemschutz, Wissenschaftliche Grundlagen, BHKG und Fahrzeug- & Gerätekunde wurden auf Basis hochgeladener B1-Ausbildungsunterlagen ergänzt (u. a. Merkblatt B1, Drehleitermaschinist, Lernfragen-IDF) — eigenständig formuliert, keine wörtlichen Übernahmen.

## Quellen

Fragenkatalog: Institut der Feuerwehr NRW (idf.nrw) · Lernkompass, ergänzt um Fragen zum BHKG NRW sowie um eigenständig formulierte Fragen aus B1-Ausbildungsunterlagen. Details und Rohmaterial: siehe `quellen/README.md`.
