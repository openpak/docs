# PlayStation 3

OpenPak runs a replacement for PlayStation Network sign-in and the PS3 services around it. A real console reaches them through its DNS setting.

!!! warning "Early stage"
    The servers are running and have been tested with the Pier emulator. A real PS3 has not been verified, and the **OpenPak PS3 Patcher** is not available yet. Expect problems and report them.

## What you need

- The console on your home network, online.
- Your OpenPak account ([create one](../account.md)).

## Set the console's DNS

OpenPak's DNS server is **145.241.199.19**. Set it as the console's DNS and leave every other
network setting automatic.

1. Open **Settings** > **Network Settings** > **Internet Connection Settings** and press X on **Custom** (answer **Yes** if asked to disconnect).
2. Choose **Wired Connection** or **Wireless**, and keep the usual choices (for wireless, pick your network and enter its key).
3. For **IP Address Setting** choose **Automatic**, for **DHCP Host Name** **Do Not Set**.
4. For **DNS Setting** choose **Manual**. Enter **145.241.199.19** as **Primary DNS** and the same address as **Secondary DNS**.
5. For **MTU** and **Proxy Server** choose **Automatic** and **Do Not Use**, then save and run **Test Connection**.

OpenPak's own names are answered for everyone. For any other name, the server answers only
consoles that have already asked for an OpenPak name, so a console using it keeps working on
the rest of the internet. Do not put this address on a PC or phone: it will refuse ordinary
lookups from a device that never asked for an OpenPak name.

## Undo

Set the DNS setting back to automatic (or to your router's address).

Pier, the PS3 emulator, does not need this setting. See [Pier](emulators/pier.md).
