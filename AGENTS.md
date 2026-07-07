# AGENTS.md

Context and rules for AI agents working in this repository. Humans should start with `README.md`.

## Project overview

- **Name**: MLOps Coding Course — a MkDocs Material documentation site that teaches end-to-end MLOps in Python.
- **Published**: https://mlops-coding-course.fmind.dev via GitHub Pages (deployed by GitHub Actions).
- **No application code**: this repo builds a static site from Markdown in `docs/`.

## Setup & core commands

All work goes through `mise` (see `mise.toml`); git hooks (`lefthook.yml`) and CI call the same tasks.

- Install: `mise run install` — sync dependencies (`uv`) and install git hooks.
- Format: `mise run format` — `dprint` for config/markup only; prose under `docs/` is intentionally not reformatted.
- Check: `mise run check` — `dprint check`, `mkdocs build --strict` (catches broken links/config), `gitleaks`.
- Build: `mise run build` — `mkdocs build`; Serve locally: `mise run serve` (live reload).

## Conventions

- Content lives in `docs/`, one numbered folder per chapter; the sidebar order comes from the numeric filename prefixes (no explicit `nav:`), so keep prefixes consistent when adding pages.
- Each page follows a consistent What / Why / How question-and-answer structure.
- Numbered lists use `1.` for every item so rendering stays dynamic; `docs/**` is excluded from `dprint` so prose formatting is preserved.
- Teach the current canonical stack: `uv`, Ruff, `ty`, `pytest`, `mise`, `lefthook`, `dprint`, `git-cliff`, MLflow 3, Docker, Python 3.14. Keep tool versions and examples in sync with the [cookiecutter-mlops-package](https://github.com/fmind/cookiecutter-mlops-package) and [mlops-python-package](https://github.com/fmind/mlops-python-package).
- Commits: Conventional Commits; no attribution. Releases use `git-cliff`.

## Repository layout

- `docs/` — course chapters (`0. Overview` → `7. Observability`), `assets/`, and `CNAME` (custom domain, copied into the built site).
- `mkdocs.yml` — site configuration (Material theme, `strict: true`); `pyproject.toml` — mkdocs dependencies (`uv`, `package = false`).
- `mise.toml` — tasks and pinned tools; `lefthook.yml` — git hooks; `dprint.jsonc` — config/markup formatter; `cliff.toml` — changelog.
- `.github/workflows/` — `ci.yml` (strict build check on PR/push) and `pages.yml` (build + deploy to GitHub Pages on push to `main`).
