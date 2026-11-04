# Xbox 360

OpenPak runs replacement services for Xbox Live on Xbox 360: sign-in, presence, matchmaking and statistics. A real console reaches them through its DNS setting.

!!! warning "Early stage"
    The servers are running and have been tested with the Wharf emulator. A real Xbox 360 has not been verified, and the **OpenPak Xbox 360 Patcher** is not available yet. Expect problems and report them.

## What you need

- The console on your home network, online.
- Your OpenPak account ([create one](../account.md)).

## Set the console's DNS

OpenPak's DNS server is **145.241.199.19**. Set it as the console's DNS and leave every other
network setting automatic.

1. Press the Guide button, then open **Settings** > **System Settings** > **Network Settings**.
2. Choose your network (wired or wireless), then **Configure Network**.
3. Open the **DNS Settings** tab and choose **Manual**.
4. Enter **145.241.199.19** as the **Primary DNS Server**. Enter the same address as the **Secondary DNS Server**.
5. Press B to save, then choose **Test Xbox Live Connection**.

OpenPak's own names are answered for everyone. For any other name, the server answers only
consoles that have already asked for an OpenPak name, so a console using it keeps working on
the rest of the internet. Do not put this address on a PC or phone: it will refuse ordinary
lookups from a device that never asked for an OpenPak name.

## Undo

Set the DNS setting back to automatic (or to your router's address).

Wharf, the Xbox 360 emulator, does not need this setting. See [Wharf](emulators/wharf.md).
