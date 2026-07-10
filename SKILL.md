---
name: open-source
description: "Use when setting up open-source governance for a project (hackathon repo or real): README, LICENSE, REUSE/SPDX, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, templates .github, conventional commits, GPG signature, git flow."
---

# Buenas prácticas Open Source según la FSF

Todos los documentos estarán escritos en lenguaje natural, y orientados para humanos y no máquinas. Los documentos tendrán ejemplos que faciliten la comprensión a las personas.

La encuesta de opción múltiple se realizará al principio de la ejecución de la SKILL. En ella se han de marcar qué partes de la estrategia Open Source se desean implementar.

**Presenta la encuesta como un único mensaje de texto plano con la lista numerada completa (todas las opciones juntas en un solo bloque), NO mediante el selector interactivo de preguntas.** El usuario responderá en un solo mensaje indicando los números que desea (por ejemplo, "1, 2, 5, 12"), un rango ("1-8"), o "todas" para implementarlas todas. No repartas las opciones en grupos ni pestañas temáticas.

1. README.md
2. LICENSE
3. REUSE.toml
4. CONTRIBUTING.md
5. SECURITY.md
6. CODE_OF_CONDUCT.md
7. GOVERNANCE.md
8. CHANGELOG.md
9. Plantillas de issues y pull requests en carpeta .github/
10. Workflow de GitHub Actions en carpeta .github/workflows/
11. Dependabot en carpeta .github/
12. Conventional commits
13. Autenticación de commits con GPG + DCO
14. Git flow y Pull Requests
15. ARCHITECTURE_DECISIONS.md

Si el usuario responde "todas" (o equivalente), se marcan las 15 opciones.

Al invocar la SKILL, una vez leído todo el documento y realizada la encuesta descrita anteriormente, se pedirán únicamente los datos relevantes para las opciones marcadas:
- Idioma en el que se generará toda la documentación (por defecto, inglés): siempre. Si se elige español o gallego, respeta sus convenciones tipográficas (no las inglesas): en los títulos y encabezados solo se capitaliza la primera palabra y los sustantivos propios (no cada palabra, a diferencia del *Title Case* inglés); y la raya (—) se emplea únicamente para incisos o aclaraciones, nunca en sustitución de los dos puntos (:).
- Nombre del proyecto: <PROJECT_NAME>: siempre
- Licencia elegida, recomendando al usuario licencias Open Source aprobadas por la OSI más comunes (el detalle está en references/license.md, que se consulta solo al generar el artefacto): solo si se marcó LICENSE o REUSE.toml. **En esta opción es OBLIGATORIO imprimir por pantalla, antes de pedir la elección, la siguiente tabla-resumen para ayudar al usuario a decidir:**

  | Licencia | Tipo | En una frase |
  |----------|------|--------------|
  | **MIT** | Permisiva | La más simple y popular: haz lo que quieras con el código, solo conserva el aviso de copyright. Máxima adopción, sin cláusula de patentes. |
  | **Apache-2.0** | Permisiva | Como MIT pero con concesión explícita de patentes y protección frente a demandas; recomendada para proyectos con implicaciones de patentes o respaldo empresarial. |
  | **BSD-3-Clause** | Permisiva | Muy parecida a MIT, añade una cláusula que prohíbe usar el nombre de los autores para promocionar derivados sin permiso. |
  | **GPL-3.0** | Copyleft | Cualquier obra derivada debe distribuirse bajo la misma licencia (código abierto obligatorio). Protege que el software siga siendo libre, pero reduce su adopción comercial. |
  | **AGPL-3.0** | Network copyleft | GPL-3.0 extendida a servicios en red: si ofreces el software como servicio web, debes publicar el código fuente a los usuarios. Ideal para SaaS que quiere evitar apropiación cerrada. |

  Tras imprimir la tabla, pregunta al usuario cuál elige y recuerda que todos estos productos Open Source se entregan sin garantías (*no warranties*).
- Cuánto tiempo se va a tardar en revisar y resolver una contribución (y disponibilidad de los mantenedores, p. ej. si son estudiantes): solo si se marcó CONTRIBUTING.md o SECURITY.md
- Nombre del hackathon en el que se ha desarrollado el proyecto, si aplica: <HACKATHON_NAME>: solo si se marcó README.md, CONTRIBUTING.md o ARCHITECTURE_DECISIONS.md
- Nombre, apellidos y correo electrónico de los mantenedores del proyecto (sirven también como titular del copyright en las cabeceras SPDX y el hueco `[fullname]` de las plantillas MIT/BSD, y como contacto de seguridad en las plantillas .github): solo si se marcó CONTRIBUTING.md, CODE_OF_CONDUCT.md, GOVERNANCE.md, SECURITY.md, LICENSE, REUSE.toml o Plantillas de issues y pull requests
- Responsabilidades grupales y reglas de voto para la toma de decisiones, si aplica: solo si se marcó GOVERNANCE.md

El año del copyright (para el hueco `[year]` de las licencias MIT/BSD y las cabeceras `SPDX-FileCopyrightText` de REUSE.toml) no se pregunta: se usa automáticamente el año actual.

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
