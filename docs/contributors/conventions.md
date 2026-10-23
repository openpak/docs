# Conventions

Rules and shapes shared by every OpenPak repository. When a repository has a reason to deviate,
the reason is written down in that repository.

## Licences

- **OpenPak's own services and tools:** AGPL-3.0-only.
- **Forks** (emulators, the Wii U/3DS/Wii/DS services and clients built on other projects): keep
  their upstream licence. Code contributed to a fork follows the fork's licence, never the
  server licence.
- **Artwork** shipped alongside a fork (icons) may carry its own licence, declared in the file.
- **This documentation:** CC BY-SA 4.0.

Never copy code from one licence into another implicitly. Each repository's `LICENSE` says
which licence applies, and by opening a pull request you agree that your contribution is
released under it.

## What every repository has

| File | What it holds |
| --- | --- |
| `README.md` | What the service is, **what works and what does not**, how to run and test it. |
| `CHANGELOG.md` | Dated, one-line history of changes. |
| `LICENSE` | The licence. |
| `example.env` | Every setting, commented, with placeholder secrets. |
| `docs/` | Documents about this repository only: protocol notes, endpoint inventories, design. |
| `docs/provenance.md` | Where each non-obvious fact came from (see the [clean-room rule](clean-room.md)). |
| `prds/` | Design documents for planned work. |

A document that more than one repository follows (a policy, a shared contract, the port plan)
lives on this site, once. Repositories link to it instead of carrying trimmed copies, which go
stale.

## Never commit

- Game files, firmware, keys, certificates and private keys, tokens.
- Packet captures, memory dumps, raw logs with player data, decompiled code.
- Production identifiers, real account credentials, test-account passwords.

Interoperability is expressed as **independently written code and sanitised conclusions**. Raw
research inputs stay outside every repository. If you are not sure whether something is safe to
commit, keep it out and describe only the behaviour it shows.

## READMEs say what is true

A README states what works today and what does not, with the evidence level: verified on real
hardware, verified in an emulator, or not verified. "A game that launches" is not evidence that
it works online. Do not round up.

## Testing expectations

- Run the repository's tests before you open a pull request: for Go, `go vet ./...` and
  `go test -race ./...`, plus the integration tests where the README lists them.
- Add a test with every fix. For console-facing replies, a test that compares the reply against
  a recorded, value-stripped shape the console accepted is the best protection there is: a
  console usually reports a bad reply with only an error code.
- Behaviour that needs a console says how it was tested: which console or emulator, which
  firmware, which game version.

## Test clients and accounts

- OpenPak emulators are OpenPak clients: each emulator profile is its own OpenPak account,
  signed in from the emulator's own OpenPak menu.
- A **multiplayer test uses separate machines**: a console plus one or more emulators, or
  emulators on different machines. Two instances on one machine are not a multiplayer test.
- Test accounts and their credentials live outside repositories, never in scripts or logs.

## Experiments

- One variable per run. State the decision rule **before** running.
- Check the obvious first: account linked, configuration present, one instance, correct game
  version.
- Record rejected approaches too. An experiment that fails eliminates a layer.
- Label every conclusion as **measured** or **inferred**, and never ship a server change that
  rests only on an inference. See [online compatibility](online-compatibility.md).

## Configuration style

- Services read their listen addresses from `<SERVICE>_HTTP_ADDR`, `<SERVICE>_GRPC_ADDR` and
  `<SERVICE>_METRICS_ADDR`, with defaults from the [port plan](ports.md).
- Internal keys fail closed: an unset key disables the route rather than leaving it open.
- Emulator hooks use `OPENPAK_<TITLE>_<PURPOSE>` variables that are **unset by default**, so a
  hook never affects another game.

## Commits and pull requests

- Commit messages are short and imperative: "Add ban lookup to the NAS login", not "Added" or
  "Fixes".
- One change per pull request. Open an issue first for anything larger than a small fix.
- Say where any protocol fact in the change comes from.
