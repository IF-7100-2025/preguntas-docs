# Requerimiento Funcional: Resolver Quiz
## Descripción
**RF-09** Este requerimiento funcional describe la capacidad del sistema para permitir a los colaboradores resolver quizzes que han sido previamente generados o se encuentran en curso. Durante este proceso, el colaborador puede responder las preguntas en cualquier orden, el sistema guarda automáticamente el progreso, permite retomar intentos incompletos y evalúa el resultado final para proporcionar retroalimentación, actualizar la experiencia (XP), la racha diaria y el rango correspondiente.

Esta funcionalidad es esencial para garantizar que la experiencia de evaluación sea flexible, continua y personalizada, manteniendo la motivación del colaborador mediante un proceso claro, justo y gamificado.

## Necesidad
Los colaboradores deben contar con una forma efectiva de continuar su proceso de aprendizaje evaluativo, permitiéndoles responder quizzes según su disponibilidad, sin perder progreso en caso de desconexión. Además, integrar la evaluación con el sistema de XP, racha y rangos potencia la motivación y el compromiso constante.

La resolución de quizzes permite medir el conocimiento adquirido, reforzar conceptos y contribuir al crecimiento dentro del sistema de aprendizaje gamificado.

## Proceso Actual
Anteriormente, la plataforma no permitía retomar quizzes iniciados, ni vinculaba directamente el resultado de un quiz con la experiencia (XP), la racha o el rango del colaborador. Tampoco existía un flujo claro que permitiera abandonar un intento y retomarlo sin pérdida de progreso.

## Solución Propuesta
Se propone implementar una funcionalidad que permita:

- Acceder a la sección “Historial Test” y continuar un quiz pendiente.

- Visualizar todas las preguntas en una sola vista con navegación libre.

- Guardado automático de respuestas marcadas.

- Posibilidad de abandonar y retomar el quiz sin pérdida de progreso.

- Corrección automática de respuestas una vez enviado el quiz.

- Cálculo de puntaje y visualización de:

    - Preguntas correctas e incorrectas.
    - Puntaje total. 
    - Retroalimentación general.

- Actualización de la experiencia (XP) del colaborador.

- Evaluación automática de la racha diaria.

- Ajuste del rango si se alcanzan nuevos umbrales de XP.

## Documentos de Referencia
- [CU-09: Resolver Quiz](../../casos-de-uso/CU-09-resolver-quizz.md)

## Documento de actores

- [CU-08: Sistema de Racha Diaria, XP y Rangos](../../arquitectura/actores.md)

## Casos de Uso Relacionados
- CU-09: Resolver Quiz

- CU-08: Sistema de Racha Diaria, XP y Rangos

## Criterios de Aceptación
1. El sistema permite seleccionar un quiz pendiente desde el historial.

2. Las preguntas se presentan en una sola vista y pueden responderse en cualquier orden.

3. El sistema guarda automáticamente cada respuesta marcada.

4. El colaborador puede abandonar el quiz y retomarlo sin pérdida de información.

5. Una vez finalizado, el sistema evalúa automáticamente el quiz.

6. El resultado incluye puntaje, retroalimentación y detalle de respuestas.

7. El sistema actualiza correctamente la XP, racha diaria y rango del colaborador.

8. El historial refleja el intento completo con su resultado.

9. El sistema notifica errores en caso de fallas de guardado o envío.

**Documento Preparado Por:** Kendall Sánchez Chinchilla
**Fecha:** 07-06-2025