# How federation works

Someone in Australia runs a node and gets it approved. From then on, rooms hosted by players in
Australia are served from Australia. Their friends in France join those rooms exactly as before.
Nobody in Australia has an Australian account, an Australian friend list or an Australian
matchmaking server: there is one of each, at openpak.org, and the node in Sydney is only where
the game's packets go.

## The one idea

A room exists on exactly one matchmaking server. Two consoles pointed at two different
matchmaking servers can never see the same room, so if matchmaking were regional, a friend
abroad could never join you. **Matchmaking therefore stays global**: one server per game, at
openpak.org.

What *can* move is anything whose address the console is told **per session** rather than per
hostname, and the transports OpenPak serves already work that way:

| Transport | How the console learns where to go | What a node runs |
| --- | --- | --- |
| Photon-compatible games | The matchmaking server hands out a game-server address per room | A game server (game role only) |
| NPLN games | The session hands out a set of STUN/TURN servers | A TURN relay |
| NEX games | Authentication hands out the secure server; gameplay is peer-to-peer | Nothing |

A node is a **relay tier, nothing more.** It holds no accounts, no friends, no console links and
no room list of its own. If it dies, the rooms on it end and everyone re-matches somewhere else.
Login, friends and matchmaking still cross the ocean once per session; the packets of the game
itself do not.

## The parts

```
                           openpak.org (home)
        ┌──────────────────────────────────────────────────────────┐
        │  account core: the register of nodes and their keys       │
        │  website: the public list of regions, the announce door   │
        │  matchmaking servers: place new rooms on nodes            │
        └──────────────────────────────────────────────────────────┘
                 ▲ announce, once a minute       ▲ room reports
                 │                               │
        ┌────────┴───────────────────────────────┴──────────┐
        │  node "au-sydney" (one or more servers):           │
        │    game server (game role only), TURN relay,       │
        │    announce loop on each server                    │
        └────────────────────────────────────────────────────┘
```

- **The core** keeps the register: each node's id, name, country and region, whether it is
  approved, and for each of its servers a key hash, the services it last announced, its latest
  hardware report and bandwidth self-test, and when it was last seen. A request made with a
  server's key is stamped with that server's node; a node cannot claim to be another.
- **The website** is a node's only door. Each server joins its node once
  (`POST https://openpak.org/api/v1/federation/join`) and then announces itself
  (`POST https://openpak.org/api/v1/federation/announce`) with its own server key, so the core is
  never exposed. `GET https://openpak.org/api/v1/regions` is the public list of nodes in
  rotation, with their region, services and live player counts. Every matchmaking server,
  the status page and the app read it.
- **The matchmaking servers** poll that list once a minute and place new rooms on it.

## Placing a room

1. A player in Sydney signs in. Home looks up which country the player's profile is in, in the
   background, so the answer is ready by the time it is needed. No answer means home.
2. The player creates a room. It is empty and the creator is in Australia, and an approved node
   for Australia runs the game server, so home answers with the **node's** address.
3. The player's console enters the room on the node. The node reports the whole room (who is in
   it and its properties) back to home on every change.
4. A friend in Lyon joins the same room through home. The room already has people in it, so it
   stays where it is: the friend is sent to the **node in Sydney**, whatever their own country.

Three details carry the design:

- **The country is asked early**, so placing a room never waits on it.
- **A room with people in it is wherever it is.** Only an empty room is placed by country. A
  joiner is sent to the room, never to their own region. That is the entire point.
- **A node reports the whole room on every change**, not a delta. A lost report is corrected by
  the next one instead of compounding.

For games that relay through TURN, it is simpler: when a player from a country with a node asks
for its relay servers, it gets that node's TURN and STUN servers; otherwise home's.

## The announce cycle

Once a minute each of a node's servers posts what it runs, with a hardware report, for
example:

```json
{"services":{"photon":"203.0.113.9:22002","turn":"203.0.113.9:3478","stun":"203.0.113.9:3478"}}
```

The core records the server's services and marks it as seen. A server that has not announced
for three minutes takes its node out of rotation: the node drops out of the regions list, and
within another minute the matchmaking servers stop placing rooms there. Rooms already on it keep
going until they end. A daily bandwidth self-test, timed by home, is checked the same way.

A service a node does not run is left out, and home's own is used for it. A node can be
TURN-only, or game-server-only.

## Trust

A node key can only enrol servers, and each server's own key can only announce and self-test.
Neither can read an account, a friend list or a link, and only home can create, approve or
revoke nodes and servers. A compromised server is revoked on its own.

A node does hold shared secrets: the game server's token secret (so tokens home minted validate
on the node) and the TURN secret (because home mints the credentials the relay checks). With
those, a rogue node could mislabel rooms or relay traffic it was sent. It could not touch
anyone's account. That ceiling is why **approval is a person looking before flipping the
switch**.

## What is deliberately not there

- **Nearest by ping.** The node for the player's country wins.
- **Room migration.** A node that dies takes its rooms with it; players re-match.
- **Regional NEX.** NEX gameplay is peer-to-peer, so a regional secure server would split the
  room list for nothing.
- **Data residency.** A region is where you play, not where your data is stored. Every account
  lives in one database at home.

To run one, see [becoming a federation node](become-a-node.md).
