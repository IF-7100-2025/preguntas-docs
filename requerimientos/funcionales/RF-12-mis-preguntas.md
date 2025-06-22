# Requerimiento Funcional: Visualización de Mis Preguntas por Colaboradores

## Descripción

**RF-12** Este requerimiento funcional describe la capacidad de los colaboradores autenticados para visualizar las preguntas que han creado dentro de la plataforma. La funcionalidad permite aplicar filtros avanzados para facilitar el seguimiento, la revisión y la organización de sus aportes.

## Necesidad

Los colaboradores necesitan un espacio donde puedan revisar sus preguntas publicadas, verificar su rendimiento (ej. popularidad, categoría, fecha) y acceder rápidamente a contenidos específicos. Esto refuerza el aprendizaje reflexivo y la mejora continua de los contenidos aportados.

## Proceso Actual

Actualmente, no existe un apartado dedicado para que los colaboradores gestionen o consulten las preguntas que han creado. Esto dificulta la edición, seguimiento y reutilización de las mismas.

## Solución Propuesta

Implementar una sección llamada **"Mis Preguntas"** con las siguientes funcionalidades:

- **Visualización de preguntas creadas** por el usuario autenticado.
- **Filtros personalizables**:
  - **Por categoría** (basado en las etiquetas asignadas).
  - **Por fecha específica** (usando un selector tipo calendario).
  - **Por orden cronológico** (más recientes o más antiguas).
  - **Por número de "me gusta"** (popularidad).
- **Interfaz amigable** con resumen de cada pregunta y enlaces a su detalle.

## Casos de Uso Relacionados

- [CU-12: Mis Preguntas](../../casos-de-uso/CU-12-Mis-Preguntas.md)

## Criterios de Aceptación

1. El sistema debe mostrar únicamente las preguntas creadas por el colaborador autenticado.
2. El usuario podrá filtrar sus preguntas por una o varias categorías.
3. El usuario podrá filtrar las preguntas por fecha específica usando un selector de calendario.
4. El usuario podrá ordenar sus preguntas por:
   - Más recientes primero
   - Más antiguas primero
   - Mayor número de "me gusta"
5. El sistema debe mostrar los resultados en una interfaz clara y navegable.
6. El filtrado debe ser reactivo y rápido, sin recargar la página completa.

---

**Documento Preparado Por:** [Luis Diego Irola Hernández]  
**Fecha:** [17-06-2025]
