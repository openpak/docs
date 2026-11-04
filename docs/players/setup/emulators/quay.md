# Quay (Wii U)

Quay is OpenPak's Wii U emulator. It is the renamed OpenPak fork of Cemu, and it is the only
Wii U emulator OpenPak builds. The long-term goal is to boot the console's own Wii U Menu and
applets and send only the network side to OpenPak.

## Status

**Early.** Quay builds, starts as Quay, and runs commercial Wii U games the way Cemu does
(New Super Mario Bros. U was run to in-game on 2026-10-27). The Wii U Menu and system
applets have not been booted yet. The OpenPak menu and sign-in carried over from the earlier
fork have not been verified in Quay, and no online game has been played with it.

## Downloads

- **Release:** [github.com/openpak/quay/releases](https://github.com/openpak/quay/releases)
  has a `v0.4.3` entry that contains no files yet.
- **Nightly:** the rolling [`nightly` pre-release](https://github.com/openpak/quay/releases/tag/nightly)
  carries Windows builds (a zip and an installer). It is rebuilt when the source changes and
  is untested against OpenPak: use it to follow progress, not to play online.

## Sign in to OpenPak

Quay has an OpenPak menu and sign-in, but they are not verified yet. On a real Wii U, see the
[Wii U guide](../wiiu.md).

## Known limits

- No online play has been tried.
- No Linux or macOS download is published.
- You supply the firmware and your own games.

Issues: [github.com/openpak/quay/issues](https://github.com/openpak/quay/issues). Say which
build you used (release or nightly) and what you saw.
