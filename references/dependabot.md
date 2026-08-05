# Dependabot (.github/dependabot.yml)

Configure Dependabot through `.github/dependabot.yml` to keep the project's dependencies up to date and secure. Dependabot opens PRs with updates and raises alerts for CVEs in dependencies, which helps keep the project safe for users and contributors.

Before generating the file, **detect the repository's actual ecosystems** (look at the manifests: `package.json` → npm, `requirements.txt`/`pyproject.toml` → pip, `Cargo.toml` → cargo, `go.mod` → gomod, `pom.xml` → maven, `Dockerfile` → docker, ...). Always add `github-actions` if there are workflows.

Example (npm project with workflows):

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    groups:
      minor-and-patch:
        update-types:
          - "minor"
          - "patch"

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

Notes:
- `schedule: weekly` is a reasonable default for a hackathon or small project; security advisories still arrive as soon as they are published.
- `groups` bundles minor/patch updates into a single PR to reduce noise; major updates go in a separate PR.
- One `updates` block per detected ecosystem and directory.
