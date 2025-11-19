# Textum Documentation

This repository contains the documentation for Textum, built with MkDocs.

## Serving Locally

### Using uv

```bash
# install uv if not already installed
pip install uv

# install dependencies
uv pip install -r docs-requirements.txt

# serve documentation locally
uv run mkdocs serve
```

The documentation will be available at `http://127.0.0.1:8000`

### Using pip

```bash
# install dependencies
pip install -r docs-requirements.txt

# serve documentation locally
mkdocs serve
```

## Building

To build the static site:

```bash
mkdocs build
```

Output will be in the `site/` directory.
