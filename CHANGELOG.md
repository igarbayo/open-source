# Changelog

Todos los cambios relevantes de este proyecto se documentan en este fichero.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y el proyecto sigue [Semantic Versioning](https://semver.org/lang/es/).

Todo mantenedor, colaborador o agente de IA que trabaje en este repositorio debe actualizar este fichero con cada cambio significativo (nuevas características, correcciones o mejoras de documentación), explicando en prosa **el porqué** del cambio y no solo qué ficheros se tocaron: el objetivo es un historial legible para humanos.

## [Unreleased]

## [1.1.0] - 2026-08-05

### Añadido

- Distribución como plugin mediante marketplace (`.claude-plugin/plugin.json` y `.claude-plugin/marketplace.json`). Hasta ahora la única vía era clonar el repositorio en una ruta exacta: si la carpeta se llamaba de otro modo la skill no se descubría, no había versionado y actualizar dependía de acordarse de hacer `git pull`. Con el marketplace, instalar y actualizar son dos comandos y la versión queda declarada. El clon se mantiene como alternativa, y sigue siendo la vía de OpenCode, que no tiene sistema de plugins.
- Paso 0 de comprobación antes de escribir: la skill lista qué artefactos ya existen en el repositorio y pregunta si sobrescribir, fusionar, omitir o escribir un `.new`. Antes generaba `README.md` y `LICENSE` directamente en la raíz, de modo que en un repositorio real machacaba los ficheros existentes sin avisar. Por defecto escribe `.new`: nunca se reemplaza nada sin confirmación explícita.
- Paso final de verificación en bucle: comprueba que existe cada fichero marcado, que no queda ningún placeholder sin sustituir, que el `LICENSE` descargado no está vacío, que `reuse lint` pasa si se generó `REUSE.toml` y que los YAML de `.github/` parsean. Corrige y repite hasta tres veces, y declara explícitamente lo que no ha podido comprobar en vez de darlo por bueno.
- `allowed-tools` en el frontmatter, derivado de lo que la skill toca de verdad, para documentar su alcance y reducir la fricción de permisos. No incluye `git`: la skill escribe documentación sobre firma de commits y protección de ramas, pero no ejecuta esas órdenes.
- Índice al principio de `references/conventional-commits.md`, que había crecido por encima de las 100 líneas y era incómodo de recorrer.

### Cambiado

- La invocación pasa a estar bajo espacio de nombres: `/open-source:open-source`. Afecta también a quien tenga el repositorio clonado en `~/.claude/skills/`, porque la presencia de `.claude-plugin/plugin.json` hace que Claude Code lo cargue como plugin `open-source@skills-dir` en lugar de como skill suelta. En OpenCode no cambia nada y se sigue invocando como `/open-source`.
- La `description` del frontmatter explica ahora qué hace la skill además de cuándo usarla, y en tercera persona, para que el modelo pueda decidir mejor cuándo activarla.
- La tabla comparativa de licencias se mueve a `references/license.md`. Estaba en `SKILL.md`, así que su coste de contexto se pagaba en toda invocación aunque el usuario no fuese a generar ninguna licencia, lo que contradecía el propio *progressive disclosure* del proyecto.
- Los placeholders pasan de `<NOMBRE>` a `{{NOMBRE}}`, porque los angulares se confunden con etiquetas XML. Se conservan los angulares allí donde los exige una especificación ajena (formato de Conventional Commits, mensajes por defecto de `git merge`/`git revert`, correo en las cabeceras SPDX y en el trailer `Signed-off-by`).
- La resolución del SHA de las GitHub Actions deja de asumir que `gh` está instalado y autenticado: cae a la API pública con `curl` y, si tampoco hay red, obliga a preguntar en vez de inventarse el SHA, que rompería el workflow en la primera ejecución.
- Instrucciones reformuladas para que no envejezcan ni dependan de un cliente concreto: se describe la encuesta sin nombrar la herramienta de selección de ningún cliente, y el aviso sobre generar textos de licencia a mano conserva el motivo pero ya no cita un código de error literal.

### Corregido

- `curl -o` podía sobrescribir un `LICENSE` existente saltándose el paso 0; ahora `references/license.md` obliga a respetar la ruta acordada.
- Terminología unificada en `SKILL.md` ("skill", "opción marcada", "encuesta"), rutas de la tabla de enrutado convertidas en enlaces y HTML heredado (`<pre>`, `<sup>`) sustituido por markdown en `references/conventional-commits.md`.

## [1.0.0] - 2026-07-05

### Añadido

- Publicación inicial de la skill `open-source` para Claude Code, creada para que configurar la gobernanza open source de un proyecto (de hackathon o real) no dependa de recordar de memoria qué documentos hacen falta ni qué debe contener cada uno.
- `SKILL.md` con la encuesta inicial de 15 opciones (README, LICENSE, REUSE.toml, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, plantillas de `.github/`, GitHub Actions, Dependabot, conventional commits, GPG + DCO, git flow y ARCHITECTURE_DECISIONS), la petición de datos condicionada a las opciones marcadas y la estructura mínima de ficheros de un proyecto open source.
- Tabla de enrutado con *progressive disclosure*: el detalle de cada artefacto vive en su propio fichero de `references/` y solo se carga si su opción fue marcada, para mantener acotado el coste de contexto.
- Las 15 referencias en `references/` con las buenas prácticas de cada artefacto según la FSF y la OSI.
- Documentación del propio repositorio aplicando la skill a sí misma (*dogfooding*): `README.md` con instalación, uso y troubleshooting; `LICENSE` MIT; y este `CHANGELOG.md`.

[Unreleased]: https://github.com/igarbayo/open-source/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/igarbayo/open-source/compare/v1.0.1...v1.1.0
[1.0.0]: https://github.com/igarbayo/open-source/releases/tag/v1.0.0
