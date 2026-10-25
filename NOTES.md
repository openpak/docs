# Notes: docs

Moved from the previous README verbatim. This file is outside `docs/`, so MkDocs does not publish it.

The public documentation for [OpenPak](https://openpak.org), published at
[docs.openpak.org](https://docs.openpak.org). It is written for three readers: players,
contributors, and people who run their own OpenPak network or a federation node.

## Rules for pages

- Say what works today and what does not. If a step is not known or not ready, write
  "not ready yet" rather than guessing.
- Never include game files, firmware, keys or console data, or instructions for obtaining
  them. Players use their own console and their own games.
- No internal hostnames, addresses or dated work notes. This is documentation, not a log.

## Deployment

Every push to `main` is checked with `mkdocs build --strict` on GitHub and deployed by Cloudflare Workers Builds (`wrangler.jsonc` serves the built `site/`).
