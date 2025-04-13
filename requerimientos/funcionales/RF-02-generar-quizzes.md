# Requerimiento Funcional: Generar Quizzes

## Descripción

*RF-02* Este requerimiento funcional describe la capacidad de la plataforma de aprendizaje colaborativo para generar pruebas estructuradas a partir del banco de preguntas previamente registradas o con ayuda de la inteligencia artificial que tendrá la capacidad de generar pruebas estructuradas. El sistema debe permitir a los colaboradores autoevaluarse de forma automatizada, registrando el historial de cada prueba y su calificación correspondiente.

## Necesidad

Los colaboradores requieren una forma estructurada de evaluar sus conocimientos adquiridos mediante las preguntas existentes en la plataforma. Actualmente no se cuenta con un mecanismo automático que genere evaluaciones personalizadas ni que almacene los resultados de estas. Implementar esta funcionalidad permitirá mejorar la experiencia de aprendizaje, facilitar el seguimiento del progreso individual y fomentar el autoaprendizaje.

## Proceso Actual

Actualmente, la plataforma solo permite consultar y registrar preguntas. Los colaboradores no tienen una forma sistematizada de realizar pruebas a partir de estas preguntas, ni existe un sistema de calificación o historial de intentos.

## Solución Propuesta

Se propone que la plataforma implemente un generador de pruebas que seleccione preguntas del banco registrado. Las pruebas deben:

- Poder ser generadas automáticamente por el sistema.
- Contener una cantidad configurable de preguntas.
- Ser calificadas automáticamente.
- Guardar un historial por usuario que incluya fecha, calificación y preguntas respondidas.

Este módulo podrá ser accedido desde el perfil del colaborador y también permitirá la revisión de pruebas pasadas.

Las pruebas pueden ser generadas tanto a partir del banco de preguntas como por inteligencia artificial, de acuerdo con las preferencias o necesidades del colaborador.

## Documentos de Referencia

- [Documento de Justificación 1: 02-Crear Pruebas]

## Casos de Uso Relacionados

- CU-01: Registrar preguntas en el sistema
- CU-02: Generación y Realización de Pruebas Automatizadas
- CU-09: Consultar historial de pruebas

## Criterios de Aceptación

- La plataforma podrá generar pruebas de forma automática utilizando las preguntas almacenadas.
- Cada prueba se calificará automáticamente al finalizar.
- Se almacenará un historial detallado de pruebas realizadas por usuario.
- El usuario podrá acceder a los resultados y respuestas desde su perfil.


---

**Documento Preparado Por:** Kendall Sánchez Chinchilla & Jaziel Rojas Serrano  
**Fecha:** 2025-04-12
