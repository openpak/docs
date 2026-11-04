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

There is no public download yet: no tagged release and no nightly build exist for Marina.
It can be built from source from [github.com/openpak/marina](https://github.com/openpak/marina).

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
