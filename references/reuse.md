# REUSE.toml and SPDX headers

Follow the REUSE 3.2 specification. **Do not use `.reuse/dep5`: it is deprecated** and was replaced by `REUSE.toml` at the root of the repository.

Strategy per file type:

- **Green field code (new)**: an SPDX header at the top of every source file, as a comment:

  ```
  # SPDX-FileCopyrightText: 2026 {{MAINTAINER_NAME}} <{{EMAIL}}>
  # SPDX-License-Identifier: MIT
  ```

  This can be automated with `pipx run reuse annotate --copyright "{{MAINTAINER_NAME}} <{{EMAIL}}>" --license MIT {{files}}`.

- **Files whose content cannot be edited** (images, binaries, datasets): a sidecar file `{{name}}.{{ext}}.license` with the two SPDX lines, or cover them via `REUSE.toml`.

- **Legacy code (brown field), documentation and bulk files**: declare them in `REUSE.toml` at the root. Minimal example:

  ```toml
  version = 1

  [[annotations]]
  path = ["docs/**", "*.md"]
  SPDX-FileCopyrightText = "2026 {{MAINTAINER_NAME}} <{{EMAIL}}>"
  SPDX-License-Identifier = "MIT"

  [[annotations]]
  path = "assets/**"
  SPDX-FileCopyrightText = "2026 {{MAINTAINER_NAME}} <{{EMAIL}}>"
  SPDX-License-Identifier = "CC-BY-4.0"
  ```

Every referenced license must have its full text in `LICENSES/{{LICENSE_ID}}.txt` (see [license.md](license.md)).

Verification: `pipx run reuse lint` (or `pip install reuse && reuse lint`) must pass without errors before considering this artifact done.
