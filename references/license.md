# LICENSE

> **IMPORTANTE: no generes el texto de la licencia a mano.** Los textos de licencia
> largos (GPL-3.0, AGPL-3.0, Apache-2.0, etc.) tienen decenas de KB. Si el modelo
> intenta reproducirlos palabra por palabra en su salida, el filtro de contenido del
> servidor bloquea la respuesta con `400 Output blocked by content filtering policy`
> y la generación del artefacto falla. **Descarga siempre el texto desde la fuente
> canónica** para que el fichero sea idéntico byte a byte al oficial:
>
> ```bash
> mkdir -p LICENSES
> # Sustituye <ID> y la URL por la licencia elegida:
> #   MIT           -> https://raw.githubusercontent.com/spdx/license-list-data/main/text/MIT.txt
> #   Apache-2.0    -> https://www.apache.org/licenses/LICENSE-2.0.txt
> #   BSD-3-Clause  -> https://raw.githubusercontent.com/spdx/license-list-data/main/text/BSD-3-Clause.txt
> #   GPL-3.0       -> https://www.gnu.org/licenses/gpl-3.0.txt
> #   AGPL-3.0      -> https://www.gnu.org/licenses/agpl-3.0.txt
> curl -sSL <URL> -o LICENSE
> cp LICENSE LICENSES/<ID>.txt
> ```
>
> Para MIT/BSD (que llevan huecos `[year]`/`[fullname]`) descarga la plantilla y luego
> rellena solo esos campos con Edit; el resto del texto no se teclea nunca a mano.

Se incluye el fichero de la licencia en la raíz del repositorio y también en la carpeta LICENSES. En la carpeta, tiene formato .txt. También se incluirá en la carpeta LICENSES/ cualquier otra cláusula adicional que sea necesaria para el software o el tipo de licencia, como BSD-3-Clause.txt.

Se debe tener en cuenta:
- Add SPDX headers in source files where possible, or use '.license' sidecar files when not.
- Keep license texts in 'LICENSES/' named by SPDX identifiers (e.g. 'LICENSES/Apache-2.0.txt').
- Ensure every license used has a corresponding text file and no unused licenses are included.
- Use OSI-approved licenses and correct SPDX license expressions.

Es necesario colocar un documento docs/COMPONENTS_LICENSE.md que explique todos los detalles de por qué se ha escogido una licencia particular para el proyecto, incluyendo cualquier consideración legal o de compatibilidad con otras licencias. Con otras licencias incluimos las licencias de todas las librerías, dependencias y assets usados en el proyecto, así como cualquier restricción o requisito adicional que pueda imponer la licencia elegida.

Las licencias Open Source aprobadas por la OSI más comunes son:
- Permisivas: MIT, BSD, Apache 2.
- Copyleft: producto derivado de un software, que debe tener su misma licencia o una con términos compatibles GPL v2, GPL v3. La licencia GPL es la más purista de la FSF, pero por lo tanto es menos probable que la tecnología con esta licencia sea adoptada.
- Network copyleft: AGPL. Es una licencia copyleft que se aplica a software que se ejecuta en servidores y se accede a través de la red. Si los usuarios tienen acceso a la web con un servicio, tienen que tener también acceso al código fuente. Es básicamente un proyecto GPL + una API web. Para montar algo en la red, AGPL 3 es la más común para evitar el robo de software por otras empresas.

Hay que hacer hincapié en que todos los productos Open Source son no warranties.

Tendrá project license y REUSE-compliant licensing metadata.
