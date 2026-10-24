# Repositories

OpenPak is not a monorepo. **Every service is its own repository** under
[github.com/openpak](https://github.com/openpak), with its own README, changelog, tests, image
and releases. A change that spans services is one pull request per repository.

!!! note
    During the alpha some repositories are still private. They are opened as they get ready;
    if a link here returns a 404, that repository is not public yet.

## Finding a repository by topic

Every repository is tagged with GitHub topics, by platform and by kind.

**Platform:**
[`switch`](https://github.com/orgs/openpak/repositories?q=topic%3Aswitch) ·
[`wiiu`](https://github.com/orgs/openpak/repositories?q=topic%3Awiiu) ·
[`3ds`](https://github.com/orgs/openpak/repositories?q=topic%3A3ds) ·
[`wii`](https://github.com/orgs/openpak/repositories?q=topic%3Awii) ·
[`ds`](https://github.com/orgs/openpak/repositories?q=topic%3Ads) ·
[`xbox`](https://github.com/orgs/openpak/repositories?q=topic%3Axbox) ·
[`xbox360`](https://github.com/orgs/openpak/repositories?q=topic%3Axbox360) ·
[`ps3`](https://github.com/orgs/openpak/repositories?q=topic%3Aps3) ·
[`core`](https://github.com/orgs/openpak/repositories?q=topic%3Acore) (shared by every console) ·
[`multi-platform`](https://github.com/orgs/openpak/repositories?q=topic%3Amulti-platform)

**Kind:**
[`infra`](https://github.com/orgs/openpak/repositories?q=topic%3Ainfra) (network services) ·
[`game-server`](https://github.com/orgs/openpak/repositories?q=topic%3Agame-server) ·
[`client`](https://github.com/orgs/openpak/repositories?q=topic%3Aclient) (what runs on the console or your phone) ·
[`emulator`](https://github.com/orgs/openpak/repositories?q=topic%3Aemulator) ·
[`tool`](https://github.com/orgs/openpak/repositories?q=topic%3Atool) ·
[`library`](https://github.com/orgs/openpak/repositories?q=topic%3Alibrary) ·
[`docs`](https://github.com/orgs/openpak/repositories?q=topic%3Adocs)

## Naming

Repository names say which family they belong to:

| Prefix | Family |
| --- | --- |
| `nx-` | Switch infrastructure |
| `nn-` | Wii U and 3DS infrastructure and the Wii/DS WFC server |
| `np-` | PlayStation 3 |
| `x360-` | Xbox 360 |
| `xb-` | Original Xbox |
| no prefix | core services (`account`, `website`, `saves`, ...), shared game-server hosts (`nex`, `npln`, ...), clients (`app`, the `*-patcher` repositories such as `switch-patcher`) and emulators |

New Xbox and Xbox 360 service names follow the names the console's own firmware uses.

## Good places to start

| Repository | What it is |
| --- | --- |
| [`account`](https://github.com/openpak/account) | The account core. Knows nothing about consoles. |
| [`website`](https://github.com/openpak/website) | openpak.org, the account portal, the title catalogue and the mobile API. |
| [`nx-baas`](https://github.com/openpak/nx-baas) | The Switch adapter. |
| [`nex`](https://github.com/openpak/nex) | The shared NEX/PRUDP game-server host for Wii U, 3DS and Switch titles. |
| [`app`](https://github.com/openpak/app) | The companion app for Android and iOS. |
| [`switch-patcher`](https://github.com/openpak/switch-patcher) | OpenPak Switch Patcher. | 
| [`wiiu-patcher`](https://github.com/openpak/wiiu-patcher), [`3ds-patcher`](https://github.com/openpak/3ds-patcher), [`wii-patcher`](https://github.com/openpak/wii-patcher), [`ds-patcher`](https://github.com/openpak/ds-patcher) | The OpenPak Wii U, 3DS, Wii and DS Patchers. |
| [`xbox-patcher`](https://github.com/openpak/xbox-patcher), [`x360-patcher`](https://github.com/openpak/x360-patcher), [`ps3-patcher`](https://github.com/openpak/ps3-patcher) | The Xbox, Xbox 360 and PS3 patchers. Placeholders, not available yet. |
| [`harbor`](https://github.com/openpak/harbor) | The Switch emulator. |
| [`docs`](https://github.com/openpak/docs) | This site. |

## Teams

Maintainers are organised in GitHub teams that match the families: **core**, **switch**,
**wiiu-3ds**, **wii-ds**, **ps3**, **xbox**, **xbox360**, **clients** and **emulators**, plus
reviewer and maintainer teams. Pull requests are reviewed by the team that owns the repository.

## Forks

Several repositories are forks of other projects: the Wii U, 3DS and Wii/DS services and
clients build on [Pretendo Network](https://github.com/PretendoNetwork) and
[WiiLink](https://github.com/WiiLink24), and every emulator is a fork of an upstream emulator.
Forks keep their upstream licence and credits. Report fork-specific problems to the OpenPak
fork, and general problems upstream.

## Releases and CI

Each repository's CI runs when a version tag (`vX.Y.Z`) is pushed, or when it is started by
hand, and builds and publishes that release. Ordinary pushes do not start a build, so run the
tests yourself before you open a pull request.
