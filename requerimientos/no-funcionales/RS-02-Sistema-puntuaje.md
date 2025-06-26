# **Requerimiento Suplementario 02: Sistema de Puntaje**

## **Estatus**

\[Aceptado\]

## **Contexto**

Fomentar la participación activa en la plataforma es crucial para el éxito del aprendizaje colaborativo. Un sistema de recompensas puede incentivar a los usuarios a involucrarse más en el proceso, ya sea creando contenido, respondiendo preguntas o calificando respuestas. Las recompensas también pueden ayudar a mantener a los usuarios motivados y comprometidos.

## **Requerimiento**

Desarrollar un sistema de recompensas donde los usuarios reciban puntos, insignias o niveles según su participación en la plataforma (por ejemplo, crear preguntas, responder, calificar, etc.). Las recompensas pueden tener un impacto directo en la visibilidad del usuario dentro de la comunidad y servir como un incentivo para generar más contenido de calidad.

## **Justificación**

Los sistemas de puntaje han demostrado ser efectivos en múltiples plataformas educativas para aumentar la motivación y la retención del usuario. En el caso de nuestra plataforma, esto se alinea con la meta de promover el aprendizaje activo, donde los estudiantes no solo consumen contenido, sino que también lo generan y validan.

## **Implicaciones**

* Requiere un sistema de tracking de actividades (crear preguntas, responder, etc.).

* Se deberá extender la base de datos para almacenar puntos, niveles e insignias.

* Es necesario implementar un sistema de cálculo automático cada vez que el usuario realiza una acción.

* La interfaz debe mostrar al usuario su puntaje actual, insignias obtenidas y nivel.

## **Alternativas Consideradas**

## **Decisión**

Se aprobó la implementación de un sistema básico de puntos y niveles que pueda extenderse en el futuro. Los puntos se otorgarán inicialmente por:

* Crear preguntas aprobadas.

* Completar quizzes.

## **Requerimientos funcionales implicados**

* \[RF-01-crear-preguntas\]
* \[RF-03-calificar-preguntas\]
* \[RF-08-sistema-racha-xp-rangos\]  
* \[RF-09-resolver-quizzes\]

## **Referencias**

[https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md](https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md)

---

**Documento Preparado Por:** \[Jose Pablo Montero\]  
 **Fecha:** \[20-06-2025\]





