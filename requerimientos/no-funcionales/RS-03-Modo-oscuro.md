# **Requerimiento Suplementario: Modo Oscuro / Accesibilidad**

## **Estatus**

[Aceptado]

## **Contexto**

La accesibilidad y la personalización visual son aspectos esenciales para mejorar la experiencia del usuario en aplicaciones modernas. En particular, el modo oscuro reduce la fatiga visual y mejora la legibilidad en entornos con poca luz.

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
