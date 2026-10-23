# Nintendo DS

DS games used Nintendo Wi-Fi Connection (WFC). OpenPak serves Wii and DS WFC games from the
same server.

!!! warning "Not ready yet"
    The DS server side is in beta, but there is **no player-ready DS path yet**:

    - The OpenPak DS patcher has no public release yet.
    - OpenPak does not publish a DNS address for consoles yet.

    This page will get real steps once both exist.

## What it will look like

The OpenPak DS patcher is a fork of WfcPatcher. It patches a dump of **your own** DS game so
that its WFC names point at OpenPak. It never ships game files.

## Link the console to your account

As on the Wii: after a game has been online through OpenPak once, open your
[account page](https://openpak.org/account), choose **Link a Wii or DS** and type the friend
code the game shows.

## The emulator

melonDS for OpenPak has a WFC redirect built in, but no public build yet. See
[emulators](emulators.md#melonds-for-openpak-ds).
