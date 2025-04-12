# Documento de Guía de Estilo de Código: Backend

### **1\. Estándares Generales de Java**

* **Convención de nombres**:

  * Clases: PascalCase \-\> UserService

  * Métodos y variables: camelCase \-\> getUserById()

  * Constantes: UPPER\_CASE \-\> MAX\_RETRIES

  * Paquetes: ucr.ac.cr.nombreDelProyecto.paquete
    
## **Manejo de errores**

El manejo de errores se hace por medio de las clases contenidas dentro del paquete ***models.***

**BaseException:** Se encarga de manejar los errores, proporciona una forma estructurada de manejar las excepciones, en la cual se retorna  por medio de métodos, mensajes  generales relacionados al error presentado. 

**ErrorCode:** Presenta errores personalizados con su correspondiente código y estado acorde a la categoría que le corresponde, seguridad, errores del servidor o errores propios del negocio.

**Ejemplos de errores:**  
UNAUTHORIZED(4001, "Unauthorized", 401\)  
INTERNAL\_ERROR(5000, "Internal server Error", 500\)

**Códigos de Estado HTTPS**  
[https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)

