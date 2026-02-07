# pr-doctor-agent

A tiny hello-world Python project with pytest and a GitHub Actions workflow that:

- runs tests on pushes to `main`
- on failure, runs an AI fixer that reads the test log + code, applies a patch, and opens a PR

## Local dev

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pytest -q
```

## GitHub Actions setup

Add these repository secrets:

- `OPENAI_API_KEY`: API key for the OpenAI API
- `OPENAI_MODEL` (optional): e.g. `gpt-5.2-codex`

`GITHUB_TOKEN` is provided automatically by GitHub Actions.

## Workflows

- `.github/workflows/tests.yml`: runs `pytest` on pushes to `main`
- `.github/workflows/auto-fix.yml`: when tests fail, uses the Codex GitHub Action to propose a fix and open a PR

## Notes

The auto-fix workflow runs Codex directly in the repository and opens/updates a pull request.
The model output is saved to `codex-output.md` and uploaded as a workflow artifact.
