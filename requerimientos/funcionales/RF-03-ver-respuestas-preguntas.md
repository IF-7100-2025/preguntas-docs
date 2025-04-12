# Requerimiento Funcional: Ver respuestas a Preguntas

## Descripción  
**RF-03** Este requerimiento funcional describe la capacidad de los usuarios de la plataforma social de aprendizaje para visualizar las respuestas a las preguntas que han sido publicadas por otros usuarios. Esta funcionalidad busca facilitar el aprendizaje colaborativo mediante el acceso a distintas perspectivas, promoviendo una mejor comprensión de los temas tratados. El alcance de este requerimiento incluye la visualización de las respuestas vinculadas a una pregunta, la identificación del autor de cada respuesta y la interacción mediante la evaluación de su utilidad.

## Necesidad  
La necesidad de esta funcionalidad se origina en la importancia de generar espacios donde los estudiantes puedan aprender no solo al formular preguntas, sino también al analizar las respuestas dadas por sus compañeros. Actualmente, muchos estudiantes se enfrentan a dificultades para entender ciertos conceptos debido a la falta de explicaciones alternativas o discusiones entre pares. Permitir la visualización de respuestas fomenta el pensamiento crítico, el contraste de ideas y el refuerzo del conocimiento desde distintas perspectivas.

## Proceso Actual  
En el estado actual de la plataforma propuesta, los usuarios no cuentan con una forma estructurada de ver las respuestas generadas por otros estudiantes. Esto limita el acceso a contenido generado colaborativamente y disminuye el potencial de aprendizaje colectivo. En ausencia de esta funcionalidad, los usuarios deben recurrir a otras fuentes de información externas o depender exclusivamente de sus propios aportes.

## Solución Propuesta  
Se propone implementar una funcionalidad que permita a los usuarios autenticados ver las respuestas asociadas a las preguntas publicadas en la plataforma. Esta funcionalidad incluirá los siguientes elementos:

- **Listado de Respuestas:** Las respuestas aparecerán listadas debajo de cada pregunta una vez que exista al menos una respuesta registrada.
- **Autoría de Respuesta:** El sistema mostrará el nombre de usuario que publicó cada respuesta.
- **Evaluación de Utilidad:** Los usuarios podrán marcar si una respuesta les resultó útil o no, para fomentar la calidad y relevancia del contenido.
- **Orden de Visualización:** Se podrán ordenar las respuestas por relevancia (utilidad), fecha de publicación o popularidad.

## Documentos de Referencia  
Por el momento no hay

## Casos de Uso Relacionados  
- [CU-02: Responder Preguntas]  
- [CU-03: Navegar y Filtrar Preguntas]  
- [CU-04: Calificar Preguntas y Respuestas]

## Criterios de Aceptación  
- Las respuestas a una pregunta se mostrarán debajo de la pregunta una vez que al menos un usuario haya respondido.  
- Se mostrará el usuario que respondió la pregunta.  
- Se podrá indicar si una respuesta fue útil o no.

---

**Documento Preparado Por:** Jose Pablo Montero Jiménez C25019  
**Fecha:** 12-04-2025
