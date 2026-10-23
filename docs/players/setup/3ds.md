# Nintendo 3DS

On a 3DS running **Luma3DS**, the OpenPak build of **nimbus** lets you choose which account and
network the console uses, and its patches point the console's Nintendo Network services at
OpenPak. nimbus is a fork of Pretendo Network's nimbus.

!!! warning "Alpha, not yet verified on hardware"
    The OpenPak 3DS servers are running, but the OpenPak build of nimbus has not been verified
    on a real console. The on-screen artwork still says Pretendo: in the OpenPak build, the
    **Pretendo** button is the OpenPak choice.

## What you need

- A 3DS with **Luma3DS 13.0 or newer** and **FBI** (or FBI Reloaded) to install CIA files.
- Your OpenPak account ([create one](../account.md)).

## Install

1. Download `nimbus.cia` (or `nimbus.3dsx`) and `nimbus.3gx` from the
   [latest nimbus for OpenPak release](https://github.com/openpak/nn-nimbus/releases/latest).
2. Copy the `3ds/nimbus/` folder from the release to the root of your SD card.
3. Install `nimbus.cia` with FBI.
4. Reboot while holding **SELECT**, and make sure **Enable loading external FIRMs and modules**
   and **Enable game patching** are both on.
5. Start nimbus, select the **Pretendo** (OpenPak) account, and sign in.
6. Open the Rosalina menu and set **Plugin Loader** to **Enabled**.

## What is not ready yet

The game-facing part of nimbus is a set of patches to the console's own system modules. They
are built from code on each console and are **not included in releases**, so the full patch set
is **not ready yet** for players. Without it, nimbus still runs and can carry an account, but
games will not reach OpenPak.

## Undo

Start nimbus and select the **Nintendo** account. To remove it completely, delete the
`3ds/nimbus/` folder and uninstall nimbus with FBI.

## The emulator

Azahar for OpenPak is not ready yet. See [emulators](emulators/azahar.md).
