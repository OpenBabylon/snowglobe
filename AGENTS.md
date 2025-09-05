# Repository Guidelines

## Project Structure & Module Organization
- `src/llm_snowglobe/`: main package
  - `snowglobe.py`: core engine and game logic
  - `ui.py`: NiceGUI web UI
  - `api.py`: FastAPI terminal UI (serves `terminal/`)
  - `assets/`, `terminal/`: static assets for UI
- `examples/`: runnable simulations and game scripts (good for smoke tests)
- `Dockerfile`, `docker_setup.sh`: container build/run
- `pyproject.toml`: Poetry config and entry points (`snowglobe_server`, `snowglobe_config`)

## Build, Test, and Development Commands
- Install (editable): `uv pip install -e .`
- Install with uv: `uv pip install`
- Run server (UI): `snowglobe_server` 
- Quick examples:
  - AI simulation: `python examples/haiwire.py`
  - Human+AI: `snowglobe_server & && python examples/ac_game.py` → open `http://localhost:8000`
- Docker: `./docker_setup.sh` builds and runs a container suitable for local use.

## Coding Style & Naming Conventions
- Python 3.10+, 4‑space indentation, UTF‑8.
- Names: `snake_case` for functions/vars, `PascalCase` for classes, module‑level constants in `UPPER_SNAKE_CASE`.
- Prefer type hints and concise docstrings. Keep imports minimal and sorted.
- No enforced linter/formatter yet; match surrounding style and keep diffs small.

## Testing Guidelines
- No formal test suite yet. Validate changes by:
  - Running examples in `examples/` and confirming expected outputs/UI flows.
  - Exercising the UI at `http://localhost:8000` and checking the generated `snowglobe.db` state.
- Add targeted tests if you introduce testable pure functions; place under `tests/` with filenames like `test_*.py` and pytest‑style assertions.

## Commit & Pull Request Guidelines
- Commits: short, imperative subject lines (e.g., "Fix button enable criteria"). Group related changes.
- PRs: include a clear description, reproduction steps, and before/after notes. Link related issues. Add screenshots/GIFs for UI changes.
- Backward compatibility: call out breaking changes and update `README.md` when commands/flows change.

## Security & Configuration Tips
- Do not commit secrets. Use `.env` for local keys and keep it ignored.
- Runtime data (e.g., `snowglobe.db`) is created in the working directory; run games and the server from the same path to share state.
