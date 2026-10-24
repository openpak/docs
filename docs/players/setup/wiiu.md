# Wii U

On a Wii U running the **Aroma** environment, the **OpenPak Wii U Patcher** (OpenPak's build of Pretendo's Inkay) redirects the
console's Nintendo Network services to OpenPak. Inkay is a fork of Pretendo Network's Inkay.

!!! warning "Alpha, not yet run on hardware"
    The OpenPak Wii U servers (accounts, friends, NAT check, SpotPass, Miiverse, eShop) are
    running, but the OpenPak build of Inkay has not been run on a real console yet. Expect
    problems and please report them.

## What you need

- A Wii U running the **release version of Aroma**, set up to autoboot (coldboot). Other
  setups, especially without coldboot, may cause problems with SpotPass.
- Your OpenPak account ([create one](../account.md)).

## Install

1. Download `Inkay-openpak.wms` from the
   [latest OpenPak Wii U Patcher release](https://github.com/openpak/wiiu-patcher/releases/latest).
2. Copy it to `sd:/wiiu/environments/aroma/modules/` on your SD card.
3. Put the card back and start the console.

The module resolves OpenPak's servers itself, so you do not change any DNS setting.

## Undo

Delete `Inkay-openpak.wms` from the modules folder and restart. The patches are applied in
memory only and never modify the console.

!!! note "About certificate checks"
    Like upstream Inkay, the module trusts the OpenPak certificate authority and relaxes some
    certificate checks while it is active. That lowers the console's security while the patcher is
    loaded. The Internet Browser keeps checking certificates normally.

## Signing in

With the patcher loaded, the console's own Nintendo Network ID screens talk to OpenPak. Every
OpenPak account automatically has a Wii U identity, and friends are shared with your other
OpenPak consoles. The exact sign-in steps on the console have not been verified yet: **not
ready yet**.

## Without a modified console

A path for an unmodified Wii U, using a DNS setting and OpenPak's certificate, exists on the
server side but is **not ready yet** for players: OpenPak does not publish a DNS address for
consoles yet.

## The emulator

The OpenPak Wii U emulator, Quay, is not ready yet. See [emulators](emulators/quay.md).
