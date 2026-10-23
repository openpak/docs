# Before you start

Read this page before you connect anything. It is short, and it is the part that can cost you
a console.

## The ban risk

!!! danger "A modified console can be banned by its vendor"
    Connecting to OpenPak means running custom firmware or a patch on your console. If that
    console ever talks to the vendor's own servers again (Nintendo, Microsoft or Sony), the
    vendor can detect the modification and ban the console from its online services, and
    sometimes the account on it. OpenPak cannot prevent or undo a ban. You take this risk
    yourself.

How to keep the risk low:

- **On the Switch, use emuMMC.** Run OpenPak from an emuMMC (an emulated copy of the system
  on the SD card), not from the console's internal system memory (sysMMC). Keep sysMMC for
  the vendor, or keep it offline.
- **Never mix networks on one system.** A system that is set to OpenPak should not also reach
  the vendor. On the Switch, OpenPak Setup has two choices, OpenPak and Nintendo; always switch
  back to **Nintendo** in OpenPak Setup, and reboot, before that system talks to Nintendo again.
- **Already banned consoles** can use OpenPak too. A ban by the vendor does not stop OpenPak.
- **Emulators** carry no console ban risk, because no real console is involved.

## Use your own console and your own games

OpenPak does not provide games, firmware, keys or any other copyrighted files, and none of
its downloads contain them. It never will, and these docs do not explain how to get them.

- You must own the consoles you connect and own the games you play.
- An emulator needs files from **your own** console (for example its keys and firmware) and
  dumps of **your own** games. Each emulator's setup section says what it needs.
- Never attach game files, firmware, keys or console dumps to a bug report or help request.

## Back up first

Before you install anything on a console, back up what matters:

- **Your save files.** OpenPak cloud saves are an alpha service and can be reset.
- **Your SD card**, if the console uses one. The setup tools write files on it.
- **Your console's system memory (NAND)**, using the usual tools for your console, before you
  change its firmware or boot setup for the first time.

## What OpenPak changes, and how to undo it

- **Switch:** OpenPak Setup writes host rules, a certificate and a boot package on the SD
  card. Choosing **Nintendo** in the same tool removes them and puts back what was there.
- **Wii U:** the Inkay module is loaded from the SD card. Remove the file and the console goes
  back.
- **3DS:** nimbus lets you choose which account and network the console uses.
- **Wii and DS:** the patchers redirect a game when it is launched through them. Launch the
  game normally and it goes to the original servers (which no longer exist for most games).

## The rules of the network

By creating an account you agree to the [Terms](https://openpak.org/terms) and the
[Privacy policy](https://openpak.org/privacy). In short: no piracy, no cheating that affects
other players, no attacks on the network, and no harassment.
