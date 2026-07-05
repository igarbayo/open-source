# Plantillas de issues y pull requests (.github/)

Las plantillas guían a los colaboradores para que aporten la información que los mantenedores necesitan, y las etiquetas predefinidas facilitan la gestión y priorización. Se generan estos ficheros (plantillas base en inglés; **traducir al idioma elegido** si no es inglés, manteniendo el frontmatter):

## .github/ISSUE_TEMPLATE/bug_report.md

```markdown
---
name: Bug report
about: Something is not working as expected
labels: bug
---

**Describe the bug**
A clear description of what happens. E.g. "The app crashes when uploading a file larger than 10 MB."

**To reproduce**
1. Go to '...'
2. Run '...'
3. See error

**Expected behavior**
What you expected to happen instead.

**Environment**
- OS: [e.g. Windows 11, Ubuntu 24.04]
- Version/commit: [e.g. v1.2.0]

**Logs / screenshots**
Paste relevant output or attach screenshots.
```

## .github/ISSUE_TEMPLATE/feature_request.md

```markdown
---
name: Feature request
about: Suggest an idea or improvement
labels: enhancement
---

**Problem**
What problem does this solve? E.g. "I always have to re-enter my settings after restart."

**Proposed solution**
What you would like to happen.

**Alternatives considered**
Other approaches you thought about, if any.
```

## .github/ISSUE_TEMPLATE/question.md

```markdown
---
name: Question
about: Ask about usage or behavior
labels: question
---

**Question**
What do you want to know? Check the README and existing issues first.

**Context**
What are you trying to achieve?
```

## .github/ISSUE_TEMPLATE/config.yml

```yaml
blank_issues_enabled: false
contact_links:
  - name: Security vulnerability
    url: <SECURITY_CONTACT_URL_OR_MAILTO>
    about: Please report vulnerabilities privately, never as a public issue (see SECURITY.md).
```

## .github/pull_request_template.md

```markdown
**What does this PR do?**
Short description and motivation. Link related issues (Closes #123).

**Checklist**
- [ ] Tests pass locally
- [ ] CHANGELOG.md updated (if user-facing change)
- [ ] Commits follow Conventional Commits
- [ ] Commits are signed off (`git commit -s`, DCO)
```

Ajusta el checklist a las opciones realmente implementadas (p. ej., quita la línea de DCO si no se adoptó, o la de CHANGELOG si no existe).