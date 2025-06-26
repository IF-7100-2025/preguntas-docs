# **Requerimiento Suplementario 01: Login (Inicio de Sesión)**

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



