# Becoming a federation node

A federation node runs relays for the main OpenPak network in your region, so players near you
get shorter paths for their game traffic. Accounts, friends and matchmaking stay on
openpak.org; see [how federation works](federation.md).

!!! warning "Draft rules"
    The admission rules below are the current defaults. Points marked **open** are not final
    yet and may change before nodes are admitted.

## The rules

- **Approval by OpenPak is required.** A node only receives players after a person at OpenPak
  has looked at it and approved it. Approval can be withdrawn.
- **A node may span several servers.** The hardware minimums are for the node in total, with a
  floor for each server.
- **Nodes are reported and checked.** A node announces itself and what it runs every minute,
  and OpenPak checks what it reports.
- **Apply through the form on openpak.org.**

## Hardware minimums

| | Minimum |
| --- | --- |
| **The node in total** | 8 CPU cores, 16 GB RAM, 160 GB SSD |
| **Each server** | 2 CPU cores, 4 GB RAM |
| **Each server's network** | Its own public IPv4 address, 1 Gbps symmetric |
| **Availability** | 99.5 % |

Bandwidth does not add up across servers: each server needs its own 1 Gbps.

## What you run

A node runs a compose setup with the relay services (not published yet, **open**): a
game server in game-only mode and a TURN relay, plus a small loop that announces the node to
openpak.org once a minute. It needs these ports open from the internet, all UDP:

| Port | Service |
| --- | --- |
| 22002, 22012/udp | Game server |
| 3478/udp | STUN/TURN |
| 49152–65535/udp | TURN relay range |

Nothing TCP needs to be reachable from outside.

## How to apply

1. Read [how federation works](federation.md), so you know what a node does and does not hold.
2. Apply with the form on [openpak.org](https://openpak.org) (**open:** the form's exact
   address).
3. If OpenPak accepts the application, you receive the node's id, its key (shown once) and the
   shared secrets the relays need.
4. Copy the node's `example.env` to `.env`, fill it in, and start it with
   `podman compose up -d` (or `docker compose`).
5. Open the firewall for the ports above.
6. Once the node shows as announcing, OpenPak checks it and approves it. From then on it is
   listed at [openpak.org/api/v1/regions](https://openpak.org/api/v1/regions) and rooms start
   landing on it.

## What you agree to

**Open:** the operator terms, how the checks are run, and what happens when a node falls below
the minimums are not published yet.

## Trust

A node holds no accounts and cannot read anyone's account, friends or links: its key
authenticates announces and nothing else. It does hold the game server's token secret and the
TURN secret, which is why every node is approved by a person first.
