# Linking a Switch, end to end

How a console gets attached to an OpenPak account, what each screen is for, and where the code
lives. The flow spans three services and two very different screens, and none of it is
guessable from any single repository. For the player's view, see [your account](../players/account.md).

## The shape of it

```
console browser                     phone browser                  services
──────────────                      ─────────────                  ────────
GET /connect/1.0.0/authorize   ─────────────────────────────────▶  nx-baas: shows a QR and,
  shows QR + waits                                                 once claimed, a 6-digit code
                                    scan QR → /link?p=<pair>  ───▶ nx-baas: sign-in page
                                    POST /link (e-mail+pass)  ───▶ account core: verify
                                    POST /link/code (123456)  ───▶ nx-baas: claim the code
POST /connect/1.0.0/qr/approve ─────────────────────────────────▶  nx-baas: approve, mint code
  person approves on the console
POST /connect/1.0.0/api/token  ─────────────────────────────────▶  nx-baas: NA tokens
GET  /2.0.0/users/me           ─────────────────────────────────▶  nx-baas: NA account object
POST /1.0.0/federation         ─────────────────────────────────▶  nx-baas + core: the link
POST /1.0.0/login              ─────────────────────────────────▶  the reply the console parses
POST /1.0.0/image_upload       ─────────────────────────────────▶  profile picture → account
```

## Why approval is on the console

Scanning a square proves you have a phone, not that you are sitting in front of that console.
The QR carries a **pairing id only**: it identifies the console's session and grants nothing.
The code is revealed on the console *after* someone signs in on the phone, typed back there,
and then approved on the console. So an onlooker with a photograph of the screen has a login
page; someone who signs in still needs the code from the screen; and the code still needs
approval from whoever holds the controller.

## The code

Six digits, shown as `123 456` because six in one run is easy to lose your place in from across
a room. Digits only, so the phone gets a numeric keypad and no letter can be mistaken for a
digit. Ten minutes, single use.

Six digits is one in a million, which is fine for something short-lived that also needs console
approval: **but only because guessing is capped**: ten wrong codes per account buys a
ten-minute wait. Keyed by the account rather than the session cookie, since a counter you can
reset by clearing a cookie is not a limit. The generator uses rejection sampling; a plain
modulo over 256 would make 0-5 likelier than 6-9.

## Two screens, two designs

The same stylesheet serves both, split by a body class, because they are read at completely
different distances:

| | Console | Phone |
| --- | --- | --- |
| Read from | a sofa, ~2 m | arm's length |
| Layout | QR and steps side by side (720p is wide and short) | one column |
| The code | the largest thing on screen | typed, not read |
| Input | a controller: visible focus ring, 60px targets | touch: 44px targets, 16px minimum |
| Edges | padded clear of the crop a television applies | normal |

Both follow the reader's system light/dark setting, and both carry their CSS **inline**: a
console browser may have no route to the website, and a link page that loses its styling at
exactly that moment is worse than one that carries its own copy.

## Where things live

| Piece | File |
| --- | --- |
| Console page (QR, code, approve) | `nx-baas/main.go`, `authorizePage` |
| Phone pages (sign in, confirm, done) | `nx-baas/link.go` |
| Codes, pairings, guess cap | `nx-baas/link.go` |
| The reply the console parses | `nx-baas/main.go`, `userObj` + the `/1.0.0/login` case |
| Profile picture hand-off | `nx-baas/avatar.go` → website `POST /internal/avatar` |

## Looking at it without a console

```sh
cd nx-baas && PREVIEW_DIR=scratch/link go test -count=1 -run DumpLinkPages .
chromium --headless --window-size=1280,720 --screenshot=scratch/console.png file://$PWD/scratch/link/link-console.html
chromium --headless --window-size=390,760  --screenshot=scratch/phone.png   file://$PWD/scratch/link/link-signin.html
```

The console page must be judged at 1280×720; every other page here at 390.
