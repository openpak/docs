# Cloud saves

OpenPak keeps backups of your game saves under your account, whichever machine made them.

!!! warning "Alpha"
    Cloud saves are partial during the alpha and may be reset. Keep your own copies of saves
    you care about.

## How saves get there

- **Switch (firmware 23.0.0 and 23.0.1):** use the console's own **Save Data Cloud** screen.
  OpenPak Setup lets the console accept OpenPak's save keys; reboot through the hekate entry
  for the system OpenPak runs on after selecting OpenPak.
- **Harbor:** the same Save Data Cloud screen, in the emulated console.
- **Other OpenPak emulators** sync saves automatically around a game session, with a conflict
  prompt when both sides changed. Those emulators are not ready yet; see
  [emulators](setup/emulators.md).

Restoring a backup made in Harbor onto a physical Switch has not been tested yet.

## Managing your saves

On [openpak.org/account/saves](https://openpak.org/account/saves) or in the app you can:

- see how much of your allowance is used;
- open a game's backups, each with its date, size and the console that made it;
- **Make current** an older version, **Download** a version, or **Delete** one or all of them.
  Deleting also removes the backup from your console's list, and cannot be undone.

## Storage allowance

OpenPak keeps a small allowance per account, and the newest two versions of each save (plus
any you pin). When the allowance is full, uploads are refused until you connect your own
storage.

## Use your own storage

Under **Your own storage** you can send saves to storage you own. OpenPak then keeps only the
index:

- **Google Drive** or **OneDrive**: sign in and OpenPak keeps your saves in a folder there.
- **S3-compatible bucket** (Amazon S3, MinIO, and other providers): endpoint, region, bucket,
  optional folder, access key and secret key.
- **WebDAV** (Nextcloud, ownCloud, a NAS): the folder URL, a username and a password or app
  password.

The connection is tested when you save it, and the secret is never shown again. **Move my saves
here** moves existing backups to the new storage. Disconnecting keeps the list, but versions
stored there cannot be read until you connect it again.
