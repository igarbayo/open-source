---
name: open-source
description: "Generates the complete open-source governance of a repository: README, LICENSE, REUSE.toml and SPDX headers, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, .github issue/PR templates, GitHub Actions, Dependabot, conventional commits, GPG/DCO signing, git flow and ADRs. Use whenever the user wants to open-source, publish, license or release a project, add community health files or governance docs to a repo (including hackathon projects), or mentions OSI licenses, REUSE/SPDX, FSF best practices or EU CRA."
allowed-tools: Read, Write, Edit, Glob, Grep, WebFetch, Bash(ls:*), Bash(mkdir:*), Bash(cp:*), Bash(wc:*), Bash(curl:*), Bash(gh api:*), Bash(gh auth status:*), Bash(pipx run reuse:*), Bash(reuse:*)
license: MIT
metadata:
  author: igarbayo
  version: "1.1.0"
---

# Buenas prácticas Open Source según la FSF

Todos los documentos estarán escritos en lenguaje natural, y orientados para humanos y no máquinas. Los documentos tendrán ejemplos que faciliten la comprensión a las personas.

La encuesta de opción múltiple se realizará al principio de la ejecución de la skill. En ella se han de marcar qué partes de la estrategia Open Source se desean implementar.

**Presenta la encuesta como un único mensaje de texto plano con la lista numerada completa (todas las opciones juntas en un solo bloque); no uses herramientas de selección interactiva aunque estén disponibles.** El usuario responderá en un solo mensaje indicando los números que desea (por ejemplo, "1, 2, 5, 12"), un rango ("1-8"), o "todas" para implementarlas todas. No repartas las opciones en grupos ni pestañas temáticas.

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

## Paso 0: comprobar qué ya existe (antes de escribir nada)

Justo después de la encuesta y **antes de pedir ningún dato o generar ningún fichero**, comprueba en el repositorio del usuario cuáles de los artefactos correspondientes a las opciones marcadas ya existen. Consulta el árbol de la sección "Estructura mínima de ficheros" para saber qué rutas revisar (por ejemplo: `README.md`, `LICENSE`, `LICENSES/`, `REUSE.toml`, `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md`, `GOVERNANCE.md`, `CHANGELOG.md`, `DCO`, `docs/`, `.github/`).

- Si **no existe ninguno**, dilo en una línea y continúa con normalidad.
- Si **existe alguno**, imprime la lista de ficheros ya presentes (ruta y, si es útil, tamaño o primera línea para identificarlos) y pregunta al usuario en un único mensaje de texto plano qué hacer con ellos. Ofrece estas cuatro opciones, que se pueden combinar por fichero (p. ej. "README: fusionar; LICENSE: omitir"):

  1. **Sobrescribir**: se reemplaza el fichero existente por el generado.
  2. **Fusionar**: se lee el fichero actual y se integra su contenido con el nuevo, conservando lo que ya dice el usuario y añadiendo solo lo que falte.
  3. **Omitir**: se deja el fichero tal cual y no se genera nada para esa opción.
  4. **Escribir `.new`**: se genera junto al original con sufijo `.new` (p. ej. `README.md.new`) para que el usuario compare y decida después.

  Si el usuario no especifica nada para un fichero concreto de la lista, **el valor por defecto es escribir `.new`**: nunca se sobrescribe un fichero existente sin confirmación explícita.

Esta comprobación no aplica a los ficheros que la skill vaya a crear por primera vez, que se escriben directamente.

Al invocar la skill, una vez leído todo el documento, realizada la encuesta y resuelto el paso 0, se pedirán únicamente los datos relevantes para las opciones marcadas (y no se pedirán los datos que solo servían para artefactos omitidos):
- Idioma en el que se generará toda la documentación (por defecto, inglés): siempre. Si se elige español o gallego, respeta sus convenciones tipográficas (no las inglesas): en los títulos y encabezados solo se capitaliza la primera palabra y los sustantivos propios (no cada palabra, a diferencia del *Title Case* inglés); y la raya (—) se emplea únicamente para incisos o aclaraciones, nunca en sustitución de los dos puntos (:).
- Nombre del proyecto: {{PROJECT_NAME}}: siempre
- Licencia elegida, recomendando al usuario las licencias Open Source aprobadas por la OSI más comunes: solo si se marcó la opción 2 (LICENSE) o la 3 (REUSE.toml). **En ese caso es OBLIGATORIO leer [license.md](references/license.md) ANTES de preguntar la licencia e imprimir por pantalla su tabla-resumen; solo después se pide la elección al usuario.**
- Cuánto tiempo se va a tardar en revisar y resolver una contribución (y disponibilidad de los mantenedores, p. ej. si son estudiantes): solo si se marcó CONTRIBUTING.md o SECURITY.md
- Nombre del hackathon en el que se ha desarrollado el proyecto, si aplica: {{HACKATHON_NAME}}: solo si se marcó README.md, CONTRIBUTING.md o ARCHITECTURE_DECISIONS.md
- Nombre, apellidos y correo electrónico de los mantenedores del proyecto (sirven también como titular del copyright en las cabeceras SPDX y el hueco `[fullname]` de las plantillas MIT/BSD, y como contacto de seguridad en las plantillas .github): solo si se marcó CONTRIBUTING.md, CODE_OF_CONDUCT.md, GOVERNANCE.md, SECURITY.md, LICENSE, REUSE.toml o Plantillas de issues y pull requests
- Responsabilidades grupales y reglas de voto para la toma de decisiones, si aplica: solo si se marcó GOVERNANCE.md

El año del copyright (para el hueco `[year]` de las licencias MIT/BSD y las cabeceras `SPDX-FileCopyrightText` de REUSE.toml) no se pregunta: se usa automáticamente el año actual.

## Enrutado

El detalle de cada opción vive en un fichero aparte dentro de `references/`. Por cada opción marcada en la encuesta, **lee su fichero correspondiente ANTES de generar ese artefacto**.

**No leas un fichero de `references/` cuya opción no se haya marcado en la encuesta.** Cargar solo lo necesario mantiene el coste de contexto acotado (progressive disclosure).

Única excepción de orden: [license.md](references/license.md) se lee antes (no al generar el artefacto, sino justo antes de preguntar la licencia), porque contiene la tabla-resumen que hay que imprimir para que el usuario decida.

| Opción marcada            | Fichero a consultar                        |
|---------------------------|--------------------------------------------|
| README.md                 | [readme.md](references/readme.md)          |
| LICENSE                   | [license.md](references/license.md)        |
| REUSE.toml                | [reuse.md](references/reuse.md)            |
| CONTRIBUTING.md           | [contributing.md](references/contributing.md) |
| SECURITY.md               | [security.md](references/security.md)      |
| CODE_OF_CONDUCT.md        | [code-of-conduct.md](references/code-of-conduct.md) |
| GOVERNANCE.md             | [governance.md](references/governance.md)  |
| CHANGELOG.md              | [changelog.md](references/changelog.md)    |
| Plantillas issues/PR      | [github-issue-pr-templates.md](references/github-issue-pr-templates.md) |
| GitHub Actions            | [github-actions.md](references/github-actions.md) |
| Dependabot                | [dependabot.md](references/dependabot.md)  |
| Conventional commits      | [conventional-commits.md](references/conventional-commits.md) |
| Git flow y Pull Requests  | [git-flow-pull-requests.md](references/git-flow-pull-requests.md) |
| Autenticación de commits con GPG + DCO | [gpg-auth.md](references/gpg-auth.md) |
| ARCHITECTURE_DECISIONS.md | [architecture-decisions.md](references/architecture-decisions.md) |

La sección "Estructura mínima de ficheros" está inline en este mismo documento y es el único sitio con el árbol completo de artefactos; consúltala al final para saber dónde va cada fichero generado.

Cuando termines de generar todos los artefactos, ejecuta el "Paso final: verificación" descrito más abajo. La skill no se da por terminada hasta que ese paso pasa.

## Paso final: verificación

Es un **bucle de validación**: ejecuta las comprobaciones, corrige lo que falle, vuelve a ejecutarlas. Repite hasta que todo pase o hasta un máximo de 3 vueltas; si tras la tercera queda algo sin resolver, dilo explícitamente al usuario en vez de darlo por bueno.

1. **Existencia.** Cada opción marcada en la encuesta (salvo las que el usuario decidió omitir en el paso 0) tiene su fichero en disco, en la ruta que indica "Estructura mínima de ficheros". Lista las que falten y genéralas.

2. **Sin placeholders sin sustituir.** Busca en todos los ficheros generados los huecos de plantilla y sustitúyelos por los datos reales recogidos al principio. Como mínimo: `[year]`, `[fullname]`, `[email]`, `{{PROJECT_NAME}}`, `{{HACKATHON_NAME}}`, `{{MAINTAINER_NAME}}`, `{{EMAIL}}`, `{{LICENSE_ID}}`, `{{SHA}}`, `TODO`, `FIXME`, `INSERT`. Un solo resultado es un fallo de verificación; la única excepción admisible es un `@{{SHA}}` de GitHub Actions que no se haya podido resolver y que ya hayas señalado explícitamente al usuario.

3. **LICENSE no vacío.** El `LICENSE` de la raíz y cada `LICENSES/{{LICENSE_ID}}.txt` existen, pesan más de 500 bytes y su contenido corresponde a la licencia elegida (comprueba la primera línea: `MIT License`, `Apache License`, `GNU GENERAL PUBLIC LICENSE`, etc.). Si la descarga con `curl` falló o dejó un fichero vacío o con un HTML de error, repítela desde la URL canónica de [license.md](references/license.md); nunca teclees el texto a mano.

4. **REUSE lint.** Solo si se generó `REUSE.toml`: ejecuta `pipx run reuse lint` (alternativa: `pip install reuse && reuse lint`). Debe terminar sin errores. Los fallos típicos son ficheros sin cabecera SPDX ni entrada en `REUSE.toml`, y licencias declaradas sin su texto en `LICENSES/`; corrígelos y vuelve a lanzarlo. Si `pipx`/`pip` no están disponibles en el entorno, indícalo al usuario y deja el comando escrito para que lo ejecute él, en lugar de dar el artefacto por validado.

5. **Sintaxis de los YAML.** Solo si se generaron `.github/workflows/*.yml`, `.github/dependabot.yml` o `.github/ISSUE_TEMPLATE/config.yml`: comprueba que parsean como YAML válido (p. ej. `python -c "import sys,yaml;[yaml.safe_load(open(f)) for f in sys.argv[1:]]" {{ficheros}}`).

Al terminar el bucle, muestra al usuario un resumen corto: qué ficheros se han creado, cuáles se han omitido o escrito como `.new`, y el resultado de cada comprobación (incluida la salida de `reuse lint` si se ejecutó). Si alguna comprobación no se pudo ejecutar, dilo; no la marques como superada.

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
│   └── {{LICENSE_ID}}.txt           # Texto completo de cada licencia usada (e.g. MIT.txt)
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
