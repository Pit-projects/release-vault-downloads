# Lokale Speicherung, Verschlüsselung und Nextcloud

## Lokale Speicherung

Release Vault ist offline nutzbar und benötigt kein zentrales Benutzerkonto.
Personen, Verträge, Unterschriften und zugehörige Dokumente werden in einer
lokalen SQLCipher-Datenbank gespeichert. Der zufällig erzeugte
256-Bit-Datenbankschlüssel liegt im geschützten Schlüsselspeicher des jeweiligen
Betriebssystems.

Ist eine Passwort- oder PIN-Sperre eingerichtet, wird der Datenbankschlüssel
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

## Optionale Nextcloud-Nutzung

Nextcloud ist vollständig optional. Für Cloud-Backups und den Geräteabgleich
werden ausschließlich bereits lokal verschlüsselte Daten übertragen. Die
lokale Datenbank bleibt führend und die App bleibt ohne Internet nutzbar.

Nextcloud-Adresse, Benutzername und Passwort werden vom Nutzer selbst
eingetragen. Zugangsdaten werden im geschützten Gerätespeicher abgelegt und
nicht Bestandteil eines Backups. Für den verschlüsselten Geräteabgleich muss
auf allen beteiligten Geräten dasselbe Backup-Passwort verwendet werden.

Bei fehlender Internetverbindung bleiben Änderungen lokal gespeichert. Eine
ausstehende Cloud-Synchronisierung wird bei einer späteren verfügbaren
Verbindung erneut versucht.
