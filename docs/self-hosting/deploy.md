# Deploying

A generic way to run the core of an OpenPak network with Podman (or Docker) and Compose. It is a
starting point for your own deployment, not a copy of how openpak.org is run.

!!! note
    This page brings up the core (database, account core, website). Adding a console family
    or a game server follows the same pattern, with that repository's `example.env` and README.

## 1. Get the sources

```sh
mkdir openpak && cd openpak
git clone https://github.com/openpak/account
git clone https://github.com/openpak/website
```

## 2. Write the environment

Each repository's `example.env` lists every setting with a comment. Start from them:

```sh
cp account/example.env account.env
cp website/example.env website.env
```

Then set at least these. Generate every secret with something like `openssl rand -base64 48`.

`account.env`:

```sh
ACCOUNT_DATABASE_URL=postgres://openpak:<db password>@db:5432/account?sslmode=disable
ACCOUNT_SESSION_SECRET=<32+ random bytes>
ACCOUNT_INTERNAL_KEY=<32+ random bytes, shared with internal callers>
ACCOUNT_HTTP_ADDR=:20000
ACCOUNT_GRPC_ADDR=:20001
ACCOUNT_ENVIRONMENT=production
# Outbound email is required in production (verification and reset mails).
ACCOUNT_SMTP_HOST=<your mail relay>
ACCOUNT_SMTP_PORT=587
ACCOUNT_SMTP_USERNAME=<user>
ACCOUNT_SMTP_PASSWORD=<password>
ACCOUNT_SMTP_FROM=<the From address>
# Where links in those mails point: your website's public address.
ACCOUNT_EMAIL_LINK_BASE=https://<your domain>
```

`website.env`:

```sh
WEBSITE_HTTP_ADDR=:20010
WEBSITE_ENVIRONMENT=production
WEBSITE_DATABASE_URL=postgres://openpak:<db password>@db:5432/website?sslmode=disable
WEBSITE_SESSION_SECRET=<32+ random bytes>
CORE_BASE_URL=http://account:20000
CORE_GRPC_ADDR=account:20001
CORE_INTERNAL_KEY=<the same value as ACCOUNT_INTERNAL_KEY>
WEBSITE_ADMIN_ACCOUNT_IDS=<your account id, once you have registered>
```

Settings left empty switch their feature off, and the site says so instead of failing. Never
commit these files.

## 3. Compose file

Save as `compose.yml` next to the two checkouts:

```yaml
services:
  db:
    image: docker.io/library/postgres:18-alpine
    restart: unless-stopped
    environment:
      POSTGRES_USER: openpak
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: account
    volumes:
      - db-data:/var/lib/postgresql/data
      - ./initdb:/docker-entrypoint-initdb.d:ro

  account:
    build: ./account
    restart: unless-stopped
    env_file: account.env
    depends_on: [db]

  website:
    build: ./website
    restart: unless-stopped
    env_file: website.env
    depends_on: [account]
    ports:
      - "127.0.0.1:20010:20010"   # only your TLS terminator should reach this
    volumes:
      - website-storage:/app/storage

volumes:
  db-data:
  website-storage:
```

The website keeps its own database. Create it on first start with an init script:

```sh
mkdir initdb
echo 'CREATE DATABASE website;' > initdb/10-website.sql
```

## 4. Start it

```sh
export DB_PASSWORD=<db password>
podman compose up -d --build      # or: docker compose up -d --build
podman compose logs -f website
```

Check health:

```sh
curl -s http://127.0.0.1:20010/healthz
```

The core answers `/healthz` and `/readyz` on its HTTP port inside the compose network.

## 5. Put TLS in front

Publish the website through a TLS terminator on your own domain (Traefik, Caddy, nginx). Keep
the core, its gRPC port and every metrics port private. Console-facing names are served by the
adapters, never by the website, so give them their own routes when you add adapters.

## 6. First account and admin

Register on your site, confirm the email (the core sends it through the SMTP relay you set),
find your account id on your account page, put it in
`WEBSITE_ADMIN_ACCOUNT_IDS` and restart the website. `/admin` then opens for you.

## Adding more

- **A console family:** clone its adapter (for example `nx-baas`, `nn-account`), copy its
  `example.env`, give it the core's internal key, and add it to the compose file with the ports
  from the [port plan](../contributors/ports.md).
- **A game server:** the same, from the game-server repository's README.
- **Ports from outside:** only game transport ports, the fixed console ports and 80/443. See
  the [port plan](../contributors/ports.md).

Health endpoints on every service let you wire up any monitor. Run the status page somewhere
other than the machine it watches: a status page on the box it monitors reports "up" right
until it cannot report at all.
