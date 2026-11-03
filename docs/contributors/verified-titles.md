# Verified titles

The record of online results observed on real hardware and OpenPak emulators, newest first. Each entry separates the owner's device test from server-side evidence; untested features stay explicit. Method: [Bringing a game online](online-compatibility.md). Served catalogue: [openpak.org/titles](https://openpak.org/titles).

Project-wide record of observed online results. Each entry distinguishes the
owner's device test from server-side evidence; untested features stay explicit.

| Game | Platform / build | Backend | Verified result | Last verified |
| --- | --- | --- | --- | --- |
| Castle Crashers Remastered (`010001300D14A000`) | Switch 1.0.7 (version `00070000`); Harbor desktop, two consoles, one PC | Switch NEX (`switch-castle-crashers-remastered`) + Pia P2P | Play with Anyone: host creates, joiner auto-joins, NAT probes both ways; both players in character select and the first level together for over two minutes | 2026-11-03 |
| Lethal League Blaze (`01003AB00983C000`) | Switch 1.23 (version `00030000`); Harbor desktop, two consoles, one PC | Switch NEX (`switch-lethal-league-blaze`) + Pia P2P | Online free for all: host creates, joiner auto-joins, both fighters on one stage, mirrored on both consoles | 2026-11-03 |
| SpeedRunners (`0100C8B00C4AE000`) | Switch 1.0.0 (version `00000000`); Harbor desktop, two consoles, one PC | Switch NEX (`switch-speedrunners`) + Pia P2P | Quick Match: shared lobby and level vote, both runners spawned in one race | 2026-11-03 |
| PAC-MAN 99 (`0100AD9012510000`) | Switch 1.1.0 (version `00020000`); Harbor desktop, two consoles, one PC | Switch NEX (`switch-pac-man-99`) | Both consoles matched into one 99-player room; the countdown ran out and the match started with both players | 2026-11-03 |
| PlateUp! (`01003F901A83E000`) | Switch 1.5.2, content 1572864; Harbor | NPLN GameSession/Gamesync, QUIC P2P | Switch online entry and hosting; Harbor connects to the Switch-hosted session | 2026-10-12 |
| Monopoly for Nintendo Switch (`01007430037F6000`) | Switch 1.0.5 (version `00050000`), two consoles | Switch NEX (`g2e041d00`, `switch-monopoly` on 23090/23091/23092) + Pia P2P | Two-player online lobby: host creates, joiner browses, joins and exchanges stations; NAT probes cross in both directions | 2026-10-12 |
| Full Metal Furies (`010079300AD54000`) | Switch + Harbor, version `00050000` | Switch NEX (`g2c82ee00`, `switch-full-metal-furies` on 23120/23121/23122) + Pia P2P | Two-player co-op works Harbor ↔ Switch: host creates, joiner browses, joins with the session key, fetches stations; NAT probes cross both ways, punch `rtt=102ms`; clean leave/idle teardown | 2026-10-13 |
| Heroes of Hammerwatch — Ultimate Edition (`0100D2B00BC54000`) | Switch v524288 (version `00080000`), two machines | Switch NEX (`g2075e100`, `switch-heroes-of-hammerwatch` on 23110/23111/23112, websocket carriage) + Pia P2P | Invite → join into the host lobby, NAT punch at 100ms, both heroes moving in real time in one shared world; ambient time-of-day stays per-client (night host, day joiner) | 2026-10-13 |
| PICO PARK (`01004EA00DF70000`) | Switch update v1.0.8, content 524288 (version `00080000`), two consoles | Switch NEX (`g2c3c9a00`, `switch-pico-park` on 23080/23081/23082), bare-NEX virtual sockets, device-to-device P2P | Host creates, joiner browses, joins with the session key, fetches stations, NAT probes cross both ways; two-player gameplay works | 2026-10-13 |

## PlateUp! — 2026-10-12

- **Owner confirmation:** “it works and harbor can connect to it as well.”
- **Host evidence:** Switch authentication at 17:34:52 UTC; session creation
  tracked to `SUCCEEDED` at 17:34:55; direct Gamesync connection, session
  stream and document writes followed.
- **Join evidence:** a second account authenticated and called
  `JoinGameSession` at 17:35:36 UTC into the Switch-created session. Both
  participants requested ICE allocation at 17:35:37. No RPC error or
  unimplemented service appeared in the inspected host/join window.
- **Deployment:** `openpak-plateup`, tenant `t-a8f1d737-lp1`; tenant/health
  ports 21128/21129 and direct Gamesync TCP 24560. Public TLS/gRPC checks pass.
- **Stack division:** this Switch build selects NPLN lobbies/Gamesync and
  QUIC peer transport. Photon is an alternative platform path, excluded by
  the Switch selection. NPLN also handles the Switch leaderboard API.
- **Still unverified:** sustained restaurant gameplay, Harbor hosting with
  Switch joining, leave/rejoin and reconnect. LeaderboardService is not yet
  implemented by the initial server profile.

Detailed [flow, capture and deployment evidence](https://github.com/openpak/npln/blob/main/titles/plateup/docs/online-flow.md).

## Monopoly for Nintendo Switch — 2026-10-12

- **Owner confirmation:** “its working!”
- **Host evidence:** two proved consoles logged in (title `01007430037F6000`,
  version `00050000`, no `UNPROVEN` fallback) and held ticketed secure
  sessions at 21:18:30/21:18:45 UTC. Host created gid `872035`
  (`max=6 open=true`) at 21:19:54; an earlier browse found 0 sessions and
  the post-create browse found 1.
- **Join evidence:** joiner browsed, joined gid `872035` at 21:20:01
  (`count=1`, full-session echo with key), fetched host stations
  (`0x15/0x29`), both sides ran `replaceURL`, and NAT probe requests
  crossed in both directions with `InitiateProbe` pushes each way
  (21:20:06). Session-part updates followed (21:20:20). No RPC error or
  unimplemented call appeared in the inspected host/join/NAT window.
- **Deployment:** `openpak-switch-monopoly` (image `ghcr.io/openpak/switch-nex:latest`
  at tag `v0.3.39`), auth/secure/health on 23090/23091/23092; Traefik SNI
  `g2e041d00-lp1.s.n.srv.nintendo.net` serves the wildcard cert; secure TCP
  23091 admitted before the host REJECT. Health `ok monopoly` 200; nexprobe
  passes both login methods with the `65c92799` access key.
- **Stack division:** NEX carries login, matchmaking, station exchange and
  NAT traversal. Ubisoft's own HTTPS (`public-ubiservices.ubi.com`:
  profiles, challenges, leaderboards, events) was never called in this
  window and stays out of scope.
- **Still unverified:** a sustained full board game to results,
  leave/rejoin and reconnect, and any Ubisoft-gated entry path.

Server profile and provenance: [Monopoly notes](https://github.com/openpak/switch-nex/blob/main/docs/monopoly.md).

## Full Metal Furies — 2026-10-13

- **Owner confirmation:** "game was played between harbor and switch."
- **Host evidence:** two proved consoles logged in (title
  `010079300AD54000`, version `00050000`, no `UNPROVEN` fallback) and
  held ticketed secure sessions at 10:00:37/10:00:46 UTC over the
  websocket carriage (method 0x6). Host created gid `914033`
  (`max=4 open=true`) at 10:00:51; an earlier browse found 0 sessions
  and the post-create browse found 1.
- **Join evidence:** joiner browsed, joined gid `914033` at 10:01:02
  (`count=1`, full-session echo with key), fetched host stations
  (`0x15/0x29`), both sides ran `replaceURL`, and NAT probe requests
  crossed in both directions with `InitiateProbe` pushes each way.
  The punch succeeded (`rtt=102ms`). Session-part updates followed
  (10:01:07–10:01:33). No RPC error or unimplemented call appeared in
  the inspected host/join/NAT window.
- **Teardown:** host closed at 10:02:33; joiner took the leave
  notifications (3007/4000) and idled out at 10:04:33. Clean
  lifecycle, no ghost session.
- **Deployment:** `openpak-switch-full-metal-furies` (local arm64
  binary mount), auth/secure/health on 23120/23121/23122; Traefik SNI
  `g2c82ee00-lp1.s.n.srv.nintendo.net` serves the wildcard cert;
  secure TCP 23121 admitted and persisted. The SNI and CONNECT key
  (`c093ff57`) are console-measured by this trace.
- **Still unverified:** a sustained full co-op run to results, 3–4
  player sessions, reverse hosting (joiner hosts), leave/rejoin and
  reconnect.

Server profile and provenance: [Full Metal Furies notes](https://github.com/openpak/switch-nex/blob/main/docs/full-metal-furies.md).

## Heroes of Hammerwatch — Ultimate Edition — 2026-10-13

- **Owner confirmation:** both heroes moving in real time in one shared
  world. The only divergence is ambient time-of-day (night on the host,
  day on the joiner) with both device clocks identical (13/10/2026
  09:13 on each).
- **Host evidence:** proved Switch login on method 0x6 (no `UNPROVEN`),
  title `0100D2B00BC54000` version `00080000`, websocket carriage end
  to end. Host created gid `876463` (`max=4 open=false`) at 07:16:10
  UTC; NAT moderate; `replaceURL` stored the host's post-NAT stations.
- **Join evidence:** the invite travelled OpenPak's invitation layer
  (Penne/five `invitation_groups`, inbox polls, mark read — all 200).
  Joiner login, secure connect and Register (cid=2), joined gid
  `876463` at 08:10:08 UTC (explicit join with full-session echo),
  fetched host stations (`0x15/0x29`), both sides ran `replaceURL`,
  `InitiateProbe` pushed both ways and the punch succeeded
  (`rtt=100ms`). No RPC error or unimplemented call in the
  host/join/punch windows.
- **Deployment:** `openpak-switch-heroes-of-hammerwatch` (image
  `ghcr.io/openpak/switch-nex:latest` at tag `v0.3.42`),
  auth/secure/health on 23110/23111/23112; Traefik SNI
  `g2075e100-lp1.s.n.srv.nintendo.net` serves the wildcard cert; secure
  TCP 23111 admitted before the host REJECT; health 23112 in the host
  voice-gathering URLs. External probes pass both login methods over
  the websocket carriage with the CONNECT-verified `1203b5eb` key.
  No version exception: installed v524288 equals the gated latest.
- **Stack division:** NEX carries login, matchmaking, station exchange
  and NAT traversal; gameplay state syncs device-to-device. Ambient
  time-of-day is per-client and cosmetic — nothing the matchmaking
  server sends drives it.
- **Still unverified:** a full dungeon run, 3–4 player sessions,
  reverse hosting (joiner hosts), leave/rejoin and reconnect.

Server profile and provenance: [Heroes of Hammerwatch notes](https://github.com/openpak/switch-nex/blob/main/docs/heroes-of-hammerwatch.md).

## PICO PARK — 2026-10-13

- **Owner confirmation:** two-player gameplay works.
- **Host evidence:** proved Switch login on method 0x6 (friends=3, no
  `UNPROVEN`), title `01004EA00DF70000` version `00080000`, ticketed secure
  session at 09:06:18 UTC. Host created gid `914015` (`max=2 open=true`) at
  09:06:25; NAT moderate.
- **Join evidence:** joiner login (nx-baas `400 Bad Request`, `UNPROVEN`
  name fallback) with ticketed secure session at 09:06:32, browse found the
  1 open session at 09:06:34, joined gid `914015` at 09:06:37 with the
  32-byte session key in the `0x1E` answer (`resp=50B`). Joiner fetched host
  stations (`0x15/0x29`, gid-only, `resp=267B`) at 09:06:40; NAT probe
  requests crossed in both directions (`targets=1 stations=2`) at 09:06:41
  with further probe activity after. No RPC error or unimplemented call in
  the host/join/station/punch windows.
- **Deployment:** `openpak-switch-pico-park` (image
  `ghcr.io/openpak/switch-nex:latest` at tag `v0.3.45`),
  auth/secure/health on 23080/23081/23082; Traefik SNI
  `g2c3c9a00-lp1.s.n.srv.nintendo.net` serves the wildcard cert; secure TCP
  23081 admitted before the host REJECT. Health `ok pico-park` 200.
- **Stack division:** NEX carries login, matchmaking, station exchange and
  NAT traversal; gameplay syncs device-to-device over the bare-NEX virtual
  sockets (no Pia SDK banner; legacy public station shape). The `0x1E`
  join answers the session key as a Buffer per the NEX IDL — the bare bool
  and the full session it replaced were both unparseable game-side.
- **Still unverified:** 3–8 player lobbies, reverse hosting, leave/rejoin
  and reconnect.

Server profile and provenance: [first-batch notes](https://github.com/openpak/switch-nex/blob/main/docs/nex-first-batch.md).
