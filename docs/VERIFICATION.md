# Technische Sichtung · 06.10.2026

[Zur Projektübersicht](../README.md)

Dieses Protokoll trennt neu ausgeführte Prüfungen von Angaben vorhandener Projektdokumentation.

## AK Löwen: neu ausgeführter Test

| Punkt | Wert |
| --- | --- |
| Repository | `koss32/Ak-loewen` |
| Gesichtet und für den Test verwendet | `release-9` / `38caaaa37abacef4eb90b8aef07f4314287662b3` |
| Runtime | Node.js `v24.19.0` |
| Testdateien | `site/tests/form.test.js`, `site/tests/hosted.test.js` |
| Ergebnis | **8 bestanden, 0 fehlgeschlagen** |
| Umfang | Originaldateien mit ihren direkt benötigten Modulen; keine Änderung am Produktcode |
| Externe Systeme | In den Tests ersetzte Telegram- und Ledger-Implementierungen |

Reproduzierbar aus der entsprechenden Revision, im Verzeichnis `site/`:

```bash
node --test tests/form.test.js tests/hosted.test.js
```

Geprüfte Fälle:

1. Gültiger Kontakt reicht aus; ungültige Kontakte werden abgewiesen.
2. Grenzen für Namen und Kommentare werden durchgesetzt.
3. Ein Termin muss zur gewählten Gruppe gehören.
4. Administrative Zusatzfelder werden nicht in die validierten Daten übernommen.
5. Bestätigter Versand wird bei Wiederholung nicht erneut ausgeführt.
6. Unklare Versandantworten führen nicht zum automatischen erneuten Versand.
7. Fehlende Konfiguration wird vor Annahme der Daten abgewiesen.
8. Bestätigter Versand bleibt auch bei anschließendem Speicherfehler bestätigt.

Dies ist eine gezielte lokale Prüfung. Vollständiger Build, vollständige Testsuite, echter Redis, echter Telegram-Versand und Livebetrieb wurden dabei nicht geprüft.

## Weitere Projekte

| Projekt | Sichtung | Neu ausgeführte Prüfung |
| --- | --- | --- |
| Recomendator | README, Abhängigkeiten, Status, vorhandener Prüfbericht und zwei Kernmodule | Keine; Testergebnisse vom 20.09.2026 bleiben als historische lokale Angaben gekennzeichnet |
| VALSET | README und Dateibaum der Projektbranch | Keine; Funktionsbeschreibungen stammen aus der Projektdokumentation |

## Veröffentlichungsumfang

Dieses Repository enthält Projektbeschreibungen und dieses Protokoll. Es veröffentlicht keine Zugangsdaten und keine vollständigen privaten Repositories. Es ändert weder Produktcode noch Deployment-Konfiguration oder Repository-Sichtbarkeit.
