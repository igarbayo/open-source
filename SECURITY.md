# Security policy

This policy follows the spirit of the EU Cyber Resilience Act. Non-commercial free software is exempt from the CRA's manufacturer obligations, and this project is a single maintainer's side project rather than a product, so nothing here is a legal commitment. It is written anyway because a skill that generates security policies for other repositories should hold itself to the standard it hands out.

## Supported versions

| Version | Supported |
|---|---|
| `1.2.x` (latest) | Yes |
| `< 1.2.0` | No |

There is no long-term support branch. Fixes land on `main` and are published in the next tagged release; the fix for a reported issue is to update, not to backport.

## Reporting a vulnerability

**Do not open a public issue for a security report.** Use either of these private channels:

1. **GitHub Private Vulnerability Reporting** — the *Security* tab of this repository, "Report a vulnerability". This is the preferred route: it keeps the report, the discussion and the eventual advisory in one place.
2. **Email** to <ignacio.garbayo@rai.usc.es>, with `SECURITY` in the subject line.

Useful things to include: what an attacker gains, the smallest reproduction you have, the version or commit you tested, and whether you intend to disclose publicly on a schedule of your own.

## Response times

The maintainer is a student, so these are best-effort commitments and not an SLA:

- **Acknowledgement of the report: within 72 hours.**
- An initial assessment — whether it is in scope, and how severe it looks — within a week.
- A fix, or an explanation of why there will not be one, as availability allows. Academic workload can make this slow, and a report that has gone quiet for two weeks is worth pinging.

## What is and is not in scope

This repository ships Markdown and JSON. It has no runtime, no dependencies to speak of, no server and no data. What it does have is a security surface that documentation repositories do have and that is easy to overlook: **the content of `SKILL.md` and `references/**` is loaded into a coding agent's context and instructs that agent to write files into the user's own project.**

In scope:

- Content in this repository that would cause an agent to write somewhere it should not, exfiltrate repository contents, or execute commands beyond generating the requested governance files — prompt injection, in other words, whether introduced deliberately or through a careless edit.
- Emitted templates that are insecure by construction: a GitHub Actions skeleton with an over-broad `permissions` block, an action pinned to a mutable tag, a workflow that interpolates untrusted input into a `run` step.
- The workflows and manifests of this repository itself.

Out of scope:

- Vulnerabilities in Claude Code, OpenCode, the `skills` CLI or any agent that loads this skill. Report those to their own maintainers.
- The output of an agent that ran the skill and then improvised. The skill describes what to generate; it cannot constrain a model that ignores it. Bugs in the generated result are welcome as ordinary issues.
- Legal adequacy of the licences, policies or CRA statements the skill generates. It is documentation, not legal advice.

## Known limitations

- No external security audit. No formal review of the emitted templates beyond the maintainer's own reading.
- Third-party actions in the emitted workflows are pinned to a full commit SHA, which removes tag hijacking but does not vouch for the action's own supply chain.
- The skill writes files into your repository. Review the diff before committing it, the same as you would for any generated code.

## Disclosure policy

Coordinated disclosure. Please give the maintainer a chance to ship a fix before publishing details — 90 days is a reasonable ceiling, and less if the fix lands sooner. Fixed issues are published as a GitHub Security Advisory and noted in [CHANGELOG.md](CHANGELOG.md). Reporters are credited by name unless they ask not to be.
