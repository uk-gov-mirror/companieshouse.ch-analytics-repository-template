
# Companies House — Analytics Repository Template

This repository is a reusable project template for the Companies House
Analytics division (Statistics, Corporate Performance, Data Engineering,
and Data Science). It is designed to be both a practical starter kit for a
new analytics project and a short demonstration of what a good README
should contain.

This template supports mixed-language projects (SQL, Python, R) and
provides a minimal opinionated layout, tooling hooks, and a small demo
script that validates the Python environment.

Key goals
---------
- Provide a consistent starting point for analytics projects across the
	organisation.
- Demonstrate clear documentation and developer workflow.
- Keep the repository tidy while remaining explicit about the files and
	tools projects often need.

Repository layout
-----------------
- `.github/` — CI/workflow configuration
- `.gitignore`, `.gitattributes` — repository-level git configs
- `pyproject.toml` — Python project metadata and dependencies
- `main.py` — tiny utility that checks whether declared Python
	dependencies are importable in the current environment (see below)
- `tools/` — auxiliary scripts (non-critical tooling)

What `main.py` does
-------------------
`main.py` is a lightweight environment-check helper intended for use in
templates and demos. It:

- Parses `pyproject.toml`'s `[project].dependencies` list.
- For each declared dependency, attempts to import the corresponding
	Python package (using a small mapping/heuristic for names that differ
	between distribution and import names).
- Prints a concise summary of installed and missing packages and exits
	with a non-zero status when any dependency is missing.

The script purposefully does not attempt to install missing packages —
it only reports their importability so that maintainers/contributors can
see whether the environment is ready.

Quickstart — creating the Python environment
-------------------------------------------
This project uses the `uv` tool for environment management (the repo
already contains a `uv.lock` file). To create or update the environment
run the following in PowerShell from the repository root:

```powershell
uv sync
```

Notes:
- `uv sync` will create or update a local environment according to the
	lockfile. If you prefer to use venv, conda, or another tool, adapt
	the workflow to match your team's standard.
- Ensure your terminal's Python is compatible with the `requires-python`
	constraint in `pyproject.toml` (the template pins `==3.11.9`).

How to use the template
-----------------------
1. Copy the repository to a new project repository (or use this as a
	 template in GitHub).
2. Update `pyproject.toml` with your project name, description, and
	 dependencies.
3. Tidy or move any project-specific configs into `.config/` or
	 `tools/` if you prefer a cleaner root (see repository notes).
4. Run `uv sync` to create the environment and then run the environment
	 check:

```powershell
# create/update env
uv sync

# run the dependency check
.\.venv\Scripts\python.exe .\main.py
```

Customising configs
--------------------
Some configuration files (for example, `.pre-commit-config.yaml` or
`.sqlfluff`) can be safely moved into a `.config/` or `tools/config/`
directory, but keep `pyproject.toml`, `.gitignore`, and `.gitattributes`
at the repository root. When you move configs, add small wrappers or
update CI commands to point tools at the new locations.

Contributing and style
----------------------
- Keep code and SQL in dedicated subdirectories for larger projects
	(for example, `src/`, `sql/`, `notebooks/`).
- Use the `main.py` dependency check in CI to validate developer
	environments quickly during onboarding.

License and authorship
---------------------
Add your preferred license and authorship notes when you create a new
project from this template.

----

If you want, I can: move a few configuration files into `.config/` and
add wrapper scripts that call tools with the new paths, then update
this README with the exact commands. Just tell me which configs you'd
like relocated.

