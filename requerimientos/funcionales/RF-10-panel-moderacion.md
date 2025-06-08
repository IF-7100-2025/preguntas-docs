# Requerimiento Funcional: Gestión de Preguntas Reportadas

## Descripción  
**RF-07** Este requerimiento funcional describe la capacidad del administrador de la plataforma para visualizar una lista de preguntas reportadas por los usuarios y tomar decisiones sobre ellas. El administrador podrá revisar el contenido de cada pregunta, así como la explicación asociada, y el material de apoyo, y decidir si desea eliminarla o rechazar el reporte. Esta funcionalidad garantiza la calidad del contenido publicado en la plataforma y mantiene el entorno de aprendizaje libre de errores o contenido inapropiado.

## Necesidad  
La necesidad de esta funcionalidad surge del requerimiento de mantener la integridad, precisión y pertinencia del contenido en la plataforma. Las preguntas incorrectas, ofensivas o mal redactadas deben poder ser señaladas por los usuarios y posteriormente evaluadas por un administrador. Esto asegura que el contenido disponible sea confiable y útil para el aprendizaje.

## Proceso Actual  
Actualmente, la plataforma no permite la revisión ni moderación de preguntas reportadas. Una vez que un usuario reporta una pregunta, no existe un flujo que permita al administrador gestionarla. Esto puede generar acumulación de contenido inapropiado o erróneo sin revisión.

## Solución Propuesta  
Se propone implementar una interfaz exclusiva para el administrador donde podrá gestionar todas las preguntas reportadas. Esta funcionalidad incluirá los siguientes elementos:

- **Visualización de Lista de Preguntas Reportadas**: El administrador podrá acceder a una sección donde se enlistan todas las preguntas que han sido marcadas como reportadas.
- **Detalle de Pregunta**: Cada ítem mostrará el enunciado de la pregunta, las opciones de respuesta, cuál fue la opción seleccionada por el usuario, la explicación que justifica la respuesta correcta, y el material de apoyo.
- **Botón "Eliminar Pregunta"**: Permitirá al administrador eliminar de forma permanente la pregunta de la base de datos. Al hacer clic, se mostrará un `Popconfirm` de Ant Design solicitando confirmación antes de ejecutar la acción.
- **Botón "Rechazar Reporte"**: Permitirá al administrador descartar el reporte. También mostrará un `Popconfirm` antes de confirmar el rechazo.
- **Mensajes de Confirmación**: Tanto la eliminación como el rechazo del reporte incluirán mensajes claros de confirmación para mejorar la experiencia del administrador y evitar errores.

## Documentos de Referencia  
No aplica por el momento.

## Casos de Uso Relacionados  
No aplica por el momento.

## Criterios de Aceptación  
- El administrador puede acceder a una vista con todas las preguntas reportadas.
- El sistema debe mostrar el contenido completo de la pregunta, sus opciones, la explicación y el material de apoyo.
- El administrador podrá eliminar una pregunta reportada y esta acción no podrá deshacerse.
- El administrador podrá rechazar el reporte si considera que la pregunta es válida.
- El sistema debe mostrar mensajes de confirmación antes de realizar acciones irreversibles como eliminar una pregunta.

---

**Documento Preparado Por:** [Minor Hernández Navarro]  
**Fecha:** [07-06-2025]
