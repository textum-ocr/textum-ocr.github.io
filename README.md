# Textum Documentation

This repository contains the documentation for Textum, built with MkDocs.

NOTE: The source code for the Textum application itself can be found here: https://git.informatik.uni-leipzig.de/textum/app

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
