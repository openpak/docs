# Architecture

OpenPak replaces the online side of many consoles with one network. The shape that makes that
possible is simple: **one console-agnostic core, a thin adapter per console family, and game
servers that trust the core's identity.**

```
            consoles and emulators (each speaks its own native protocols)
     Switch      Wii U / 3DS     Wii / DS      Xbox / 360       PS3        phone app
        │             │              │              │             │             │
   ┌────┴────┐  ┌─────┴─────┐  ┌─────┴────┐  ┌──────┴─────┐  ┌────┴─────┐  ┌────┴────┐
   │ Switch  │  │ Wii U/3DS │  │  WFC     │  │ Xbox and   │  │  PS3     │  │ website │
   │ adapter │  │ adapters  │  │ server   │  │ 360 svcs   │  │ adapter  │  │ + API   │
   └────┬────┘  └─────┬─────┘  └─────┬────┘  └──────┬─────┘  └────┬─────┘  └────┬────┘
        └─────────────┴──────────────┴───── internal gRPC ────────┴─────────────┘
                                     │
                         ┌───────────┴───────────┐
                         │      account core      │  accounts, sessions, links,
                         │  (knows no consoles)   │  friends, presence, invitations,
                         └───────────┬───────────┘  moderation, events
                                     │
        platform-neutral services: saves · news · mods · chat · voice · connectivity · status
                                     │
        game servers: NEX/PRUDP · NPLN · Photon-compatible · per-publisher backends
```

## The account core knows nothing about consoles

The [account core](https://github.com/openpak/account) holds accounts, web sessions, email
verification and recovery, two-step sign-in, the friend graph, presence, invitations,
moderation and an event stream. It has **no console protocol code at all**, and a guard test
fails the build if a console package is ever imported.

What it has instead is a generic **link**: a binding between an account and a subject in a
namespace (`switch`, `wfc`, and so on). The link moves through a small state machine (pending,
active, revoking, revoked). The core does not know what a Switch user id or a WFC profile is; it
stores the subject an adapter gives it.

That buys three things:

- **Adding a console never touches the core.** A new family is a new adapter.
- **One identity everywhere.** Friends, blocks, presence and bans live in one place, so a friend
  added on one console is a friend on all of them, and a ban applies on every platform.
- **Every new account gets an identity on every network**, created automatically, so a friend
  on one console can see you on another without extra steps.

The core is only reachable on the internal network. Its gRPC calls are authenticated with an
internal key and fail closed without it.

## Adapters

An adapter speaks one console family's native protocols on one side and the core's contracts
on the other. It owns that family's identifiers (user ids, friend codes, tokens), mints them
once per account, and never lets them migrate.

| Family | Adapter repositories |
| --- | --- |
| Switch | `nx-baas` (accounts, device auth, console link, friends), with `nx-shop`, `nx-penne`, `nx-pctl`, `nx-bcat` split out by service |
| Wii U and 3DS | `nn-account`, `nn-friends`, plus content services `nn-boss`, `nn-juxtaposition`, `nn-soap` |
| Wii and DS | `nn-wfc` |
| PS3 | `np-account`, `np-trophy` |
| Xbox 360 | `x360-*`, one repository per service |
| Original Xbox | `xb-*`, one repository per service |

Adapters answer **in the console's own words**. A console parses replies strictly and often
reports a malformed reply with nothing more than an error code, so adapters keep recorded,
value-stripped reply shapes in their tests and compare against them.

## Platform-neutral services

| Service | What it does |
| --- | --- |
| `website` | openpak.org: the account portal, the title catalogue, the public mobile API (OpenAPI 3.1), the network profile and the admin pages. |
| `saves` | Cloud saves, with optional storage owned by the player. |
| `news` | News channels delivered to consoles. |
| `mods` | The mods catalogue. |
| `chat` | One neutral message store for every surface. |
| `voice` | Voice chat for the phone app. |
| `connectivity` | Multiplayer endpoint leases, TURN credentials and relay allocation. |
| `status` | The status page, run away from the machines it watches. |

Console-facing handlers from these services are mounted by the adapter that the console
already talks to, rather than getting console-facing hostnames of their own.

## Game servers

Game servers serve the online part of specific games. Most of them are one shared host per
protocol family, with one small package per game:

- **NEX/PRUDP** (`nex`, `switch-nex`): one image; a container runs one title.
- **NPLN** (`npln`): one image; a container runs one title.
- **Per-publisher backends** (`photon`, `demonware`, `eos`, `t17`, `klei`, `playfab` and
  others): one process for every title that uses that backend.

Game servers never keep their own accounts. They trust tokens signed for OpenPak identities, so
a player is the same person on every server.

## How a console finds OpenPak

- **Network profile.** `GET https://openpak.org/api/v1/network/profile?platform=<name>` says
  which names a client should send to OpenPak. It is generated from the routing the server
  actually runs, so it cannot drift from reality.
- **Signed redirect ceiling.** Clients only accept names inside a signed list of domain
  families, so a compromised server cannot widen what consoles redirect. See
  [signed redirect ceiling](signed-ceiling.md).
- **Console DNS.** For consoles whose only setting is a DNS server, a resolver answers from the
  same profile, so real consoles and emulators cannot drift apart.
- **Trust.** Consoles trust an OpenPak certificate authority, installed by the console-side tool
  (the OpenPak Switch, Wii U and 3DS Patchers) or by the emulator.

## Events, not polling the database

The core emits durable events (`friend_requested`, `friend_accepted`, `invitation_sent`,
`account_banned` and others) inside the same transaction that commits the change, so a
notification is never promised for something that did not happen. Adapters follow the stream
to push notifications to online consoles and to revoke tokens when an account is banned or a
link is revoked.

## Health

Every service answers "is it running" over HTTP (`/healthz`, and `/readyz` where it has
dependencies), so nothing has to infer health from a socket. UDP-only services expose a small
HTTP health port next to their game ports.

## One repository per service

Each service is its own repository with its own README, changelog, tests, image and release.
Shared Go code is a library repository consumed with a `replace` directive and a committed
`vendor/` tree, so every repository builds alone. See [repositories](repositories.md).
