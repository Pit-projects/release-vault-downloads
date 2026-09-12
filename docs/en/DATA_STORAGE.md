# Local storage, encryption, and Nextcloud

[Deutsch](../DATENSPEICHERUNG.md) | **English**

## Local storage

Release Vault works offline and does not require a central user account.
Contact details, contracts, signatures, and associated documents are stored in
a local SQLCipher database. The randomly generated 256-bit database key is kept
in the protected credential storage provided by the operating system.

When password or PIN protection is enabled, the database key receives
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

## Optional Nextcloud use

Nextcloud is entirely optional. Only data that has already been encrypted
locally is transferred for cloud backups and device synchronization. The local
database remains authoritative, and the app continues to work without an
internet connection.

Users provide their own Nextcloud address, username, and password. Credentials
are stored in protected device storage and are not included in backups. The same
backup password must be configured on all participating devices for encrypted
device synchronization.

If no internet connection is available, changes remain stored locally. Any
pending cloud synchronization is retried when a connection becomes available
again.
