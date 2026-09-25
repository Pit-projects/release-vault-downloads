# Local storage, encryption, and cloud providers

[Deutsch](../DATENSPEICHERUNG.md) | **English**

## Local storage

Release Vault works offline and does not require a central user account.
Contacts, contracts, signatures, and associated documents are encrypted
locally: in a SQLCipher database on Android and in an AES-256-GCM-encrypted
data file on Windows. Keys are kept in the protected credential storage
provided by the respective operating system.

When password or PIN protection is enabled, the local data key receives
additional AES-256-GCM protection. The required wrapping key is derived from
the user's input with Argon2id and a random salt. Passwords and PINs are not
stored as plain text.

## Encrypted backups

Backups contain a versioned data representation and are authenticated and
encrypted with AES-256-GCM before they are saved. The backup key is derived
from a separate backup password using PBKDF2-HMAC-SHA-256 with 310,000
iterations.

Before restoring data, the app verifies the backup format, authenticity, and
content. Local data is replaced only after the user confirms the restoration.

## Optional cloud backup and synchronization

Cloud backups and device synchronization can use **one** connected provider at
a time: Nextcloud, Google Drive, or Dropbox. The current connection must be
disconnected before switching providers. Backup and synchronization data is
encrypted locally before transfer. The app continues to work offline; pending
changes can be synchronized when a connection becomes available. Every
participating device must use the same backup password.

- **Nextcloud:** Users enter their own server address, username, and password.
  When synchronization is enabled, completed contracts are also stored as
  **unencrypted, directly readable PDF copies** in the user's Nextcloud
  `Releases PDF` folder.
- **Google Drive:** Sign-in is handled by Google. New connections store
  encrypted app data in a visible `Release Vault` folder in My Drive. To
  migrate older backups, the app can also access its previous hidden app-data
  area. Existing data is copied, not deleted.
- **Dropbox:** Sign-in takes place in the browser. The app uses only its own
  folder under `Apps/Release Vault`.

Cloud credentials and the backup password retained for automatic backups are
kept in protected device storage and are not included in backups. Manually
exported backup files can also be saved to a storage location offered by the
device's file picker; this does not provide ongoing device synchronization.
