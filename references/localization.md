# Localization

Read this file **only when the documentation language chosen by the user is not English**. It describes typographic conventions that differ from English ones, so that the generated documents read as if a native speaker had written them instead of as a translation from English.

These rules apply to the *generated* documentation, never to this skill's own instructions.

## General rule: sentence case, not Title Case

English uses Title Case in headings (`## Getting Started With The Project`). Most other languages do not. In them, headings and titles capitalize **only the first word and proper nouns**.

Apply sentence case to every heading, table header and list title of the generated documents.

## Spanish

**Capitalization.** Only the first word and proper nouns:

| Wrong (English habit) | Right |
|---|---|
| `## Guía De Contribución` | `## Guía de contribución` |
| `## Cómo Reportar Un Fallo` | `## Cómo reportar un fallo` |
| `## Política De Seguridad` | `## Política de seguridad` |
| `## Decisiones De Arquitectura` | `## Decisiones de arquitectura` |

Proper nouns keep their capitals: `## Instalación con Docker`, `## Integración con GitHub Actions`.

**The em dash (`—`).** In Spanish it introduces a parenthetical remark or an aside, always in pairs when the clause is embedded, and it never replaces a colon:

| Wrong | Right |
|---|---|
| `Requisitos — Node.js 20 y npm 10.` | `Requisitos: Node.js 20 y npm 10.` |
| `El proyecto — nacido en un hackathon — sigue activo.` | correct: the dashes enclose an aside |
| `Respuesta en 48 horas — salvo en agosto.` | `Respuesta en 48 horas, salvo en agosto.` |

When a list item pairs a term with its definition, use a colon, not a dash: `- **Mantenedor**: revisa y aprueba pull requests.`

## Galician

The same two rules apply: sentence case in headings, and the em dash reserved for asides rather than used in place of a colon.

| Wrong | Right |
|---|---|
| `## Guía De Contribución` | `## Guía de contribución` |
| `## Como Informar Dun Fallo` | `## Como informar dun fallo` |
| `Requisitos — Node.js 20 e npm 10.` | `Requisitos: Node.js 20 e npm 10.` |

## Other languages

This file currently documents Spanish and Galician. If the user picks a language not covered here, still apply the general sentence-case rule and follow that language's own typographic conventions rather than English ones. New language sections can be added here without touching `SKILL.md`.
