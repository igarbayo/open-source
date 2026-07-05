# Dependabot (.github/dependabot.yml)

Se configura Dependabot para mantener las dependencias del proyecto actualizadas y seguras mediante `.github/dependabot.yml`. Dependabot abre PRs con actualizaciones y alerta de CVEs en dependencias, lo que contribuye a mantener el proyecto seguro para usuarios y colaboradores.

Antes de generar el fichero, **detecta los ecosistemas reales del repositorio** (mira los manifiestos: `package.json` → npm, `requirements.txt`/`pyproject.toml` → pip, `Cargo.toml` → cargo, `go.mod` → gomod, `pom.xml` → maven, `Dockerfile` → docker, ...). Añade siempre `github-actions` si existen workflows.

Ejemplo (proyecto npm con workflows):

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

Notas:
- `schedule: weekly` como default razonable para hackathon/proyecto pequeño; los avisos de seguridad llegan igualmente en cuanto se publican.
- Los `groups` agrupan actualizaciones minor/patch en una sola PR para reducir ruido; las major van en PR separada.
- Un bloque `updates` por cada ecosistema/directorio detectado.