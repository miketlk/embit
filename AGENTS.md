# AGENTS.md

## Project intent
- `embit` is a minimal, auditable Bitcoin library for Python 3 and MicroPython.
- Favor small, explicit changes over broad refactors.

## Where to look first
- Core package: `src/embit/`
- Tests (default): `tests/tests/`
- Integration tests (requires daemons): `tests/integration/`
- Docs and API notes: `docs/`, `README.md`
- Packaging/config: `pyproject.toml`, `.pre-commit-config.yaml`, `setup.py`

## Local dev and validation
- Prefer the existing Poetry environment first (for example: `poetry env info -p` / `poetry run ...`).
- If Poetry is unavailable for the repo, use the existing virtualenv: `. .venv/bin/activate`
- Main test pass: `pytest`
- MicroPython-style suite: `cd tests && micropython ./run_tests.py`
- Integration suite: `python tests/integration/run_tests.py` (needs `bitcoind` and `elementsd` available)
- Formatting: `pre-commit run -a` (Black is configured)
- After any Python change:
  - run relevant/affected tests
  - `ruff check --fix <file>`
  - repeat until no issues remain
- Treat Ruff security findings (`S`) as high priority:
  - fix them, or
  - justify inline with minimal scope
- Run package inspect helper: `python tools/package-inspect.py` to validate package contents

## Ephemeral Workspace
- Use `.ai/` for temporary work:
  - `.ai/plans/` - plans/reasoning
  - `.ai/context/` - extracted snippets
  - `.ai/runs/` - logs/outputs
- Never commit `.ai/` contents.

## Change guardrails
- Keep runtime dependencies minimal; avoid adding new runtime deps unless clearly justified.
- Treat packaging/release-sensitive files as high-risk: `pyproject.toml`, `setup.py`, `.gitmodules`, `src/embit/util/ctypes_secp256k1.py`, `src/embit/util/prebuilt/*`, and `secp256k1/**`.
- Do not introduce install-time hooks or hidden execution paths (`.pth`, `sitecustomize.py`, `usercustomize.py`, custom setup commands).
- Never write code comments about implementation process, fulfilling user prompts, or plan steps/phases; comments must describe code behavior or rationale only.

## Docs/config sync
- If behavior changes, update relevant docs in `README.md` and/or `docs/api/*` in the same change.
- Keep guidance consistent across Python 3 and MicroPython paths; call out platform-specific limitations explicitly.
