# Requerimiento Funcional: Sistema de Racha Diaria, XP y Rangos

## Descripción

**RF-08** Este requerimiento funcional describe la capacidad del sistema para registrar, actualizar y mostrar el progreso de los colaboradores a través de un sistema de experiencia (XP), rachas diarias y rangos. La funcionalidad busca incentivar la participación continua mediante recompensas simbólicas que representen el compromiso del usuario dentro de la plataforma.

Este mecanismo gamificado motiva a los colaboradores a interactuar constantemente, promoviendo el aprendizaje activo y la colaboración entre pares. El sistema llevará un seguimiento automático de la actividad del usuario, calculará su XP, actualizará su racha diaria y ajustará su rango correspondiente.

## Necesidad

Los entornos virtuales de aprendizaje a menudo enfrentan el reto de mantener la constancia e interés de los usuarios. La implementación de este sistema atiende esa necesidad motivacional mediante la gamificación, reconociendo el esfuerzo sostenido de los colaboradores.

Otorgar XP, mantener una racha diaria visible y asignar rangos progresivos estimula el compromiso del colaborador, refuerza conductas deseadas y crea una experiencia de usuario más atractiva y personalizada.

## Proceso Actual

Actualmente, la plataforma no ofrece una forma automatizada de registrar ni recompensar la constancia o la actividad del colaborador. No existen mecanismos visibles que muestren el progreso ni elementos motivacionales que promuevan la participación regular.

## Solución Propuesta

Se propone implementar un sistema gamificado de seguimiento de progreso que incluya:

- **Asignación de XP** por actividades como:
  - Publicar preguntas (**10 XP**)
  - Comentar quizzes de 5 preguntas (**20 XP**) o más de 5 (**50 XP**)
  - Resolver quizzes (XP proporcional al desempeño)
- **Racha diaria**: El sistema detectará si el colaborador ha tenido actividad continua día a día. Si hubo actividad el día anterior, la racha incrementa. Si no, se reinicia a 1.
- **Sistema de rangos**: Se definirán umbrales de XP para alcanzar los siguientes niveles:
  - Aprendiz (0–199 XP)
  - Pensador (200–599 XP)
  - Sabio (600+ XP)
- **Visualización en perfil**: El colaborador podrá ver su racha, XP y rango actualizados en su perfil.
- **Manejo de errores y zonas horarias**: El sistema será robusto ante fallas de conexión y considerará zonas horarias para usuarios internacionales.

## Documentos de Referencia

- [CU-08: Sistema de Racha Diaria, XP y Rangos](../../casos-de-uso/)
- [Documento de actores](../../arquitectura/actores.md)

## Casos de Uso Relacionados

- CU-08: Sistema de Racha Diaria, XP y Rangos

## Criterios de Aceptación

1. El sistema asigna XP según el tipo de actividad realizada.
2. La racha diaria incrementa si hay actividad en días consecutivos.
3. Si no hay actividad durante un día, la racha se reinicia.
4. El sistema actualiza automáticamente el rango del colaborador si alcanza el XP necesario.
5. El perfil muestra en tiempo real la racha, XP acumulado y rango.
6. El sistema debe manejar correctamente zonas horarias.
7. El sistema debe notificar errores si falla el registro de actividad.
8. Las actualizaciones de progreso deben reflejarse inmediatamente tras la acción del colaborador.

---

**Documento Preparado Por:** Kendall Sánchez Chinchilla  
**Fecha:** 03-06-2025
