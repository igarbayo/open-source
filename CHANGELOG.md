# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and this project adheres to [Semantic Versioning](https://semver.org/).

Every maintainer, contributor or AI agent working on this repository must update this file with each significant change (new features, fixes or documentation improvements), explaining in prose **why** the change was made and not just which files were touched: the goal is a history that humans can read.

## [Unreleased]

### Added

- Installation in a single command, `npx skills add igarbayo/open-source`, promoted to the top of both READMEs and to the first subsection of *Installation*. The [skills CLI](https://github.com/vercel-labs/skills) already discovered this repository without any change on our side — its root directory counts as a discovery location because it contains a `SKILL.md`, and it additionally reads `.claude-plugin/marketplace.json` and `plugin.json`, so the plugin work from `1.1.0` pays off twice. Until now the shortest path on offer was cloning into an exact path, which is friction that loses installations before they happen: the point of a governance skill is that someone can try it in the ten seconds between deciding to open source a project and losing interest.
- A skills.sh badge linking to the directory listing, the same format the Vercel Labs repository uses for itself.
- Coverage of the CLI route across the rest of the README: rows in the invocation table for Claude Code and OpenCode installs made through `npx skills add`, a compatibility bullet noting it needs Node.js, and a troubleshooting row for the most likely stumble — the CLI installs into the current project unless `--global` is passed, and the session has to be restarted before a new skill is picked up.

### Changed

- The marketplace route is no longer labelled "recommended". It is now described for what it actually is, the route native to Claude Code that manages the skill as a versioned plugin, while the CLI is presented as the fastest and the only one that covers both supported agents. Two routes cannot both be the recommendation, and the one to lead with is the one that costs a single command.

## [1.2.0] - 2026-08-05

### Changed

- The whole artifact is now written in English: the body of `SKILL.md`, all the files under `references/`, the README and this changelog. The repository was previously in a mixed state — an English frontmatter `description` and English emitted templates wrapped in Spanish prose — which is the worst of both worlds. English is the language of the repository's topics, description and commits, it matches the vocabulary the `description` competes with in the system prompt, and it is what makes contributions from non-Spanish speakers possible in a repository whose subject is open source collaboration.
- The language of the instructions and the language of the generated documentation are now explicitly separate axes. Writing the skill in Spanish was never what made it able to produce Spanish documentation: the output language has always been a question in the survey, with English as the default. `SKILL.md` now says so outright so the model does not carry the instruction language over into the output.
- This changelog uses the canonical Keep a Changelog section names (Added / Changed / Fixed) and links the English editions of the Keep a Changelog and Semantic Versioning specifications instead of the Spanish ones.
- The README is now bilingual: `README.md` in English with `README.es.md` linked at the top, which is the standard pattern for this. The Spanish version is a full translation, not a stub.

### Added

- `references/localization.md`, holding the Spanish and Galician typographic conventions (sentence case in headings, the em dash reserved for asides and never used in place of a colon). They used to live inline in `SKILL.md`, so their context cost was paid on every invocation even when the documentation was going to be generated in English. They are now loaded only when the chosen language is not English, and new languages can be added without touching `SKILL.md`.

### Fixed

- The survey and the conflict-resolution step now accept answers in any language ("all", "todas", …), so switching the option list to English does not force the user to reply in English.
- The `1.0.1` release was missing from this changelog entirely, even though the tag and the GitHub release existed and the `[1.1.0]` compare link already pointed at it. Its entry is now written up below.
- Spanish leftovers inside emitted content: `Sí`/`No` cells in the SECURITY.md support table, inline comments inside the GitHub Actions YAML skeletons, branch examples such as `feature/nombre-funcion`, and the `Signed-off-by: Nombre <email>` trailer. These were being copied verbatim into the user's own repository.

## [1.1.0] - 2026-08-05

### Added

- Distribution as a plugin through a marketplace (`.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`). Until now the only route was cloning the repository into an exact path: if the folder had any other name the skill was not discovered, there was no versioning, and updating depended on remembering to `git pull`. With the marketplace, installing and updating are two commands and the version is declared. Cloning remains as an alternative, and is still the route for OpenCode, which has no plugin system.
- A step 0 check before writing: the skill lists which artifacts already exist in the repository and asks whether to overwrite, merge, skip or write a `.new` file. It used to generate `README.md` and `LICENSE` straight into the root, so in a real repository it clobbered existing files without warning. The default is now to write `.new`: nothing is ever replaced without explicit confirmation.
- A final verification loop: it checks that every marked file exists, that no placeholder is left unsubstituted, that the downloaded `LICENSE` is not empty, that `reuse lint` passes if `REUSE.toml` was generated, and that the `.github/` YAML files parse. It fixes and repeats up to three times, and explicitly reports what it could not check instead of assuming it passed.
- `allowed-tools` in the frontmatter, derived from what the skill actually touches, to document its scope and reduce permission friction. It does not include `git`: the skill writes documentation about commit signing and branch protection, but it does not run those commands.
- A table of contents at the top of `references/conventional-commits.md`, which had grown past 100 lines and was awkward to navigate.

### Changed

- Invocation is now namespaced: `/open-source:open-source`. This also affects anyone with the repository cloned into `~/.claude/skills/`, because the presence of `.claude-plugin/plugin.json` makes Claude Code load it as the plugin `open-source@skills-dir` rather than as a standalone skill. Nothing changes in OpenCode, where it is still invoked as `/open-source`.
- The frontmatter `description` now explains what the skill does as well as when to use it, and does so in the third person, so the model can decide better when to activate it.
- The license comparison table moved to `references/license.md`. It used to live in `SKILL.md`, so its context cost was paid on every invocation even when the user was not going to generate a license at all, which contradicted the project's own *progressive disclosure*.
- Placeholders changed from `<NAME>` to `{{NAME}}`, because angle brackets get confused with XML tags. Angle brackets are kept wherever an external specification requires them (the Conventional Commits format, the default `git merge`/`git revert` messages, and the email in SPDX headers and in the `Signed-off-by` trailer).
- Resolving the SHA of a GitHub Action no longer assumes `gh` is installed and authenticated: it falls back to the public API with `curl` and, if there is no network either, it forces asking rather than inventing a SHA, which would break the workflow on its first run.
- Instructions reworded so they neither age badly nor depend on a specific client: the survey is described without naming any client's selection tool, and the warning about generating license texts by hand keeps its reasoning but no longer quotes a literal error code.

### Fixed

- `curl -o` could overwrite an existing `LICENSE`, bypassing step 0; `references/license.md` now requires respecting the agreed path.
- Unified terminology in `SKILL.md` ("skill", "marked option", "survey"), routing table paths turned into links, and inherited HTML (`<pre>`, `<sup>`) replaced with markdown in `references/conventional-commits.md`.

## [1.0.1] - 2026-07-18

### Added

- Compatibility with OpenCode, documented in the README together with its own installation paths. The skill format is an open standard, so it already worked there; what was missing was saying so and explaining that OpenCode also reads the Claude Code folders, so an existing clone is reused.
- A guardrail in `references/license.md` against writing license texts by hand. Reproducing a long license word by word in the model output was slow, error-prone and could be blocked by the provider's output filters, which made the whole artifact fail; the text is now always downloaded from its canonical source.

### Changed

- More detailed license selection guidance in `SKILL.md`, so the user gets a real comparison before choosing rather than a bare list of identifiers.
- Spanish and Galician typographic conventions added to `SKILL.md`, because the generated documentation was following English capitalization rules in headings regardless of the chosen language.

### Fixed

- Several corrections to `SKILL.md` for more predictable behaviour, so that the same request produces the same artifacts instead of depending on how the instructions were read.

## [1.0.0] - 2026-07-05

### Added

- Initial release of the `open-source` skill for Claude Code, built so that setting up the open source governance of a project (hackathon or real) does not depend on remembering from memory which documents are needed or what each one must contain.
- `SKILL.md` with the initial 15-option survey (README, LICENSE, REUSE.toml, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, `.github/` templates, GitHub Actions, Dependabot, conventional commits, GPG + DCO, git flow and ARCHITECTURE_DECISIONS), the data request conditioned on the marked options, and the minimum file structure of an open source project.
- A routing table with *progressive disclosure*: the details of each artifact live in their own `references/` file and are loaded only if the option was marked, to keep the context cost bounded.
- The 15 references in `references/` with the best practices for each artifact according to the FSF and the OSI.
- Documentation of the repository itself by applying the skill to it (*dogfooding*): `README.md` with installation, usage and troubleshooting; an MIT `LICENSE`; and this `CHANGELOG.md`.

[Unreleased]: https://github.com/igarbayo/open-source/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/igarbayo/open-source/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/igarbayo/open-source/compare/v1.0.1...v1.1.0
[1.0.1]: https://github.com/igarbayo/open-source/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/igarbayo/open-source/releases/tag/v1.0.0
