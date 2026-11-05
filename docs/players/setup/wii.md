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

## DNS

The patched game looks up OpenPak's server names through `*.openpak.org`, so the Wii needs
no special DNS setting: the console's normal DNS (your router's) resolves them. The
`*.openpak.org` record is live.

## Link the console to your account

The Wii has no login of its own, so linking is done with a code, and a Wii plays online
only once it is linked.

1. Connect to Nintendo Wi-Fi Connection in any game. While the console is not linked, the
   connection is refused and a code is shown:
    - **Mario Kart Wii** shows a message: `This Wii is not linked to an OpenPak account yet`,
      a code like `QXZP-7K2M` and a 5-digit number (error code 22100).
    - **Every other game** shows an error code between **24000 and 29999**. That number is
      your link code.
2. Open [openpak.org/link](https://openpak.org/link) (or **Link a Wii or DS** in the OpenPak
   app), sign in and enter the code or the number. With the 5-digit number, use a phone or
   computer on the **same Wi-Fi as the Wii**, or also type the name you play as in that game
   (your Mii's name).
3. Check that the page names your Wii, the game and your name, and approve.
4. Connect again in the game: you are online.

A code works once and expires after 15 minutes; connecting again shows a fresh one. One account
can link several consoles; unlink one from your [account page](https://openpak.org/account),
optionally erasing its online game data. Linking by friend code is no longer possible.

## Undo

Launch the game normally, without the launcher or the codes.

## The emulator

Marina, the OpenPak Wii emulator, is not ready yet. See [emulators](emulators/marina.md).
