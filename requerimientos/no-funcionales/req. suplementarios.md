# **Requerimiento Suplementario: Login (Inicio de Sesión)**

## **Estatus**

\[Aceptado\]

## **Contexto**

Es el proceso mediante el cual un usuario (colaborador o admin) proporciona sus credenciales, como la contraseña y un nombre de usuario, con el fin de acceder a la plataforma y realizar operaciones como crear preguntas y responder quices.

## **Requerimiento**

La plataforma debe permitir a los usuarios iniciar sesión en la plataforma mediante un formulario de login. Este formulario debe solicitar al usuario su nombre de usuario y contraseña, los cuales serán verificados con las credenciales almacenadas en la base de datos. En caso de que las credenciales sean correctas, el sistema permitirá el acceso al usuario, y se le redirigirá a su página principal.

## **Justificación**

Este requerimiento es necesario para garantizar que solo los usuarios registrados puedan acceder a la plataforma y participar en el proceso de aprendizaje colaborativo. Sin un mecanismo de inicio de sesión, cualquier persona podría interactuar con la plataforma sin control, lo que comprometería la seguridad y la integridad del contenido.

## **Implicaciones**

Este requerimiento implica la creación de un sistema de autenticación que interactúa con la base de datos donde se almacenarán las credenciales y se verificarán cada vez que el usuario ingrese a la plataforma después de haber cerrado su sesión.

## **Alternativas Consideradas**

**Autenticación multifactor**: Se evaluó añadir una autenticación multifactor, con un código que llegaba al correo personal, para mayor seguridad. Sin embargo, esta alternativa fue descartada debido a su complejidad y el tiempo adicional que requiere.

## **Decisión**

Se decidió implementar un formulario de login sencillo que reciba un nombre de usuario y una contraseña. La razón por la cual se optó por esta solución simple es porque la plataforma no necesita un sistema de autenticación complejo. El formulario de login básico es suficiente para garantizar que solo los usuarios registrados puedan acceder a la plataforma.

## **Requerimientos funcionales implicados**

* Caso de Uso: Iniciar Sesión

## **Referencias**

[https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md](https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md)

---

**Documento Preparado Por:** Luis Mario Ballar Zamora

**Fecha:** 05-05-2025



# **Requerimiento Suplementario: Sistema de Puntaje**

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


# **Requerimiento Suplementario: Modo Oscuro / Accesibilidad**

## **Estatus**

[Aceptado]

## **Contexto**

La accesibilidad y la personalización visual son aspectos esenciales para mejorar la experiencia del usuario en aplicaciones modernas. En particular, el modo oscuro reduce la fatiga visual, ahorra batería en dispositivos móviles y mejora la legibilidad en entornos con poca luz.

## **Requerimiento**

La plataforma debe ofrecer al usuario la posibilidad de alternar entre modo claro y modo oscuro desde la interfaz gráfica. Esta configuración debe mantenerse persistente durante la sesión del usuario, y reflejarse de manera uniforme en todos los componentes visuales de la plataforma.

## **Justificación**

El modo oscuro es una funcionalidad ampliamente solicitada por los usuarios por sus beneficios ergonómicos y estéticos. Su implementación mejora la inclusión, permitiendo a usuarios con sensibilidad visual adaptar la interfaz a sus necesidades. También es una práctica moderna de diseño de UX/UI que aumenta la percepción de calidad de la plataforma.

## **Implicaciones**

* Requiere una estructura de estilos (por ejemplo, variables CSS o uso de frameworks como Tailwind con `darkMode`) que permita alternar dinámicamente los colores.
* Se deberá agregar un control visual (ícono de sol/luna, toggle o menú de configuración) accesible en el header o menú lateral.
* Puede requerir almacenar la preferencia del usuario en `localStorage`, `sessionStorage` o en el perfil del usuario autenticado.
* Todos los componentes (formulario, botones, tablas, menú, etc.) deben ajustarse visualmente al modo seleccionado.

## **Alternativas Consideradas**

* Detectar automáticamente el modo según las preferencias del sistema operativo. Esta alternativa se evaluó pero se descartó como única opción, ya que no ofrece control directo al usuario.

## **Decisión**

Se implementará una opción de cambio manual entre modo claro y modo oscuro, accesible desde el menú de usuario. Esta decisión busca maximizar la accesibilidad, la personalización y la satisfacción del usuario.

## **Requerimientos funcionales implicados**

* [RF-02-generar-quizzes]
* [RF-09-resolver-quizzes]
* [RF-12-mis-preguntas]


## **Referencias**

[https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md](https://github.com/IF-7100-2025/docs/blob/main/proyecto/casos/comunidad-de-aprendizaje.md)

---

**Documento Preparado Por:** Jose Pablo Montero  
**Fecha:** 25-06-2025


