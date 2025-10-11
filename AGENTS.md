# Repository Guidelines

## Project Structure & Module Organization
This repository curates experiments on epistemic state updates for LLM agents. Store the working manuscript `Epistemic State Updates in LLM Agents via Public Announcement and Graded Modal Logic.docx` under `docs/paper/` alongside exported PDFs. Place runnable code in `src/epistemic_ai/` with subpackages: `agents/` for agent policies, `logic/` for modal reasoning utilities, and `pipelines/` for evaluation workflows. Keep shared prompts under `assets/prompts/` and raw transcripts under `data/raw/` (paired with a README describing provenance). Mirror every module with an equivalent `tests/...` path so failures map cleanly.

## Build, Test, and Development Commands
Work in Python 3.11. Create or refresh a virtual environment with `python -m venv .venv && source .venv/bin/activate`. Install dependencies via `pip install -r requirements-dev.txt` and commit the file whenever toolchains change. Run `python -m pytest` for unit tests, `pytest tests/integration -m "not slow"` for cross-agent checks, and `black src tests` plus `ruff check src tests` before pushing. Use `scripts/render_paper.sh` to convert the manuscript to PDF; keep the script idempotent and re-run it whenever the doc changes.

## Coding Style & Naming Conventions
Adopt PEP 8/PEP 484 with 4-space indentation, `snake_case` for functions, `PascalCase` for agent classes, and UPPER_SNAKE_CASE for constants. Keep prompt templates as Markdown fragments named `action_goal.md` inside `assets/prompts/`. Run `black`, `ruff`, and `mypy --strict` locally; configuration should live in `pyproject.toml` once introduced—place overrides next to the relevant module.

## Testing Guidelines
Use `pytest` with `pytest-cov`; target ≥90% statement coverage for `src/epistemic_ai/logic`. Name tests `test_<unit>_<behavior>` and parametrize cross-agent scenarios rather than duplicating fixtures. Store experiment fixtures in `tests/fixtures/` and keep synthetic data lightweight (<100 KB). For slow LLM calls, add a `@pytest.mark.slow` marker and provide cached transcripts under `data/derived/`.

## Commit & Pull Request Guidelines
Write commits in the imperative with a concise scope prefix, e.g., `logic: add graded belief updater`. Reference the relevant experiment or manuscript section in the body and list observable impacts. Pull requests need a summary, reproduction instructions, updated coverage output, and a checklist confirming doc updates (paper, changelog, assets). Attach before/after artefacts when modifying prompts or generated transcripts so reviewers can trace epistemic effects.
