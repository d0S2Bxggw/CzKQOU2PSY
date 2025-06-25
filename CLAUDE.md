# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build/Lint/Test Commands
- Run all tests: `make test` or `uv run pytest`
- Run single test: `uv run pytest tests/test_file.py::test_function -v`
- Run quick tests: `uv run pytest -v -m quick`
- Run linting: `make lint` or `uv run black . && uv run isort . && uv run ruff check .`
- Fix linting issues: `make autofix` or `uv run ruff check --fix .`
- Run type checking: `make mypy` or `uv run mypy src/webdataset`
- Run coverage: `make coverage` or `uv run pytest --cov=webdataset --cov-report=term-missing`
- Build documentation: `make docs`
- Serve documentation locally: `make serve` or `uv run mkdocs serve`
- Create virtual environment: `make venv`
- Clean project: `make clean`
- Update README and docs: `make readme`
- Generate FAQ: `make faq` or `uv run python3 helpers/faq.py`
- Check versions: `make versions` or `uv run python3 helpers/versions.py`

## Release Commands
- Test patch release: `make testpatch`
- Release current version: `make release`
- Create patch release: `make patch`
- Create minor release: `make minorrelease`
- Create major release: `make majorrelease`

## Code Style Guidelines
- Line length: 120 characters
- Formatting: Black + isort with Black profile
- Docstrings: Google style (pydocstyle convention)
- Type hints: Use proper type annotations from typing module
- Imports: Use from typing import Only absolute imports, not relative
- Error handling: Use explicit exceptions with helpful messages
- Naming: Follow Python conventions (snake_case for functions/variables)
- Testing: Mark tests with @pytest.mark.quick for fast-running tests
- Documentation: Update docstrings when changing function behavior
- Avoid using deprecated or obsolete functions

## Project Structure
- Package name: webdataset
- Version: 1.0.0
- Python compatibility: 3.10+
- Source code in `src/webdataset/`
- Tests in `tests/`

## Code Analysis Guidelines
- When analyzing code for issues like security vulnerabilities, focus only on code in `src/webdataset/`
- Exclude test files (`tests/`), build scripts (`tasks.py`), and helper utilities (`helpers/`) from security analysis
- These non-core files (tests, tasks.py, helpers) may contain shell commands or other practices that would be inappropriate in library code
- For security vulnerabilities like shell injection, only evaluate the actual library code
- The `safe_eval` function in utils.py is secure as it restricts input to alphanumeric characters and underscores
- The `gopen_pipe` function in gopen.py deliberately uses shell=True for its intended functionality
- The download function in cache.py correctly handles file downloads with temporary files and atomic renames, preventing race conditions
- The exception handling in cache.py:148-150 is appropriate for handling race conditions where files may be deleted by other processes during directory walking

## Memory Instructions
- When the user says "remember this" or "remember", add appropriate notes to this CLAUDE.md file for persistent memory
- Place these notes in the most relevant section, or add a new section if needed

## Git Instructions
- When the user says "commit", perform the following actions:
  1. Add all modified files with `git add`
  2. Generate a commit message automatically that reflects the changes based on our conversation and `git diff`
  3. Commit the changes with the generated commit message
  
## Command Shortcuts
- When the user says "next?", list any remaining issues from the most recently generated list of tasks or problems
