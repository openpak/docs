# The signed redirect ceiling

Every OpenPak client (console setup tools, console DNS, emulators) follows this contract. The
goal: **adding a redirect family is a server change only**, with no new client release, and a
compromised server **cannot widen** what clients redirect.

If you implement it, implement all of it. If the contract has to change, every implementation
changes with it.

## The model

- The **ceiling** is, per platform, the list of domain families a client is allowed to
  redirect. It is a **signed file** fetched at boot.
- It is signed with an **Ed25519 key that never touches a server**. Clients pin the public key.
  The server only serves the signed bytes; it cannot produce new ones.
- The **profile** (`GET /api/v1/network/profile?platform=…`, unsigned) says what to redirect
  *now*. A client applies every profile name that lies inside the verified ceiling and **drops,
  one by one and logged, any name outside it**. It never discards the whole profile because one
  name is outside.
- A list compiled into the client is only the **first-boot fallback**, used when no verified
  ceiling has ever been cached.

## Pinned public key

```
algorithm  Ed25519
public     0fd2a2660868e53d20fc811e3f15710cb1ad157ba7da8019f7a59e8ad604d87c   (hex, 32 bytes raw)
           D9KiZgho5T0g/IEePxVxDLGtFXun2oAZ96WeitYE2Hw=                        (base64)
keyid      36e8bcdd93c2c1a1d7e5d87bbba05a7a4f97882131cf6878f1c053a25a377fe4   (sha256 of the raw key)
```

Clients hold a **list** of pinned keys (one today), so a new key can be added before the old one
is retired.

## Endpoint

`GET https://openpak.org/api/v1/network/ceiling` returns `200 application/json`. It is public,
needs no authentication, and carries `ETag` and `Cache-Control: public, max-age=300`.

**Bootstrap rule:** fetch it from the pinned `openpak.org` origin with normal public TLS trust.
Never through a redirect the client itself installed, never with the OpenPak CA, and never from
a URL taken from the profile.

### Envelope

```json
{
  "payload": "<base64 of the exact payload bytes>",
  "signatures": [ { "keyid": "<hex>", "sig": "<base64 Ed25519 signature over the payload bytes>" } ]
}
```

Verify the signature over the **decoded payload bytes** (never a re-serialisation), then parse
those bytes. Accept if at least one signature is valid under a pinned key with that keyid.

### Payload

```json
{
  "type": "openpak-ceiling",
  "version": 3,
  "issued": "2026-09-24T10:30:00Z",
  "platforms": {
    "switch": [".nintendo.net", ".nintendo.com"],
    "wiiu":   [".nintendo.net", ".nintendowifi.net", ".openpak.org"]
  }
}
```

(Example values. Fetch the endpoint for the real list.)

- `type` must equal `openpak-ceiling`. `version` is a positive integer that grows with every
  signing. Unknown fields are ignored.
- Platform keys are the profile's platform names (`switch`, `wiiu`, `3ds`, `wii`, `ds`, and
  more as platforms are added).
- Each family starts with `.`, is lower case, and has **at least two labels**: `.ea.com` is
  valid, `.com` or a bare public suffix is not. A client rejects the **whole** ceiling file if
  any entry is malformed. A family covers its apex and everything below it (`.ea.com` covers
  `ea.com` and `x.ea.com`).

## Client rules

1. **Boot.** Load the cached ceiling (re-verify its signature on load), fetch a fresh one (2 s
   timeout, no retry loop, never block the console or emulator), verify it, and accept it only if
   its `version` is **at least the highest version ever accepted**. Persist that number: it is
   the rollback protection. Then fetch the profile and filter it through the ceiling for the
   client's own platform.
2. **Failure.** A bad signature, unknown keyid, malformed file, lower version or timeout keeps the
   cached verified ceiling; with none, the compiled fallback. Log the reason once.
3. **Cache.** Store the envelope bytes exactly as received, write atomically, and restrict the
   file's permissions where the platform has them.
4. **Change notice, for the affected platform only.** At boot, record a digest of the
   *effective* redirect set for the client's platform: the sorted list of applied entries after
   filtering. While running, re-check ceiling and profile every **6 hours** (±10 % jitter) and
   after an OpenPak sign-in. If the digest changes, show **one** notice per new digest, along
   the lines of *"OpenPak updated this system's network redirects. Restart the game (or the
   emulator) to use them."* A change to another platform's list never changes this platform's
   digest, so it never notifies.
5. **Consoles** cannot be told in the background. The setup tool shows the same notice when it
   is opened and the set it would install differs from the installed one. Consoles that use
   OpenPak's console DNS need nothing: the resolver re-reads on its own.

## Server side

- The ceiling is edited and signed **offline**, on a machine that holds the private key, with a
  tool that bumps `version` and writes the envelope. The signed file is then copied to the
  server, which serves it unchanged.
- The profile generator and the console DNS validate platform families against the signed
  ceiling, so adding a family needs no server release either.
- Adding a family, end to end: add it to the ceiling and sign, publish the signed file, add the
  family to the platform map the profile is generated from. Clients pick it up at their next
  boot; running ones show the notice.
