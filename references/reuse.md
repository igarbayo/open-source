# REUSE.toml y cabeceras SPDX

Seguimos la especificación REUSE 3.2. **No usar `.reuse/dep5`: está deprecado** y fue reemplazado por `REUSE.toml` en la raíz del repositorio.

Estrategia por tipo de fichero:

- **Código green field (nuevo)**: cabecera SPDX al inicio de cada fichero fuente, como comentario:

  ```
  # SPDX-FileCopyrightText: 2026 <MAINTAINER_NAME> <email>
  # SPDX-License-Identifier: MIT
  ```

  Se puede automatizar con `pipx run reuse annotate --copyright "<NAME> <email>" --license MIT <ficheros>`.

- **Ficheros donde no se puede editar el contenido** (imágenes, binarios, datasets): fichero sidecar `<nombre>.<ext>.license` con las dos líneas SPDX, o cubrirlos vía `REUSE.toml`.

- **Código heredado (brown field), documentación y ficheros masivos**: declararlos en `REUSE.toml` en la raíz. Ejemplo mínimo:

  ```toml
  version = 1

  [[annotations]]
  path = ["docs/**", "*.md"]
  SPDX-FileCopyrightText = "2026 <MAINTAINER_NAME> <email>"
  SPDX-License-Identifier = "MIT"

  [[annotations]]
  path = "assets/**"
  SPDX-FileCopyrightText = "2026 <MAINTAINER_NAME> <email>"
  SPDX-License-Identifier = "CC-BY-4.0"
  ```

Cada licencia referenciada debe tener su texto completo en `LICENSES/<SPDX-ID>.txt` (ver references/license.md).

Verificación: `pipx run reuse lint` (o `pip install reuse && reuse lint`) debe pasar sin errores antes de dar por terminado este artefacto.