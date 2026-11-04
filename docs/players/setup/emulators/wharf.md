# Wharf (Xbox 360)

Wharf is OpenPak's Xbox 360 emulator, built on Xenia Edge. It boots the console's own
dashboard and connects it to OpenPak's Xbox 360 services.

## Status

**Experimental. Dashboard sign-in works.** On 2026-11-03 the dashboard signed in to OpenPak
end to end: the Xbox Live connection test passes, sign-in finishes, and you appear online to
your friends on other OpenPak consoles. That is as far as it has been tested.

Not verified: playing any game online, messages, matchmaking, and the dashboard's online
modules. Many games do not run in the emulator at all, and the Xbox Live sign-up screens
("Join Xbox Live") do not work, so use an account you made at [openpak.org](https://openpak.org).

## Downloads

There is no public download yet: no tagged release and no nightly build exist for Wharf.
Wharf can only be built from source for now
([github.com/openpak/wharf](https://github.com/openpak/wharf)).

## Sign in to OpenPak

Wharf has no login window of its own. Use the dashboard's normal Xbox Live sign-in with your
OpenPak account; Wharf sends the console's traffic to OpenPak, so you do not change any DNS
setting.

## Known limits

- No game has been played online.
- Controller input in the dashboard is incomplete.
- You supply the console's system files and your own games. Third-party launchers such as
  Aurora are your own choice and are not part of OpenPak.

Issues: [github.com/openpak/wharf/issues](https://github.com/openpak/wharf/issues). Say which
build you used and what you saw.
