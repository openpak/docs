# Troubleshooting

Start with the basics, then look up your error code below.

## First checks

1. **Is OpenPak up?** Check [status.openpak.org](https://status.openpak.org).
2. **Did you reboot?** Consoles read their network setup only at boot. After installing,
   re-applying or switching networks, reboot.
3. **Is the game on its latest version?** OpenPak refuses outdated games (see 2124-3001).
4. **Does the game have a server?** Check its state on
   [openpak.org/titles](https://openpak.org/titles). *Requestable* means there is no server
   yet.
5. **Is your setup tool current?** On the Switch, start OpenPak Switch Patcher with a connection and
   accept the update it offers, then select **OpenPak** again and reboot.
6. **One tool per console.** Do not run two network-switching tools on the same system. They
   overwrite each other's settings.

## Switch error codes

| Code | What it means | What to do |
| --- | --- | --- |
| **2124-3001** | "A software update is required." OpenPak only accepts the latest version of each game. | Update the game to its latest version. OpenPak never forces a download; it only refuses old versions. |
| **2123-0011** | The console could not register its device certificate, so nothing can sign in. This happens when the emuMMC is set to hide the console's identity (`blank_prodinfo_emummc=1` in `/exosphere.ini`), which tools that prepare a console for Nintendo often set. | Open OpenPak Switch Patcher and select **OpenPak** again: it turns that setting off while OpenPak is active, and back on when you select Nintendo. Reboot afterwards. |
| **2618-0006** | A game's NAT check failed, usually at once. The NAT-check names were answered by the console's own host rules instead of a real resolver, often because of a broad wildcard rule (such as `*.nintendo.net`) added by hand or by another tool. | Remove your own wildcard rules for Nintendo names from `/atmosphere/hosts/`, re-apply OpenPak with the latest OpenPak Switch Patcher and reboot. If it persists, check the status page: the NAT-check servers may be down. |
| **2124-5110** | The OpenPak account is suspended or has been deleted. | If you think this is a mistake, write to [contact@openpak.org](mailto:contact@openpak.org). |
| **2124-0041** | The console could not get a sign-in token for this game. | Report the game, with its title and version (see below). |

## Wii U error codes

| Code | What it means | What to do |
| --- | --- | --- |
| **0108** "Account has been banned" | The OpenPak account is suspended or has been deleted. | Write to [contact@openpak.org](mailto:contact@openpak.org) if you think this is a mistake. |

## Other problems

**The Switch stops at "Failed to apply 'openpak_ksp'" during boot.**
The console's firmware was updated while OpenPak was selected. Press POWER to continue, open
OpenPak Switch Patcher and select **Nintendo**. Select OpenPak again once the new firmware is supported.

**OpenPak Switch Patcher refuses to install.**
The console's firmware is not a supported version (22.5.0, 23.0.0 or 23.0.1). The message names
the version the console runs.

**"OpenPak updated the Switch's network redirects."**
OpenPak added or changed services. Select OpenPak again and reboot.

**eShop titles from OpenPak's eShop do not launch.**
A Loader module of your own in `/atmosphere/kips` (an overclock module, for example) is loaded
ahead of OpenPak's. OpenPak Switch Patcher names it in a warning. Remove it to use OpenPak's eShop.

**Harbor crashes in a game on Android.**
Try another GPU driver first. Several crashes have been traced to particular driver versions.

**A game starts but online does not work.**
A game that launches is not proof that it works online. Check its notes on the titles page,
then report what you saw.

## Getting help

- Signed in: open a request at [openpak.org/help](https://openpak.org/help). Say what
  happened, on which console or emulator, and what you already tried. You can attach one file
  (up to 10 MB): a screenshot, a log or a crash report. Answers appear there and in the app.
- A game that does not work: open an issue in the repository that serves it. See
  [reporting bugs](../contributors/reporting.md) for what to include.

Never attach game files, firmware, keys, `prod.keys`, PRODINFO or console dumps.
