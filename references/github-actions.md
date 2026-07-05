# Workflows de GitHub Actions (.github/workflows/)

Se automatizan build, lint, tests y seguridad como CI en push y pull request. Scorecard y CodeQL reportan vulnerabilidades y malas prácticas en la pestaña Security del repositorio.

Reglas de seguridad de los workflows (obligatorias):
- `permissions: read-all` a nivel de workflow; elevación mínima y justificada por job donde haga falta.
- Todas las actions de terceros **fijadas a SHA de commit completo**, nunca a tags mutables (elimina el riesgo de tag hijacking en supply chain). Escribe `uses: owner/action@<SHA> # vX.Y.Z` y **resuelve el SHA real** del tag antes de generar el fichero (página de releases de la action o `gh api repos/<owner>/<action>/git/ref/tags/<tag>`).

**Adapta los comandos de build/lint/test al stack real del proyecto** — léelo del repo (package.json scripts, Makefile, pyproject.toml...), no lo inventes. Si el proyecto no compila (p. ej. Python puro), omite build.yml. Esqueletos:

## build.yml / test.yml / lint.yml (mismo patrón, cambia el paso final)

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
      - uses: actions/checkout@<SHA> # vX.Y.Z
      - uses: actions/setup-node@<SHA> # vX.Y.Z — o setup-python/setup-go según stack
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
      - uses: actions/checkout@<SHA> # vX.Y.Z
      - uses: ossf/scorecard-action@<SHA> # vX.Y.Z
        with:
          results_file: results.sarif
          results_format: sarif
      - uses: github/codeql-action/upload-sarif@<SHA> # vX.Y.Z
        with:
          sarif_file: results.sarif

  codeql:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
    steps:
      - uses: actions/checkout@<SHA> # vX.Y.Z
      - uses: github/codeql-action/init@<SHA> # vX.Y.Z
        with:
          languages: javascript # ajustar a los lenguajes del repo
      - uses: github/codeql-action/analyze@<SHA> # vX.Y.Z
```

Se pueden añadir notificaciones de estado para mantener informado al equipo, pero los cuatro workflows anteriores son la base mínima.