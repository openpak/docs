# The clean-room rule

OpenPak replaces console network services. Some of what it replaces already has an
implementation OpenPak may not use: source-available but non-free code, or code under a
licence that cannot be combined with OpenPak's. This page is how OpenPak stays clear of it.

## The wall

Code under an incompatible licence cannot be forked, vendored or carried across. What OpenPak
can take from it is **facts**, recorded in the repository's `docs/provenance.md`, and its own
rewrites.

**Allowed: read these and write them down.**

- Ports, hostnames, endpoint paths, method and opcode numbers, protocol ids.
- Wire formats: the field names and types a console sends or expects, error and result codes.
- Flows: what talks to what, in what order, and what a working run looks like.
- Status: what actually runs, what is a stub, what was never finished.

Those are facts about a console and a protocol. A port number is not authorship.

**Not allowed:**

- Copying, translating, porting or paraphrasing their source, in whole or in part.
- Mirroring their structure: file layout, package split, type and function names, table
  schemas, the shape of their handlers.
- Lifting their comments, documentation or commit messages.

**The test:** could you have written this line having only read a *description* of what the
server does? If yes, write it. If you are reproducing how someone else chose to express it,
stop.

In practice: read to learn the endpoint, close the file, then write OpenPak's version in
OpenPak's shape, with OpenPak's account integration, error handling and conventions.

## Allowed inputs

1. **Observed console behaviour.** What a real console sends is a fact about the console: your
   own captures, the error codes it shows, the endpoints it resolves.
2. **Public protocol documentation.** For example Kinnay's NintendoClients documentation and
   wiki, the Pretendo Network wiki, SwitchBrew and published research write-ups.
3. **Compatibly licensed code.** Pretendo Network's AGPL-3.0 libraries (`nex-go`,
   `nex-protocols-go`, `nex-protocols-common-go`) and other code whose licence is compatible
   with AGPL-3.0-only. Check each dependency's exact version and notices before adding it.
4. **OpenPak's own repositories.**

## Never as input

- Leaked or confidential vendor material, including development kits and their documentation.
- Official signing keys. Never seek or store them; a design that a key would make unnecessary
  is still the right clean-room answer.
- Game or firmware files in a repository, ever.

## Record where a fact came from

Every component that implements a protocol keeps a `docs/provenance.md`: each non-obvious fact
(a port, an endpoint, a field, an opcode) and where it came from: a capture of OpenPak's own, a
public document, or another OpenPak repository. That is what makes "we wrote it from the
facts" checkable later instead of a claim.

Record what you could not explain, too. An observation that made no sense, a value that seemed
arbitrary, a behaviour with no cause you could find: write it down and mark it unexplained.
Another component's measurement is often the missing half. Two facts that contradict each
other are a finding, not a problem to resolve before writing.

## In a pull request

Say where the protocol facts in your change come from. If you have read code you may not copy
for the area you are working on, say so, and keep your change to what the facts support.
