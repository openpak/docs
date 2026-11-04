# Nintendo DS

DS games used Nintendo Wi-Fi Connection (WFC). OpenPak serves Wii and DS WFC games from the
same server.

!!! warning "Patcher not released yet"
    The DS server side is in beta, but the OpenPak DS Patcher has no public release yet. This
    page will get real steps once it does.

The patched game looks up OpenPak's server names through `*.openpak.org`, so the DS needs no
special DNS setting: your router's DNS resolves them, once the `*.openpak.org` wildcard record
is live.

## What it will look like

The OpenPak DS Patcher is a fork of WfcPatcher (repository: [ds-patcher](https://github.com/openpak/ds-patcher)). It patches a dump of **your own** DS game so
that its WFC names point at OpenPak. It never ships game files.

## Link the console to your account

As on the Wii: after a game has been online through OpenPak once, open your
[account page](https://openpak.org/account), choose **Link a Wii or DS** and type the friend
code the game shows.

## The emulator

melonDS for OpenPak has a WFC redirect built in, but no public build yet. See
[emulators](emulators/melonds.md).
