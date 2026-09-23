# Notizen & offene Themen

Loses Sammelbecken für Ideen, offene Fragen und nächste Schritte rund um die App — kein fertiger Plan, nur Gedächtnisstütze.

## Content-Pflege (Stand: umgesetzt)
- Fragen liegen live in Firestore (`packs/{packId}/questions`), Admin-Bereich in der App erlaubt Hinzufügen/Bearbeiten/Löschen ohne Redeploy.
- Admin-Bereich hat jetzt eine eigene **Berufe/Packs-Verwaltung**: neue Packs anlegen, zwischen Packs wechseln und Fragen je Pack getrennt pflegen — ohne den für Lernende aktiven Brandmeister-Bestand anzufassen.
- Neuer **Bulk-Import**: im Bereich „Fragen verwalten" kann eine JSON-Datei (Format wie in `fragen/*.json`) für den gerade gewählten Pack importiert werden — praktisch für größere Startbestände wie die beiden unten.

## Vorbereitete Berufe (Stand: Fragenkataloge fertig, noch nicht live in Firestore)
- **Rettungssanitäter**: `fragen/rettungssanitaeter_master.json` — 90 Fragen, 8 Themenbereiche (Berufskunde & Rechtsgrundlagen, Anatomie & Physiologie, Basismaßnahmen & Vitalfunktionen, Reanimation/BLS, Traumatologie, Schock & internistische Notfälle, Hygiene & Infektionsschutz, Rechtskunde, Einsatztaktik & Fahrzeug-/Gerätekunde, Kommunikation & Psychologie). Quellen: `quellen/rettungssanitaeter_quellen.md`.
- **Notfallsanitäter**: `fragen/notfallsanitaeter_master.json` — 122 Fragen, 13 Themenbereiche (u. a. Rechtskunde, Pharmakologie, Kardiologie, Reanimation/ALS, Traumatologie, Pädiatrie, Gynäkologie & Geburtshilfe). Deutlich anspruchsvolleres Niveau als Rettungssanitäter (3-jährige Fachausbildung inkl. invasiver Maßnahmen). Quellen: `quellen/notfallsanitaeter_quellen.md`.
- Beide Kataloge sind eigenständig formuliert (keine wörtlichen Übernahmen aus Prüfungskatalogen/Lehrbüchern), im selben Format wie der Brandmeister-Bestand (`n`/`s`/`q`/`o`/`c`).
- **Fehlt noch, damit sie live nutzbar sind** (braucht echten Admin-Login, der wurde absichtlich nicht automatisiert): im Admin-Bereich „+ Neues Pack anlegen" für `Rettungssanitäter` und `Notfallsanitäter`, dann jeweils bei „Fragen verwalten" → „Fragen aus JSON importieren" die passende Datei aus `fragen/` auswählen. Danach im Pack-Umschalter in der App selbst (noch zu bauen, siehe unten) für Lernende sichtbar machen.
- Noch offen: eigener **Pack-Umschalter in der Lernenden-Oberfläche** (aktuell sieht jeder nur `brandmeister`/`CURRENT_PACK`), damit Nutzer zwischen den Berufen wählen können — bisher nur admin-seitig vorbereitet.

## Offene Themen für später
- **Monetarisierung**: Zielbild bereits festgelegt (siehe Doc „Brandmeister Quiz – Monetarisierung & Erweiterung"): Einmalkauf pro Beruf/Pack, kein Abo. Zahlungsintegration (Stripe o. ä.) bewusst noch nicht umgesetzt — erst sinnvoll, wenn reale Nutzerzahlen da sind.
- **Spendenlink**: fehlt noch (braucht Seans echten PayPal.me-/Ko-fi-Account).
- **Erweiterung um weitere Berufe**: Datenmodell + Admin-Werkzeuge stehen (Pack anlegen, JSON-Import, isolierte Verwaltung). Rettungssanitäter/Notfallsanitäter-Inhalte sind vorbereitet (siehe oben), müssen nur noch importiert und in der Lernenden-UI sichtbar gemacht werden.

## Quellen-Workflow
Siehe `quellen/README.md` für die Ablage von Rohmaterial und `README.md` für den Gesamt-Workflow (Quelle → Frage → Firestore).
