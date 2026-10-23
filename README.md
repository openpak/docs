# OpenPak docs

The public documentation for [OpenPak](https://openpak.org), published at
[docs.openpak.org](https://docs.openpak.org). It is written for three readers: players,
contributors, and people who run their own OpenPak network or a federation node.

## Working on it

The site is built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).
Pages are Markdown files under `docs/`; the navigation is in `mkdocs.yml`.

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve          # preview at http://127.0.0.1:8000
.venv/bin/mkdocs build --strict # what CI runs
```

Every push to `main` is checked with `mkdocs build --strict` on GitHub and deployed by Cloudflare Workers Builds (`wrangler.jsonc` serves the built `site/`).

## Rules for pages

- Say what works today and what does not. If a step is not known or not ready, write
  "not ready yet" rather than guessing.
- Never include game files, firmware, keys or console data, or instructions for obtaining
  them. Players use their own console and their own games.
- No internal hostnames, addresses or dated work notes. This is documentation, not a log.

## License

The text is licensed [CC BY-SA 4.0](LICENSE). OpenPak's code lives in its own repositories
under their own licences (AGPL-3.0-only for OpenPak's servers).
