# OpenPak documentation

OpenPak is an open replacement online network for Nintendo, Xbox and PlayStation consoles
and for the emulators that run their games. The official servers for many of these consoles
are shutting down or already gone. OpenPak runs the services that let those consoles and
their games go online again: accounts, friends, presence, matchmaking, cloud saves, news and
shops. You keep the real console firmware and the real games. Only the network side is
replaced.

!!! warning "OpenPak is in public alpha"
    Things will break. Accounts, friend lists, console links and cloud saves may be reset
    without notice, and there is no uptime promise. Keep your own copies of anything you
    care about, especially save files. Please report what you find.

## Pick your path

- **I want to play.** Start with [what OpenPak is and what works today](players/index.md),
  read [before you start](players/before-you-start.md), then follow the
  [setup guide](players/setup/index.md) for your console or emulator.
- **I want to help build it.** Read the [architecture](contributors/architecture.md), how the
  [repositories are organised](contributors/repositories.md) and the
  [clean-room rule](contributors/clean-room.md).
- **I want to run a server.** See [running your own network](self-hosting/index.md) and
  [becoming a federation node](self-hosting/become-a-node.md).

## Useful links

| | |
| --- | --- |
| Website and account | [openpak.org](https://openpak.org) |
| Which games work | [openpak.org/titles](https://openpak.org/titles) |
| Feature status | [openpak.org/features](https://openpak.org/features) |
| Downloads | [openpak.org/downloads](https://openpak.org/downloads) |
| Is it down? | [status.openpak.org](https://status.openpak.org) |
| Help request (signed in) | [openpak.org/help](https://openpak.org/help) |
| Source code | [github.com/openpak](https://github.com/openpak) |
| Contact | [contact@openpak.org](mailto:contact@openpak.org) |

## The rules OpenPak keeps

- **No game or firmware files.** OpenPak never ships games, firmware, keys or console data,
  and never explains how to get them. Use your own console and your own games.
- **The console, not the game.** On Switch, Wii U and 3DS, OpenPak changes where the console
  connects and leaves game code alone. Wii and DS games have no other way in, so their
  patchers redirect each game.
- **Clean room.** Implementations OpenPak may not legally copy are used only for facts
  (ports, wire formats), never for code.
- **Copyleft.** OpenPak's own code is AGPL-3.0. Anyone may run their own network.

OpenPak builds on the work of [Pretendo Network](https://github.com/PretendoNetwork),
[WiiLink](https://github.com/WiiLink24), [Kinnay](https://github.com/kinnay) (NintendoClients
and the Game Server List) and the upstream emulator projects its forks are based on.

!!! note "Not affiliated"
    OpenPak is an independent community project. It is not affiliated with, endorsed by or
    sponsored by Nintendo, Microsoft or Sony. All trademarks belong to their owners.
