# Documento de Guía de Estilo de Código: Backend

## 1. Estándares Generales de Java

### **Convención de nombres:**

* Clases: PascalCase \-\> UserService

* Métodos y variables: camelCase \-\> getUserById()

* Constantes: UPPER\_CASE \-\> MAX\_RETRIES

* Paquetes: ucr.ac.cr.nombreDelProyecto.paquete

## 2. División de Capas
Utilizaremos el patrón arquitectónico CQRS (Command Query Responsibility Segregation) que separa claramente las operaciones de escritura (Commands) de las de lectura (Queries), mejorando la escalabilidad, claridad y organización del código. En el contexto del problema se implementará porque:

- Permite desacoplar la lógica de negocio entre lo que modifica el estado del sistema y lo que consulta información.

- Facilita la validación específica por cada tipo de operación.

- Mejora el mantenimiento del código y la incorporación de nuevas funcionalidades

```
src/
└── main/
    ├── java/
    │   └── com/tuempresa/tuapp/
    │       ├── api/                                ← Capa de exposición
    │       │   ├── exceptions/                     ← Excepciones personalizadas
    │       │   ├── rest/                           ← Endpoints (GET, POST, etc)
    │       │   └── types/                          ← Tipos de DTOs
    │       │       ├── request/                    ← Objetos de entrada (DTOs de request)
    │       │       └── response/                   ← Objetos de salida (DTOs de response)
    │
    │       ├── config/                             ← Configuraciones generales
    │       │   └── OpenAiConfig.java               ← Configuración del cliente OpenAI
    │
    │       ├── events/                             ← Eventos del sistema
    │       │   └── actions/                        ← Acciones relacionadas a eventos
    │
    │       ├── handlers/                           ← Manejadores de CQRS
    │       │   ├── commands/                       ← Comandos (escritura)
    │       │   │   └── impl/                       ← Implementaciones de comandos
    │       │   └── queries/                        ← Consultas (lectura)
    │       │       └── impl/                       ← Implementaciones de queries
    │
    │       ├── jpa/                                ← Capa de persistencia
    │       │   ├── entities/                       ← Entidades JPA
    │       │   └── repositories/                   ← Repositorios JPA (interfaces)
    │
    │       ├── kafka/                              ← Integración con Kafka
    │
    │       └── models/                             ← Miscelaneo o Excepciones personalizadas
    └── resources/
        ├── application.yml                         ← Configuración general
        └── ...                                     ← Otros recursos
        
                ← Otros archivos estáticos o de configuración
```

## 3. Manejo de Errores

El manejo de errores se hace por medio de las clases contenidas dentro del paquete ***models.***

**BaseException:** Se encarga de manejar los errores, proporciona una forma estructurada de manejar las excepciones, en la cual se retorna  por medio de métodos, mensajes  generales relacionados al error presentado.

**ErrorCode:** Presenta errores personalizados con su correspondiente código y estado acorde a la categoría que le corresponde, seguridad, errores del servidor o errores propios del negocio.

**Ejemplos de errores:**  
UNAUTHORIZED(4001, "Unauthorized", 401\)  
INTERNAL\_ERROR(5000, "Internal server Error", 500\)

**Códigos de Estado HTTPS**  
[https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)
