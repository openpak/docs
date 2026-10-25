# Docs

OpenPak's Docs.

| | |
| --- | --- |
| Site | [docs.openpak.org](https://docs.openpak.org) |
| Built with | MkDocs, with the Material theme |
| Licence | CC BY-SA 4.0 (text) |

## Contributing

Pages are Markdown files under `docs/`; the navigation is in `mkdocs.yml`. Page rules are in [NOTES.md](NOTES.md).

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve          # preview at http://127.0.0.1:8000
.venv/bin/mkdocs build --strict # what CI runs
```

## Licence

The text is licensed [CC BY-SA 4.0](LICENSE). OpenPak's code lives in its own repositories
under their own licences (AGPL-3.0-only for OpenPak's servers).
