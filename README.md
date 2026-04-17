# update-coverage-badge

[![Coverage](https://img.shields.io/badge/Coverage-0%25-red)](https://jedi-knights.github.io/update-coverage-badge/)

A GitHub Action that runs your project's coverage command, updates the shields.io badge in `README.md` via [`jedi-knights/coverage-badge`](https://github.com/jedi-knights/coverage-badge), and commits the result back to the repository. Handles Python + uv setup internally.

## Usage

```yaml
- uses: actions/checkout@v6
  with:
    token: ${{ secrets.GH_TOKEN }}

- uses: jedi-knights/update-coverage-badge@v0
  with:
    github-token: ${{ secrets.GH_TOKEN }}
```

### With a private registry

```yaml
- uses: jedi-knights/update-coverage-badge@v0
  with:
    github-token: ${{ secrets.GH_TOKEN }}
    index-name: artifactory
    index-username: ${{ secrets.ARTIFACTORY_USER }}
    index-password: ${{ secrets.ARTIFACTORY_TOKEN }}
```

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `github-token` | yes | — | Token used to push the badge commit |
| `python-version` | no | `3.13` | Python version to use |
| `uv-version` | no | `latest` | uv version to install |
| `coverage-command` | no | `uv run invoke coverage` | Command that produces the coverage report |
| `index-name` | no | `''` | Private index name from `pyproject.toml` |
| `index-username` | no | `''` | Username for the private index |
| `index-password` | no | `''` | Password or token for the private index |
| `commit-message` | no | `chore: update coverage badge [skip ci]` | Commit message for the badge update |

## Outputs

| Output | Description |
|---|---|
| `coverage-percentage` | Coverage percentage as a bare number (e.g. `"87.5"`) |
