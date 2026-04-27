# uv-project-care

A GitHub template repo that ships a [uv](https://github.com/astral-sh/uv) project with the three CI jobs from [Care and maintenance of a uv project](https://pydevtools.com/handbook/how-to/how-to-take-care-of-a-uv-project/) pre-wired:

- **An auto-feeder for the lockfile.** A Dependabot config (`.github/dependabot.yml`) opens weekly PRs that bump `uv.lock`.
- **A standing vet appointment.** An `audit.yml` workflow runs `uv audit` on every push and on a weekly schedule, failing the build on findings.
- **A weekly groomer.** An `autoupdate-hooks.yml` workflow runs `prek auto-update` on a Monday-morning cron and opens a PR with the diff.

After scaffolding, the project's recurring maintenance is a 30-minute home checkup once a month.

## Use this template

Click the green **Use this template** button, then in the new repo:

1. Edit `pyproject.toml` to set your project name, description, and dependencies. Replace the `src/uv_project_care/` package with your own.
2. Enable the workflow permission toggle at **Settings → Actions → General → Workflow permissions → "Allow GitHub Actions to create and approve pull requests"**. Without this, the autoupdate-hooks workflow can't open PRs.
3. Push a commit. `test.yml` and `audit.yml` will run on the push; the first scheduled `autoupdate-hooks.yml` PR will appear the following Monday at 9am UTC.

## What's in the box

| File | Purpose |
|---|---|
| `.github/dependabot.yml` | Weekly `uv.lock`, `pyproject.toml`, and `actions/*` updates |
| `.github/workflows/test.yml` | Run `uv run pytest` on every push and PR |
| `.github/workflows/audit.yml` | Run `uv audit` on every push and PR; fail the build on findings |
| `.github/workflows/autoupdate-hooks.yml` | Weekly scheduled `prek auto-update`; opens a PR with the diff |
| `.pre-commit-config.yaml` | Minimal Ruff lint + format hook config |
| `pyproject.toml` | uv project skeleton |
| `src/uv_project_care/` | Placeholder package |
| `tests/test_basic.py` | One smoke test so CI has something to exercise |

## Pin actions to a SHA?

The workflows pin GitHub Actions to a tag (`@v6`, `@v8.1.0`). For tighter supply-chain protection, pin to a full SHA. See [How to pin GitHub Actions by SHA for Python projects](https://pydevtools.com/handbook/how-to/how-to-pin-github-actions-by-sha-for-python-projects/).

## Read the why

The full reasoning behind these choices is in [Care and maintenance of a uv project](https://pydevtools.com/handbook/how-to/how-to-take-care-of-a-uv-project/) on the Python Developer Tooling Handbook.
