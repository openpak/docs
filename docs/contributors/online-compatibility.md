# Bringing a game online

A general method for taking a game whose online mode fails against OpenPak, for any backend
and any function the game needs from a server (identity, configuration, matchmaking, presence,
saves, sessions, peer-to-peer or relay), finding **which layer** is failing, and building the
missing piece in the right order.

Two rules sit above everything on this page:

- **The console, not the game.** OpenPak changes where a console connects and what it trusts;
  it does not patch game code. A game that seems to need a game-code change is a finding to
  write down and discuss, not a patch to ship. (One exception exists on the Switch, for a game
  that checks a key inside its own code; it was a deliberate, reviewed decision.)
- **No server change on the strength of an inference.** Measure the client first, then change
  the server. A guess costs a deploy, a test run and someone's evening; a measurement costs
  minutes.

## Choose the test client

- **An OpenPak emulator first** where one exists. It is cheaper to restart and can show more of
  what the game does. On the Switch that is [Harbor](../players/setup/emulators/harbor.md).
- **Confirm on real hardware** before calling a game working. A result seen only in an emulator
  may be an emulator gap rather than a server bug.
- **Multiplayer means separate machines**: a console plus an emulator, or emulators on
  different machines.
- **Trust long-standing working setups over one-off failures.** A single failed session on a
  setup that always worked is usually a confound (account state, region, transient server
  state). Reproduce it before believing it.

## The layered model

A game going online passes through gates, in order. Each has a typical symptom when it fails.

| # | Gate | Typical symptom of failure |
| --- | --- | --- |
| 1 | **Name resolution** | Nothing dials; wrong hosts; an instant error. |
| 2 | **Transport** (TCP/UDP) | Connections refused or timing out; NAT checks unanswered. |
| 3 | **Session security** (TLS, DTLS, custom crypto) | The handshake dies, or completes and the connection closes at once. |
| 4 | **Protocol handshake** | A preface or init exchange, then a close. |
| 5 | **Identity and credentials** | Connects, then cancels the first request; auth errors. |
| 6 | **Feature calls and payloads** | Requests arrive; replies are wrong or partly work. |
| 7 | **Peer-to-peer and session data** | The lobby works; connecting to the other player fails. |

Work from the bottom. Proving a lower gate good is as valuable as finding the failing one.

## What a server must provide

Whatever the backend, what a game needs from a server falls into a few classes. Find the
missing one and where the game expects to get it.

1. **Identity**: who the player is on this service (account link, player ids, friend codes).
   Missing: the game connects, then cancels its first request.
2. **Credentials and tokens**: proof of identity for each service, often exchanged from an
   identity token by a bootstrap call. Missing: auth attempted with an empty or rejected
   credential.
3. **Trust material**: what makes the client accept the server (certificate chains, pinned
   keys). Missing: the handshake completes, then an immediate close or a certificate error code.
4. **Configuration**: per-game settings the client cannot hardcode (endpoints, environment ids,
   feature flags). Missing: the game connects but skips requests, or says the feature is not
   available.
5. **Feature state and payloads**: the actual game data. Missing: calls arrive and get wrong or
   empty answers. This is where per-game handlers are written.
6. **Session and peer coordination**: what lets two players find each other (session ids,
   external addresses, relay). Missing: matchmaking works, the peer connection fails.

For each class the question is the same: **what exact fields does the client expect, where
does it expect them from, and what does it do when they are missing?**

## Measure the client

Cheapest first; each step can make the next unnecessary.

1. **Read the client's own logs.** Emulator logs show DNS resolution order, connections, sizes
   and system calls with their results. Which host a game actually dialled settles which
   backend it uses.
2. **Read the traffic, both directions.** Where the client allows it, log the plaintext of its
   connections. A sanitised probe that records metadata only (handshake parameters, frame
   types and sizes, field *names*, timing) answers: did the client speak, what did it say, when
   did it stop?
3. **Ask the operating system whether the client is reading.** On the client's host,
   `ss -tnp` shows a socket's receive queue. A non-zero, non-draining `Recv-Q` means the bytes
   the server sent are sitting there unread, and no change to their shape will help.
4. **Put a complete server on the port.** If the client still refuses to speak to a full,
   known-good implementation, the gate is on the client side; if it speaks, the difference is
   in the payloads.
5. **Compare.** When two similar games behave differently on the same server, or one game
   behaves differently on two clients, the difference is the finding.

### What is not evidence

- **A string is not a code path.** Release builds often compile their logging out, so an error
  message you are hunting may never print.
- **A linked SDK is not a feature.** A game can ship a networking library and never use it
  online. Only observed traffic settles which backend a game uses.
- **A plausible constant is not a measured one.** A guessed timeout or size, defended and later
  corrected, can be wrong both times.
- **Arithmetic is evidence too.** A size that is not a whole multiple of what you assumed means
  the assumption is wrong.

## The experiment sequence

1. **Baseline.** Reproduce the failure with the normal redirects on. Record the order of
   events and the error code, and write a sanitised summary.
2. **Sanity.** Account linked, configuration present, one instance, latest game version. An
   outdated or base-only install is a classic false lead.
3. **Tap the failing service** with a probe and watch what the client sends.
4. **Serve the minimum** that was observed, never invented. See what changes.
5. **Climb the credential chain.** When a request is attempted with a wrong or missing input,
   find where that input should come from and fix the source, not the symptom.
6. **Re-baseline after every fix**, so regressions and older breakage are not misattributed.

Record every experiment in the repository: hypothesis, method, decision rule, observation (with
a confidence label), and what was left out. Rejected approaches are progress.

## Server-side pitfalls that look like protocol bugs

- **HTTP/2 by accident.** A TLS terminator that negotiates HTTP/2 with a client while the
  backend speaks HTTP/1.1 resets the connection; it looks exactly like a routing failure. Pin
  ALPN to `http/1.1` where the backend needs it.
- **Dispatch by hostname.** Adapters that serve many console hostnames route by `Host`. An
  internal call without the right `Host` header gets a 404.
- **Boot-time configuration.** Consoles read redirects (and the signed ceiling) at boot. A
  console that "doesn't go anywhere" after a change has usually not been rebooted.
- **NAT checks need a real resolver and two addresses.** The NAT-check names must resolve to two
  different public addresses, and some consoles reject an answer synthesised by their own host
  rules.
- **Log what the client sent, not what you assume it sent.** One line of header logging often
  ends a whole theory.

## Done means

A game is **live** when it has been played online on real hardware, with the tested modes
written down. Until then it is beta or alpha on the titles page, and the README says what was
and was not verified.
