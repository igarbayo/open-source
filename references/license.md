# LICENSE

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
