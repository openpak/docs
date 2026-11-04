# Xbox (original)

OpenPak is building replacement services for the original Xbox's Xbox Live. The console reaches them through its DNS setting.

!!! warning "Early stage"
    Some of the services are running, but no real original Xbox has been verified and the **OpenPak Xbox Patcher** is not available yet. Expect problems.

## What you need

- The console on your home network, online.
- Your OpenPak account ([create one](../account.md)).

## Set the console's DNS

OpenPak's DNS server is **145.241.199.19**. Set it as the console's DNS and leave every other
network setting automatic.

1. In the dashboard, open **Settings** > **Network Settings**.
2. Open **TCP/IP Settings** (or **Configure**) and set **DNS** to **Manual**.
3. Enter **145.241.199.19** as the **Primary DNS**. Enter the same address as the **Secondary DNS**. Leave IP address, subnet mask and gateway as they are.
4. Save and run the network test.

OpenPak's own names are answered for everyone. For any other name, the server answers only
consoles that have already asked for an OpenPak name, so a console using it keeps working on
the rest of the internet. Do not put this address on a PC or phone: it will refuse ordinary
lookups from a device that never asked for an OpenPak name.

## Undo

Set the DNS setting back to automatic (or to your router's address).

Berth, the Xbox emulator, does not need this setting. See [Berth](emulators/berth.md).
