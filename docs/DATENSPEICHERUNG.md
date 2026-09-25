# Lokale Speicherung, Verschlüsselung und Cloud-Anbieter

## Lokale Speicherung

Release Vault ist offline nutzbar und benötigt kein zentrales Benutzerkonto.
Personen, Verträge, Unterschriften und zugehörige Dokumente werden lokal
verschlüsselt gespeichert: auf Android in einer SQLCipher-Datenbank, unter
Windows in einer AES-256-GCM-verschlüsselten Datendatei. Die Schlüssel werden
im geschützten Schlüsselspeicher des jeweiligen Betriebssystems verwahrt.

Ist eine Passwort- oder PIN-Sperre eingerichtet, wird der lokale Datenschlüssel
zusätzlich mit AES-256-GCM geschützt. Der dafür benötigte Schlüssel wird mit
Argon2id und einem zufälligen Salt aus der Eingabe abgeleitet. Passwort und PIN
werden nicht als Klartext gespeichert.

## Verschlüsselte Backups

Backups enthalten ein versioniertes Datenabbild und werden vor dem Speichern mit
AES-256-GCM authentifiziert verschlüsselt. Der Backup-Schlüssel wird mit
PBKDF2-HMAC-SHA-256 und 310.000 Iterationen aus einem separaten Backup-Passwort
abgeleitet.

Vor einer Wiederherstellung prüft die App Format, Authentizität und Inhalt des
Backups. Erst nach Bestätigung wird der lokale Datenbestand ersetzt.

## Optionale Cloud-Sicherung und Synchronisierung

Für Cloud-Backups und den Geräteabgleich kann jeweils **ein** Anbieter verbunden
werden: Nextcloud, Google Drive oder Dropbox. Ein Anbieterwechsel setzt voraus,
dass die bisherige Verbindung zuerst getrennt wird. Backups und
Synchronisationsdaten werden vor der Übertragung lokal verschlüsselt. Die App
bleibt auch ohne Internet nutzbar; ausstehende Änderungen können bei einer
späteren Verbindung abgeglichen werden. Auf allen beteiligten Geräten muss
dasselbe Backup-Passwort verwendet werden.

- **Nextcloud:** Die Nutzerin oder der Nutzer trägt Serveradresse,
  Benutzernamen und Passwort selbst ein. Bei aktivierter Synchronisierung
  werden abgeschlossene Verträge zusätzlich als **unverschlüsselte, direkt
  lesbare PDF-Kopien** im eigenen Nextcloud-Ordner `Releases PDF` abgelegt.
- **Google Drive:** Die Anmeldung erfolgt über Google. Neue Verbindungen
  speichern verschlüsselte Appdaten in einem sichtbaren Ordner `Release Vault`
  unter „Meine Ablage“. Für die Übernahme älterer Sicherungen kann die App
  außerdem auf ihren bisherigen verborgenen Appdatenbereich zugreifen; dabei
  werden vorhandene Daten kopiert, nicht gelöscht.
- **Dropbox:** Die Anmeldung erfolgt im Browser. Die App verwendet nur ihren
  eigenen Ordner unter `Apps/Release Vault`.

Cloud-Anmeldedaten und das für automatische Sicherungen hinterlegte
Backup-Passwort werden im geschützten Gerätespeicher abgelegt und nicht in
Backups übernommen. Manuell exportierte Backup-Dateien können auch über den
Dateidialog in einen vom Gerät angebotenen Speicherort gesichert werden; das
ist keine laufende Gerätesynchronisierung.
