---
name: open-source
description: "Generates the complete open-source governance of a repository: README, LICENSE, REUSE.toml and SPDX headers, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, .github issue/PR templates, GitHub Actions, Dependabot, conventional commits, GPG/DCO signing, git flow and ADRs. Use whenever the user wants to open-source, publish, license or release a project, add community health files or governance docs to a repo (including hackathon projects), or mentions OSI licenses, REUSE/SPDX, FSF best practices or EU CRA."
allowed-tools: Read, Write, Edit, Glob, Grep, WebFetch, Bash(ls:*), Bash(mkdir:*), Bash(cp:*), Bash(wc:*), Bash(curl:*), Bash(gh api:*), Bash(gh auth status:*), Bash(pipx run reuse:*), Bash(reuse:*)
license: MIT
metadata:
  author: igarbayo
  version: "1.2.0"
---

# Open source best practices according to the FSF

Every document must be written in natural language and aimed at humans, not machines. Documents must include examples that make them easier for people to understand.

These instructions are written in English. The language of the *generated* documentation is a separate choice made by the user (see the language question below); English is only the default, never a constraint.

The multiple-choice survey runs at the very beginning of the skill. In it, the user marks which parts of the open source strategy they want to implement.

**Present the survey as a single plain-text message containing the full numbered list (every option together in one block); do not use interactive selection tools even if they are available.** The user replies in a single message with the numbers they want (for example, "1, 2, 5, 12"), a range ("1-8"), or "all" to implement every option. Do not split the options into thematic groups or tabs.

1. README.md
2. LICENSE
3. REUSE.toml
4. CONTRIBUTING.md
5. SECURITY.md
6. CODE_OF_CONDUCT.md
7. GOVERNANCE.md
8. CHANGELOG.md
9. Issue and pull request templates in .github/
10. GitHub Actions workflows in .github/workflows/
11. Dependabot in .github/
12. Conventional commits
13. Commit authentication with GPG + DCO
14. Git flow and pull requests
15. ARCHITECTURE_DECISIONS.md

If the user answers "all" (or an equivalent), all 15 options are marked. Accept the answer in whatever language the user writes it (for example, "todas" or "todo"); the option list is in English, but the user does not have to be.

## Step 0: check what already exists (before writing anything)

Right after the survey and **before asking for any data or generating any file**, check which of the artifacts corresponding to the marked options already exist in the user's repository. Consult the tree in the "Minimum file structure" section to know which paths to inspect (for example: `README.md`, `LICENSE`, `LICENSES/`, `REUSE.toml`, `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md`, `GOVERNANCE.md`, `CHANGELOG.md`, `DCO`, `docs/`, `.github/`).

- If **none of them exist**, say so in one line and continue as usual.
- If **some do exist**, print the list of files already present (path and, where useful, size or first line to identify them) and ask the user in a single plain-text message what to do with them. Offer these four options, which can be combined per file (e.g. "README: merge; LICENSE: skip"):

  1. **Overwrite**: the existing file is replaced by the generated one.
  2. **Merge**: the current file is read and its content integrated with the new one, preserving what the user already wrote and adding only what is missing.
  3. **Skip**: the file is left untouched and nothing is generated for that option.
  4. **Write `.new`**: the file is generated next to the original with a `.new` suffix (e.g. `README.md.new`) so the user can compare and decide later.

  Accept the user's choices in whatever language they write them. If the user says nothing about a specific file in the list, **the default is to write `.new`**: an existing file is never overwritten without explicit confirmation.

This check does not apply to files the skill will create for the first time, which are written directly.

Once the whole document has been read, the survey answered and step 0 resolved, ask only for the data relevant to the marked options (do not ask for data that only served artifacts that were skipped):
- Language in which all the documentation will be generated (English by default): always. **If the chosen language is not English, it is MANDATORY to read [localization.md](references/localization.md) BEFORE generating any document** and to follow its typographic conventions.
- Project name: {{PROJECT_NAME}}: always
- Chosen license, recommending the most common OSI-approved open source licenses: only if option 2 (LICENSE) or option 3 (REUSE.toml) was marked. **In that case it is MANDATORY to read [license.md](references/license.md) BEFORE asking about the license and to print its summary table on screen; only then is the user asked to choose.**
- How long it will take to review and resolve a contribution (and the maintainers' availability, e.g. whether they are students): only if CONTRIBUTING.md or SECURITY.md was marked
- Name of the hackathon the project was built at, if applicable: {{HACKATHON_NAME}}: only if README.md, CONTRIBUTING.md or ARCHITECTURE_DECISIONS.md was marked
- Full name and email address of the project maintainers (they are also used as the copyright holder in the SPDX headers and in the `[fullname]` slot of the MIT/BSD templates, and as the security contact in the .github templates): only if CONTRIBUTING.md, CODE_OF_CONDUCT.md, GOVERNANCE.md, SECURITY.md, LICENSE, REUSE.toml or the issue and pull request templates were marked
- Group responsibilities and voting rules for decision-making, if applicable: only if GOVERNANCE.md was marked

The copyright year (for the `[year]` slot of the MIT/BSD licenses and the `SPDX-FileCopyrightText` headers of REUSE.toml) is never asked for: the current year is used automatically.

## Routing

The details of each option live in a separate file inside `references/`. For every option marked in the survey, **read its corresponding file BEFORE generating that artifact**.

**Do not read a file from `references/` whose option was not marked in the survey.** Loading only what is needed keeps the context cost bounded (progressive disclosure).

There are two exceptions to that rule:
- [license.md](references/license.md) is read earlier than the rest — not when generating the artifact, but right before asking about the license — because it contains the summary table that must be printed for the user to decide.
- [localization.md](references/localization.md) is not tied to any survey option: it is loaded based on the answer to the language question, and only when the chosen language is not English.

| Marked option            | File to consult                        |
|---------------------------|--------------------------------------------|
| README.md                 | [readme.md](references/readme.md)          |
| LICENSE                   | [license.md](references/license.md)        |
| REUSE.toml                | [reuse.md](references/reuse.md)            |
| CONTRIBUTING.md           | [contributing.md](references/contributing.md) |
| SECURITY.md               | [security.md](references/security.md)      |
| CODE_OF_CONDUCT.md        | [code-of-conduct.md](references/code-of-conduct.md) |
| GOVERNANCE.md             | [governance.md](references/governance.md)  |
| CHANGELOG.md              | [changelog.md](references/changelog.md)    |
| Issue/PR templates        | [github-issue-pr-templates.md](references/github-issue-pr-templates.md) |
| GitHub Actions            | [github-actions.md](references/github-actions.md) |
| Dependabot                | [dependabot.md](references/dependabot.md)  |
| Conventional commits      | [conventional-commits.md](references/conventional-commits.md) |
| Git flow and pull requests | [git-flow-pull-requests.md](references/git-flow-pull-requests.md) |
| Commit authentication with GPG + DCO | [gpg-auth.md](references/gpg-auth.md) |
| ARCHITECTURE_DECISIONS.md | [architecture-decisions.md](references/architecture-decisions.md) |

The "Minimum file structure" section is inline in this same document and is the only place with the full tree of artifacts; consult it at the end to know where each generated file goes.

When you have finished generating every artifact, run the "Final step: verification" described below. The skill is not done until that step passes.

## Final step: verification

This is a **validation loop**: run the checks, fix whatever fails, run them again. Repeat until everything passes or up to a maximum of 3 rounds; if something is still unresolved after the third, say so explicitly to the user instead of calling it good.

1. **Existence.** Every option marked in the survey (except those the user chose to skip in step 0) has its file on disk, at the path indicated by "Minimum file structure". List the missing ones and generate them.

2. **No unsubstituted placeholders.** Search every generated file for template slots and replace them with the real data collected at the beginning. At minimum: `[year]`, `[fullname]`, `[email]`, `{{PROJECT_NAME}}`, `{{HACKATHON_NAME}}`, `{{MAINTAINER_NAME}}`, `{{EMAIL}}`, `{{LICENSE_ID}}`, `{{SHA}}`, `TODO`, `FIXME`, `INSERT`. A single hit is a verification failure; the only acceptable exception is a GitHub Actions `@{{SHA}}` that could not be resolved and that you have already flagged explicitly to the user.

3. **LICENSE not empty.** The root `LICENSE` and every `LICENSES/{{LICENSE_ID}}.txt` exist, weigh more than 500 bytes and their content matches the chosen license (check the first line: `MIT License`, `Apache License`, `GNU GENERAL PUBLIC LICENSE`, etc.). If the `curl` download failed or left an empty file or an HTML error page, retry it from the canonical URL in [license.md](references/license.md); never type the text by hand.

4. **REUSE lint.** Only if `REUSE.toml` was generated: run `pipx run reuse lint` (alternative: `pip install reuse && reuse lint`). It must finish without errors. Typical failures are files with neither an SPDX header nor an entry in `REUSE.toml`, and declared licenses whose text is missing from `LICENSES/`; fix them and run it again. If `pipx`/`pip` are not available in the environment, tell the user and leave the command written out for them to run, rather than treating the artifact as validated.

5. **YAML syntax.** Only if `.github/workflows/*.yml`, `.github/dependabot.yml` or `.github/ISSUE_TEMPLATE/config.yml` were generated: check that they parse as valid YAML (e.g. `python -c "import sys,yaml;[yaml.safe_load(open(f)) for f in sys.argv[1:]]" {{files}}`).

When the loop ends, show the user a short summary: which files were created, which were skipped or written as `.new`, and the result of each check (including the `reuse lint` output if it ran). If a check could not be run, say so; do not mark it as passed.

## Minimum file structure

Below is the minimum file structure (if every option is implemented) that an open source project following the practices described in this document should have. A real project may contain more files and folders depending on its needs.

```
project-root/
├── README.md                        # Entry point: description, badges, usage examples
├── LICENSE                          # Main license file at the repository root
├── CONTRIBUTING.md                  # Contributor guide: setup, style, commits
├── SECURITY.md                      # Security policy aligned with the EU CRA
├── CODE_OF_CONDUCT.md               # Code of conduct (Contributor Covenant)
├── GOVERNANCE.md                    # Decision-making, roles and conflict resolution
├── CHANGELOG.md                     # Change history (Keep a Changelog)
├── DCO                              # Developer Certificate of Origin
├── REUSE.toml                       # License declaration for files without SPDX headers
├── LICENSES/
│   └── {{LICENSE_ID}}.txt           # Full text of every license used (e.g. MIT.txt)
├── docs/
│   ├── COMPONENTS_LICENSE.md        # Legal rationale for the license choice and dependencies
│   ├── GPG_KEY.md                   # Instructions to configure GPG and verify signatures
│   └── ARCHITECTURE_DECISIONS.md    # Design decisions, technologies and development process
└── .github/
    ├── dependabot.yml               # Automatic dependency and CVE updates
    ├── pull_request_template.md     # Pull request template
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md            # Bug report template
    │   ├── feature_request.md       # Feature request template
    │   ├── question.md              # Question template
    │   └── config.yml               # Template chooser configuration
    └── workflows/
        ├── build.yml                # CI: project build
        ├── lint.yml                 # CI: static analysis and code style
        ├── test.yml                 # CI: automated test run
        └── security.yml             # CI: security scanning (Scorecard, etc.)
```
