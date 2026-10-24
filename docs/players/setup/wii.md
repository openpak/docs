# Wii

Wii games used Nintendo Wi-Fi Connection (WFC), which closed long ago. OpenPak runs a WFC
replacement server based on WiiLink's, and the **OpenPak Wii Patcher** (a build of WiiLink's WFC patcher) sends
each game to it.

!!! warning "Alpha, not yet run on hardware"
    The OpenPak Wii Patcher has not been run on a real console yet.

## What you need

- A Wii that can run homebrew.
- Your own game discs, or your own backups if you use a USB loader.
- Your OpenPak account ([create one](../account.md)), to link the console to it.

## The pieces

The [latest OpenPak Wii Patcher release](https://github.com/openpak/wii-patcher/releases/latest)
has two ways in:

- **The launcher**, `openpak-wfc-launcher.dol`: start it from the Homebrew Channel and it boots
  your disc with OpenPak's patch applied.
- **Gecko codes**, `openpak-wfc-gecko-codes.zip`: one code per game, for USB loaders and
  Riivolution.

## DNS: not ready yet

The patched game still looks up OpenPak's server names through the console's DNS setting, and
OpenPak does not publish a DNS address for consoles yet. Until it does, the Wii path is **not
ready yet** for players.

## Link the console to your account

The Wii has no login of its own. After a game has been online through OpenPak once, open your
[account page](https://openpak.org/account), choose **Link a Wii or DS** and type the friend
code the game shows.

## Undo

Launch the game normally, without the launcher or the codes.

## The emulator

Marina, the OpenPak Wii emulator, is not ready yet. See [emulators](emulators/marina.md).
