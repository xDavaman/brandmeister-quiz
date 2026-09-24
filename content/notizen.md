# Notizen & offene Themen

Loses Sammelbecken für Ideen, offene Fragen und nächste Schritte rund um die App — kein fertiger Plan, nur Gedächtnisstütze.

## Content-Pflege (Stand: umgesetzt)
- Fragen liegen live in Firestore (`packs/{packId}/questions`), Admin-Bereich in der App erlaubt Hinzufügen/Bearbeiten/Löschen ohne Redeploy.
- Admin-Bereich hat eine eigene **Berufe/Packs-Verwaltung**: neue Packs anlegen, zwischen Packs wechseln und Fragen je Pack getrennt pflegen — ohne den für Lernende aktiven Bestand anzufassen.
- **Bulk-Import**: im Bereich „Fragen verwalten" kann eine JSON-Datei (Format wie in `fragen/*.json`) für den gerade gewählten Pack importiert werden.
- **Pack-Umschalter in der Lernenden-Oberfläche** ist gebaut und live: Nutzer können zwischen Berufen wählen.

## Live-Berufe (Stand: alle drei live in Firestore, importiert)
- **Brandmeister**: `fragen/brandmeister_master.json` — **557 Fragen**, 17 Themenbereiche. Ursprünglich 295 Fragen (FwDV 1/3/7/10/500/810, Einsatz- & Löschlehre, Fahrzeug- & Gerätekunde, Rechtliche Grundlagen, Wissenschaftliche Grundlagen, BHKG). Erweitert um 262 neue, eigenständig formulierte Fragen auf Basis hochgeladener B1-Ausbildungsunterlagen (u. a. Merkblatt B1, Drehleitermaschinist, Lernfragen-IDF): 7 komplett neue Themenbereiche (ABC-Einsatz · Strahlenschutz, Gefahren der Einsatzstelle, Technische Hilfeleistung · Straße, E-/Hybridfahrzeuge, Drehleiter, Staatsbürgerkunde, Vorbeugender Brandschutz) sowie Erweiterungen der Bereiche Atemschutz, Wissenschaftliche Grundlagen, BHKG und Fahrzeug- & Gerätekunde. Rohdatei der 262 neuen Fragen separat unter `fragen/new_combined_all.json`.
- **Rettungssanitäter**: `fragen/rettungssanitaeter_master.json` — 90 Fragen, 8 Themenbereiche. Quellen: `quellen/rettungssanitaeter_quellen.md`.
- **Notfallsanitäter**: `fragen/notfallsanitaeter_master.json` — 122 Fragen, 13 Themenbereiche. Quellen: `quellen/notfallsanitaeter_quellen.md`.
- Alle Kataloge sind eigenständig formuliert (keine wörtlichen Übernahmen aus Prüfungskatalogen/Lehrbüchern), im selben Format (`n`/`s`/`q`/`o`/`c`).
- **Gesamtzahl aller Fragen über alle drei Berufe: 769** (557 + 90 + 122).

## Wichtige Fixes (Stand: erledigt)
- Firestore-Security-Rules: fehlende `packProgress`-Subcollection-Regel ergänzt (Cloud-Sync für den Lernfortschritt lief zuvor für alle Nutzer still auf Fehler).
- Admin-Dokument `admins/{uid}` angelegt, damit „Berufe/Packs verwalten" im Admin-Bereich sichtbar ist.

## Offene Themen für später
- **Monetarisierung**: Zielbild bereits festgelegt (siehe Doc „Brandmeister Quiz – Monetarisierung & Erweiterung"): Einmalkauf pro Beruf/Pack, kein Abo. Zahlungsintegration (Stripe o. ä.) bewusst noch nicht umgesetzt — erst sinnvoll, wenn reale Nutzerzahlen da sind.
- **Spendenlink**: fehlt noch (braucht Seans echten PayPal.me-/Ko-fi-Account).

## Quellen-Workflow
Siehe `quellen/README.md` für die Ablage von Rohmaterial und `README.md` für den Gesamt-Workflow (Quelle → Frage → Firestore).
