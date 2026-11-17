# Flugbuch – Offline-Web-App (PWA)

## Stand dieses Pakets

- Bestehende Flugbuch-Oberfläche und Funktionen übernommen.
- Web-App-Manifest ergänzt.
- Service Worker ergänzt: App-Shell wird nach dem ersten Online-Aufruf zwischengespeichert.
- Bestehende lokale Speicherung (`localStorage`) und Backup/Restore bleiben erhalten.
- Kein CloudKit-/iCloud-Sync aktiv: dafür sind ein persönlicher iCloud-Container, CloudKit-Web-Konfiguration und Zugangsdaten erforderlich. Diese kann ich nicht ohne Einrichtung in deinem Apple-Konto fertig aktivieren. Bitte vor der Einrichtung keine vertraulichen Zugangsdaten in öffentlichen Dateien hinterlegen.

## Kostenlos bereitstellen

Die Dateien müssen unter einer HTTPS-Adresse erreichbar sein. Eine kostenlose Möglichkeit ist GitHub Pages:

1. Auf github.com ein kostenloses Konto erstellen/anmelden.
2. Ein neues Repository erstellen, z. B. `flugbuch-pwa`.
3. Alle Dateien aus diesem Ordner ins Repository hochladen (index.html, manifest.webmanifest, service-worker.js, icon.svg).
4. In **Settings → Pages** als Quelle den Hauptbranch und Ordner `/ (root)` auswählen.
5. Die von GitHub angezeigte HTTPS-Adresse auf dem iPhone in Safari öffnen.
6. Safari: **Teilen → Zum Home-Bildschirm**.
7. Die Adresse auch auf dem iPad öffnen und dort ebenfalls zum Home-Bildschirm hinzufügen.

## Offline-Verhalten

Die App muss zuerst online über HTTPS geladen werden, damit Safari den Service Worker installieren und die Dateien zwischenspeichern kann. Danach kann die Oberfläche offline geöffnet werden. Flüge werden weiterhin pro Gerät im lokalen Browser-Speicher gehalten. Safari-Speicherdaten nicht löschen; regelmässige Backups über die eingebaute Backup-Funktion behalten.

## iCloud-Synchronisation – nächster Schritt

Diese Version synchronisiert noch nicht zwischen Geräten. Die aktuelle HTML-Datei hat einen lokalen Speicherpfad (`localStorage`) und eine optionale, nicht konfigurierte `db`-Schnittstelle. Für echte iCloud-Synchronisation muss die Datenlogik auf CloudKit JS umgestellt werden (Flüge, Profil, Flugplatz-Koordinaten sowie Löschmarkierungen), und CloudKit muss im Apple-Developer-Portal konfiguriert werden. Erst nach Eintragung der echten Container-/Web-Konfiguration kann diese Funktion sicher getestet werden.

## Wichtige Hinweise

- Offline-Betrieb ist lokal je Gerät; iCloud-Abgleich benötigt Internet.
- Eine PWA benötigt keine 7-Tage-Xcode-Signatur.
- Kostenloses Hosting hat eigene Nutzungsbedingungen und kann sich ändern.
- Vor produktiver Nutzung: Backup erstellen und PDF-, Import-/Export- sowie Offline-Verhalten auf beiden Geräten testen.


## Erweiterung: Recency (90 Tage)

Die Flugmaske enthält jetzt ein Feld „Starts gesamt“ sowie die vorhandenen Felder
„Landungen Tag“ und „Landungen Nacht“. Alle drei Felder starten standardmässig
mit 0. Die Statistik zeigt die Summe der Starts und Landungen aus den jeweils
letzten 90 Tagen. Die Startanzahl wird auch in den CSV-Export aufgenommen.
