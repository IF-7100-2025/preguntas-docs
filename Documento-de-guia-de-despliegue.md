Proceso de Despliegue de **Plataforma de aprendizaje**

## Guía Técnica de Despliegue desde Desarrollo hasta Producción (provisional)

Grupo: _Conti_  
_Versión 1.0 \- Despliegue Local_

Elaborado por Brandon Vargas Solano C28223

## Preparación para el despliegue

### Requisitos Previos

#### Software mínimo:

- Git Latest version
- Git Bash latest version
- Java Version \+17

#### Hardware recomendado:

- 8 GB de RAM
- 1 núcleo de CPU
- 2 GB de almacenamiento

#### Checklist Pre-Despliegue

### **1\. Clonar el repositorio**

Abre una terminal y ejecuta:

`git clone https://github.com/leocamachocr/spring-cloud-basic-example.git`  
`cd spring-cloud-basic-example`

### **2\. Iniciar los servicios (cada uno en una terminal nueva)**

### **Terminal 1: Servidor Eureka (Dashboard de servicios)**

#### 1. Navega al directorio `eureka`:

`cd eureka/`

#### 2. Inicia el servidor Eureka:

`./gradlew bootRun`

#### 3. Espera a que carguen las dependencias y aparezca

`Started EurekaServerApplication`.

**Verificación:** Abre [http://localhost:8761](http://localhost:8761) para ver el dashboard.

### **Terminal 2: Servicio de Autenticación**

#### 1. Navega al directorio `authentication-service`:

`cd authentication-service/`

#### 2. Inicia el servicio de autenticación:

`./gradlew bootRun`

#### 3. Espera a que cargue y veas los logs de Spring Boot.

### **Terminal 3: Servicio Básico**

#### 1. Navega al directorio `basic-service`:

`cd basic-service/`

#### 2. Inicia el servicio básico:

`./gradlew bootRun`

#### 3. Espera a que cargue.

**Verificación:** Revisa Eureka en [http://localhost:8761](http://localhost:8761) para confirmar que el servicio esté marcado como "UP".



### **Terminal 4: Gateway (Puerta de enlace)**

#### 1. Navega al directorio `gateway`:

`cd gateway/`

#### 2. Inicia el gateway:

`./gradlew bootRun`

#### 3. Espera a que cargue.

### **Verificación:** Todos los servicios deben aparecer como "UP" en Eureka.



### **3\. Detener los servicios**

Para detener los servicios, en cada terminal, presiona `Ctrl + C` para detener el servicio.

**Nota:** No importa el orden en que apagues los servicios.

---

### **Resumen de URLs clave**

| Servicio | URL                                            |
| -------- | ---------------------------------------------- |
| Eureka   | [http://localhost:8761](http://localhost:8761) |
| Gateway  | [http://localhost:8080](http://localhost:8080) |
| Auth     | [http://localhost:8081](http://localhost:8081) |
| Basic    | [http://localhost:8082](http://localhost:8082) |

---

### **Notas adicionales:**

- Asegúrate de tener **Java** y **Gradle** instalados.

- Si hay errores, verifica que cada servicio se haya registrado correctamente en Eureka antes de continuar.
