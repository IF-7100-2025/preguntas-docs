## Caso de uso: **Generar quizzes**

## Descripción
Este caso de uso describe el proceso mediante el cual un usuario puede generar una prueba estructurada a partir de un banco de preguntas registradas por un usuario o generadas por inteligencia artificial en la plataforma de aprendizaje colaborativo, realizar la autoevaluación y registrar el historial de resultados y calificaciones.

## Actores
- **Primarios**: Usuario (Colaborador y Administrador)
- **Secundarios**: Sistema 

## Precondiciones
1. El usuario debe estar autenticado en el sistema.

## Postcondiciones
1. Se genera una prueba estructurada a partir del banco de preguntas.
2. Se almacena el historial de la prueba realizada y su calificación.

# Flujo Principal
1. El usuario accede a la sección de autoevaluaciones.
2. El usuario selecciona la opción **"Generar Nueva Prueba"**.
3. El sistema genera automáticamente una prueba estructurada utilizando preguntas del banco.
4. El sistema presenta la prueba al usuario.
5. El usuario responde todas las preguntas de la prueba.
6. El usuario envía la prueba para su evaluación.
7. El sistema corrige automáticamente la prueba.
8. El sistema muestra la calificación al usuario.
9. El sistema guarda el historial de la prueba realizada, incluyendo:
   - Preguntas presentadas
   - Respuestas seleccionadas
   - Calificación obtenida
   - Fecha y hora de la prueba

# Flujo Alternativo

### FA-01: Error en la generación de la prueba
- En el paso 3, si no hay suficientes preguntas en el banco, el sistema notifica al usuario y da la opción de generar preguntas por cuenta propia o por medio de inteligencia artificial (5 preguntas).

## Prototipos
![Prototipo generar quices en la plataforma](imagenes/prototipo-generar-quicezz-act.png)

## Requerimientos Especiales
- El sistema debe validar que el texto de la pregunta no exceda los 200 caracteres.
- El sistema debe validar que el texto de la pregunta contenga al menos 50 caracteres.
- Cada pregunta debe tener al menos dos opciones de respuesta y una respuesta correcta seleccionada.

## Escenarios de Prueba

| Escenario | Salida Esperada |
|:---|:---|
| Estudiante autenticado accede a "Crear Pregunta", ingresa texto válido, opciones, selecciona una respuesta correcta y asigna categorías, luego hace clic en "Guardar". | La pregunta se guarda exitosamente y se muestra un mensaje de confirmación. |
| Estudiante autenticado accede a "Crear Pregunta" e intenta guardar una pregunta sin ingresar texto. | El sistema muestra un mensaje de error indicando que el texto de la pregunta es obligatorio. |
| Estudiante autenticado accede a "Crear Pregunta" e intenta guardar una pregunta con menos de dos opciones de respuesta. | El sistema muestra un mensaje de error indicando que debe haber al menos dos opciones de respuesta. |
| Estudiante autenticado accede a "Crear Pregunta" e intenta crear una pregunta con más de 200 caracteres. | El sistema muestra un mensaje de error indicando que excedió la cantidad de caracteres permitidos. |
| Estudiante autenticado accede a "Crear Pregunta" e intenta crear una pregunta con menos de 50 caracteres. | El sistema muestra un mensaje de error indicando que la cantidad de caracteres ingresados es insuficiente. |

**Documento Preparado Por:** Kendall Sánchez & Jaziel Rojas  
**Fecha:** 2025-04-12
