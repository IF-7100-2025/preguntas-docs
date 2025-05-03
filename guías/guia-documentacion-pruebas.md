# **📚 Guía de Pruebas Unitarias y de Integración

## **1️⃣ Introducción**

Esta guía está destinada a la creación de pruebas unitarias y de integración. A lo largo de este documento, aprenderás cómo usar las herramientas **Mockito**, **Junit** **Spring Boot Test** y **Gherkin** para crear, ejecutar y verificar las pruebas de tu aplicación.

## **2️⃣ ¿Qué son las Pruebas Unitarias y de Integración?**

* **Pruebas Unitarias**: Son pruebas que validan el comportamiento de unidades de código individuales, como métodos o funciones. Estas pruebas verifican que el código de la unidad específica funcione como se espera.

* **Pruebas de Integración**: Son pruebas que verifican la correcta interacción de diferentes módulos o componentes dentro del sistema. Por ejemplo, cómo se comunican el frontend y el backend o cómo se integra la aplicación con la base de datos.

## **3️⃣ Herramientas a Utilizar 🛠️**

### **Spring Boot Test**

Es una herramienta de Spring que proporciona soporte completo para realizar pruebas de aplicaciones basadas en **Spring Boot**. Permite ejecutar pruebas tanto **unitarias** como de **integración**, simulando un entorno completo de la aplicación sin necesidad de desplegar un servidor real. Utiliza anotaciones como `@SpringBootTest` para cargar el contexto de la aplicación durante las pruebas.

### **Mockito**

Es un marco de pruebas que permite **simular objetos (mocks)** en las pruebas unitarias. Se usa principalmente para aislar las unidades de código y evitar dependencias externas como bases de datos o servicios. Con **Mockito**, puedes simular el comportamiento de clases y objetos, controlando su comportamiento y verificando las interacciones entre ellos durante las pruebas.

### **JUnit**

Es un framework ampliamente utilizado para realizar pruebas unitarias. Proporciona las anotaciones necesarias como ``@Test``, ``@BeforeEach``, ``@AfterEach``, entre otras, para estructurar y ejecutar pruebas de manera eficiente. Además, permite verificar los resultados mediante aserciones, como **assertEquals()**, **assertTrue()**, etc. Es esencial para ejecutar pruebas de manera automatizada en Java.

---

## **3️⃣ Estructura del Proyecto con Patrón CQRS 🗂️**



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

                              ├── controllers    	\<-- Aquí van las pruebas de los controladores

                              └── integration    	\<-- Aquí van las pruebas de integración

### **Ubicación de las Pruebas:**

* **Pruebas Unitarias de Handlers**: Se encuentran en la carpeta `src/test/java/.../handlers/`.

* **Pruebas de Integración**: Se encuentran en la carpeta `src/test/java/.../integration/`.

* **Pruebas de Controladores**: Si tienes controladores, las pruebas para ellos se almacenan en `controllers/`.

## **4️⃣ Cómo Realizar Pruebas Unitarias 🧑‍💻**

### **Paso 1: Configurar Mockito y JUnit para las Pruebas Unitarias**

Para poder realizar pruebas unitarias utilizando **Mockito** y **JUnit** en un proyecto de **Gradle**, primero debes agregar las dependencias necesarias en el archivo `build.gradle`.

#### **Incluir las dependencias en Gradle:**

1. Abre tu archivo `build.gradle.kts`

2. Agrega las siguientes dependencias en la sección `dependencies`:

        dependencies {

          // Dependencia de JUnit 5 para las pruebas unitarias

          testImplementation 'org.junit.jupiter:junit-jupiter-api:5.7.0'

          testImplementation 'org.junit.jupiter:junit-jupiter-engine:5.7.0'

          // Dependencia de Mockito para simular objetos (mocks)

          testImplementation 'org.mockito:mockito-core:4.0.0'

          // Para usar las anotaciones de JUnit y Mockito

          testImplementation 'org.mockito:mockito-junit-jupiter:4.0.0'

        }


* **JUnit 5**: La versión moderna de JUnit, que incluye soporte para pruebas basadas en anotaciones como `@Test`.

* **Mockito**: Para crear mocks de objetos y simular dependencias.

* **Mockito-JUnit Jupiter**: Esta dependencia es necesaria para integrar **Mockito** con **JUnit 5** y poder usar las anotaciones de **Mockito** junto con JUnit.

3. En la sección `test` de tu `build.gradle`, asegúrate de tener esto para que Gradle reconozca que usarás JUnit 5:

        test {

          useJUnitPlatform() // Indica que se usará JUnit 5

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


**Explicación**:

* **Mockito** se usa para simular el `UserRepository`, lo que permite probar el servicio sin tener que acceder a una base de datos real.

* **JUnit** organiza la prueba y verifica que el nombre del usuario devuelto sea "Juan Pérez" utilizando `assertEquals()`.

### **Paso 3: Ejecutar la Prueba**

1. Para ejecutar las pruebas unitarias en **IntelliJ IDEA**:

   * Haz clic derecho sobre el archivo de prueba y selecciona **Run 'UserServiceTest'**.

2. También puedes ejecutar las pruebas desde la línea de comandos con Gradle:

        ./gradlew test

Esto ejecutará todas las pruebas en tu proyecto, incluyendo las pruebas unitarias configuradas con **JUnit** y **Mockito**.

## **5️⃣ Cómo Realizar Pruebas de Integración 🔄**

### **Paso 1: Configurar las Dependencias para las Pruebas de Integración**

En un proyecto de **Gradle** que utiliza **Spring Boot**, necesitas agregar las dependencias necesarias para realizar pruebas de integración. Estas dependencias permiten que puedas probar toda la aplicación en un entorno controlado, simulando la interacción entre los componentes del sistema.

#### **Incluir las dependencias en Gradle:**

1. Abre el archivo `build.gradle.kts`.

2. Asegúrate de agregar las siguientes dependencias en la sección `dependencies`:

          dependencies {
        // Dependencia de Spring Boot Test para realizar pruebas de integración
        testImplementation 'org.springframework.boot:spring-boot-starter-test'


        // Dependencia de JUnit 5 (si aún no la has agregado)
        testImplementation 'org.junit.jupiter:junit-jupiter-api:5.7.0'
        testImplementation 'org.junit.jupiter:junit-jupiter-engine:5.7.0'


        // Dependencia de Mockito (si es necesario para la integración con mocks)
        testImplementation 'org.mockito:mockito-core:4.0.0'
      }

* **`spring-boot-starter-test`**: Proporciona todas las herramientas necesarias para realizar pruebas en aplicaciones basadas en Spring Boot, como `@SpringBootTest`, `@AutoConfigureMockMvc`, entre otras.

* **JUnit 5**: Asegúrate de tener configurada la dependencia de **JUnit 5** para organizar y ejecutar las pruebas.

* **Mockito**: Si necesitas crear mocks de componentes en las pruebas de integración, añade **Mockito** como en el caso de las pruebas unitarias.

3. En la sección `test` de tu archivo `build.gradle`, agrega lo siguiente para usar JUnit 5 en las pruebas de integración:

### **Paso 2: Escribir una Prueba de Integración con Spring Boot Test**

Una vez configuradas las dependencias, puedes escribir una **prueba de integración** para verificar cómo interactúan los componentes de tu aplicación. Aquí tienes un ejemplo de cómo escribir una prueba para un **Command Handler** que interactúa con el **repositorio** y verifica que el usuario se ha registrado correctamente en la base de datos.

#### **Ejemplo de prueba de integración usando Spring Boot Test:**

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.context.SpringBootTest;
    import org.junit.jupiter.api.Test;
    import static org.junit.jupiter.api.Assertions.*;


    @SpringBootTest // Carga el contexto completo de Spring
    public class CreateUserCommandHandlerIntegrationTest {


      @Autowired
      private CreateUserCommandHandler handler;


      @Autowired
      private UserRepository userRepository;


      @Test
      public void testHandleCreateUserCommandIntegration() {
          // Crear el comando para el registro de usuario
          CreateUserCommand command = new CreateUserCommand("Juan Pérez", "juan@example.com");


          // Ejecutar el handler que procesa el comando
          User result = handler.handle(command);


          // Verificar que el usuario fue creado en la base de datos
          assertNotNull(result);
          assertTrue(userRepository.existsById(result.getId())); // Verifica que el usuario exista en la base de datos
      }
    }


**Explicación**:

* **`@SpringBootTest`**: Esta anotación carga todo el contexto de Spring para realizar pruebas de integración, lo que significa que se simula el comportamiento de toda la aplicación, incluyendo la base de datos.

* **`@Autowired`**: Inyecta las dependencias necesarias, como el `CreateUserCommandHandler` y el `UserRepository`, para que puedas usarlas en la prueba.

* **Verificación**: Se verifica que el usuario ha sido **creado correctamente** y almacenado en la base de datos utilizando `userRepository.existsById()`.

### **Paso 3: Ejecutar la Prueba de Integración**

Para ejecutar las pruebas de integración:

1. **Ejecuta la prueba** en **IntelliJ IDEA** haciendo clic derecho sobre el archivo de prueba y seleccionando **Run 'CreateUserCommandHandlerIntegrationTest'**.

2. O también puedes ejecutar las pruebas desde la línea de comandos con Gradle:

./gradlew test

Esto ejecutará todas las pruebas en tu proyecto, incluyendo las pruebas de integración.

## **6️⃣ Escribir Pruebas con Gherkin 📝**

**Gherkin** es un lenguaje de propósito específico (DSL) utilizado para describir el comportamiento del sistema de manera comprensible para todas las partes involucradas en el proyecto. A continuación, aprenderás cómo usar Gherkin para documentar los **escenarios de prueba** sin necesidad de ejecutar las pruebas automáticamente.

### **Paso 1: Configuración de Gherkin sin Cucumber**

Para trabajar con **Gherkin** sin **Cucumber**, simplemente necesitas agregar la dependencia de **Gherkin** en tu proyecto **Gradle**. Esto te permitirá escribir los archivos `.feature` que describen los escenarios de prueba.

#### **Incluir la dependencia de Gherkin en Gradle:**

1. Abre tu archivo `build.gradle.kts`.

2. Agrega la siguiente dependencia para Gherkin en la sección `dependencies`:  
          
          dependencies {

        // Dependencia de Gherkin para trabajar con archivos .feature
        testImplementation 'io.cucumber:gherkin:20.1.0'
        
        }

     
   Con esta dependencia, puedes trabajar con **archivos `.feature`** y escribir los escenarios de prueba utilizando la sintaxis de **Gherkin**, sin necesidad de integrar Cucumber para la ejecución automática de las pruebas.**Paso 2: Estructura de Archivos y Creación de Archivos .feature**  
1. **Crea una carpeta para los archivos `.feature`**:

   * En tu proyecto, dentro de la carpeta `src/test/resources`, crea una carpeta llamada **`features`**. Aquí es donde colocarás todos los archivos `.feature` que describen los escenarios de prueba.

2. **Crear un archivo `.feature`**:

   * Dentro de la carpeta `features`, crea un archivo con la extensión `.feature`. Los archivos `.feature` contienen los **escenarios de prueba** en formato **Gherkin**.

   #### **Ejemplo de archivo `.feature`:**

        Feature: Registro de Usuario


        Scenario: Registro con datos válidos

        Given que el usuario está en la página de registro

        When el usuario ingresa el nombre "Juan Pérez" y el correo "juan@example.com"

        Then el sistema debería registrar al usuario y enviar un correo de verificación

        

        Scenario: Registro con correo duplicado

        Given que el usuario está en la página de registro

        When el usuario ingresa el correo "juan@example.com"

        Then el sistema debería mostrar un mensaje de error indicando que el correo ya está registrado

   

**Explicación**:

* **Feature**: Representa una funcionalidad o una característica que estamos probando (en este caso, el registro de usuario).

* **Scenario**: Es un escenario o caso de prueba dentro de esa funcionalidad.

  * **Given**: Describe el contexto inicial (por ejemplo, el usuario está en la página de registro).

  * **When**: Describe la acción que realiza el usuario.

  * **Then**: Describe el resultado esperado después de realizar la acción.


  ### **Paso 2: Organización de los Archivos `.feature`**

Para organizar bien los archivos de prueba, puedes agruparlos en subcarpetas según el tipo de funcionalidad que estés probando. Por ejemplo, si tienes diferentes funcionalidades como **registro de usuario** y **login**, podrías organizar los archivos de la siguiente manera:

    src/test/resources/features/

    ├── registro

    │   └── registro-usuario.feature

    └── login

      └── login-usuario.feature

## **7️⃣ Conclusión 🎯**

Ahora sabes cómo realizar **pruebas unitarias y de integración** usando **Mockito**, **Spring Boot Test** y **Gherkin** dentro de un proyecto que sigue el patrón **CQRS**. Siguiendo estos pasos, podrás asegurarte de que tanto los **command handlers** como los **componentes integrados** funcionen correctamente.

Recuerda:

* **Mockito** para simular dependencias y realizar pruebas unitarias.

* **Spring Boot Test** para verificar la integración entre los componentes del sistema.

* **Gherkin** para documentar escenarios de prueba de manera clara y comprensible.
