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

| File                     | Responsibility                                                                                            |
| ------------------------ | --------------------------------------------------------------------------------------------------------- |
| `app/main.py`            | Routes: `/`, `/start`, `/toggle/{id}`, `/reset`, `/dismiss-modal`                                         |
| `app/game_logic.py`      | Pure functions: `generate_board()`, `toggle_square()`, `check_bingo()`                                    |
| `app/game_service.py`    | `GameSession` dataclass -- all state mutations                                                            |
| `app/models.py`          | Pydantic models: `GameState`, `BingoSquareData`, `BingoLine`                                              |
| `app/data.py`            | Question bank (`QUESTIONS`, `FREE_SPACE`)                                                                 |
| `app/templates/`         | Jinja2; `components/game_screen.html` is the HTMX swap target                                             |
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

---

## Design Guide

**Aesthetic:** Premium minimal dark. Charcoal base, single indigo accent for interaction, amber reserved exclusively for bingo wins. Restraint over decoration — no neon glows, no gradients on text, no decorative borders.

### Design Tokens (CSS variables in `app/static/css/app.css`)

| Variable          | Value                    | Use                            |
| ----------------- | ------------------------ | ------------------------------ |
| `--bg`            | `#0c0c0f`                | Page background                |
| `--surface-1`     | `#161619`                | Header, cards                  |
| `--surface-2`     | `#1e1e24`                | Board squares, raised surfaces |
| `--surface-3`     | `#26262d`                | Hover / active surface         |
| `--border`        | `rgba(255,255,255,0.08)` | Default borders                |
| `--border-strong` | `rgba(255,255,255,0.15)` | Hover borders                  |
| `--accent`        | `#6366f1`                | Buttons, marked squares        |
| `--accent-dim`    | `rgba(99,102,241,0.15)`  | Marked square background       |
| `--accent-hover`  | `#818cf8`                | Accent hover state             |
| `--text-1`        | `#f4f4f5`                | Primary text                   |
| `--text-2`        | `#a1a1aa`                | Secondary text                 |
| `--text-3`        | `#71717a`                | Muted / placeholder text       |
| `--win-bg`        | `rgba(251,191,36,0.12)`  | Winning square fill            |
| `--win-border`    | `#fbbf24`                | Winning square border          |
| `--win-text`      | `#fbbf24`                | Winning square text            |

### Typography

- **Headings** (`h1`, game title): `Syne 800` via Google Fonts CDN → use `.font-display` class
- **Body / UI**: `Figtree 400/600/700` via Google Fonts CDN → loaded as default body font
- Both fonts are loaded in `app/templates/base.html`

### Animation Utilities

| Class                       | Effect                                    | Use                                                         |
| --------------------------- | ----------------------------------------- | ----------------------------------------------------------- |
| `.fade-in`                  | `opacity 0→1` + `translateY 8px→0`, 350ms | Page/screen entry on `#game-container` inner divs           |
| `.modal-enter`              | `scale 0.96→1` + opacity, 200ms           | Bingo modal card                                            |
| `.board-square`             | `scale 0.9→1` + opacity, 250ms            | Every board square button                                   |
| `.stagger-1` – `.stagger-5` | `animation-delay` 0–220ms                 | Applied to squares per board row (`(loop.index0 // 5) + 1`) |

### State Semantics

- **Indigo** (`--accent`, `--accent-dim`) = marked/active squares only
- **Amber** (`--win-*`) = winning bingo line only — never use `bg-amber-*` / `text-amber-*` outside that context
- Never mix the two accent colors on the same element

### Do-Nots

- No neon glow utilities (`.glow-cyan`, `.glow-lime`, `.glow-magenta` are no-ops — kept for backward compat only)
- No new layout primitives without adding to `app/static/css/app.css` first
- No Tailwind, Bootstrap, or other CSS frameworks
- No JavaScript animations — CSS only

---

## Agents

`Quiz Master`, `TDD` (+ `TDD Red/Green/Refactor`), `UI Review`, `Pixel Jam`
