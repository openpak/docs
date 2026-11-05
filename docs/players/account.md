# Your account

One OpenPak account covers every console and emulator you link to it.

## Create an account

1. Go to [openpak.org/register](https://openpak.org/register).
2. Enter an email address you control, a password, and your handle. **The handle is
   permanent**; your display name can be changed later.
3. Confirm your email address with the link OpenPak sends you. Links expire after 24 hours;
   you can ask for a new one from your account page.
4. Sign in at [openpak.org/login](https://openpak.org/login).

You must be at least 16. Consoles ask for a country and a date of birth when they link; the
date of birth is how the minimum age is checked.

If you forget your password, use **Forgot password** on the sign-in page and follow the
emailed link.

## Turn on two-step sign-in (recommended)

On your [account page](https://openpak.org/account), turn on two-factor sign-in. Add the key to
an authenticator app, type the code it shows, and store the recovery codes somewhere safe.
From then on, signing in asks for a code from the app, or one of the recovery codes.

!!! note
    The Harbor emulator's first-run account page cannot finish a two-factor sign-in yet.
    Choose **Later** there and link the user from the emulated console's settings instead,
    which does support it. The Switch console link supports two-factor sign-in.

## Link a console or emulator

Linking attaches a console user (or an emulator profile) to your account and gives it a friend
code. How you link depends on the platform:

| Platform | How it links |
| --- | --- |
| Switch (console) | From the console's own account screens. See below. |
| Harbor (Switch emulator) | The first-run setup has an OpenPak account page: **Sign in**, **Create account** or **Later**. You can also link from the emulated console's settings, as on a real Switch. |
| Wii U | With the OpenPak Wii U Patcher installed, the console's own Nintendo Network ID screens talk to OpenPak. Link an existing ID with your OpenPak password. See below. |
| 3DS | Sign in from the OpenPak 3DS Patcher app (see the [3DS setup](setup/3ds.md)). Not yet verified on hardware. |
| Wii and DS | These consoles have no login of their own and play online only once linked. Connect in any game: it is refused and shows a code (Mario Kart Wii: an 8-character code; other games: an error code from 24000 to 29999). Enter it at [openpak.org/link](https://openpak.org/link) from the same Wi-Fi (or add the name you play as), then connect again. See [Wii](setup/wii.md) and [DS](setup/ds.md). |
| Other OpenPak emulators | Sign in from the emulator's OpenPak menu. |

### Linking a Switch

The Switch links through its normal account-linking flow, which OpenPak answers instead of the
vendor:

1. On the console, open **System Settings → Users**, pick the user and choose
   **Link Nintendo Account**.
2. The console shows an OpenPak page with a QR code. Scan it with your phone and sign in with
   your OpenPak account (and your two-step code, if you use one).
3. The console then shows a **six-digit code**. Type it on your phone.
4. Approve the link on the console.

Codes are valid for ten minutes and work once. Approval happens on the console on purpose: a
photo of the screen is not enough to link someone else's account.

### Linking a Wii U

On the Wii U your OpenPak password **is** your console password. Your account already has a
Wii U Network ID (the same name as your OpenPak handle). There is nothing to create on the
console, you only link the existing ID.

1. **Once, on openpak.org:** sign out and back in. OpenPak can only prepare your console
   password while it sees you type your password, so every account needs one fresh sign-in on
   the website or in the app. After that it stays in step on its own: signing in and changing
   your password keep the console password the same as your OpenPak password. (A password
   reset does too, the next time you sign in.)
2. Open your [account page](https://openpak.org/account) and find **Linked platforms → Sign in
   on a Wii U or 3DS**. It shows the **Network ID** to type.
3. On the Wii U, open **System Settings → Users**, pick the user (or create a new user) and
   choose **Link Nintendo Network ID**, then **Link an existing ID**.
4. Type the Network ID shown on your account page and your OpenPak password.

If your OpenPak password cannot be typed on a Wii U (longer than 16 characters, accented
letters, a space, or it contains your Network ID), the account page says so and offers
**Set a separate console password**. That one is 6 to 16 letters, digits and keyboard symbols,
without spaces or accents, and must not contain your Network ID. You confirm it with your
OpenPak password (and your two-step code, if you use one). The app has the same setting in
its account details.

!!! note
    The menu names above are the Wii U's own and can differ slightly between languages and
    system versions. The 3DS uses the same Network ID and password.

## See and revoke links

Your [account page](https://openpak.org/account) lists every linked console and emulator under
**Linked platforms**, and every signed-in browser, app or device. **Revoke link** detaches a
console; signing out a device ends that session. The companion app shows the same lists.

## Your friend codes

A console gets a friend code when it links. Your codes are on your account page, and friends
can add you with them from the website, the app or a console. See
[friends and chat](friends.md).

## Delete your account

See [privacy and account deletion](privacy.md).
