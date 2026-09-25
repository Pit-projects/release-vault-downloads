# Datenschutzerklärung

Release Vault verarbeitet Personen-, Vertrags-, Standort- und
Unterschriftsdaten standardmäßig lokal und verschlüsselt auf dem Gerät.

Cloud-Backups und der Geräteabgleich über **Nextcloud, Google Drive oder
Dropbox** sind optional. Es kann nur ein Anbieter gleichzeitig verbunden
werden. Backups und Synchronisationsdaten werden vor der Übertragung lokal
verschlüsselt. Bei Google Drive wird ein sichtbarer Ordner `Release Vault`
genutzt; zur Übernahme älterer Daten kann zusätzlich der bisherige verborgene
Appdatenbereich gelesen werden. Bei Dropbox wird nur der eigene App-Ordner
verwendet. Bei aktivierter Nextcloud-Synchronisierung werden abgeschlossene
Verträge zusätzlich als **unverschlüsselte PDF-Kopien** im Nextcloud-Ordner
`Releases PDF` gespeichert. Die App ist auch ohne Cloud-Verbindung und ohne
zentrales Benutzerkonto nutzbar.

Standortdaten werden nur nach ausdrücklicher Auswahl erfasst. Für die
Tagesprognose werden die gewählten Standortkoordinaten an Open-Meteo
übermittelt. Wird eine Adresse ausdrücklich in Google Maps geöffnet, wird sie
erst dann an Google Maps übergeben. Bei der optionalen Remote-Unterzeichnung
werden die dafür erforderlichen Vertragsdaten an den Unterzeichnungsdienst
übermittelt. Personenbezogene Daten können in den dafür vorgesehenen
Datenschutzfunktionen exportiert oder gelöscht werden.

Weitere technische Einzelheiten enthält die Seite
[Lokale Speicherung, Verschlüsselung und Cloud-Anbieter](DATENSPEICHERUNG.md).
