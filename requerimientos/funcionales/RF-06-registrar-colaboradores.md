# Requerimiento Funcional: Registro de Colaboradores

## Descripción  
**RF-06** Este requerimiento funcional describe la capacidad de los nuevos colaboradores para registrarse en la plataforma social de aprendizaje colaborativo. El propósito de esta funcionalidad es permitir la creación de cuentas personales que den acceso a las funcionalidades de la plataforma. El alcance de este requerimiento incluye el formulario de registro, validaciones básicas de entrada, y el envío de una confirmación al correo electrónico.

## Necesidad  
La plataforma está orientada a fomentar el aprendizaje colaborativo entre estudiantes. Para participar activamente en la plataforma, es necesario que cada colaborador tenga una cuenta personalizada. Esto permite una experiencia segura, personalizada y organizada, además de garantizar que las interacciones se asocien a un perfil de colaborador (como la creación de preguntas). La funcionalidad de registro es fundamental para habilitar el acceso controlado y seguro al ecosistema de la plataforma.

## Proceso Actual  
Actualmente, no existe una funcionalidad de registro implementada en la plataforma. Esto impide que los colaboradores puedan interactuar, publicar preguntas y crear quices. El acceso está restringido, y no es posible rastrear la participación o progreso de cada persona.

## Solución Propuesta  
Se propone implementar una funcionalidad que permita a los nuevos colaboradores registrarse en la plataforma proporcionando datos básicos. Esta funcionalidad incluirá los siguientes elementos:  
- **Formulario de Registro de Colaborador:** Una interfaz que recoja los datos requeridos para el registro: nombre de usuario, correo electrónico y contraseña.  
- **Validación de Formato de Correo:** El sistema deberá verificar que el correo ingresado tenga un formato válido (por ejemplo, que contenga “@” y “.com “).  
- **Validación de Seguridad de Contraseña:** Se establecerán criterios mínimos (al menos 8 caracteres, mayúsculas, minúsculas y un número) para garantizar contraseñas seguras.  
- **Confirmación de Registro (opcional):** Tras completar el registro, el colaborador debe recibir un correo de confirmación que valide su correo y le permita iniciar sesión en la plataforma.  
- **Almacenamiento Seguro de Credenciales:** Las contraseñas deberán almacenarse en la base de datos usando un algoritmo de cifrado (hash).

## Documentos de Referencia  
- [Historia de Usuario 16: Registrarse en la Plataforma]

## Casos de Uso Relacionados  
- [CU-06: Registrarse en la Plataforma]  

## Criterios de Aceptación  
1. El formulario de registro deberá permitir el ingreso de un correo electrónico, una contraseña y un nombre de usuario.  
2. El sistema deberá validar que el correo tenga un formato válido.  
3. El sistema deberá validar que la contraseña cumpla los criterios de seguridad definidos anteriormente (al menos 8 caracteres, mayúsculas, minúsculas y un número).  
4. El sistema deberá guardar de forma segura las credenciales del colaborador.  
5. El sistema podrá enviar un correo de confirmación tras completar el registro (opcional).

## Referencias  
- [Documento de Justificación 2: 06-Registro de Colaborador]

---

**Documento Preparado Por:** Axel Solís Vargas  
**Fecha:** 16/04/2025
