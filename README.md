# Textum Documentation

This repository contains the documentation for Textum, built with MkDocs.

## Serving Locally

```bash
# install dependencies
uv sync
# serve documentation locally
uv run mkdocs serve
```

The documentation will be available at `http://127.0.0.1:8000`

## Building

To build the static site:

```bash
uv run mkdocs build
```

Output will be in the `site/` directory.
