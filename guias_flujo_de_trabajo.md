# Guía de Flujo de Trabajo para el Desarrollo (Basado en GitHub Flow)

Este documento describe el flujo de trabajo recomendado para el desarrollo de la Plataforma Social de Aprendizaje, basado en el modelo de GitHub Flow. El objetivo es asegurar un proceso de desarrollo colaborativo, eficiente y con un historial de cambios claro.

## 1. Estrategia de Ramas

GitHub Flow se centra en un modelo de ramas simple y efectivo. A continuación, se define la estructura de ramas principales y secundarias que utilizaremos:

### Uso de Ramas Principales

* **`main` (Producción):** Esta rama representa el código que está actualmente en producción o listo para ser desplegado. **Cualquier código en `main` debe ser estable y funcional.** Solo se fusionarán a esta rama cambios que hayan sido completamente probados y aprobados.

* **`develop` (Integración):** Esta rama actuará como la rama de integración principal para todas las nuevas funcionalidades y correcciones de errores. Los desarrolladores trabajarán en ramas secundarias y luego las fusionarán a `develop`. **Esta rama siempre debe reflejar el estado actual del desarrollo.**

### Uso de Ramas Secundarias

Las ramas secundarias se utilizarán para aislar el trabajo en funcionalidades específicas, correcciones de errores, hotfixes y releases. Estas ramas siempre se crearán a partir de la rama `develop` (o `main` en el caso de hotfixes).

* **Ramas de Características (`feature/`)**: Se utilizan para desarrollar nuevas funcionalidades.
    * Se ramifican desde `develop`.
    * El nombre debe ser descriptivo y conciso, utilizando el prefijo `feature/`.
    * **Ejemplo:** `feature/implementar-login`, `feature/crear-perfil-usuario`

* **Ramas de Corrección de Errores (`bugfix/`)**: Se utilizan para corregir errores identificados en la rama `develop`.
    * Se ramifican desde `develop`.
    * El nombre debe ser descriptivo y conciso, utilizando el prefijo `bugfix/`.
    * **Ejemplo:** `bugfix/error-en-validacion-formulario`, `bugfix/problema-con-carga-de-imagenes`

* **Ramas de Hotfix (`hotfix/`)**: Se utilizan para corregir errores críticos encontrados en la rama `main` (producción).
    * **Se ramifican directamente desde `main`.**
    * Después de la corrección, se fusionan tanto a `main` (para desplegar la solución inmediata) como a `develop` (para asegurar que la corrección se incluya en la próxima versión).
    * El nombre debe ser descriptivo y conciso, utilizando el prefijo `hotfix/`.
    * **Ejemplo:** `hotfix/seguridad-vulnerable`, `hotfix/error-critico-en-pago`

* **Ramas de Release (`release/`)**: Se utilizan para preparar una nueva versión para su despliegue a producción.
    * Se ramifican desde `develop` cuando se considera que una versión está lista para ser lanzada.
    * En esta rama se pueden realizar las últimas correcciones de errores y ajustes de documentación específicos para la release.
    * Una vez que la release está lista, se fusiona a `main` (y se etiqueta con el número de versión) y también se fusiona de vuelta a `develop`.
    * El nombre debe indicar la versión, utilizando el prefijo `release/`.
    * **Ejemplo:** `release/1.0.0`, `release/1.1.0`

## 2. Reglas para la Creación y Fusión de Ramas

Para mantener la coherencia y la calidad del código, se seguirán las siguientes reglas para la creación y fusión de ramas:

### Convenciones de Nomenclatura para Ramas

* **Ramas Principales:**
    * Producción: `main`
    * Integración: `develop`
* **Ramas Secundarias:**
    * Características: `feature/<nombre-descriptivo>` (en minúsculas, palabras separadas por guiones)
    * Corrección de Errores: `bugfix/<nombre-descriptivo>` (en minúsculas, palabras separadas por guiones)
    * Hotfix: `hotfix/<nombre-descriptivo>` (en minúsculas, palabras separadas por guiones)
    * Release: `release/<version>` (ej. `release/1.0.0`)

### Uso de Pull Requests y Revisiones de Código

* **Todas las fusiones a las ramas `develop` y `main` deben realizarse a través de Pull Requests (PRs).** Esto garantiza que el código sea revisado antes de ser integrado en las ramas principales.

* **Proceso de Pull Request:**
    1.  Un desarrollador crea una rama secundaria (feature, bugfix, hotfix) y realiza los cambios necesarios.
    2.  Una vez que el trabajo está completo y se han realizado pruebas unitarias y de integración, el desarrollador crea un Pull Request dirigido a la rama objetivo (`develop` para features y bugfixes, `main` para hotfixes y releases desde su rama correspondiente).
    3.  **Se requiere al menos una revisión de código positiva por otro miembro del equipo antes de que el PR pueda ser fusionado.** El revisor debe verificar la calidad del código, el cumplimiento de los estándares, la lógica implementada y la ausencia de errores obvios.
    4.  Una vez que el PR ha sido aprobado, el desarrollador (o un miembro autorizado del equipo) puede fusionar la rama secundaria a la rama objetivo.
    5.  Después de la fusión, la rama secundaria debe ser eliminada para mantener el repositorio limpio.

* **Consideraciones para la Revisión de Código:**
    * La revisión debe ser exhaustiva y constructiva.
    * Se deben proporcionar comentarios claros y específicos sobre las áreas de mejora.
    * El autor del PR debe abordar todos los comentarios antes de que se apruebe la fusión.

Este flujo de trabajo basado en GitHub Flow nos permitirá mantener un código base organizado, facilitar la colaboración entre los miembros del equipo y asegurar la calidad de la Plataforma Social de Aprendizaje.