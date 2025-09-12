# Project Source Combiner

Create a single text archive of your project’s source code. 

This script walks a project directory, skips typical non-functional files and binaries, extracts code and Markdown from notebooks, and writes everything to one file with per-file tags.

* Default output: `full_project_source.txt`

* Default project root: parent of the script’s directory (assumes the script lives in `tools/`). Falls back to current working directory if `__file__` is unavailable.

## Why this exists

* Share a compact snapshot of the codebase (for code review, compliance, or AI ingestion).

* Diff code snapshots between releases.

* Search/reference the whole project from a single file.

## Features

* Skips common noise: VCS folders, caches, virtualenvs, build artifacts, `node_modules`, etc.

* Ignores binary files by extension and by sniffing for null bytes in the first 1 KB.

* Smart directory exclusion:

* Anywhere: `.git`, `__pycache__`, `node_modules`, …

    * Root-only: `data` at the project root is excluded, but nested `src/app/data` is kept.

    * Pattern-based: directories ending with `.egg-info`.

* Jupyter notebooks (`.ipynb`):

    * Outputs only code and markdown cells.
  
    * Strips all outputs.

    * Labels cells as `# --- Code Cell N ---` or `# --- Markdown Cell N ---`.

* Safe file reads: UTF-8 with `errors="replace"` to avoid crashes on odd encodings.

* Deterministic output ordering (directories and filenames sorted).

## Requirements

* Python: 3.9+ (uses modern type hints like `tuple[str, ...]`).

* Dependencies: Standard library only.

## Installation

Place the script in `tools/` at the project root, or anywhere you prefer.
