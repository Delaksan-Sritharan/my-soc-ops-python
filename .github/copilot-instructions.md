# Copilot Workspace Instructions

## Mandatory Dev Checklist

**Run before every commit -- no exceptions:**

```bash
uv run ruff check .   # Lint -- must pass with zero errors
uv run pytest         # Tests -- all must be green
```

No unused imports. New routes must return HTMX-friendly partial templates.

---

## Project

**Soc Ops** -- Social Bingo. Players find real people matching 5x5 icebreaker prompts to get bingo.
**Stack:** Python 3.13, FastAPI, Jinja2, HTMX, itsdangerous, uv

```bash
uv sync
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

## Architecture

| File | Responsibility |
|------|----------------|
| `app/main.py` | Routes: `/`, `/start`, `/toggle/{id}`, `/reset`, `/dismiss-modal` |
| `app/game_logic.py` | Pure functions: `generate_board()`, `toggle_square()`, `check_bingo()` |
| `app/game_service.py` | `GameSession` dataclass -- all state mutations |
| `app/models.py` | Pydantic models: `GameState`, `BingoSquareData`, `BingoLine` |
| `app/data.py` | Question bank (`QUESTIONS`, `FREE_SPACE`) |
| `app/templates/` | Jinja2; `components/game_screen.html` is the HTMX swap target |
| `app/static/css/app.css` | Custom utility classes -- see [css-utilities.instructions.md](instructions/css-utilities.instructions.md) |

## Conventions

- **Type hints** on every function signature; `snake_case` / `PascalCase`.
- Game logic = pure functions in `game_logic.py`. Mutations only in `GameSession` methods.
- Pydantic models are **frozen** -- use `.model_copy(update={...})`, never mutate in place.
- Routes return **partial HTML** for HTMX; no full-page reloads.
- CSS utilities only -- no Tailwind/Bootstrap. Add new classes to `app.css`.

## Pitfalls

- Session state is **in-memory** -- resets on server restart.
- **HTMX needs a real browser** -- VS Code Simple Browser will not work; use `http://localhost:8000`.
- Secret key is hardcoded for dev -- do not deploy as-is.

## Agents

`Quiz Master`, `TDD` (+ `TDD Red/Green/Refactor`), `UI Review`, `Pixel Jam`
