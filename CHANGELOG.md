# Changelog

Todos los cambios relevantes de este proyecto se documentan en este fichero.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y el proyecto sigue [Semantic Versioning](https://semver.org/lang/es/).

Todo mantenedor, colaborador o agente de IA que trabaje en este repositorio debe actualizar este fichero con cada cambio significativo (nuevas características, correcciones o mejoras de documentación), explicando en prosa **el porqué** del cambio y no solo qué ficheros se tocaron: el objetivo es un historial legible para humanos.

## [Unreleased]

## [1.0.0] - 2026-07-05

### Añadido

- Publicación inicial de la skill `open-source` para Claude Code, creada para que configurar la gobernanza open source de un proyecto (de hackathon o real) no dependa de recordar de memoria qué documentos hacen falta ni qué debe contener cada uno.
- `SKILL.md` con la encuesta inicial de 15 opciones (README, LICENSE, REUSE.toml, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT, GOVERNANCE, CHANGELOG, plantillas de `.github/`, GitHub Actions, Dependabot, conventional commits, GPG + DCO, git flow y ARCHITECTURE_DECISIONS), la petición de datos condicionada a las opciones marcadas y la estructura mínima de ficheros de un proyecto open source.
- Tabla de enrutado con *progressive disclosure*: el detalle de cada artefacto vive en su propio fichero de `references/` y solo se carga si su opción fue marcada, para mantener acotado el coste de contexto.
- Las 15 referencias en `references/` con las buenas prácticas de cada artefacto según la FSF y la OSI.
- Documentación del propio repositorio aplicando la skill a sí misma (*dogfooding*): `README.md` con instalación, uso y troubleshooting; `LICENSE` MIT; y este `CHANGELOG.md`.

[Unreleased]: https://github.com/igarbayo/open-source/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/igarbayo/open-source/releases/tag/v1.0.0
