# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Course materials for the Zero to Mastery Machine Learning course: Jupyter notebooks, markdown lessons, datasets, images and slide PDFs. There is no application code, package, test suite or linter. The "build" is an MkDocs site (the online course book at dev.mrdbourke.com/zero-to-mastery-ml).

## Layout and notebook conventions

- `section-1-…` → `section-4-…`: course sections in chronological order (concepts/setup → pandas/NumPy/Matplotlib/Scikit-Learn → structured data projects → TensorFlow/Keras deep learning). `communicating-your-work.md` at the root is the final module.
- Notebook filename suffixes carry meaning (see each section's `README.md`):
  - `introduction-*` — starting point for each tool module.
  - `*-video.ipynb` — code written live in the video lectures; keep in sync with the videos, don't "improve" them.
  - No `-video` suffix — annotated versions with extra explanation.
  - `-v1` / `-v2` — versions; higher is newer. `-OLD` — deprecated/broken, kept for reference only; ignore.
  - `*-exercises.ipynb` / `*-exercises-solutions.ipynb` — paired exercise/solution notebooks.
- `data/` holds all course datasets. Notebooks load them via relative paths (`../data/heart-disease.csv`) or via `https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/...` so they also work in Colab. Run notebooks from inside their section folder so `../data` resolves.
- The bulldozer dataset ships as `data/bluebook-for-bulldozers.zip`; its unzipped contents and derived `*.parquet` files are gitignored, as are `*.pkl`/`*.joblib` model files.

## Docs site (MkDocs)

`docs/` contains **copies** of source files, not the originals. The canonical sources live in the section folders, `communicating-your-work.md` and `images/`. Edit the source, then re-copy — don't edit `docs/*.ipynb` directly. Exceptions not handled by the copy step: `docs/index.md` (docs-only) and `docs/a-6-step-framework-…md` (a separate copy of the section-1 file; update both by hand).

Preview locally (requires `pip install mkdocs-material mkdocs-jupyter`):

```bash
./make_docs.sh   # copies notebooks/markdown/images into docs/ then runs `mkdocs serve`
```

- Site nav is defined in `mkdocs.yml`; notebooks render via the `mkdocs-jupyter` plugin.
- `.github/workflows/make_docs.yml` deploys on push to `master`/`main` with `mkdocs gh-deploy`. It duplicates the copy list from `make_docs.sh` — when adding or renaming a notebook in the book, update **both** files plus the `nav` in `mkdocs.yml`.
- CI installs mkdocs-material-insiders via a private token secret, so it only runs on the upstream (non-fork) repo.
