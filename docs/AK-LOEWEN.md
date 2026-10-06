# AK Löwen · Sportclub-Website und Telegram-Integration

[Zur Projektübersicht](../README.md) · [Quellcode](https://github.com/koss32/Ak-loewen/tree/release-9/site) · [Projektwebsite](https://www.ak-loewen.de/)

## Aufgabe

Eine zentrale Anlaufstelle für Sportangebote in Solingen: Programme, Trainingsgruppen, Trainer, Zeiten, Preise und die Anfrage für ein Probetraining. Die Telegram-Integration ist Teil desselben Produkts.

## Umsetzung im Repository

- Lokalisierte Seiten für Deutsch, Russisch, Ukrainisch und Türkisch.
- Gemeinsame Datendatei für Programme, Gruppen, Termine und weitere Seiteninhalte.
- Webformular mit serverseitiger Prüfung von Kontakt, Gruppenauswahl, Termin und Einwilligung.
- Telegram-Abläufe für Buchung, Status und Kontakt mit dem Team.
- Redis-basierte Anfragezustände, Deduplizierung und eine Begrenzung wiederholter Anfragen.
- Build-Skript für statische Seiten; getrennte HTTP-Endpunkte und Servermodule.

**Stack:** JavaScript (ES Modules), HTML/CSS, Node.js, Upstash Redis, Telegram Bot API und Vercel-Konfiguration. ESLint, Node-Test-Runner und Browserprüfungen mit Playwright sind im Projekt vorhanden.

## Ein konkretes technisches Beispiel

Eine Probetraining-Anfrage kann nach einem Verbindungsproblem erneut gesendet werden. Das System verwendet eine Anfrage-ID und einen Fingerprint der Daten:

| Situation | Verhalten im geprüften Servicemodul |
| --- | --- |
| Anfrage wurde bereits bestätigt zugestellt | Vorhandenes Ergebnis zurückgeben, ohne erneut zu senden |
| Dieselbe ID mit abweichenden Daten | Konflikt melden |
| Telegram-Antwort ist unklar oder die Verbindung bricht ab | Zustand `uncertain`; kein automatisches erneutes Senden |
| Telegram bestätigt den Versand, danach scheitert das Speichern | Bestätigung erhalten; ein erneuter Aufruf bleibt zunächst `pending` |

Dieses Beispiel macht Eingabeprüfung, Zustandsmodell und Fehlerszenarien anhand überschaubarer Dateien nachvollziehbar.

## Code zum Einstieg

Die Links verweisen auf die am 06.10.2026 gesichtete Revision `38caaaa37abacef4eb90b8aef07f4314287662b3`, nicht auf einen später veränderbaren Branch-Stand.

| Datei | Inhalt |
| --- | --- |
| [validate-request.js](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/site/server/validate-request.js) | Validierung und Auswahl zulässiger Eingabefelder |
| [hosted-trial.js](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/site/server/hosted-trial.js) | Anfragezustände, Versand und Fehlerbehandlung |
| [form.test.js](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/site/tests/form.test.js) | Grenzen für Kontakt, Namen, Termine und Eingabefelder |
| [hosted.test.js](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/site/tests/hosted.test.js) | Wiederholungen und unklare Versandantworten |
| [package.json](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/site/package.json) | Abhängigkeiten und Projektbefehle |

## Prüfung und Status

Am **06.10.2026** wurden die beiden oben verlinkten Testdateien mit ihren Originalabhängigkeiten aus derselben Revision unter **Node.js 24.19.0** lokal ausgeführt: **8 Tests bestanden, 0 fehlgeschlagen**. Externe Systeme waren durch Testimplementierungen ersetzt. Das prüft diese Logik, nicht den echten Versand oder die gesamte Anwendung.

Der [Release-9-Bericht](https://github.com/koss32/Ak-loewen/blob/38caaaa37abacef4eb90b8aef07f4314287662b3/docs/releases/RELEASE-9.md) dokumentiert eine Veröffentlichung unter `www.ak-loewen.de`. Die Website konnte bei dieser Portfoliosichtung nicht unabhängig abgerufen werden; die aktuelle Erreichbarkeit wird daher hier nicht als geprüft ausgewiesen.

Die Default-Branch des Repositories enthält Navigation und historische Unterlagen. Für diese Projektbeschreibung wurde der Code von `release-9` gesichtet; dadurch wird keine Arbeitsbranch umgestellt. Automatische Erinnerungen sind laut Projektdokumentation eine deaktivierte zukünftige Funktion.

[Prüfprotokoll](VERIFICATION.md)
