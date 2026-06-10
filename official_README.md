# example-uv-based-project

A minimal [uv](https://docs.astral.sh/uv/) project on Python 3.13. The example script makes one HTTP request with `requests` and prints the response object. The goal is to be the canonical reference for how a CEU class repo should be laid out — copy this structure for your own project.

## What's in this repo

| File              | What it does                                                            |
| ----------------- | ----------------------------------------------------------------------- |
| `pyproject.toml`  | Declares dependencies (`requests`) and Python version (`==3.13.*`).     |
| `.python-version` | Pins the interpreter to 3.13. `uv` auto-downloads it if missing.        |
| `uv.lock`         | Fully resolved, cross-platform, hashed pin of every transitive dep. Generated automatically by `uv`     |
| `main.py`         | The script.                                                             |
| `.gitignore`      | Excludes `.venv/` and `__pycache__/` from git.                          |

## One-time: install uv

macOS / Linux:

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Source of truth: https://docs.astral.sh/uv/getting-started/installation/

## How to Run this project

```sh
git clone <this-repo>
cd example-uv-based-project
uv sync          # creates .venv/, downloads Python 3.13 if needed, installs deps from uv.lock
## >> Activate the virtualenv in .env (created in the previous command)
python main.py
```

## Start your own uv project

```sh
uv init --bare my-project   # no src/, no build system — same shape as this repo
cd my-project
echo "3.13" > .python-version
uv add requests             # edits pyproject.toml + updates uv.lock
uv run main.py              # once you've written one
```

## Push / Share for review
1) Ensure your project lives on GitHub (can be a private repo)
2) Commit all files: `.python-version`, `pyproject.yml`, `uv.lock`
3) Send the repo url to tothz@ceu.edu. If this is a private project, invite @zoltanctoth first.

## Cheat sheet for pip / conda users

| Task                  | pip / conda                                                            | uv                                       |
| --------------------- | ---------------------------------------------------------------------- | ---------------------------------------- |
| Create environment    | `python -m venv .venv` / `conda create -n x python=3.13`               | `uv sync` (reads `.python-version`)      |
| Install a package     | `pip install requests`                                                 | `uv add requests`                        |
| Install from lockfile | `pip install -r requirements.txt`                                      | `uv sync`                                |
| Freeze dependencies   | `pip freeze > requirements.txt`                                        | `uv lock` (cross-platform + hashed) Updates automatically, no need to execute manually      |
| Run a script (venv)          | `source .venv/bin/activate && python main.py`                          | `source .venv/bin/activate && python main.py` (same)                         |
| Run a script (uv command)          | `source .venv/bin/activate && python main.py`                          | `uv run main.py`                         |

Mental model: `pyproject.toml` ≈ `requirements.txt` (what you want),
`uv.lock` ≈ `pip freeze` output (what you resolved to — but cross-platform
and hashed). Commit both.
