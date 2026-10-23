# Emulators

OpenPak keeps its own forks of emulators. They are OpenPak clients, not emulators with an
online mode bolted on: each emulator profile is signed in to its own OpenPak account, and the
firmware-first ones boot the console's real system software and reach OpenPak the way a real
console does.

For every emulator, **you supply everything copyrighted yourself, from your own console**:
keys, firmware, system files and your own games. OpenPak provides none of it, and no OpenPak
emulator ever downloads any.

| Emulator | Console | Based on | State |
| --- | --- | --- | --- |
| [Harbor](#harbor-switch) | Switch | Eden | Alpha. Test builds published. |
| [Quay](#quay-wii-u) | Wii U | Cemu | Early. Not built yet. |
| [Marina](#marina-wii) | Wii (and GameCube through the Wii) | Dolphin | Early. Builds on Linux. |
| [Azahar for OpenPak](#azahar-for-openpak-3ds) | 3DS | Azahar | Transitional. No builds. |
| [melonDS for OpenPak](#melonds-for-openpak-ds) | DS | melonDS | Transitional. No builds. |
| [Wharf](#wharf-xbox-360) | Xbox 360 | Xenia Edge | Experimental. No builds. |
| [Berth](#berth-xbox) | Xbox | xemu | Experimental. No builds. |
| [Pier](#pier-playstation-3) | PlayStation 3 | RPCS3 | Experimental. No builds. |

Each fork keeps its upstream licence, and none of them is an official release of the project
it is based on. Report problems to the OpenPak fork, not upstream.

---

## Harbor (Switch)

Harbor is OpenPak's Switch emulator, built on Eden. It boots the firmware's own HOME menu,
setup and applets, and plays games online through OpenPak with your OpenPak account, friends,
invitations, news and cloud saves.

**State: alpha.** Online play has been verified against a real Switch in a few games:

- **Full Metal Furies**: two-player co-op between Harbor and a Switch (create, join, NAT
  punch-through and leave).
- **PlateUp!**: a Switch hosts and Harbor joins.
- **Go-Go Town!**: a Switch hosts, Harbor joins, both play together.
- **Minecraft: Nintendo Switch Edition**: worked in both directions between a Switch and
  Harbor on Android.

Anything not listed is not verified. A game that starts is not proof that it works online.

### What you need

- A Linux x86_64 PC, or an Android phone (ARM64, Android 10 or newer). Windows and macOS have
  no builds.
- From **your own** Switch: `prod.keys`, and the system firmware as a zip or a folder of NCA
  files. Firmware 23.0.1 is the tested version on desktop; 22.5.0 on Android.
- Your own game dumps, with their updates (OpenPak requires the latest version of each game)
  and any DLC.

### Install and connect

1. Download a build from the [Harbor releases](https://github.com/openpak/harbor/releases):
   the Linux archive, or on Android the **legacy** APK (the one that has been run on a phone).
   Builds are test builds signed with a test key.
2. Start Harbor. The setup wizard walks through a device check, your keys, firmware, games,
   optional DLC and updates, a graphics driver choice on Android, an OpenPak account page and
   an opt-in crash-report question.
3. On the account page choose **Sign in** or **Create account**. The emulated console's first
   user is linked to that account. **Later** keeps Harbor offline.

Two-factor accounts cannot finish sign-in on the wizard page yet: choose **Later**, then link
the user from the emulated console's settings, as on a [real Switch](../account.md#linking-a-switch).

### Known limits

- On Android, GPU drivers matter. If a game crashes, try another driver before reporting a
  bug.
- News received during a session shows only after the next boot.
- The friend page shows "Offline" without a duration.

Issues: [github.com/openpak/harbor/issues](https://github.com/openpak/harbor/issues). Include
the Harbor version, platform, GPU driver and what you saw.

---

## Quay (Wii U)

Quay will be OpenPak's Wii U emulator, booting the console's own Wii U Menu and applets.
**Not ready yet:** the code is still a copy of the retired OpenPak Cemu fork, has not been
built or run as Quay, and has no public build. Releases will appear at
[github.com/openpak/quay/releases](https://github.com/openpak/quay/releases).

---

## Marina (Wii)

Marina is OpenPak's Wii emulator, built on Dolphin. The goal is to boot the console's own
System Menu and IOS from your NAND backup, and to run GameCube software through the Wii's own
path, as on hardware.

**Not ready yet:** Marina builds on Linux but has not been run against firmware, a game or
OpenPak, and there is no public build.

What exists so far: a **Config → Wii → Connect Nintendo WFC to OpenPak** checkbox, an
**OpenPak → Sign in** menu (the account names you and authorises cloud saves; WFC itself has no
accounts), and cloud saves for Wii titles. You will need your own NAND backup made with BootMii
on your own console, imported with **Tools → Import BootMii NAND Backup**, and your own games.

---

## Azahar for OpenPak (3DS)

A fork of Azahar that points the emulated console's HTTP traffic at OpenPak and adds the
shared OpenPak sign-in, menu and cloud saves.

**Not ready yet:** none of it has been run against a game, and no build is published while
this fork is transitional (a successor is planned). Azahar does not emulate NEX, so friends and
online play are not available in it; it covers the account and content side only.

When builds exist: sign in from the **OpenPak** menu (left of Help), then turn on the
connection under **Configure → General → OpenPak**. It cannot be changed while a game runs.

---

## melonDS for OpenPak (DS)

A fork of melonDS with a Nintendo WFC redirect to OpenPak, cloud saves for `.sav` files and the
shared OpenPak menu.

**Not ready yet:** not run against a game, and no build is published while this fork is
transitional (a successor is planned).

When builds exist: sign in from the **OpenPak** menu (left of Help), then turn on **Connect
Nintendo WFC to OpenPak** in the Wi-Fi settings. You supply your own ROMs, and for firmware
boot, the firmware and BIOS from a DS you own.

---

## Wharf (Xbox 360)

Wharf is OpenPak's Xbox 360 emulator, built on Xenia Edge. It boots the console's own
dashboard and connects it to OpenPak's Xbox 360 services. The dashboard's Xbox Live connection
test passes against OpenPak, but sign-in does not complete yet.

**Not ready yet:** no public build, and no sign-in. Releases will appear at
[github.com/openpak/wharf/releases](https://github.com/openpak/wharf/releases).

---

## Berth (Xbox)

Berth is OpenPak's original Xbox emulator, built on xemu. It boots a dashboard you supply, but
no OpenPak service has been reached from it yet.

**Not ready yet:** no public build, and no way to sign in to OpenPak. Releases will appear at
[github.com/openpak/berth/releases](https://github.com/openpak/berth/releases).

---

## Pier (PlayStation 3)

Pier is OpenPak's PS3 emulator, built on RPCS3. It boots the console's own XMB, and the XMB's
own sign-in form signs in to OpenPak with an OpenPak email and password. Friends' online status
comes through.

**Not ready yet:** online game sessions do not work yet, part of the setup is still a manual
step, and there is no public build. Releases will appear at
[github.com/openpak/pier/releases](https://github.com/openpak/pier/releases).
