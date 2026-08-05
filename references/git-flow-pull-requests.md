# Git flow and pull requests

## Git flow

### Main branches
- **`main`** (or `master`): contains only the stable code that is in production. Releases are marked here with *tags* (e.g. `v1.0.0`).
- **`develop`**: contains the code being developed for the next release. It is the main integration branch.

### Supporting branches

#### Feature branches (`feature/*`)
- **Created from:** `develop`
- **Merged into:** `develop`
- **Purpose:** develop new features isolated from the rest of the code.
- **Flow:** `develop` ➔ `feature/feature-name` ➔ `develop`

#### Release branches (`release/*`)
- **Created from:** `develop`
- **Merged into:** `main` **and** `develop`
- **Purpose:** stabilize a new release, fix minor bugs and prepare the move to production. No new features are added.
- **Flow:**
    1. `develop` ➔ `release/v1.1.0`
    2. `release/v1.1.0` ➔ `main` (tagged as `v1.1.0`)
    3. `release/v1.1.0` ➔ `develop`

#### Hotfix branches (`hotfix/*`)
- **Created from:** `main`
- **Merged into:** `main` **and** `develop` (or into the `release` branch if one is active).
- **Purpose:** fix critical, immediate bugs directly in the production environment.
- **Flow:**
    1. `main` ➔ `hotfix/bug-fix`
    2. `hotfix/bug-fix` ➔ `main` (tagged as `v1.0.1`)
    3. `hotfix/bug-fix` ➔ `develop`


## Pull requests

Configure both `main` and `develop` to require code reviews before a pull request can be merged. This is done in the repository's Branches section, setting protection rules for both branches. Direct commits to these two branches are blocked. This guarantees that every contribution is reviewed by at least one other contributor before being merged, which improves code quality and reduces the chance of introducing bugs into the project.
