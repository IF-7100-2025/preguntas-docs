# Requerimiento Funcional: Visualizar Interfaz de Inicio para Colaboradores

## Descripción

**RF-07** Este requerimiento funcional describe la capacidad de los colaboradores autenticados de la plataforma social de aprendizaje para visualizar la interfaz de inicio al acceder a la plataforma. Esta interfaz proporcionará un menú lateral para la navegación principal y una sección central para la exploración de categorías, además de una visualización básica de su información personal dentro del menú lateral.

El alcance de este requerimiento incluye la presentación estructurada del menú lateral con las opciones definidas, la sugerencia de categorías en la sección principal, la funcionalidad de búsqueda de categorías (a nivel de interfaz), y la visualización del nombre de usuario y rango al interactuar con la opción correspondiente del menú lateral.

## Necesidad

Actualmente, al iniciar sesión, los colaboradores necesitan una forma clara y organizada de acceder a las funcionalidades principales de la plataforma y de descubrir contenido relevante. Esta interfaz de inicio busca proporcionar una navegación intuitiva y un punto de partida para la interacción del colaborador con la plataforma, facilitando el acceso a la creación de contenido, la revisión de su actividad y la exploración de temas de interés.

## Proceso Actual

En el estado actual del sistema, al iniciar sesión un colaborador podría ser redirigido a una página genérica o a una vista sin una organización clara de las funcionalidades disponibles y sin una sección dedicada a la exploración de categorías. Esto puede dificultar la navegación y la rápida identificación de las opciones relevantes para el usuario.

## Solución Propuesta

Se propone desarrollar una interfaz de inicio para los colaboradores autenticados que contenga los siguientes elementos:

- **Menú Lateral:** Un menú fijo en la parte izquierda de la pantalla con las siguientes opciones: Información Personal (interactivo), Crear Quiz, Crear Pregunta, Historial de Quizzes, Mis Preguntas. El título de este menú será "Usuario".
- **Sección Principal (Exploración de Categorías):** Un área principal donde se mostrarán unas pocas categorías de estudio aleatorias y un campo de entrada de texto para buscar categorías.
- **Visualización de Información Personal:** Al interactuar (clic) con la opción "Información Personal" del menú lateral, se mostrará el nombre de usuario y el rango del colaborador dentro del mismo menú lateral.

## Documentos de Referencia

- [Documento de actores](../../arquitectura/actores.md)
- [CU-07: Visualizar interfaz de inicio para colaboradores](casos-de-uso/CU-07-visualizar-inicio-colaborador.md)

## Casos de Uso Relacionados

- [CU-07: Visualizar interfaz de inicio para colaboradores](casos-de-uso/CU-07-visualizar-inicio-colaborador.md)

## Criterios de Aceptación

1. En la página principal, se mostrará un menú lateral con las siguientes opciones:
    * Información Personal (al hacer clic, se mostrará el nombre de usuario y el rango del usuario).
    * Crear Quiz
    * Crear Pregunta
    * Historial de Quizzes
    * Mis Preguntas
2. En la sección principal de la página, se sugerirán unas pocas categorías de estudio aleatorias (ej: Matemáticas, Ciencias Naturales, Programación, etc.).
3. En la sección principal de la página, habrá un campo de entrada de texto para que el usuario pueda buscar categorías de estudio específicas.
4. En la sección "Información Personal" del menú lateral, al interactuar con ella, el usuario podrá ver su nombre de usuario y su rango dentro de la plataforma.
5. El nombre en la parte superior del menú lateral se mostrará como "Usuario".

---

**Documento Preparado Por:** Kendall Sánchez Chinchilla C27227
**Fecha:** 05-10-2025

---