# setup-repo-test

Temporary repository for testing the setup-repo skill.

## Development

Requires [uv](https://docs.astral.sh/uv/), which runs pre-commit and its hooks, and
[Node.js](https://nodejs.org/), which runs the pinned OpenSpec CLI. One-time setup:

```
uv sync
uvx pre-commit install
npm ci --ignore-scripts
```

Run all local checks:

```
uvx pre-commit run --all-files
uv run pytest
npx openspec validate --all --no-interactive
```

CI (`.github/workflows/ci.yml`) runs these checks on pushes to `master` and on pull requests.
The `check` job is required before merge. The hooks check whitespace, YAML, TOML and JSON,
lint and format Python with Ruff, lint shell scripts with shellcheck, scan for secrets with
gitleaks and audit workflows with zizmor.

- Dependabot updates GitHub Actions, pre-commit hooks, Python and npm packages weekly, after
  a 7-day cooldown.
- CodeRabbit reviews pull requests (`.coderabbit.yaml`).
- OpenSpec changes and specs live in `openspec/`. `package.json` pins the CLI. On a
  Dependabot bump, `.github/workflows/openspec-regenerate.yml` regenerates the
  `.claude/skills/openspec-*` files, approves the CI runs of that commit and enables
  auto-merge.

## License

MIT
