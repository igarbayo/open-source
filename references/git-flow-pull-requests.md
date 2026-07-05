# Git flow y pull requests

## Git flow

### Ramas principales
- **`main`** (o `master`): Contiene únicamente el código estable que está en producción. Las versiones se marcan aquí mediante *tags* (ej. `v1.0.0`).
- **`develop`**: Contiene el código en desarrollo para la próxima versión. Es la rama de integración principal.

### Ramas de soporte

#### Ramas de funcionalidad (`feature/*`)
- **Nacen de:** `develop`
- **Se fusionan en:** `develop`
- **Propósito:** Desarrollar nuevas características aisladas del resto del código.
- **Flujo:** `develop` ➔ `feature/nombre-funcion` ➔ `develop`

#### Ramas de lanzamiento (`release/*`)
- **Nacen de:** `develop`
- **Se fusionan en:** `main` **y** `develop`
- **Propósito:** Estabilizar una nueva versión, corregir bugs menores y preparar el paso a producción. No se añaden nuevas funcionalidades.
- **Flujo:**
    1. `develop` ➔ `release/v1.1.0`
    2. `release/v1.1.0` ➔ `main` (se etiqueta como `v1.1.0`)
    3. `release/v1.1.0` ➔ `develop`

#### Ramas de corrección Rápida (`hotfix/*`)
- **Nacen de:** `main`
- **Se fusionan en:** `main` **y** `develop` (o en la rama `release` si hay una activa).
- **Propósito:** Solucionar errores críticos e inmediatos directamente en el entorno de producción.
- **Flujo:**
    1. `main` ➔ `hotfix/solucion-error`
    2. `hotfix/solucion-error` ➔ `main` (se etiqueta como `v1.0.1`)
    3. `hotfix/solucion-error` ➔ `develop`


## Pull requests

Se configurarán tanto la rama main como la rama develop para que requieran revisiones de código antes de permitir la fusión de pull requests. Esto se puede hacer en la sección de Branches del repositorio, estableciendo reglas de protección para ambas ramas. Se bloquerán los commits directos a estas dos ramas. Esto garantiza que todas las contribuciones sean revisadas por al menos otro colaborador antes de ser fusionadas, lo que mejora la calidad del código y reduce la probabilidad de introducir errores en el proyecto.