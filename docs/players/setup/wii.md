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
no special DNS setting: the console's normal DNS (your router's) resolves them. The Wii path
works once the `*.openpak.org` wildcard record is live.

## Link the console to your account

The Wii has no login of its own, so linking is done with a code.

**Mario Kart Wii** shows the code itself. Connect to Wi-Fi Connection while the console is
not linked yet: the message of the day on the Wi-Fi menu ends with
`Link this Wii at openpak.org/link` and a code like `QXZP-7K2M`. Open
[openpak.org/link](https://openpak.org/link) (or **Link a Wii or DS** in the OpenPak app),
sign in, enter the code and approve. Nothing else is needed on the console. The code works
once and expires after 30 minutes; connect again to get a fresh one. A console that is already
linked is not shown a code.

**Other games** do not display a message, so use the friend code instead: after the game has
been online through OpenPak once, open your [account page](https://openpak.org/account),
choose **Link a Wii or DS** and type the friend code the game shows.

## Undo

Launch the game normally, without the launcher or the codes.

## The emulator

Marina, the OpenPak Wii emulator, is not ready yet. See [emulators](emulators/marina.md).
