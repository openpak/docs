# Azahar for OpenPak (3DS)

A fork of Azahar that points the emulated console's HTTP traffic at OpenPak and adds the
shared OpenPak sign-in, menu and cloud saves.

## Status

**Not ready yet.** None of it has been run against a game. This fork is transitional: a
successor is planned, and no build is advertised from it until then.

## Downloads

- **Release:** [github.com/openpak/azahar/releases/latest](https://github.com/openpak/azahar/releases/latest),
  once a tagged release exists.
- **Nightly:** the rolling [`nightly` pre-release](https://github.com/openpak/azahar/releases/tag/nightly),
  rebuilt when the source changes. It is untested: use it to follow progress, not to play.

## Sign in to OpenPak

1. Sign in from the **OpenPak** menu (left of Help).
2. Turn on the connection under **Configure → General → OpenPak**. It cannot be changed while a
   game runs.

## Known limits

- Azahar does not emulate NEX, so friends and online play are not available in it; it covers
  the account and content side only.
- The fork retires once its successor lands.

Issues: [github.com/openpak/azahar/issues](https://github.com/openpak/azahar/issues). Say which
build you used (release or nightly) and what you saw.
