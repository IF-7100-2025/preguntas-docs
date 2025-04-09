# Documento de Guía de Estilo de Código: Backend

### **1\. Estándares Generales de Java**

* **Convención de nombres**:

  * Clases: PascalCase \-\> UserService

  * Métodos y variables: camelCase \-\> getUserById()

  * Constantes: UPPER\_CASE \-\> MAX\_RETRIES

  * Paquetes: ucr.ac.cr.nombreDelProyecto.paquete

**Patrón de Arquitectónico**  
**CQRS:** Separa las operaciones de lectura (queries) de las operaciones de escritura (commands). 

**Command:** Las operaciones modifican el estado de la aplicación, y no devuelven datos, solo retornar si la operación fue exitosa o no.

**Query:** Son operaciones que solo leen datos, sin modificar el estado de la aplicación. Estas operaciones generalmente devuelven los datos solicitados.

**Estructura de paquetes**

api/  
  ├── exceptions/  
  ├── rests/  
  ├── types/  
config/  
handlers/  
  ├── commands/  
  │	└── impl/  
  ├── queries/  
  │	└── impl/  
jpa/
  ├── entities/  
  ├── repositories/  
models/  


### **api/**

* **exceptions/**: Contiene clases y definiciones de excepciones personalizadas que manejan errores específicos de la API.

* **rests/**: Incluye los controladores o endpoints REST que exponen la funcionalidad de la API, manejando las solicitudes HTTP y enviando respuestas.

* **types/**: Contiene los **DTOs** que estructuran y organizan los datos que se intercambian entre el cliente y el servidor en una API

### **2\. config/**

* Contiene clases de configuración para la aplicación, como configuraciones de seguridad, bases de datos, beans de Spring, y otros aspectos técnicos del proyecto. En nuestro caso contiene la configuración de **CORS**, la cual permite que haya comunicación entre el frontend y el backend.

### **3\. handlers/**

* **commands/**: Aquí se gestionan los comandos en el contexto de **CQRS**. Contiene lógica para modificar el estado del sistema.

  * **impl/**: Implementaciones específicas de los comandos, manejadores de la lógica para cada comando.

* **queries/**: Aquí se gestionan las consultas en el contexto de **CQRS**. Contiene lógica para obtener información sin modificar el estado.

  * **impl/**: Implementaciones específicas de las consultas, manejadores de la lógica para cada consulta.

### **4\. jpa/**

* **entities/**: Define las entidades de JPA, que son representaciones de las tablas de la base de datos.

* **repositories/**: Contiene interfaces de repositorios que se encargan de la persistencia de las entidades, generalmente extendiendo de JpaRepository o CrudRepository de Spring Data.

### **5\. models/**

* Define los modelos de dominio de la aplicación, que son representaciones de conceptos del negocio. Esto incluye clases que podrían no estar directamente relacionadas con la persistencia de datos pero que definen la lógica de negocio.



## **Manejo de errores**

El manejo de errores se hace por medio de las clases contenidas dentro del paquete ***models.***

**BaseException:** Se encarga de manejar los errores, proporciona una forma estructurada de manejar las excepciones, en la cual se retorna  por medio de métodos, mensajes  generales relacionados al error presentado. 

**ErrorCode:** Presenta errores personalizados con su correspondiente código y estado acorde a la categoría que le corresponde, seguridad, errores del servidor o errores propios del negocio.

**Ejemplos de errores:**  
UNAUTHORIZED(4001, "Unauthorized", 401\)  
INTERNAL\_ERROR(5000, "Internal server Error", 500\)

**Códigos de Estado HTTPS**  
[https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)

