# Nintendo DS

DS games used Nintendo Wi-Fi Connection (WFC). OpenPak serves Wii and DS WFC games from the
same server.

!!! warning "Patcher not released yet"
    The DS server side is in beta, but the OpenPak DS Patcher has no public release yet. This
    page will get real steps once it does.

The patched game looks up OpenPak's server names through `*.openpak.org`, so the DS needs no
special DNS setting: your router's DNS resolves them (the `*.openpak.org` record is live).

## What it will look like

The OpenPak DS Patcher is a fork of WfcPatcher (repository: [ds-patcher](https://github.com/openpak/ds-patcher)). It patches a dump of **your own** DS game so
that its WFC names point at OpenPak. It never ships game files.

## Link the console to your account

A DS plays online only once it is linked to your account.

1. Connect to Nintendo Wi-Fi Connection in the game. While the DS is not linked, the
   connection is refused with an error code between **24000 and 29999**. That number is your
   link code.
2. Open [openpak.org/link](https://openpak.org/link) (or **Link a Wii or DS** in the OpenPak
   app), sign in and enter the number. Use a phone or computer on the **same Wi-Fi as the DS**,
   or also type the name you play as in that game (the nickname the game shows, often your DS
   user name).
3. Check that the page names your DS and the game, and approve.
4. Connect again in the game: you are online.

The number works once and expires after 15 minutes; connecting again shows a fresh one.
Unlink a DS from your [account page](https://openpak.org/account). Linking by friend code is no
longer possible.

## The emulator

melonDS for OpenPak has a WFC redirect built in, but no public build yet. See
[emulators](emulators/melonds.md).
