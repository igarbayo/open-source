---
name: open-source
description: "Use when setting up open-source governance for a project (repo hackathon o real): README, LICENSE, REUSE/SPDX, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, plantillas .github, conventional commits, firma GPG, git flow."
---

# Buenas prácticas Open Source según la FSF

Todos los documentos estarán escritos en lenguaje natural, y orientados para humanos y no máquinas. Los documentos tendrán ejemplos que faciliten la comprensión a las personas.

La encuesta de opción múltiple se realizará al principio de la ejecución de la SKILL En ella se han de marcar qué partes de la estrategia Open Source se desean implementar:
- [ ] README.md
- [ ] LICENSE
- [ ] REUSE.toml
- [ ] CONTRIBUTING.md
- [ ] SECURITY.md
- [ ] CODE_OF_CONDUCT.md
- [ ] GOVERNANCE.md
- [ ] CHANGELOG.md
- [ ] Plantillas de issues y pull requests en carpeta .github/
- [ ] Workflow de GitHub Actions en carpeta .github/workflows/
- [ ] Dependabot en carpeta .github/
- [ ] Conventional commits
- [ ] Autenticación de commits con GPG + DCO
- [ ] Git flow y Pull Requests
- [ ] ARCHITECTURE_DECISIONS.md
- [ ] Todo lo anterior

Al invocar la SKILL, una vez leído todo el documento y realizada la encuesta descrita anteriormente, se pedirán únicamente los datos relevantes para las opciones marcadas:
- Idioma en el que se generará toda la documentación (por defecto, inglés): siempre
- Nombre del proyecto: <PROJECT_NAME>: siempre
- Licencia elegida, recomendando al usuario licencias Open Source aprobadas por la OSI más comunes: permisivas: MIT, Apache-2.0, BSD-3-Clause; copyleft: GPL-3.0; network copyleft: AGPL-3.0 (el detalle está en references/license.md, que se consulta solo al generar el artefacto): solo si se marcó LICENSE o REUSE.toml
- Cuánto tiempo se va a tardar en revisar y resolver una contribución: solo si se marcó CONTRIBUTING.md
- Nombre del hackathon en el que se ha desarrollado el proyecto, si aplica: <HACKATHON_NAME>: solo si se marcó README.md, CONTRIBUTING.md o ARCHITECTURE_DECISIONS.md
- Nombre, apellidos y correo electrónico de los mantenedores del proyecto: solo si se marcó CONTRIBUTING.md, CODE_OF_CONDUCT.md, GOVERNANCE.md o SECURITY.md
- Responsabilidades grupales y reglas de voto para la toma de decisiones, si aplica: solo si se marcó GOVERNANCE.md

## Enrutado

El detalle de cada opción vive en un fichero aparte dentro de `references/`. Por cada casilla marcada en la encuesta, **lee su fichero correspondiente ANTES de generar ese artefacto**.

**No leas un fichero de `references/` cuya opción no se haya marcado en la encuesta.** Cargar solo lo necesario mantiene el coste de contexto acotado (progressive disclosure).

| Opción marcada            | Fichero a consultar                        |
|---------------------------|--------------------------------------------|
| README.md                 | references/readme.md                       |
| LICENSE                   | references/license.md                      |
| REUSE.toml                | references/reuse.md                        |
| CONTRIBUTING.md           | references/contributing.md                 |
| SECURITY.md               | references/security.md                     |
| CODE_OF_CONDUCT.md        | references/code-of-conduct.md              |
| GOVERNANCE.md             | references/governance.md                   |
| CHANGELOG.md              | references/changelog.md                    |
| Plantillas issues/PR      | references/github-issue-pr-templates.md    |
| GitHub Actions            | references/github-actions.md               |
| Dependabot                | references/dependabot.md                   |
| Conventional commits      | references/conventional-commits.md         |
| Git flow y Pull Requests  | references/git-flow-pull-requests.md       |
| Autenticación de commits con GPG + DCO | references/gpg-auth.md              |
| ARCHITECTURE_DECISIONS.md | references/architecture-decisions.md       |

La sección "Estructura mínima de ficheros" está inline en este mismo documento y es el único sitio con el árbol completo de artefactos; consúltala al final para saber dónde va cada fichero generado.

## Estructura mínima de ficheros

A continuación se muestra la estructura mínima (en caso de elegir implementar todas las opciones) de ficheros que debe tener un proyecto open source siguiendo las prácticas descritas en este documento. Un proyecto real puede contener más ficheros y carpetas según sus necesidades.

```
project-root/
├── README.md                        # Punto de entrada: descripción, badges, ejemplos de uso
├── LICENSE                          # Fichero de licencia principal en la raíz
├── CONTRIBUTING.md                  # Guía para contribuidores: setup, estilo, commits
├── SECURITY.md                      # Política de seguridad alineada con EU CRA
├── CODE_OF_CONDUCT.md               # Código de conducta (Contributor Covenant)
├── GOVERNANCE.md                    # Toma de decisiones, roles y resolución de conflictos
├── CHANGELOG.md                     # Historial de cambios (Keep a Changelog)
├── DCO                              # Developer Certificate of Origin
├── REUSE.toml                       # Declaración de licencias para ficheros sin cabecera SPDX
├── LICENSES/
│   └── <LICENSE-ID>.txt             # Texto completo de cada licencia usada (e.g. MIT.txt)
├── docs/
│   ├── COMPONENTS_LICENSE.md        # Justificación legal de la elección de licencia y dependencias
│   ├── GPG_KEY.md                   # Instrucciones para configurar GPG y verificar firmas
│   └── ARCHITECTURE_DECISIONS.md    # Decisiones de diseño, tecnologías y proceso de desarrollo
└── .github/
    ├── dependabot.yml               # Actualizaciones automáticas de dependencias y CVEs
    ├── pull_request_template.md     # Plantilla para pull requests
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md            # Plantilla para reportar bugs
    │   ├── feature_request.md       # Plantilla para solicitar funcionalidades
    │   ├── question.md              # Plantilla para preguntas
    │   └── config.yml               # Configuración del selector de plantillas
    └── workflows/
        ├── build.yml                # CI: compilación del proyecto
        ├── lint.yml                 # CI: análisis estático y estilo de código
        ├── test.yml                 # CI: ejecución de tests automatizados
        └── security.yml             # CI: escaneo de seguridad (Scorecard, etc.)
```
