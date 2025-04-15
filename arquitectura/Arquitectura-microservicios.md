# Arquitectura de Microservicios - Plataforma Social de Aprendizaje

## Diagrama de microservicios

El siguiente diagrama representa los componentes principales de la plataforma, incluyendo el API Gateway, el servicio de descubrimiento (Eureka) y cada microservicio con su base de datos (cuando aplica).

 ![Diagrama de Microservicios](Diagrama-MS.png)

```plantuml
@startuml
skinparam componentStyle rectangle

' Colores personalizados
!define AUTH_COLOR #FFD580
!define EMAIL_COLOR #E6E6E6
!define QUESTION_COLOR #B3E6FF
!define TEST_COLOR #D5FFB3
!define AI_COLOR #FFCCCB
!define CONTRIBUTOR_COLOR #CCFFCC
!define ADMIN_COLOR #D5B3FF

' Cliente externo
actor Frontend 

' Gateway y Eureka
component "API Gateway" as Gateway #White
component "Eureka" as Eureka #White

' Microservicios con colores
component "Auth Service" as Auth <<Auth>> AUTH_COLOR
component "Email Service" as Email <<Email>> EMAIL_COLOR
component "Question Service" as Question <<Question>> QUESTION_COLOR
component "Test Service" as Test <<Test>> TEST_COLOR
component "AI Service" as AI <<AI>> AI_COLOR
component "Contributor Service" as Contributor <<Contributor>> CONTRIBUTOR_COLOR
component "Admin Service" as Admin <<Admin>> ADMIN_COLOR

' Bases de datos
database "DB Auth" as DBAuth
database "DB Question" as DBQuestion
database "DB Test" as DBTest
database "DB Contributor" as DBContributor
database "DB Admin" as DBAdmin
database "DB AI" as DBAI

' Conexiones desde el usuario
Frontend --> Gateway : Solicitudes HTTP

' Gateway se comunica con todos los servicios
Gateway --> Auth
Gateway --> Question
Gateway --> Test
Gateway --> Contributor
Gateway --> Admin

' Todos los servicios se registran en Eureka
Auth --> Eureka
Email --> Eureka
Question --> Eureka
Test --> Eureka
AI --> Eureka
Contributor --> Eureka
Admin --> Eureka
Gateway --> Eureka




' Conexiones a base de datos
Auth --> DBAuth
Question --> DBQuestion
Test --> DBTest
Contributor --> DBContributor
Admin --> DBAdmin
AI --> DBAI

@enduml

```
## Definción de Microservicios:

### Auth Service:
Encargado de autenticación, generación de tokens y registro de colaboradores.

### Email Service:
Servicio de envío de correos.

### Question Service:
Gestión de preguntas, respuestas y su calificación. Además puede emitir eventos de reporte (manejados por Admin Service).

### Test Service:
Gestión de las pruebas de autoevaluación.

### AI Service:
Comunicación con la API de OpenAI para generar calificación automática de preguntas y generación de preguntas. 

### Contributor Service:
Gestión del perfil de los colaboradores, puntos XP, rachas, historial de pruebas, niveles (Aprendiz → Pensador → Sabio), etc.

### Admin Service:
Aquí se hace la moderación, revisión de reportes, eliminación de contenido (preguntas), sanciones a colaboradores (bannearlos), y configuración de normas de la comunidad.
