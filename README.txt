PurineTracker Offline-Prototyp – v0.10

Inhalt:
- index.html: App-Oberfläche und Logik
- PurineTracker_Import_v1.json: Lebensmittel-Importdaten aus Excel v1.6
- manifest.webmanifest: PWA-Metadaten
- sw.js: Cache für Offline-Aufruf nach initialem Laden
- Start-PurineTracker.cmd / .ps1: lokaler Windows-Start ohne Python und ohne Installation

Neu in v0.6 – vollständiges Backup und Wiederherstellung:
- Export eines persönlichen Vollbackups (Tagesprotokoll, Gewicht, Blutwerte, Favoriten)
- Backupformat v3; ältere Backups im Format v2 werden ebenfalls angenommen
- Wiederherstellung ersetzt alle persönlichen Daten auf diesem Gerät vollständig
- Vor dem Ersetzen wird automatisch eine Sicherheitskopie zum Download bereitgestellt
- Backup wird vor dem Eingriff geprüft; ungültige Dateien werden abgewiesen
- Lebensmittel-Stammdaten bleiben bei der Wiederherstellung unverändert
- Leere importierte Messreihen bleiben leer; Startwerte werden nicht ungefragt neu angelegt
- Rezepte und Einstellungen sind im Backupformat als vorbereitete Bereiche enthalten; Rezeptverwaltung ist noch nicht implementiert

Wichtige Hinweise:
Dies ist weiterhin ein technischer Prototyp, noch keine produktionsreife Android-App. Die App speichert persönliche Daten lokal im Browser (IndexedDB und localStorage). Bewahre exportierte Backups zusätzlich außerhalb des Geräts auf.

Start unter Windows:
1. ZIP-Datei vollständig entpacken.
2. Den Ordner PurineTracker_Prototyp öffnen.
3. Doppelklick auf Start-PurineTracker.cmd.
4. Der Browser öffnet die App automatisch. Das schwarze Fenster muss geöffnet bleiben.
5. Zum Beenden im schwarzen Fenster Q drücken.

Der lokale Server ist nur an 127.0.0.1 gebunden und damit nur auf diesem Laptop erreichbar. Es werden keine Daten an einen Server übertragen.

Hinweis zur Gesundheit:
Der Harnsäure-Äquivalentwert ist ein rechnerischer Orientierungswert für Lebensmittel und keine Vorhersage des Blut-Harnsäurewerts.


NEU IN V0.4: Rezeptverwaltung. Rezepte mit Zutaten aus der Lebensmitteldatenbank anlegen, Fertiggewicht erfassen, Werte pro 100 g berechnen und Portionen in das Tagesprotokoll übernehmen. Backups werden im Format v4 exportiert; v2/v3 bleiben importierbar.


NEU IN V0.5: Tagesprotokoll nach Mahlzeiten gruppiert, Zwischensummen je Mahlzeit, Einträge bearbeiten (Lebensmittel/Rezept, Menge, Datum, Mahlzeit), Wochen- und Monatsauswertungen. Durchschnittswerte berücksichtigen ausschließlich dokumentierte Tage. Backup-Export im Format v5; Wiederherstellung unterstützt v2 bis v5.


KORREKTUR IN V0.5.1: Purin-Durchschnitt in Wochen- und Monatsauswertung liest jetzt das tatsächlich gespeicherte Feld purine_mg. Bearbeitungsformular nutzt die volle Zeilenbreite; auf schmalen Bildschirmen werden die Eingabefelder einspaltig angeordnet. Backup-Format bleibt v5.


NEU IN V0.6 – TAGESSTATUS UND KALENDER
- Tage mit mindestens einem Eintrag starten als „Offen“.
- „Tageserfassung abschließen“ speichert den Status lokal.
- Abgeschlossene Tage lassen sich jederzeit wieder öffnen.
- Neue, bearbeitete oder gelöschte Einträge öffnen den betroffenen Tag erneut; wenn der letzte Eintrag gelöscht wird, erscheint „Keine Angaben“.
- Der Kalender zeigt Abgeschlossen, Offen und Keine Angaben und erlaubt die Tagesauswahl.
- Wochen- und Monatsdurchschnitte berücksichtigen weiterhin alle Tage mit mindestens einem Eintrag, unabhängig vom Abschlussstatus.
- Backup-Format v6 enthält zusätzlich abgeschlossene Tagesstatus. Backups v2 bis v5 bleiben importierbar; ältere Backups enthalten naturgemäß keine Tagesstatus.
- IndexedDB wird von Version 3 auf 4 erweitert; vorhandene Einträge, Rezepte und Messwerte werden nicht gelöscht.


NEU IN V0.7 – BEDIENKOMFORT BEI DER LEBENSMITTELERFASSUNG
- Favoriten werden bei leerer Suche direkt als eigener Bereich angezeigt.
- Zuletzt verwendete Lebensmittel werden aus dem vorhandenen Tagesprotokoll abgeleitet und darunter angezeigt (maximal 8, ohne Duplikate).
- Die Suche durchsucht weiterhin alle 619 importierten Lebensmittel; Favoriten stehen in Suchtreffern zuerst.
- Mahlzeit wird vor der Lebensmittelsuche gewählt und lokal gemerkt, damit mehrere Zutaten derselben Mahlzeit schneller erfasst werden können.
- Mengen-Schnellwahl für 50, 100, 150 und 200 g; die Eingabe kann weiterhin frei angepasst werden.
- „Speichern & nächstes Lebensmittel“ speichert den Eintrag und lässt die Erfassungsmaske für den nächsten Eintrag geöffnet. Datum und Mahlzeit bleiben erhalten.
- „Speichern & Tagesübersicht“ führt wie bisher nach dem Speichern zurück zur Tagesübersicht.
- Keine Änderung am IndexedDB-Schema oder am Backupformat v6. Vorhandene persönliche Daten und Backups bleiben kompatibel.
- Service-Worker-Cache wurde auf v7 angehoben, damit Browser die neue Oberfläche laden.

TESTHINWEIS V0.7
Die JavaScript-Syntax und die Importdaten wurden lokal geprüft. Ein echter Browser-/Android-Test muss noch erfolgen. Nach dem Austausch der App-Dateien bitte den Server und Browser neu starten bzw. die Seite vollständig neu laden. Persönliche Daten bleiben im Browserprofil gespeichert; vor dem Update ist ein Vollbackup weiterhin sinnvoll.


NEU IN V0.8 – ERNÄHRUNGSVERLAUF
- Fortschritt enthält jetzt einen Ernährungstrend für die letzten 30 Tage, 90 Tage oder den gesamten dokumentierten Verlauf.
- Tageswerte werden aus allen Einträgen des jeweiligen Datums summiert.
- Durchschnittswerte berücksichtigen ausschließlich Tage mit mindestens einem Eintrag; Tage ohne Angaben werden nicht als 0 mg gewertet.
- Purin und Harnsäure-Äquivalent werden getrennt ausgewiesen.
- Der Verlauf wird auch nach Änderungen am Tagesprotokoll aktualisiert.
- Keine Änderung am IndexedDB-Schema oder Backupformat v6; vorhandene Daten bleiben kompatibel.
- Der Ernährungstrend ist ausdrücklich keine Vorhersage des Blutwerts.


NEU IN V0.9 – MESSWERTE KORRIGIEREN UND DIAGRAMME EHRLICHER DARSTELLEN
- Gewichtsmessungen und Harnsäure-Laborwerte können jetzt über „Bearbeiten“ geändert werden. Die bestehende Datensatz-ID bleibt erhalten; es wird kein zusätzlicher Messpunkt angelegt.
- Beim Bearbeiten lassen sich Datum und Messwert korrigieren. Das ist auch für den bisher undatierten Ausgangs-Laborwert möglich.
- Gewicht- und Blutwertdiagramme zeigen bei nur einer Messung ausdrücklich, dass noch kein Verlauf vorliegt. Es wird keine Verbindungslinie als Trend gezeichnet.
- Der Ernährungsverlauf positioniert dokumentierte Tage nach ihrem tatsächlichen Kalenderabstand. Zwischen nicht aufeinanderfolgenden dokumentierten Tagen wird keine Linie gezeichnet; Tage ohne Einträge werden nicht als Nullwerte dargestellt.
- IndexedDB-Schema und Vollbackupformat v6 bleiben unverändert. Vorhandene persönliche Daten, Rezepte und Backups bleiben kompatibel.
- Service-Worker-Cache auf v9 angehoben.

UPDATE-HINWEIS
1. Vor dem Update in der bisherigen App ein vollständiges Backup exportieren.
2. ZIP in einen neuen Ordner entpacken (nicht in den alten Ordner hineinmischen).
3. Die neue Version mit Start-PurineTracker.cmd starten.
4. Die App verwendet denselben lokalen Ursprung http://127.0.0.1:8765; deshalb bleiben die vorhandenen Browserdaten bei normalem Update im selben Browserprofil erhalten. Nicht Browserdaten/Website-Daten löschen.
5. Nach dem Start prüfen, ob Tagesdaten, Rezepte, Gewicht und Laborwert vorhanden sind. Anschließend Bearbeiten-Funktion testen.

TESTSTATUS
- JavaScript-Syntaxprüfung und Daten-/Dateistrukturprüfung lokal durchgeführt.
- Kein automatisierter echter Android-/Browser-UI-Test durchgeführt. Bitte die Bearbeiten-Funktion zunächst mit einem Testwert prüfen und vor dem Update ein Backup aufbewahren.


NEU in v0.10:
- Eingabeformulare für Gewicht und Laborwerte werden nach dem Speichern vollständig geleert.
- Monats- und Jahresübersicht orientiert sich am ausgewählten Tag. Sie zeigt dokumentierte Ernährungsmittelwerte sowie erste/letzte Gewichts- und Blutmessung im Zeitraum.
- Keine Ernährungstage ohne Einträge werden als 0 mg interpretiert.
