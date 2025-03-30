# Proceso de Despliegue de **Plataforma de aprendizaje**

## Guía Técnica de Despliegue desde Desarrollo hasta Producción (provisional)

**Grupo:** _Conti_  
**Versión:** 1.0 - Despliegue Local  
**Elaborado por:** Brandon Vargas Solano C28223  

---

## 📋 Preparación para el despliegue

### 🔍 Requisitos Previos

#### 💻 Software mínimo:
- Git (última versión)
- Git Bash (última versión)
- Java (Versión 17+)

#### ⚙️ Hardware recomendado:
- 8 GB de RAM
- 1 núcleo de CPU
- 2 GB de almacenamiento

#### ✅ Checklist Pre-Despliegue

---

## 🚀 Proceso de Despliegue

### 1. Clonar el repositorio

```bash
git clone https://github.com/leocamachocr/spring-cloud-basic-example.git
cd spring-cloud-basic-example
```

### 2. Iniciar los servicios (cada uno en una terminal nueva)

#### Terminal 1: Servidor Eureka (Dashboard de servicios)
```bash
cd eureka/
./gradlew bootRun
```
**Verificación:**  
🔹 Espera hasta ver el mensaje `Started EurekaServerApplication`  
🔹 Accede al dashboard en [http://localhost:8761](http://localhost:8761)

#### Terminal 2: Servicio de Autenticación
```bash
cd authentication-service/
./gradlew bootRun
```
**Verificación:**  
🔹 Observa los logs de Spring Boot para confirmar inicio exitoso

#### Terminal 3: Servicio Básico
```bash
cd basic-service/
./gradlew bootRun
```
**Verificación:**  
🔹 Comprueba en Eureka [http://localhost:8761](http://localhost:8761) que el servicio aparezca como "UP"

#### Terminal 4: Gateway (Puerta de enlace)
```bash
cd gateway/
./gradlew bootRun
```
**Verificación final:**  
🔹 Todos los servicios deben aparecer como "UP" en el dashboard de Eureka

---

### ⏹ Detener los servicios
En cada terminal, presiona `Ctrl + C` para detener los servicios.  
**Nota:** El orden de apagado no es relevante.

---

## 🔗 Resumen de URLs clave

| Servicio  | URL                                      |
|-----------|------------------------------------------|
| Eureka    | [http://localhost:8761](http://localhost:8761) |
| Gateway   | [http://localhost:8080](http://localhost:8080) |
| Auth      | [http://localhost:8081](http://localhost:8081) |
| Basic     | [http://localhost:8082](http://localhost:8082) |

---

## 📌 Notas adicionales

- ✅ Verifica que tienes **Java** y **Gradle** correctamente instalados
- 🐞 Si encuentras errores:
  - Confirma que cada servicio se registró correctamente en Eureka
  - Revisa los logs de cada servicio para identificar problemas
- ⏱ Los tiempos de inicio pueden variar según tu hardware

---

> **Tip:** Mantén todas las terminales visibles para monitorear fácilmente los logs de cada servicio.
