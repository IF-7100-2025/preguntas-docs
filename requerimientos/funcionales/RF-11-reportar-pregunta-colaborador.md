# Requerimiento Funcional: Reportar Pregunta durante la Resolución de un Quiz

## Descripción

**RF-11** Este requerimiento funcional establece la capacidad de los colaboradores autenticados para reportar preguntas mientras resuelven un quiz en la plataforma social de aprendizaje. Esta funcionalidad permite identificar preguntas con problemas de redacción, contenido inapropiado o ambigüedad, contribuyendo a la mejora continua de la calidad del contenido evaluativo.

El alcance de este requerimiento incluye la integración del botón de reporte dentro del flujo de resolución del quiz, la interfaz para capturar la razón del reporte, el almacenamiento del mismo, y el control del límite de reportes permitidos por colaborador al día.

## Necesidad

Actualmente no existe un mecanismo integrado que permita a los colaboradores reportar preguntas problemáticas durante la realización de un quiz. Esta limitación impide la retroalimentación directa y oportuna sobre la calidad del contenido evaluativo, afectando la experiencia de aprendizaje y la confiabilidad del sistema.

Este requerimiento responde a la necesidad de ofrecer a los colaboradores una vía efectiva y no intrusiva para señalar posibles errores o problemas en las preguntas, asegurando un proceso continuo de revisión y mejora por parte de los administradores del contenido.

## Proceso Actual

En la situación actual, los colaboradores no pueden reportar preguntas mientras resuelven un quiz. Cualquier problema detectado debe comunicarse por canales externos, lo que representa una carga adicional y una desconexión del proceso de evaluación. Además, no existe un control automático sobre la cantidad de reportes ni una forma de registrar y categorizar las razones de los mismos.

## Solución Propuesta

Se propone implementar una funcionalidad que permita a los colaboradores reportar preguntas directamente desde el entorno del quiz, sin interrumpir el flujo de resolución. Esta funcionalidad contemplará los siguientes componentes:

- **Botón de Reporte:** Un ícono en forma de banderita roja visible junto a cada pregunta del quiz.
- **Formulario Emergente (Modal):** Al presionar el botón, se despliega un formulario que permite seleccionar la razón del reporte.
- **Selección de Razón:** Lista predefinida de razones (contenido inapropiado, confusa, mal redactada, otra).
    - Si se selecciona “otra”, se habilita un campo obligatorio de texto con un máximo de 20 caracteres.
    - Campo adicional opcional para comentarios con un límite de 400 caracteres.
- **Límite de Reportes:** 
    - El sistema permitirá un máximo de 10 reportes por colaborador al día.
    - Solo se permite un reporte por pregunta.
- **Validaciones:** No se podrá enviar un reporte sin haber seleccionado una razón. El sistema mostrará un mensaje de advertencia en ese caso.
- **Actualización del Puntaje:** Una vez enviada la solicitud, la pregunta queda excluida del cálculo del puntaje del quiz, independientemente de si fue respondida correctamente o no.
- **Notificación de Confirmación:** Tras el envío exitoso, se muestra un mensaje en pantalla confirmando que el reporte ha sido registrado.

## Casos de Uso Relacionados

- [Documento caso de uso 11](../../casos-de-uso/CU-11-reportar-pregunta-colaborador.md)

## Criterios de Aceptación

1. El colaborador debe poder reportar preguntas directamente desde un quiz en curso mediante un botón visible.
2. El formulario de reporte debe incluir razones predefinidas y campos para "otra razón" y comentarios adicionales con validaciones de longitud.
3. El sistema debe validar que se seleccione una razón antes de permitir el envío.
4. El sistema debe impedir más de un reporte por pregunta y limitar a 10 reportes diarios por colaborador.
5. Una vez reportada, la pregunta debe ser excluida del cómputo del puntaje final del quiz.
6. El sistema debe mostrar una notificación de éxito al enviar el reporte o un mensaje de error si ocurre una falla técnica.
7. Si el colaborador ha alcanzado el límite diario, el sistema debe mostrar el mensaje correspondiente y bloquear nuevos reportes.

---

**Documento Preparado Por:** [Kendall Sánchez Chinchilla C27227]  
**Fecha:** [17-06-2025]

---