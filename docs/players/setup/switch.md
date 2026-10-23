# Nintendo Switch

On a Switch running Atmosphère, **OpenPak Setup** (`openpak.nro`) switches the console between
Nintendo's servers and OpenPak's, and back. It is the only thing you install.

!!! danger "Ban risk"
    Run OpenPak from an **emuMMC**, not from sysMMC, and never let a system that is set to
    OpenPak talk to Nintendo. See [before you start](../before-you-start.md).

## What you need

- A Switch that can run custom firmware, with **hekate** as the bootloader and
  **Atmosphère 1.12.0** (the official release package) booted from hekate with a standard
  `pkg3` or `fss0` entry in `bootloader/hekate_ipl.ini`.
- System firmware **22.5.0, 23.0.0 or 23.0.1**. OpenPak Setup refuses to install on any other
  version and tells you which version the console runs.
- An emuMMC (strongly recommended).
- Your OpenPak account ([create one](../account.md)).
- Your own games, updated to their **latest version**. OpenPak refuses outdated game versions
  (error 2124-3001, see [troubleshooting](../troubleshooting.md)).

Setting up custom firmware itself is outside these docs. Follow the usual community guides for
your console model.

## Install

1. Download `openpak.nro` from the
   [latest OpenPak Setup release](https://github.com/openpak/openpak-nro/releases/latest).
2. Copy it into the `/switch/` folder on your SD card.
3. Boot your emuMMC with Atmosphère and open the Homebrew Menu (by default Atmosphère opens it
   in place of the Album).
4. Start **OpenPak Setup**. It shows two entries:

    ```
    Nintendo                       Active
    OpenPak
    ```

5. Select **OpenPak** with **A**. The change is written at once.
6. Accept the reboot it offers. The console only reads its new network setup at boot.

That is all. OpenPak Setup also keeps your own hekate boot entry working: it builds an
OpenPak boot package next to the official one and updates the hekate entries itself.

After OpenPak is active:

- **The Album opens the Album again.** Hold **R** while opening the Album to get the Homebrew
  Menu.
- **The eShop entry opens OpenPak's eShop**, a homebrew store. Titles from it launch normally.
- **Link your user**: System Settings → Users → your user → **Link Nintendo Account**. See
  [linking a Switch](../account.md#linking-a-switch).

## What it changes

Selecting OpenPak:

- writes a marked block of host rules into `/atmosphere/hosts/default.txt` and
  `/atmosphere/hosts/emummc.txt`, pointing the services OpenPak serves at OpenPak. Anything
  else in those files is kept. Other tools' redirects for the same names are commented out so
  the choice really decides where the console goes;
- installs the OpenPak certificate authority so the console trusts OpenPak's servers;
- builds `/atmosphere/package3-openpak` (Atmosphère with OpenPak's changes) and points your
  hekate entries at it; the original package is left untouched;
- turns on the console's device certificate for the emuMMC (needed to sign in);
- installs OpenPak's News channels and the patches that let the console's News read them;
- on firmware 23.0.x, lets Save Data Cloud accept OpenPak's save keys (see below);
- installs one small data-only patch for **Crash Team Racing Nitro-Fueled**, which checks a
  key inside the game itself that no console-level change can reach. It is the only game
  patch OpenPak ships, and it is removed when you select Nintendo.

Backups of every file it changes are kept in `/switch/openpak/system`. **Do not delete that
folder while OpenPak is enabled.**

!!! info "A console on OpenPak reaches only OpenPak"
    System updates, the vendor eShop, telemetry and every third-party service a game dials go
    to OpenPak. Services OpenPak does not answer yet simply fail to connect. Nothing reaches
    the vendor while OpenPak is selected.

## Switch back to Nintendo

Open OpenPak Setup, select **Nintendo**, and accept the reboot. This is a full revert: the host
rules, certificate, boot package and patches are removed, and every file OpenPak changed is
put back the way it was.

!!! warning "Before a firmware update"
    Select **Nintendo** before you update the console's firmware, then update, then select
    OpenPak again once the new firmware is supported. If you forget, hekate may stop at
    *Failed to apply 'openpak_ksp'*; press POWER to continue booting, then select Nintendo.
    On an unsupported firmware OpenPak Setup warns you at launch; selecting Nintendo always
    works.

## Cloud saves

On firmware 23.0.0 and 23.0.1 the console's own **Save Data Cloud** screen backs up to
OpenPak. After selecting OpenPak, reboot through the hekate entry for the system OpenPak runs
on. See [cloud saves](../cloud-saves.md).

## Updates and failure reports

- When OpenPak Setup starts with a connection it checks for a newer release and offers it:
  **A** to update, **B** for not now. Nothing is downloaded without that yes, and it only ever
  downloads from the OpenPak Setup releases on GitHub.
- Some OpenPak changes need you to re-apply: if the tool says *"OpenPak updated the Switch's
  network redirects. Re-apply OpenPak and reboot"*, select OpenPak again and reboot.
- If the tool fails, it saves a small report under `/switch/openpak/reports/` and asks before
  sending it (**A** send, **B** don't, **X** always, **Y** never). Reports carry the versions,
  what was being done and the error text; no account token or console identifier.

## Known limits

- Presence, invitations, matchmaking and NAT traversal are partial; joining a game from an
  invitation does not always work yet.
- Only firmware 22.5.0, 23.0.0 and 23.0.1 are supported. Some pieces (News patches) wait for
  matching builds on 23.x.
- A Loader module of your own in `/atmosphere/kips` (an overclock module, for example) is
  loaded ahead of OpenPak's and can stop eShop titles from launching. OpenPak Setup names it in
  a warning and leaves it alone.

Problems: see [troubleshooting](../troubleshooting.md), or report them at
[openpak-nro issues](https://github.com/openpak/openpak-nro/issues).
