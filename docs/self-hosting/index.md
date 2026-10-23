# Running your own network

OpenPak's own code is free software under the **AGPL-3.0**. Anyone may run their own network
from it: for a household, a community, or to develop against.

There are two different things you can do:

| | Your own network | A federation node |
| --- | --- | --- |
| What it is | A separate, independent network with its own accounts | A relay box for the main OpenPak network, in your region |
| Accounts and friends | Your own | Stay on openpak.org |
| Needs approval | No | Yes, by OpenPak |
| Clients | Need to be pointed (and signed) for your network | Unchanged; players are sent to your node automatically |
| Guide | This page and [deploying](deploy.md) | [Becoming a federation node](become-a-node.md) |

If what you want is to make OpenPak faster for players near you, a
[federation node](become-a-node.md) is almost always the better choice.

## Your obligations under the AGPL

If you run a modified OpenPak service for other people over a network, the AGPL requires you
to offer those users the source code of your modified version. Forked components (emulators,
the Wii U/3DS/Wii/DS services built on other projects) keep their own licences; check each
repository's `LICENSE`.

## What a network needs

At minimum:

| Piece | Role |
| --- | --- |
| **PostgreSQL** | Storage for the core and for most services. Migrations apply on startup. |
| **`account`** | The account core. Reachable only on your internal network. |
| **`website`** | Sign-up, sign-in, the account portal, the mobile API, the network profile and the admin pages. |
| **A TLS terminator** | In front of everything public (for example Traefik). The website must never be served on a console-facing hostname. |

Then, for each console family you want to serve, its adapter and the services it needs (for
example `nx-baas` for the Switch, `nn-account` and `nn-friends` for the Wii U and 3DS, `nn-wfc`
for the Wii and DS), and the game servers for the games you want. The optional
platform-neutral services (`saves`, `news`, `mods`, `chat`, `connectivity`) each add a feature.
See the [architecture](../contributors/architecture.md) and the [port plan](../contributors/ports.md).

## What is different from openpak.org

Running the servers is the easy half. The clients are built to trust **openpak.org**, and that
is deliberate:

- **The signed redirect ceiling** is verified against OpenPak's pinned public key and fetched
  from the pinned `openpak.org` origin. A separate network needs its own signing key, its own
  ceiling, and client builds that pin them. See
  [signed redirect ceiling](../contributors/signed-ceiling.md).
- **Console trust.** Consoles trust the OpenPak certificate authority that the setup tools
  install. A separate network needs its own CA, its own certificates for the console-facing
  names, and setup tools built with that CA.
- **Server address.** Some clients can be pointed elsewhere without a rebuild (for example
  OpenPak Setup for the Switch reads a server address from `/switch/openpak/server.txt`), but the
  trust points above still need your own builds.

!!! note "Not ready yet"
    A complete, documented path for building every client for an independent network is not
    ready yet. Today, running your own network is practical for development and for people
    comfortable building the clients themselves.

## Images

During the alpha, OpenPak's container images are not public, so build images from each
repository's `Dockerfile`. [Deploying](deploy.md) shows how.

## Security basics

- Generate every secret yourself: at least 32 random bytes each (`openssl rand -base64 48`).
  Never reuse the placeholders from `example.env`.
- Keep the core's gRPC, every internal key, metrics and pprof off the public internet.
- Keep admin access closed by default: the website's admin pages open only for the account ids
  you list in `WEBSITE_ADMIN_ACCOUNT_IDS`.
- Keep the redirect-ceiling signing key off every server.
