Let me open `project-uv/README.md` to see its current content so I can add the relevant uv usage and commands.
Ran tool

Here’s an append-ready section you can add to `project-uv/README.md`:

```markdown
## Quick Start

- Create/use project venv and install deps:
```powershell
uv sync
```

- Strict, reproducible install (CI):
```powershell
uv sync --frozen
```

- Run a script/command in the project env:
```powershell
uv run python main.py
```

## Managing Dependencies

- Add a dependency (updates `pyproject.toml` and `uv.lock`):
```powershell
uv add <package>
```

- Remove a dependency:
```powershell
uv remove <package>
```

- Update lockfile after edits:
```powershell
uv lock
```

- Upgrade all within constraints:
```powershell
uv lock --upgrade
```

- Upgrade one package:
```powershell
uv lock --upgrade-package <package>
```

## Lockfile (`uv.lock`) Behavior

- `uv add <pkg>` updates both `pyproject.toml` and `uv.lock`.
- `uv lock` resolves and writes exact versions.
- `uv sync` installs to match `uv.lock` (creates `.venv` if needed).
- Use `uv sync --frozen` to fail if the lockfile would change.

## Common Tasks

- Show dependency tree:
```powershell
uv tree
```

- Build and publish:
```powershell
uv build
uv publish
```

## Environments

- Create venv:
```powershell
uv venv
```

- Use the currently active environment instead of the project `.venv`:
```powershell
uv sync --active
uv run --active python -V
```

- Fix warning about mismatched `VIRTUAL_ENV`:
  - Either activate the project venv:
```powershell
.\.venv\Scripts\Activate.ps1
```
  - Or clear the active env before running uv:
```powershell
Remove-Item Env:VIRTUAL_ENV
```
  - Or explicitly target the active env with `--active` (see above).

## Handy PowerShell Tips

- Check active virtual env path:
```powershell
$env:VIRTUAL_ENV
```

- Print Python environment path:
```powershell
python -c "import sys; print(sys.prefix)"
```

- List all environment variable values:
```powershell
(Get-ChildItem Env:).Value
```

- Shorten prompt path (add to `$PROFILE`):
```powershell
function prompt { "$(Split-Path -Leaf $PWD)> " }
```

## Command Reference (top-level)

- Project: `uv init`, `uv add`, `uv remove`, `uv lock`, `uv sync`, `uv run`, `uv tree`, `uv build`, `uv publish`
- Tools: `uvx <tool>`, `uv tool run/install/uninstall/list`, `uv tool update-shell`, `uv tool dir`
- Envs & Python: `uv venv`, `uv python install/list/pin/dir`
- pip-compat: `uv pip install/uninstall/list/show/freeze/check/tree/compile/sync`
- Cache & self: `uv cache dir/clean/prune`, `uv self update`
```
