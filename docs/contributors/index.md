# Contributing to OpenPak

Thanks for helping. OpenPak is in public alpha, and the most useful things right now are clear
bug reports and test results from real consoles and games. Code is welcome too.

## Where to start

- [Architecture](architecture.md): how the pieces fit, and why the account core knows nothing
  about consoles.
- [Repositories](repositories.md): one repository per service, and how to find the right one.
- [Building and running](building.md): getting a service running on your machine.
- [Conventions](conventions.md): licences, repository layout, testing and commits.
- [Clean-room rule](clean-room.md): what you may and may not use as input. Read this before
  writing any server code.
- [Online compatibility](online-compatibility.md): the method for bringing a game online.
- [Signed redirect ceiling](signed-ceiling.md) and [port plan](ports.md): two shared contracts.
- [Reporting bugs](reporting.md): what to include, and where security reports go.

## The short version of the rules

1. Open an issue first for anything bigger than a small fix, so the approach is agreed before
   you spend time on it.
2. One change per pull request. Run the repository's tests.
3. Never commit game files, firmware, keys, certificates, captures, dumps, player data or
   decompiled code.
4. Never copy code across a licence wall. Facts are fine; code is not.
5. Write commit messages in the imperative: what changed and why.

## The name and logo

The code is AGPL-3.0, and anyone may run it. Only OpenPak and its approved federation nodes may
use the name "OpenPak" and the logo. A fork or independent network must use its own name, and
may say it is "based on OpenPak software".

The organisation-wide [CONTRIBUTING](https://github.com/openpak/.github/blob/main/CONTRIBUTING.md)
and [Code of Conduct](https://github.com/openpak/.github/blob/main/CODE_OF_CONDUCT.md) apply to
every repository.
