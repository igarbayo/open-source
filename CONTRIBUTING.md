# Contributing

Thank you for taking the time to read this. It genuinely means a lot. `open-source` is a small project maintained by one person, and the fact that you are here considering contributing to it is not something taken for granted.

Before anything else, the honest expectation about timing: **the maintainer is a student, so there is no fixed review time and it can be long.** A pull request may sit for weeks during term. That is not disinterest, and a polite ping on a PR that has gone quiet is welcome rather than rude.

## What this repository is

It ships Markdown and JSON, and nothing else. There is no build, no test runner and no dependency manifest. The artifact is a skill in the [Agent Skills](https://github.com/vercel-labs/skills) format:

- `SKILL.md` — the survey, the writing rules and the routing table. It is loaded into the agent's context **on every invocation**, so every line added here is paid for by every user, every time.
- `references/*.md` — one file per generated artifact, loaded only when the corresponding option was selected. This is where detail belongs.
- `.claude-plugin/` — the plugin and marketplace manifests for Claude Code.

That split is the whole architecture, and it is the first thing to check a change against: **if what you are adding is detail about one artifact, it goes in `references/`, not in `SKILL.md`.**

## Setting up

There is nothing to install to edit the files. To actually exercise a change you need a coding agent that reads the Agent Skills format — Claude Code or OpenCode — and a throwaway repository to point it at:

```bash
git clone https://github.com/igarbayo/open-source.git
cd open-source

# Install your working copy into the agent, per project or globally
npx skills add ./ 
# or symlink/clone it into ~/.claude/skills/open-source or ~/.config/opencode/skills/open-source
```

Then, from a scratch repository, invoke the skill and read what it produces. A skill is a prompt: the only meaningful test is running it and looking at the files that come out.

The one automated check that exists locally is REUSE compliance, which CI also enforces:

```bash
pipx run reuse lint
```

## Making a change

1. **Fork** the repository and create a branch with a descriptive name off `main`: `feature/scorecard-badge`, `fix/broken-routing-path`.
2. Make the change. Keep the diff to one concern.
3. Run `pipx run reuse lint`. If you added a file, it may need an entry in `REUSE.toml`.
4. **Try it.** Run the skill against a scratch repository and confirm the generated output is what you expected. Paste the relevant part of that output into the pull request — for a change to a prompt, the generated result *is* the evidence.
5. Open a pull request against `main`, describing what changes for the user of the skill, not only which files moved.
6. A pull request needs approval from **at least one maintainer** before it merges.

## Style

The repository has no formatter configured, so the style is the one already in the files. Match it:

- Prose in **English**, aimed at a human reader, explaining *why* and not only *what*. `README.md` is mirrored by `README.es.md`; if you change one, change the other.
- The instructions are written in English, but the documentation the skill *generates* can be in any language. Those are separate axes — do not conflate them. Language-specific typographic conventions live in `references/localization.md`.
- Sentence-case headings, no trailing whitespace, one trailing newline.
- Every new file needs licensing metadata: an SPDX header, or an entry in `REUSE.toml` for formats that admit no comments.
- Workflows follow the rules this repository imposes on the ones it generates: `permissions: read-all` at workflow level with minimal per-job elevation, and every third-party action pinned to a **full commit SHA** with the tag in a trailing comment.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/), which is also what the skill teaches:

```
feat: add the OpenSSF Scorecard workflow
fix: correct the relative path in the routing table
docs: explain the output-language question in the README
```

Commits are **GPG-signed** in this repository. Configure signing before your first commit:

```bash
git config user.signingkey <YOUR_KEY_ID>
git config commit.gpgsign true
```

## Changelog

[CHANGELOG.md](CHANGELOG.md) follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project follows [Semantic Versioning](https://semver.org/). **Any significant change adds an entry under `## [Unreleased]`**, written in prose that explains the reasoning. A history that reads like a list of touched files is not worth keeping.

## Definition of done

A contribution is ready when all of the following hold:

- It does one thing, and the pull request says what that thing changes for the user.
- Detail lives in `references/`; `SKILL.md` grew only if the change genuinely belongs to the survey or the routing table.
- It has been run against a real repository and the output was inspected.
- `pipx run reuse lint` passes and CI is green.
- `CHANGELOG.md` has an entry under `[Unreleased]`.
- `README.md` and `README.es.md` agree with each other and with the behaviour.

## Reporting things

- **Bugs and ideas**: [open an issue](https://github.com/igarbayo/open-source/issues). For a bug, say which agent you used, how you installed the skill, what you asked for and what it produced.
- **Security**: do not use the issue tracker. Follow [SECURITY.md](SECURITY.md).
- **Conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) applies to every space in this project.
