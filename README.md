# AI Engineering Roadmap

A public, hands-on knowledge base and portfolio for becoming an AI Engineer,
built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Local development

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install mkdocs-material
mkdocs serve          # preview at http://127.0.0.1:8000
```

## Adding an article

1. Create a Markdown file under the relevant stage folder in `docs/`.
2. Add tags at the top of the file:
   ```yaml
   ---
   tags:
     - RAG
   ---
   ```
3. Link it from that stage's `index.md`.

## Deploy

```bash
mkdocs gh-deploy      # builds and pushes to the gh-pages branch
```
