# Harbor (Switch)

Harbor is OpenPak's Switch emulator, built on Eden. It boots the firmware's own HOME menu,
setup and applets, and plays games online through OpenPak with your OpenPak account, friends,
invitations, news and cloud saves.

## Status

**Alpha.** Online play has been verified against a real Switch in a few games:

- **Full Metal Furies**: two-player co-op between Harbor and a Switch (create, join, NAT
  punch-through and leave).
- **PlateUp!**: a Switch hosts and Harbor joins.
- **Go-Go Town!**: a Switch hosts, Harbor joins, both play together.
- **Minecraft: Nintendo Switch Edition**: worked in both directions between a Switch and
  Harbor on Android.

Anything not listed is not verified. A game that starts is not proof that it works online.

## What you need

- A Linux x86_64 PC, or an Android phone (ARM64, Android 10 or newer). Windows and macOS have
  no builds.
- From **your own** Switch: `prod.keys`, and the system firmware as a zip or a folder of NCA
  files. Firmware 23.0.1 is the tested version on desktop; 22.5.0 on Android.
- Your own game dumps, with their updates (OpenPak requires the latest version of each game)
  and any DLC.

## Downloads

- **Release:** [github.com/openpak/harbor/releases/latest](https://github.com/openpak/harbor/releases/latest).
  Take the Linux archive, or on Android the **legacy** APK (the one that has been run on a
  phone).
- **Nightly:** the rolling [`nightly` pre-release](https://github.com/openpak/harbor/releases/tag/nightly),
  rebuilt when the source changes and untested. The nightly installs as a separate app,
  **Harbor Nightly**, so it sits next to the release instead of replacing it, with its own
  settings and data.

Builds are test builds signed with a test key.

## Install and sign in to OpenPak

1. Install a build from the downloads above.
2. Start Harbor. The setup wizard walks through a device check, your keys, firmware, games,
   optional DLC and updates, a graphics driver choice on Android, an OpenPak account page and
   an opt-in crash-report question.
3. On the account page choose **Sign in** or **Create account**. The emulated console's first
   user is linked to that account. **Later** keeps Harbor offline.

Two-factor accounts cannot finish sign-in on the wizard page yet: choose **Later**, then link
the user from the emulated console's settings, as on a [real Switch](../../account.md#linking-a-switch).

## Known limits

- On Android, GPU drivers matter. If a game crashes, try another driver before reporting a
  bug.
- News received during a session shows only after the next boot.
- The friend page shows "Offline" without a duration.

Issues: [github.com/openpak/harbor/issues](https://github.com/openpak/harbor/issues). Include
the Harbor version (and whether it is the nightly), platform, GPU driver and what you saw.
