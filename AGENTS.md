# Repository Guidelines

## Project Structure & Module Organization
- `trendradar/`: core crawler, analysis, notification, report, and storage logic.
- `mcp_server/`: MCP server entrypoint plus tools and services.
- `config/`: runtime configuration (`config.yaml`, `frequency_words.txt`).
- `output/`: generated reports and sample data (for example, `output/news/*.db`).
- `docker/`: container build files, compose config, and `manage.py` helpers.
- `_image/` and `README*.md`: documentation assets and guides.

## Build, Test, and Development Commands
- `./setup-mac.sh` or `setup-windows.bat`/`setup-windows-en.bat`: install `uv` and project dependencies.
- `uv sync`: create `.venv` and install Python deps (same outcome as the setup scripts).
- `uv run python -m trendradar`: run a local crawl/analysis pass using `config/config.yaml`.
- `./start-http.sh` or `start-http.bat`: run the MCP server in HTTP mode at `http://localhost:3333/mcp`.
- `docker compose -f docker/docker-compose.yml up -d`: run the prebuilt containers locally.

## Coding Style & Naming Conventions
- Python 3.10+, 4-space indentation, and PEP 8-style formatting.
- Naming: `snake_case` for functions/variables, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants.
- Keep config keys aligned with existing names in `config/config.yaml`.

## Testing Guidelines
- No automated test suite is configured in this repo.
- For changes, do a smoke run: `uv run python -m trendradar` and, if relevant, `./start-http.sh`.
- If you add tests, place them under `tests/` and use `test_*.py` names; document any new test commands.

## Commit & Pull Request Guidelines
- Commit messages are short, imperative, and sentence case (examples from history: `Update crawler.yml`, `Refactor crawler job in GitHub Actions workflow`).
- PRs should include a clear summary, linked issue (if any), and notes about config or behavior changes.
- If changes affect reports or web output, include a screenshot or a sample artifact from `output/` or `index.html`.

## Security & Configuration Tips
- Treat `config/config.yaml` as sensitive; do not commit real tokens or webhook URLs.
- Prefer environment variables (see `docker/docker-compose.yml`) for secrets in container setups.
