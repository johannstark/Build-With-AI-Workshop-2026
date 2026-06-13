## Project Context
You are an expert AI development agent working on a dual-service Python repository.

- `./agent`: An AI agent built using the Agent Development Kit (ADK).
- `./mcp`: A custom Model Context Protocol (MCP) server designed to fetch and expose information.

## Tooling & Package Management

This project strictly uses **`uv`** as the fast Python package installer and resolver.

- **Environment Management:** Always use `uv venv` and `uv pip` for managing dependencies. 
- **Executing Scripts:** Run scripts via `uv run <script_name>.py` to ensure correct environment resolution.
- **Adding Dependencies:** Use `uv pip compile` or `uv pip sync` when package definitions change. Do not use standard `pip` or `poetry`.

## Safety & Git Boundaries

You are encouraged to inspect the repository state, but you have hard limits regarding version control.

- ✅ **Allowed:** `git status`, `git diff`, `git log`, and `git add` (to stage files for review).
- 🚫 **Strictly Forbidden:** **Never** execute `git commit` or `git push`. The human developer retains exclusive control over committing and deploying changes.

## Coding Style & Guidelines

All Python code across both `./agent` and `./mcp` must strictly follow the **Google Python Style Guide**.

- **Naming Conventions:** 
  - `module_name`, `package_name`, `method_name`, `function_name`, `instance_var_name`
  - `ClassName`, `ExceptionName`
  - `GLOBAL_CONSTANT_NAME`
- **Type Hints:** Type annotations are required for all function signatures, arguments, and return types.
- **Docstrings:** Use Google-style docstrings for all modules, classes, and public functions:

```python
  def fetch_data(source_id: str) -> dict:
      """Fetches data from the specified source.

      Args:
          source_id: A unique identifier for the information source.

      Returns:
          A dictionary containing the parsed source data.

      Raises:
          ValueError: If the source_id is empty or invalid.
      """
```

- **Formatting & Linting**: Run your formatting checks locally using ruff matching the Google standard before declaring work done.

## Testing Strategy & TDD Workflow

We practice strict Test-Driven Development (TDD) principles here.

- 🧪 **Mandatory Unit Tests**: Every single time you write new code, modify existing logic, or fix a bug, you must create or update corresponding unit tests.
- 🔄 **Continuous Execution**: Keep tests running continuously during development. Before asking for human feedback, ensure the relevant test suite passes.
- **Test Command**: Run your tests using uv run pytest targeting the specific module you are changing (e.g., uv run pytest agent/tests/).

## Project Layout & Wiring

- `./agent`: Core ADK implementation. Agent logic, prompts, and tool definitions live here.
- `./mcp`: MCP Server implementation. Standard tools and resources exposed to the LLM router live here.
- For deeper technical design, refer to localized readmes inside those respective directories.

## Definition of Done

Before completing a task, verify the following checklist:

 1. All new and modified functions have comprehensive unit tests.
 2. uv run pytest runs and passes with zero failures.
 3. Code complies with Google Python Style guidelines (including docstrings and type hints).
 4. git status shows code is clean or staged, with no accidental temporary or untracked files left behind.