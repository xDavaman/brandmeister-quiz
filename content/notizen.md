# Notizen & offene Themen

Loses Sammelbecken für Ideen, offene Fragen und nächste Schritte rund um die App — kein fertiger Plan, nur Gedächtnisstütze.

## Content-Pflege (Stand: umgesetzt)
- Fragen liegen live in Firestore (`packs/brandmeister/questions`), Admin-Bereich in der App erlaubt Hinzufügen/Bearbeiten/Löschen ohne Redeploy.
- Datenmodell ist multi-pack-fähig angelegt (`packs/{packId}/...`), aktuell nur `brandmeister` befüllt.

## Offene Themen für später
- **Monetarisierung**: noch nicht besprochen — Optionen könnten z. B. Freemium (Grundfunktionen kostenlos, Zusatzfeatures/weitere Berufe kostenpflichtig), einmaliger Kaufpreis, oder Abo sein. Muss noch mit den Anforderungen (Zielgruppe, Umfang) abgeglichen werden.
- **Erweiterung um weitere Berufe**: z. B. Notfallsanitäter, Rettungssanitäter. Datenmodell ist vorbereitet (neues Pack anlegen + Fragen befüllen + Pack-Umschalter in der App-UI ergänzen), aber noch nicht umgesetzt.

## Quellen-Workflow
Siehe `quellen/README.md` für die Ablage von Rohmaterial und `README.md` für den Gesamt-Workflow (Quelle → Frage → Firestore).
