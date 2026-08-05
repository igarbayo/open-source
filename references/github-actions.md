# GitHub Actions workflows (.github/workflows/)

Build, lint, tests and security are automated as CI on push and pull request. Scorecard and CodeQL report vulnerabilities and bad practices in the repository's Security tab.

Workflow security rules (mandatory):
- `permissions: read-all` at workflow level; minimal, justified elevation per job where needed.
- Every third-party action **pinned to a full commit SHA**, never to mutable tags (this removes the risk of supply-chain tag hijacking). Write `uses: owner/action@{{SHA}} # vX.Y.Z` and **resolve the real SHA** of the tag before generating the file.

### How to resolve the SHA of a tag

Do not assume any tool is installed: try these in order and use the first one that works.

1. If `gh` is available and authenticated (`gh auth status`):

   ```bash
   gh api repos/{{OWNER}}/{{ACTION}}/git/ref/tags/{{TAG}} --jq .object.sha
   ```

2. Otherwise, with `curl` against the public API (no authentication needed; the limit is 60 requests per hour per IP):

   ```bash
   curl -sSL https://api.github.com/repos/{{OWNER}}/{{ACTION}}/git/ref/tags/{{TAG}}
   # e.g. https://api.github.com/repos/actions/checkout/git/ref/tags/v4.2.2
   ```

   The SHA is in `.object.sha`. If `.object.type` is `tag` (an annotated tag), that SHA belongs to the tag object: follow the `.object.url` field to get the real commit.

3. If there is no `curl` either, or no network, **do not invent the SHA**: open the action's releases page (`https://github.com/{{OWNER}}/{{ACTION}}/releases`) or ask the user, and leave the file with the documented `@{{SHA}}` marker until you have the value. An invented SHA breaks the workflow on its first run.

**Adapt the build/lint/test commands to the project's real stack** — read it from the repo (package.json scripts, Makefile, pyproject.toml...), do not make it up. If the project does not compile (e.g. plain Python), skip build.yml. Skeletons:

## build.yml / test.yml / lint.yml (same pattern, only the last step changes)

```yaml
name: build
permissions: read-all
on:
  push:
    branches: [main, develop]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@{{SHA}} # vX.Y.Z
      - uses: actions/setup-node@{{SHA}} # vX.Y.Z — or setup-python/setup-go depending on the stack
        with:
          node-version: 22
      - run: npm ci
      - run: npm run build   # test.yml: npm test · lint.yml: npm run lint
```

## security.yml (OpenSSF Scorecard + CodeQL)

```yaml
name: security
permissions: read-all
on:
  push:
    branches: [main]
  pull_request:
  schedule:
    - cron: "30 5 * * 1"

jobs:
  scorecard:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
      id-token: write
    steps:
      - uses: actions/checkout@{{SHA}} # vX.Y.Z
      - uses: ossf/scorecard-action@{{SHA}} # vX.Y.Z
        with:
          results_file: results.sarif
          results_format: sarif
      - uses: github/codeql-action/upload-sarif@{{SHA}} # vX.Y.Z
        with:
          sarif_file: results.sarif

  codeql:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
    steps:
      - uses: actions/checkout@{{SHA}} # vX.Y.Z
      - uses: github/codeql-action/init@{{SHA}} # vX.Y.Z
        with:
          languages: javascript # adjust to the repository's languages
      - uses: github/codeql-action/analyze@{{SHA}} # vX.Y.Z
```

Status notifications can be added to keep the team informed, but the four workflows above are the minimum baseline.