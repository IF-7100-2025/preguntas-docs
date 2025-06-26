# **Guía de Pruebas Unitarias y Manuales**

## **Introducción**

Esta guía está destinada a la creación de pruebas unitarias y de integración. A lo largo de este documento, aprenderás cómo usar las herramientas **Mockito**, **Junit** **Spring Boot Test** y **Gherkin** para crear, ejecutar y verificar las pruebas de tu aplicación.

***

## **Pruebas unitarias**

### **¿Qué son las Pruebas Unitarias?**

**Pruebas Unitarias**: Son pruebas que validan el comportamiento de unidades de código individuales, como métodos o funciones. Estas pruebas verifican que el código de la unidad específica funcione como se espera.

## **Herramientas a Utilizar**

### **Spring Boot Test**

Es una herramienta de Spring que proporciona soporte completo para realizar pruebas de aplicaciones basadas en **Spring Boot**. Permite ejecutar pruebas tanto **unitarias** como de **integración**, simulando un entorno completo de la aplicación sin necesidad de desplegar un servidor real. Utiliza anotaciones como `@SpringBootTest` para cargar el contexto de la aplicación durante las pruebas.

### **Mockito**

Es un marco de pruebas que permite **simular objetos (mocks)** en las pruebas unitarias. Se usa principalmente para aislar las unidades de código y evitar dependencias externas como bases de datos o servicios. Con **Mockito**, puedes simular el comportamiento de clases y objetos, controlando su comportamiento y verificando las interacciones entre ellos durante las pruebas.

### **JUnit**

Es un framework ampliamente utilizado para realizar pruebas unitarias. Proporciona las anotaciones necesarias como ``@Test``, ``@BeforeEach``, ``@AfterEach``, entre otras, para estructurar y ejecutar pruebas de manera eficiente. Además, permite verificar los resultados mediante aserciones, como **assertEquals()**, **assertTrue()**, etc. Es esencial para ejecutar pruebas de manera automatizada en Java.

---

## **Estructura del Proyecto con Patrón CQRS**

    question-service

    ├── gradle

    ├── src

    │   └── main

    │   	└── java

    │       	└── ucr

    │           	└── ac

    │               	└── cr

    │                   	└── learningcommunity

    │                       	└── questionservice

    │                           	├── api            	\<-- Aquí van los controladores

    │                           	├── config         	\<-- Configuración general

    │                           	├── handlers       	\<-- Aquí van los command handlers

    │                           	├── jpa            	\<-- Aquí va la lógica de acceso a datos

    │                           	└── models         	\<-- Modelos de datos

    │   └── resources

    └── test

      └── java

          └── ucr

              └── ac

                  └── cr

                      └── learningcommunity

                          └── questionservice

                              ├── handlers       	\<-- Aquí van las pruebas unitarias de los handlers

### **Ubicación de las Pruebas:**

* **Pruebas Unitarias de Handlers**: Se encuentran en la carpeta `src/test/java/.../handlers/`.

## **Cómo Realizar Pruebas Unitarias**

### **Paso 1: Configurar Mockito y JUnit para las Pruebas Unitarias**

Para poder realizar pruebas unitarias utilizando **Mockito** y **JUnit** en un proyecto de **Gradle**, primero debes agregar las dependencias necesarias en el archivo `build.gradle`.

#### **Incluir las dependencias en Gradle:**

1. Abre tu archivo `build.gradle.kts`

2. Agrega las siguientes dependencias en la sección `dependencies`:

        dependencies {

        // Dependencia de JUnit 5 para las pruebas unitarias
        testImplementation("org.junit.jupiter:junit-jupiter-api:5.7.0")

        testImplementation("org.junit.jupiter:junit-jupiter-engine:5.7.0")

        // Dependencia de Mockito para simular objetos (mocks)
        testImplementation("org.mockito:mockito-core:4.0.0")

        // Para usar las anotaciones de JUnit y Mockito
        testImplementation("org.mockito:mockito-junit-jupiter:4.0.0")

        }


* **JUnit 5**: La versión moderna de JUnit, que incluye soporte para pruebas basadas en anotaciones como `@Test`.

* **Mockito**: Para crear mocks de objetos y simular dependencias.

* **Mockito-JUnit Jupiter**: Esta dependencia es necesaria para integrar **Mockito** con **JUnit 5** y poder usar las anotaciones de **Mockito** junto con JUnit.

3. En la sección `test` de tu `build.gradle`, asegúrate de tener esto para que Gradle reconozca que usarás JUnit 5:

        tasks.withType<Test> {
          useJUnitPlatform()
        }

### **Paso 2: Crear un Mock y Realizar una Prueba Unitaria**

Una vez configurado **JUnit** y **Mockito**, puedes escribir tus pruebas unitarias. A continuación, te muestro un ejemplo de cómo realizar una prueba unitaria con un mock de un repositorio usando **Mockito**.

#### **Ejemplo de prueba unitaria con Mockito y JUnit:**
    import static org.mockito.Mockito.*;
    import static org.junit.jupiter.api.Assertions.assertEquals;


    public class UserServiceTest {


      @Test
      public void testGetUserById() {
          // Crear un mock del UserRepository
          UserRepository userRepository = mock(UserRepository.class);


          // Definir el comportamiento del mock
          when(userRepository.findById(1)).thenReturn(new User(1, "Juan Pérez"));


          // Crear el servicio que depende del mock
          UserService userService = new UserService(userRepository);


          // Ejecutar el método de la unidad de código
          User user = userService.getUserById(1);


          // Usar JUnit para verificar el resultado
          assertEquals("Juan Pérez", user.getName());
      }
    }

En caso de que se realicen varios test en una sola clase la creación del mock debe hacerse por medio de:

`@BeforeEach
    void setUp() {
}`

Para que el escenario base pueda ser compartido entre los diferentes test.

**Explicación**:

**Mockito** se usa para simular el `UserRepository`, lo que permite probar el servicio sin tener que acceder a una base de datos real.

**JUnit** organiza la prueba y verifica que el nombre del usuario devuelto sea "Juan Pérez" utilizando `assertEquals()`.

### **Paso 3: Ejecutar la Prueba**

1. Para ejecutar las pruebas unitarias en **IntelliJ IDEA**:

   * Haz clic derecho sobre el archivo de prueba y selecciona **Run 'UserServiceTest'**.

2. También puedes ejecutar las pruebas desde la línea de comandos con Gradle:

        ./gradlew test

Esto ejecutará todas las pruebas en tu proyecto, incluyendo las pruebas unitarias configuradas con **JUnit** y **Mockito**.

## **Porcentaje de cobertura en las pruebas**

Para que las pruebas unitarias se consideren satisfactorias y cumplan con los estándares del proyecto, 
se requiere alcanzar una cobertura mínima del 80% en los componentes handlers de cada microservicio.
Este nivel de cobertura garantiza que la lógica de negocio se valide de forma adecuada,
así como la existencia de un código funcional, confiable y mantenible.

## **Funcionalidades cubiertas por medio de las pruebas**

Para el proyecto se decidió que las pruebas unitarias estuvieran enfocadas en cubrir las historias de usuario desarrolladas
a lo largo del sprint, estas historias de usuario son las siguientes:

- US01 Registrar preguntas
- US02 Crear puebas
- US03 Resolver quizzes
- US13 Reporte de contenido
- US14 Racha diaria, XP y rangos
- US16 Registrarse en la plataforma
- US20 Iniciar sesion en la plataforma

## **Jacoco**

Dado que Spring Boot no posee por defecto una manera de verificar el estado de cobertura del codigo, se incoporó Jacoco a los test unitarios,
JaCoCo (Java Code Coverage) es una herramienta que permite medir la cobertura de código en proyectos Java, incluyendo aquellos desarrollados con Spring Boot.
Su propósito principal es verificar qué partes del código son ejecutadas durante las pruebas unitarias, ayudando a identificar secciones no probadas y mejorar la calidad del software.
JaCoCo genera reportes detallados por medio de un html que muestran el resultado de los test realizados.

Para implementar Jacoco en el código necesita mofificar el archivo `build.gradle.kts` de la siguiente manera:

`plugins {
         java
         id("org.springframework.boot") version "3.4.3"
         id("io.spring.dependency-management") version "1.1.7"
         id("jacoco")
}`

`tasks.withType<Test> {
	tasks.test {
		finalizedBy(tasks.jacocoTestReport)
	}
	tasks.jacocoTestReport {
		dependsOn(tasks.test)
	}
}`

`jacoco {
   toolVersion = "0.8.13"
   reportsDirectory = layout.buildDirectory.dir("customJacocoReportDir")
}`

`tasks.jacocoTestReport {
   reports {
      xml.required = false
      csv.required = false
      html.outputLocation = layout.buildDirectory.dir("jacocoHtml")
   }
}`

Una vez ejecutados los test de manera exitosa el reporte se maneja de manera dinamica en el código para ser consultado.

## **Microservicios probados**

Dado que se decidió probar la lógica de negocio, los servicios que contienen pruebas son los servicios de: ia, preguntas y 
el servicio de autentificación, sin embargo, el servicio de autentificación no tiene sus pruebas ejecutadas de manera automática debido
a la limitante de que el mismo se encuentra construído con la versión de gradle 8.4, la cual no posee la facilidad de ejecutar las mismas por medio
del wrapper con el comando ./gradlew test. En cuanto a los servicios de Eureka, Gateway y Email los mismos no fueron probados al estar mayórmente enfocados 
a proveer servicios y configuración del entorno.

***

## Pruebas Manuales

### **¿Qué son las Pruebas Manuales?**

**Pruebas Manuales**: Consisten en verificar de forma directa que una funcionalidad del sistema funcione según lo esperado, sin el uso de automatización.

## **Herramientas a Utilizar**

### **Postman**

Herramienta que permite enviar y validar solicitudes HTTP para probar el comportamiento de APIs de forma rápida y sencilla.

**Preparación del entorno**

Para realizar pruebas manuales primero se deben comprobar 2 aspectos:

- a. Que Postman tenga las URLs correctas, encabezados y autenticación configurados.
- b. Que cada uno de los microservicios se encuentre en ejecucion.

**Revisión del Caso de Uso**

Por medio de las pruebas manuales se busca que las cartas definidas cumplan con los criterios de aceptación que poseen:
Para ello se contemplan 2 escenarios:

- a. El flujo ideal o normal de operación.
- b. Escenarios concretos a validar, en este caso las cartas definidas.

**Criterios de validación**

Una prueba se considera exitosa si:

La API responde con el código correcto (200 o 201).

La información devuelta es coherente con el caso de uso.

**Ejecución de pruebas**

Establecer la URL del endpoint de manera manual o por medio de la variable.

Seleccionar el método HTTP correspondiente (GET, POST, PUT).

Definir el cuerpo de la solicitud en caso de que se requiera.

Agregar el token con la sesion iniciada.

Envíar la solicitud desde Postman.

Verificar el código de respuesta y el contenido.

Verificar que el mensaje obtenido en la respuesta sea satisfactorio

**Cobertura de pruebas manuales**

Al igual que las pruebas unitarias cada prueba manual debe validar una funcionalidad,
en este caso cada una debe estar ligada a una carta que se debe haber completado de manera
satisfactoria por medio de sus criterios de aceptación.
