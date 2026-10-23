# Building and running a service

Every repository's README is the authority for that repository. This page is the common
pattern, so the READMEs make sense.

## What you need

- **Go** (the version in each repository's `go.mod`) for most services.
- **PostgreSQL** for services that keep state. Migrations apply automatically at startup.
- **Podman or Docker** for test databases and container builds.
- Some game servers are C# (.NET); emulators and console clients use their own toolchains
  (CMake/Ninja, devkitPro, Flutter). Their READMEs say what.

## Run a Go service

The core services follow one shape. For the account core:

```sh
git clone https://github.com/openpak/account
cd account
cp example.env .env          # then fill in the required values
set -a; source .env; set +a
go run ./cmd/account
```

`example.env` lists every variable with a comment, marks which are required, and uses
placeholder secrets you must replace. **Never commit `.env`.** Secrets that are shared between
services (for example the core's internal key) must match on both sides.

Most services then need the core. A minimal local stack is:

1. PostgreSQL.
2. `account`, the core (HTTP and internal gRPC).
3. `website`, pointed at the core with the same internal key (`CORE_INTERNAL_KEY` must equal
   the core's `ACCOUNT_INTERNAL_KEY`).
4. Whatever adapter or game server you are working on.

The [port plan](ports.md) gives every service a fixed block of ports, so a local stack does not
collide with itself. [Deploying](../self-hosting/deploy.md) has a compose file for the core
pieces.

## Tests

For Go services the definition of done is:

```sh
go vet ./...
go test -race ./...
```

Services with a database also have integration tests behind a build tag, run against a
throwaway PostgreSQL:

```sh
docker run -d --name openpak-pg-test -e POSTGRES_PASSWORD=test \
  -e POSTGRES_DB=account_test -p 54329:5432 postgres:18-alpine
go test -tags integration -race -count=1 ./...
```

The integration tests drop and recreate the schema of the test database. Never point them at a
database you care about.

## Shared Go code

Shared code lives in library repositories (for example `nx-common`, `x360-common`,
`xb-common`). A service consumes one with a `replace` directive and a committed `vendor/` tree,
so it builds on its own, in CI and on your machine, without a sibling checkout. If you work on
several modules at once, a local `go.work` is fine; CI ignores it.

## Looking at pages without a console

Console-facing pages (such as the Switch link pages) and the website can be rendered to files
by a test, so they can be checked in a browser at the sizes that matter: a phone (390 px wide),
a desktop (1280 px) and, for console pages, 1280×720. The repository README gives the exact test
name.

## Emulators and console clients

These build with their upstream toolchains, described in each README:

| Repository | Build |
| --- | --- |
| `harbor` | CMake and Ninja (desktop), Gradle (Android), following Eden's build guide |
| `openpak-nro` | devkitA64 in a container: `podman run --rm -v "$PWD":/src -w /src docker.io/devkitpro/devkita64 make`; `make test` checks the logic on the host |
| `nn-inkay` | devkitPPC and wut, or the repository's container build |
| `nn-nimbus` | `docker/build.sh` builds the toolchain image and the app |
| `app` | Flutter: `flutter pub get`, `flutter test`, `flutter run` (add `--dart-define=OPENPAK_BASE_URL=...` for a local stack) |

Some emulator forks depend on the shared `openpak-client` library, which is not public yet;
their READMEs say when that blocks an outside build.
