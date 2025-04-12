# Requerimiento Funcional: Crear Preguntas por estudiantes

## Descripción

**RF-01** Este requerimiento funcional describe la capacidad de los estudiantes autenticados de la plataforma social de aprendizaje para crear y publicar preguntas relacionadas con temas específicos de diversas materias. Esta funcionalidad fomenta el aprendizaje colaborativo, permitiendo que los estudiantes contribuyan al repositorio de contenido académico mediante la formulación de preguntas que pueden ser respondidas por otros miembros de la comunidad.

El alcance de este requerimiento incluye la interfaz del estudiante para la creación de preguntas, el almacenamiento estructurado de las mismas, y su correcta categorización para facilitar su consulta y análisis posterior.

## Necesidad

Actualmente, los estudiantes universitarios enfrentan desafíos al momento de repasar y reforzar conceptos clave. Esta funcionalidad aborda esa necesidad permitiendo que los estudiantes generen contenido educativo en forma de preguntas, fortaleciendo el aprendizaje entre pares y ofreciendo un canal para recibir retroalimentación y aclarar dudas. Esta dinámica es coherente con el objetivo principal de la plataforma: potenciar el aprendizaje activo, colaborativo y contextualizado.

## Proceso Actual

En el estado actual del sistema, no existe ninguna funcionalidad que permita a los estudiantes crear preguntas dentro de la plataforma. Las dudas y repasos dependen de clases presenciales o de plataformas externas no integradas al contexto académico de la comunidad estudiantil. Esto limita el acceso al conocimiento generado por otros estudiantes con intereses similares.

## Solución Propuesta

Se propone desarrollar una funcionalidad que permita a los estudiantes autenticados crear preguntas en la plataforma. Esta funcionalidad contemplará los siguientes componentes:

- **Formulario de Creación de Pregunta:** Una interfaz que permitirá al estudiantes ingresar el texto de la pregunta y las posibles respuestas.
- **Tipo de Pregunta:** La pregunta será de selección múltiple con al menos dos opciones y una o más respuestas correctas.
- **Asignación de Autor:** El sistema registrará automáticamente al estudiante que creó la pregunta.
- **Categorización:** El estudiante deberá seleccionar una o varias categorías relevantes para la pregunta, a partir de una lista predefinida o dejar que la inteligencia artificial categorice la pregunta.
- **Indicación de Respuesta Correcta:** El estudiante deberá señalar cuál o cuáles de las opciones de respuesta son correctas.
- **Adjuntos Opcionales:** Se permitirá incluir archivos (imágenes) de forma opcional para complementar el contenido de la pregunta.

## Documentos de Referencia

- nada por el momento

## Casos de Uso Relacionados

- [CU-01: crear preguntas]

## Criterios de Aceptación

1. El estudiante autenticado podrá crear y publicar preguntas sobre temas específicos.
2. La pregunta será de tipo selección múltiple con opciones y al menos una respuesta correcta.
3. El sistema deberá registrar al autor de la pregunta.
4. Las preguntas deben estar asociadas a una o varias categorías.
5. Se debe permitir la indicación de las respuestas correctas.
6. Se podrá incluir material adicional (una fotografia) de un tamaño de maximo 2 MB y es opcional adjuntarlo en la pregunta.

---

**Documento Preparado Por:** [Brandon Vargas Solano C28223]  
**Fecha:** [11-04-2025]

---
