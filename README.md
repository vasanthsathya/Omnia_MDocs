# Omnia MD Documentation

This is the MkDocs-based documentation using Markdown files.

## Structure

- `docs/` - Source files (Markdown format)
- `site/` - Generated HTML output
- `mkdocs.yml` - MkDocs configuration
- `requirements.txt` - Python dependencies

## Build Instructions

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Build Documentation

```bash
mkdocs build
```

### Serve Documentation (for development)

```bash
mkdocs serve
```

Then open http://127.0.0.1:8000 in your web browser.

## Theme

This documentation uses the Material for MkDocs theme.

## Configuration

Main configuration is in `mkdocs.yml`.