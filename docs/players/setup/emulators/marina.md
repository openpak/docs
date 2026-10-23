# Marina (Wii)

Marina is OpenPak's Wii emulator, built on Dolphin. The goal is to boot the console's own
System Menu and IOS from your NAND backup, and to run GameCube software through the Wii's own
path, as on hardware.

## Status

**Not ready yet.** Marina builds on Linux but has not been run against firmware, a game or
OpenPak.

What exists so far: a **Config → Wii → Connect Nintendo WFC to OpenPak** checkbox, an
**OpenPak → Sign in** menu and cloud saves for Wii titles.

## Downloads

- **Release:** [github.com/openpak/marina/releases/latest](https://github.com/openpak/marina/releases/latest),
  once a tagged release exists.
- **Nightly:** the rolling [`nightly` pre-release](https://github.com/openpak/marina/releases/tag/nightly),
  rebuilt when the source changes. It is untested: use it to follow progress, not to play.

## Sign in to OpenPak

1. Make a NAND backup with BootMii on **your own** Wii and import it with **Tools → Import
   BootMii NAND Backup**. Bring your own games.
2. Choose **OpenPak → Sign in**. The account names you and authorises cloud saves; Nintendo WFC
   itself has no accounts.
3. Tick **Config → Wii → Connect Nintendo WFC to OpenPak**.

## Known limits

- Untested end to end: no game has gone online through Marina yet.
- Linux only for now.

Issues: [github.com/openpak/marina/issues](https://github.com/openpak/marina/issues). Say which
build you used (release or nightly) and what you saw.
