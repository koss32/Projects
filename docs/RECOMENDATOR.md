# Recomendator · Persönlicher Film- und Serienkatalog

[Zur Projektübersicht](../README.md)

## Aufgabe

Bewertungen und gesehene Filme bzw. Serien in einer Anwendung zusammenführen. Empfehlungen berücksichtigen den persönlichen Bestand und das aus Bewertungen abgeleitete Geschmacksprofil.

## Umsetzung im privaten Repository

- Next.js-Anwendung mit React, TypeScript und Tailwind CSS.
- PostgreSQL-Schema mit Supabase, SQL-Migrationen, Benutzerrechten und Row Level Security.
- Versionierte Bewertungen und Geschmacksprofile.
- TMDB-Anbindung für Suche, Katalogdaten und Empfehlungskandidaten.
- Serverseitige Ausschlüsse bereits gesehener bzw. ausgeblendeter Titel.
- Zod-Schemas für Eingaben sowie ein MCP-Server mit neun registrierten Werkzeugen.
- Export/Import und PWA-Dateien; optionaler Gemini-Adapter.

## Architektur

| Bereich | Aufgabe |
| --- | --- |
| React / Next.js | Bedienoberfläche und HTTP-Routen |
| Domain-Module | Bewertungen, Sammlung, Kandidatenauswahl und Empfehlungen |
| PostgreSQL / Supabase | Datenspeicherung, Profilversionen, Transaktionen und Benutzerrechte |
| TMDB-Adapter | Suche und Aufbereitung externer Katalogdaten |
| MCP-Schicht | Werkzeuge für autorisierte Lese-, Schreib- und Empfehlungsoperationen |

## Ein konkretes technisches Beispiel

Das Empfehlungsmodul lädt den persönlichen Bestand, bildet Ausschlüsse und bewertet Kandidaten anhand des Profils. Es erzeugt anschließend einen Kontext mit Ablaufzeit und Kandidaten-IDs. Beim Speichern einer Auswahl wird dieser Kontext erneut serverseitig geprüft.

Das MCP-Modul prüft vor Domain-Aufrufen die für das jeweilige Werkzeug benötigte Berechtigung. Lesender Zugriff und Schreibzugriff werden im Code getrennt behandelt.

## Status und Grenzen

**Entwicklungsprojekt; vollständiger Livebetrieb ist hier nicht bestätigt.** Die gesichtete README beschreibt eine lokale Rekonstruktion. Der vorhandene Prüfbericht vom **20.09.2026** berichtet lokale TypeScript-, Lint-, Unit-, PGlite-, Build- und Browserprüfungen. Diese Prüfungen wurden für das Portfolio nicht erneut ausgeführt.

PGlite verwendet eine lokale Datenbankumgebung; die Browsertests ersetzen APIs. Das dokumentiert keine erfolgreiche Integration mit echtem Supabase, TMDB, Gemini, ChatGPT oder einem Android-Gerät.

Der vollständige Quellcode bleibt privat. Diese Seite veröffentlicht eine technische Beschreibung, keine Nutzerdaten, Zugangsdaten oder Kopie des privaten Repositories.

**Grundlage der Beschreibung:** `koss32/Recomendator`, Branch `recomendator`, Revision `7760e95bb79f927d247c80e589c4f9777543bf10`; gesichtet wurden README, package.json, Projektstatus, Prüfbericht, `src/lib/domain/recommendations.ts` und `src/lib/mcp/server.ts`. Diese internen Quellen sind für Besucher des öffentlichen Portfolios nicht zugänglich.
