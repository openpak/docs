# Reporting bugs

Clear reports from real consoles and games are the most useful contribution OpenPak can get
during the alpha.

## Where to report

| Problem | Where |
| --- | --- |
| A game does not work | An issue in the repository that serves it. The game's entry on [openpak.org/titles](https://openpak.org/titles) says which service that is. |
| The website or your account | An issue in [`website`](https://github.com/openpak/website) or [`account`](https://github.com/openpak/account). |
| A console setup tool or an emulator | An issue in that repository (for example [`openpak-nro`](https://github.com/openpak/openpak-nro/issues) or [`harbor`](https://github.com/openpak/harbor/issues)). Report OpenPak fork problems to the fork, not upstream. |
| Not sure | Sign in and use [openpak.org/help](https://openpak.org/help); the team moves it to the right place. |
| A security problem | **Never in public.** See below. |

The organisation's [CONTRIBUTING](https://github.com/openpak/.github/blob/main/CONTRIBUTING.md)
and [SUPPORT](https://github.com/openpak/.github/blob/main/SUPPORT.md) pages say the same, in
more detail.

## What to include

- The console or emulator, and its version (for an emulator, also the platform and GPU driver).
- The system firmware version.
- The game, its version and region.
- The error code shown, exactly as shown.
- What you did just before it happened, and whether it happens every time.
- Logs and screenshots, if you have them.

**Never attach** game files, firmware, keys, `prod.keys`, PRODINFO or console dumps.

## Security issues

Report vulnerabilities privately, following the
[security policy](https://github.com/openpak/.github/blob/main/SECURITY.md):

- Preferred: GitHub's **Report a vulnerability** button on the affected repository's Security
  tab.
- Or email [contact@openpak.org](mailto:contact@openpak.org) with "Security" in the subject.

Include the affected service, what an attacker can do and how to reproduce it. A proof of
concept against your own account is fine. Do not access other people's accounts or data, do not
degrade the service for others, and do not keep data you come across.
