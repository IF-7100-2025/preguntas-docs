# **Documentación de Pruebas**

## **Plan de Ejecución de Pruebas**

### **1\. Definición de los Tipos de Pruebas a Ejecutar**

#### **Pruebas Unitarias**

* **Objetivo:** Validar el comportamiento de las unidades individuales de código, como métodos y funciones.

* **Herramientas:** JUnit.

* **Alcance:** Cada método o función del código será probado en aislamiento, utilizando entradas conocidas y verificando que la salida sea la esperada.

#### **Pruebas de Integración**

* **Objetivo:** Verificar que los diferentes módulos del sistema interactúan correctamente entre sí.

* **Herramientas:** Spring Boot Test, MockMvc.

* **Alcance:** Se probarán las interacciones entre los componentes del sistema, como la comunicación entre el frontend y el backend, la integración con la base de datos, etc.

# **Escenarios de Pruebas según las Historias de Usuario**

## **2\. Identificación de los Criterios de Aceptación de Cada Historia de Usuario**

### **Historia de Usuario 1: Registro de Usuario**

* **Criterios de Aceptación:**

  1. El sistema debe permitir el registro con nombre, correo electrónico y contraseña válidos.

  2. Se debe enviar un correo de verificación tras un registro exitoso.

  3. El correo electrónico debe ser único (no registrado previamente).

### **Historia de Usuario 2: Login de Usuario**

* **Criterios de Aceptación:**

  1. El usuario podrá iniciar sesión con su correo electrónico y contraseña.

  2. Si las credenciales son incorrectas, se mostrará un mensaje de error.

  3. Si las credenciales son correctas, el usuario será redirigido a su página de inicio.

---

## **3\. Definición de Casos de Prueba Basados en los Escenarios Funcionales**

### **Caso de Prueba 1: Registro de Usuario**

* **Entrada:** Nombre: "Juan Pérez", Correo: "juan@example.com", Contraseña: "123456"

* **Acción:** El usuario ingresa los datos y presiona "Registrar".

* **Resultado Esperado:** El sistema valida los datos, envía el correo de verificación y muestra un mensaje de éxito.

### **Caso de Prueba 2: Login con Usuario Existente**

* **Entrada:** Correo: "juan@example.com", Contraseña: "123456"

* **Acción:** El usuario ingresa las credenciales y presiona "Iniciar sesión".

* **Resultado Esperado:** El sistema redirige al usuario a la página de inicio.

### **Caso de Prueba 3: Login con Contraseña Incorrecta**

* **Entrada:** Correo: "juan@example.com", Contraseña: "incorrecta"

* **Acción:** El usuario ingresa las credenciales incorrectas y presiona "Iniciar sesión".

* **Resultado Esperado:** El sistema muestra un mensaje de error indicando que las credenciales son incorrectas.

---

## **4\. Validación de Flujos Alternativos y Manejo de Errores**

### **Flujo Alternativo 1: Registro con Datos Incorrectos**

* **Entrada:** Nombre: "Juan", Correo: "juan", Contraseña: "123"

* **Acción:** El usuario ingresa datos incorrectos y presiona "Registrar".

* **Resultado Esperado:** El sistema muestra un mensaje de error indicando que el correo o la contraseña no son válidos.

### **Flujo Alternativo 2: Login con Usuario No Registrado**

* **Entrada:** Correo: "inexistente@example.com", Contraseña: "123456"

* **Acción:** El usuario intenta iniciar sesión con un correo no registrado.

* **Resultado Esperado:** El sistema muestra un mensaje de error indicando que el usuario no existe.

---

# **Resultados de Ejecución de Pruebas**

## **5\. Registro y Documentación de los Resultados Obtenidos**

### **Pruebas Unitarias**

* **Resultado:** Todas las pruebas unitarias pasaron correctamente.

* **Errores:** Ninguno.

### **Pruebas de Integración**

* **Resultado:** Las pruebas de integración fueron exitosas para la comunicación entre el frontend y el backend.

* **Errores:** Se detectaron errores menores en la validación de la autenticación, ya corregidos.

### **Pruebas de UI**

* **Resultado:** Las pruebas de interfaz mostraron que todos los formularios y botones funcionan correctamente.

* **Errores:** Se encontraron problemas de visualización en dispositivos móviles que se están investigando.

---

## **6\. Reporte de Errores y su Seguimiento**

### **Error 1: Validación de Correo Electrónico**

* **Descripción:** La validación del correo electrónico no se realizaba correctamente en el formulario de registro.

* **Estado:** Resuelto. Se corrigió la expresión regular para aceptar correctamente los correos electrónicos.

### **Error 2: Redirección Después del Login**

* **Descripción:** La redirección al inicio no funcionaba correctamente.

* **Estado:** En progreso. Actualmente se está investigando el flujo de autenticación.

---

## **7\. Criterios de Aprobación para el Pase a Producción**

* **Requisitos para Pase a Producción:**

  1. Todas las pruebas unitarias deben pasar exitosamente.

  2. Las pruebas de integración deben haber validado exitosamente la comunicación entre módulos.

  3. No deben existir errores críticos relacionados con la autenticación o la interfaz de usuario.

  4. Los flujos alternativos y de manejo de errores deben haber sido verificados y correctamente implementados.

