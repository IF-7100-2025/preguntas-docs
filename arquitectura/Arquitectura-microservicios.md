# Arquitectura de Microservicios - Plataforma Social de Aprendizaje

## Diagrama de Microservicios

El siguiente diagrama representa los componentes principales de la plataforma, incluyendo el API Gateway, el servicio de descubrimiento (Eureka) y los microservicios con sus respectivas bases de datos (cuando aplica).

![Diagrama de Microservicios](Img/Diagrama-microservicios.png)

```plantuml
@startuml
skinparam componentStyle rectangle

' Colores personalizados
!define AUTH_COLOR #FFD580
!define EMAIL_COLOR #E6E6E6
!define AI_COLOR #FFCCCB
!define COMMON_COLOR #B3E6FF

' Cliente externo
actor Frontend 

' Gateway y Eureka
component "API Gateway" as Gateway #White
component "Eureka" as Eureka #White

' Microservicios con colores
component "Auth Service" as Auth <<Auth>> AUTH_COLOR
component "Email Service" as Email <<Email>> EMAIL_COLOR
component "AI Service" as AI <<AI>> AI_COLOR
component "Collaborative Learning Service" as Common <<Common>> COMMON_COLOR

' Bases de datos
database "DB Auth" as DBAuth
database "DB CL" as DBCommon
database "DB AI" as DBAI

' Conexiones desde el usuario
Frontend --> Gateway : Solicitudes HTTP

' Gateway se comunica con todos los servicios
Gateway --> Auth
Gateway --> Email
Gateway --> AI
Gateway --> Common

' Todos los servicios se registran en Eureka
Auth --> Eureka
Email --> Eureka
AI --> Eureka
Common --> Eureka
Gateway --> Eureka

' Conexiones a base de datos
Auth --> DBAuth
Common --> DBCommon
AI --> DBAI

@enduml
```

## Definición de Microservicios
Auth Service:
Encargado de la autenticación de colaboradores y administradores, generación de tokens y registro de colaboradores.

## Email Service:
Servicio encargado de la gestión y envío de correos electrónicos a los colaboradores y administradores de la plataforma.

## AI Service:
Servicio encargado de la integración con la API de OpenAI para generar calificaciones automáticas de preguntas y también generar nuevas preguntas de manera inteligente.

## Collaborative Learning Service:
Este microservicio gestiona la creación, calificación y retroalimentación de preguntas, respuestas y pruebas. Permite a los colaboradores publicar preguntas, recibir respuestas, calificar contenido y generar pruebas estructuradas a partir de las preguntas registradas, con el objetivo de fomentar el aprendizaje colaborativo y el refuerzo de conceptos clave entre los estudiantes.
