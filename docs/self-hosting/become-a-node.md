# Becoming a federation node

A federation node runs relays for the main OpenPak network in one region, so players near you
get shorter paths for their game traffic. Accounts, friends and matchmaking stay on
openpak.org; a node only relays game traffic. Read [how federation works](federation.md) first.

## The short version

- **A node is one region, one operator and one approval.** It runs on one or more servers.
- **OpenPak approves every node.** Meeting the minimums makes a node eligible, not approved.
  Nothing is served from a node until a person at OpenPak approves it.
- **Applications are accepted from every location except mainland China and Russia**,
  through the form on openpak.org. Within that, OpenPak approves nodes where it wants them.
- **The box is dedicated to OpenPak.** OpenPak Node OS (Fedora CoreOS) is the preferred
  install.
- **Every server reports and is checked.** Each server announces every minute with a hardware
  report, and runs a daily bandwidth self-test that home times itself. A node that falls short
  leaves rotation automatically, and comes back once it is compliant again.
- **Voluntary and unpaid**, with no warranty either way.

## Requirements

| Requirement | Minimum | Counted |
| --- | --- | --- |
| CPU cores | 8 per node, and 2 per server | all servers together, and each server |
| RAM | 16 GB per node, and 4 GB per server | all servers together, and each server |
| Storage | 160 GB NVMe or SSD per node (HDD does not count) | all servers together |
| Address | Its own public IPv4 per server: no carrier-grade NAT (100.64.0.0/10) or private ranges. IPv6 is wanted but not required. | each server |
| Bandwidth | 1 Gbps symmetric (declared port speed) | each server; it does not add up across servers |
| Measured bandwidth | At least 100 Mbps each way in the daily self-test | each server |
| Liveness | An announce within the last 3 minutes | each server |
| Self-test | A self-test within the last 72 hours | each server |
| Availability | 99.5 % target | the node (a published target, not machine-enforced) |

Reported RAM and disk within 10 % of a figure count, because the operating system reports a
little less than a machine is sold with. The application page always shows the current figures.

## Where nodes are wanted

Applications are accepted from every location except nodes inside **mainland China and
Russia**. Licensing, national firewalls, sanctions and surveillance law there conflict with the
operator terms, so OpenPak cannot accept nodes in either. Players there are served from
neighbouring regions.

Within that, OpenPak keeps a list of wanted locations: a region, a country and a city, and how
many nodes each one wants. The form takes applications for a location that is open and still
wants more nodes. Anywhere else you get *"OpenPak is not looking for nodes there yet"* and can
join a waitlist for your country. Europe (home) is served by OpenPak itself.

## How to apply

1. Sign in on [openpak.org](https://openpak.org) and open **Account → Run a region node**
   ([openpak.org/account/operator](https://openpak.org/account/operator)). The page shows the
   current minimums.
2. Pick an open location, then give your city, hosting provider and a contact email for
   operations and security.
3. Describe the planned servers (up to six on the form): for each, CPU cores, RAM, storage size
   and whether it is NVMe or SSD, bandwidth, IPv6, and roles (game server, TURN, STUN, NPLN
   relay).
4. Accept the [operator terms](https://openpak.org/operators). The form checks your plan against
   the minimums and tells you exactly what is short before it accepts.
5. Follow the status on the same page: **In review**, **Question for you** (answer it to return
   it to review), **Approved** (with your node's id), **Not accepted** (with the reason) or **On
   the waitlist**. You can have one application in review at a time.
6. When an application is approved, OpenPak creates the node and sends you its **node key**
   privately. The node starts out unapproved for traffic until its servers are up and checked.

## Bringing servers up

Each server must be dedicated to OpenPak: run nothing else on the box. OpenPak Node OS (Fedora
CoreOS) is the preferred install.

Each server runs the OpenPak node compose setup with the node key (`OPENPAK_NODE_KEY`) and its
own `SERVER_NAME`. On first start it joins the node and receives its own **server key**, stored
locally; every later call uses that server key.

- The node key's only power is to enrol servers. OpenPak can rotate it; servers that already
  joined keep their keys.
- One compromised server can be revoked on its own without touching the rest of the node.
- Re-joining with the same server name replaces that server's key (for a reinstalled machine).
- Open the UDP ports your roles need from the internet; the node setup's README lists them.
  Nothing TCP needs to be reachable from outside.

!!! note "Not ready yet"
    The node compose setup is not published yet. It will be linked here when it is.

## What each server reports

- **Every minute**, an announce: its roles with their addresses, and a hardware report (CPU
  cores, RAM, data filesystem size, whether storage is NVMe/SSD, public IPv4 and IPv6, declared
  port speed). Home compares the address the announce came from with the IPv4 the server
  claims, which catches NAT and proxies.
- **Once a day**, when home says it is due, a bandwidth self-test: the server downloads a fixed
  transfer from home (100 MB by default) and uploads the same amount. Home times both legs
  itself, so a server cannot report its own figure.

Reports are self-declared. They decide one thing only: whether the node is in rotation.
Approval stays a human decision.

## Approval and rotation

- Nothing is served from a node, or listed at
  [openpak.org/api/v1/regions](https://openpak.org/api/v1/regions), until OpenPak approves it.
- Approval is refused while the node or any of its servers is short, and the refusal lists every
  shortfall.
- An approved node is **in rotation** when it has at least one server, and every server is
  reporting, has a public IPv4 that matches where it announces from, announces at least one
  role, has a fresh self-test and meets the per-server floors, and the node meets the totals.
- An approved node that falls short, or has a server that stops reporting, **leaves rotation
  automatically**: it disappears from the regions list and gets no new rooms or sessions, but
  keeps its approval. It returns on its own once compliant. Rooms already on it carry on.
- A server you retire for good should be revoked; a silent server keeps the whole node out of
  rotation.

## Operator terms, in short

The full text is at [openpak.org/operators](https://openpak.org/operators). In short:

- Reports must be truthful.
- **No logging or keeping of player data** beyond what running the relay needs at that moment:
  no packet captures, no kept IP logs, no per-player records, and no sharing, selling or
  analysing of traffic.
- **Data processing agreement**: player IP addresses and game traffic are processed only to host
  rooms. Logs go no further than operational need and are deleted within 7 days. No other use.
  Security incidents are reported to OpenPak within 72 hours, and everything is deleted when
  you leave.
- **No modification of traffic**: relay it as it arrives, with no injection, blocking, delay or
  reordering. No modified OpenPak software, and the shared secrets are used for nothing else.
- Keep a working security contact, and report a compromise or leaked key at once to
  [contact@openpak.org](mailto:contact@openpak.org) or through the
  [security policy](https://github.com/openpak/.github/blob/main/SECURITY.md).
- OpenPak can take a server or node out of rotation, revoke its keys or end its approval at any
  time. You can stop at any time; tell OpenPak first.

## Trust

Neither the node key nor a server key can read accounts, friends or links. A node that is not
approved and in rotation can only join, announce and self-test. A node does hold the shared
secrets its relays need, which is why every node is looked at by a person before it carries
anyone's game.
