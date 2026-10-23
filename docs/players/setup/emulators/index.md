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
| [Harbor](harbor.md) | Switch | Eden | Alpha. Test builds published. |
| [Quay](quay.md) | Wii U | Cemu | Early. Not built yet. |
| [Marina](marina.md) | Wii (and GameCube through the Wii) | Dolphin | Early. Builds on Linux. |
| [Azahar for OpenPak](azahar.md) | 3DS | Azahar | Transitional. No tested build. |
| [melonDS for OpenPak](melonds.md) | DS | melonDS | Transitional. No tested build. |
| [Wharf](wharf.md) | Xbox 360 | Xenia Edge | Experimental. No tested build. |
| [Berth](berth.md) | Xbox | xemu | Experimental. No tested build. |
| [Pier](pier.md) | PlayStation 3 | RPCS3 | Experimental. No tested build. |

Each fork keeps its upstream licence, and none of them is an official release of the project
it is based on. Report problems to the OpenPak fork, not upstream.

## Downloads: releases and nightly

Every emulator repository has two kinds of build on its GitHub releases page:

- **Releases** (`releases/latest`): tagged builds. Where one exists, start here.
- **Nightly**: a rolling pre-release tagged `nightly`, rebuilt automatically when the source
  changes. It is the newest code and has had no testing at all. Expect it to break.

A nightly build is not a sign that an emulator is ready: the state on each page is what has
actually been tested. Builds are test builds, signed with a test key where signing applies.

## Harbor (Switch)

Alpha: boots the Switch's own HOME menu and plays a few verified games online.
See [Harbor](harbor.md).

## Quay (Wii U)

Not ready yet. See [Quay](quay.md).

## Marina (Wii)

Not ready yet. See [Marina](marina.md).

## Azahar for OpenPak (3DS)

Not ready yet. See [Azahar for OpenPak](azahar.md).

## melonDS for OpenPak (DS)

Not ready yet. See [melonDS for OpenPak](melonds.md).

## Wharf (Xbox 360)

Not ready yet. See [Wharf](wharf.md).

## Berth (Xbox)

Not ready yet. See [Berth](berth.md).

## Pier (PlayStation 3)

Not ready yet. See [Pier](pier.md).
