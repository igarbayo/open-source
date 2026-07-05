# Autenticación de commits: GPG + DCO

Son **dos mecanismos distintos e independientes**; este proyecto adopta ambos:

## Firma GPG (autentica al autor)

Todos los commits vendrán firmados con GPG (`git commit -S`, o automático con la configuración):

```
git config --global user.signingkey <GPG_KEY_ID>
git config --global commit.gpgsign true
```

Se restringirá en GitHub que solo se acepten commits firmados, mediante reglas de protección en la sección Branches del repositorio, sobre la rama principal (main o master) y cualquier rama de desarrollo (develop, staging, ...). Esto garantiza que se pueda verificar la identidad del autor de cada cambio.

Además, se colocará un documento docs/GPG_KEY.md que explique cómo generar una clave GPG, cómo configurarla en Git y GitHub, y cómo verificar la autenticidad de los commits firmados (`git log --show-signature`).

## DCO (certifica el derecho a contribuir)

El DCO (Developer Certificate of Origin) no es una firma criptográfica: es una declaración legal de que el colaborador tiene derecho a aportar su contribución bajo la licencia del proyecto.

- Se incluirá en la raíz del repositorio un fichero `DCO` con el texto íntegro del Developer Certificate of Origin 1.1 (https://developercertificate.org/).
- Cada commit debe llevar el trailer `Signed-off-by: Nombre <email>`, que se añade con `git commit -s` (minúscula; distinto de `-S` de GPG — se pueden combinar: `git commit -s -S`).
- Opcionalmente, se puede exigir en CI con la GitHub App "DCO" o una action equivalente que rechace PRs con commits sin sign-off.
- CONTRIBUTING.md debe explicar el sign-off como requisito del proceso de PR.