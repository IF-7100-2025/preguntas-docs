# 📦 Plataforma de Aprendizaje - Guía Técnica de Despliegue

**Grupo:** Conti  
**Versión:** 2.0  
**Autor:** Brandon Vargas Solano - C28223

---

## 🧠 Descripción General

Este proyecto implementa una arquitectura de microservicios usando **Spring Boot**, **Spring Cloud**, **Kafka**, **Redis**, y **Docker**. Incluye CI/CD con GitHub Actions, y puede ejecutarse en entornos de desarrollo, pruebas o producción (localmente).

---

## 📋 1. Preparación para el Despliegue

### ✅ Requisitos de Software

| Herramienta    | Versión mínima       |
| -------------- | -------------------- |
| Java           | 21                   |
| Git            | Latest               |
| Gradle         | Incluido con wrapper |
| Docker         | 20+                  |
| Docker Compose | 1.29+                |
| pgAdmin4       | PostgreSQL 16        |

## [Enlace a tutorial de instalacion de pgAdmin4 ](https://www.youtube.com/watch?v=w9ax9-s2jbE)

### 💻 Requisitos de Hardware (mínimos sugeridos)

- 8 GB de RAM
- 1 CPU
- 2 GB de almacenamiento libre

---

## 📌 Checklist Pre-Despliegue

Antes de ejecutar cualquier entorno, asegurate de cumplir con lo siguiente:

- [ ] **Archivo `.env` creado y suministrado previamente**, que contiene:

  - `JWT_SECRET`
  - `GATEWAY_JWT_SECRET`
  - `OPENAI_API_KEY`
  - `SENDGRID_API_KEY`

- [ ] ¿Tenés la **última versión del proyecto** (`main` o rama correspondiente)?

- [ ] **Bases de datos creadas manualmente** (si estás en entorno local sin contenedores):

  - `auth_db`
  - `questions_db`
  - `ia_db`
  - Estas deben existir y estar disponibles desde **pgAdmin 4**.

- [ ] Archivos sensibles **no versionados** deben estar presentes **en tu entorno local**:

  - 🔐 API Key de OpenAI:
    `ia-service/src/main/resources/application-secret.yml`
  - 📧 Credenciales de SendGrid:
    `email-service/src/main/resources/email-credentials.yml`
  - 🗄️ Configuración de contraseñas de base de datos:
    `./shared-config/application-db-secrets.yml`
    Este archivo debe contener algo como:

    ```yaml
    dataConfig:
      password: password
    ```

- [ ] Docker instalado y funcionando correctamente (solo necesario si vas a levantar Redis, Kafka, etc. en contenedores).

---

## 🖥️ Opción 1: Desarrollo Local usando Gradle (sin IDE)

Esta opción permite correr todos los microservicios manualmente desde consola, **sin abrir el IDE**, ejecutando directamente los servicios con `./gradlew bootRun`.

Ideal para entornos de desarrollo donde:

- Ya tenés las bases de datos en **pgAdmin**
- Los secretos están configurados localmente
- No necesitás contenedores, solo los servicios como procesos
- Pero necesitan levantar **infraestructura auxiliar** como Kafka, Redis, Zookeeper

#### Comando

```bash
docker-compose -f compose-base.yml up -d
```

- Levantara **infraestructura auxiliar** como Kafka, Redis, Zookeeper.

---

### ▶️ Ejecutar el script

Desde la raíz del proyecto, corré:

```bash
./run-all.sh
```

Este script abrirá cada servicio en segundo plano.

---

### 📄 Archivo: `run-all.sh`

```bash
#!/bin/bash

services=(
  "eureka"
  "gateway"
  "authentication-service"
  "question-service"
  "ia-service"
  "email-service"
)

for service in "${services[@]}"; do
  echo "🚀 Iniciando $service..."
  cd "$service" && ./gradlew bootRun &
  cd ..
done

echo " Todos los servicios están corriendo en segundo plano"
echo "Usa 'pkill -f bootRun' para detenerlos todos"
```

> ⚠️ Asegurate de ejecutarlos desde una consola GitBash.

---

### 🔍 Verificación

Una vez corriendo:

- ✅ Eureka Dashboard: [http://localhost:8761](http://localhost:8761)
- ✅ API Gateway: [http://localhost:8080](http://localhost:8080)

---

### Opción 2: 🧪 Entorno de Desarrollo Asistido con Docker e IntelliJ (desarrollo)

Esta opción está pensada para desarrollar (dev) para ejecutar los microservicios manualmente (desde el IDE o usando `./run-all.sh`) pero necesitan levantar **infraestructura auxiliar** como Kafka, Redis, Zookeeper y las bases de datos de `auth_db`, `questions_db`, `ia_db`.

---

#### Comando

```bash
docker-compose -f compose-base.yml up -d
```

---

#### 🧰 Servicios que se levantan

- Kafka
- Zookeeper
- Redis

---

#### 🗃️ Dependencias externas

- Las bases de datos `auth_db`, `questions_db`, `ia_db` **se ejecutan desde el entorno de desarrollo en PGAdmin 4** (no en contenedores).
- Los microservicios **se ejecutan desde el código fuente**, ya sea:

  - En el IDE (ej. IntelliJ IDEA)

---

#### 🔐 Manejo de configuración sensible

- No se usan variables de entorno (`.env`)
- No se activa ningún perfil (`SPRING_PROFILES_ACTIVE`)
- Cada microservicio accede localmente a sus archivos de configuración:

  - `application-secret.yml` (API Key de OpenAI)
  - `email-credentials.yml` (Credenciales para envío de correos)
  - `shared-config/` (Conexión a base de datos)

  ### Si no posee alguno pedirlos para ejecutar, ya que no se versionan.

---

#### 🧪 Verificación

Una vez levantados Redis, Kafka y Zookeeper:

1. Ejecutá los servicios desde el IDE (recomanderdado)
2. Accedé a:

   - **Eureka**: [http://localhost:8761](http://localhost:8761)
   - **Gateway**: [http://localhost:8080](http://localhost:8080)

---

### Opción 3: ⚙️ Entorno de Preproducción (Imágenes locales + variables + perfil docker)

Este entorno simula un despliegue más cercano a producción, pero **construyendo las imágenes localmente**. Se usa para validar el correcto funcionamiento **antes de publicar las imágenes a Docker Hub**.

---

#### ▶️ Comando

```bash
docker-compose -f docker-compose.yml up --build
```

---

#### 🔧 Características

- **Crea imágenes localmente** usando los `Dockerfile` de cada microservicio
- Usa variables de entorno definidas en el archivo `.env`:

  - `JWT_SECRET`, `OPENAI_API_KEY`, `SENDGRID_API_KEY`, etc.

- Usa `SPRING_PROFILES_ACTIVE=docker` en cada servicio
- Las bases de datos están contenerizadas, quiere decir que NO usara pgAdmin 4 para este paso:
  - `postgres-auth`, `postgres-questions`, `postgres-ia`

---

#### 📂 Estructura contenerizada

- 🔁 Servicios de infraestructura:

  - Kafka
  - Zookeeper
  - Redis

- 🛢️ Bases de datos:

  - PostgreSQL para cada microservicio

- 📦 Servicios:

  - Eureka Server
  - API Gateway
  - Microservicios: auth-service, question-service, ia-service, email-service

---

#### 🧪 Verificación (IMPORTANTE)

1. Asegurate de tener `.env` con todas las variables necesarias configuradas.
2. Ejecutá el comando anterior.
3. Verificá los accesos:

   - Eureka: [http://localhost:8761](http://localhost:8761)
   - Gateway: [http://localhost:8080](http://localhost:8080)

---

### 🚨 Importante

Este entorno **sí requiere**:

- Variables de entorno (`.env`) (para respaldo de configuracion de variables de entorno)
- Archivos sensibles (`application-secret.yml`, `email-credentials.yml`) presentes **dentro de cada contenedor** o montados en la build

---

## 🚢 Opción 4: Producción con Imágenes desde Docker Hub

Esta opción representa el **despliegue en producción real**, utilizando las **imágenes ya construidas y publicadas** en una cuenta de Docker Hub.

---

### ▶️ Comando

```bash
docker-compose -f docker-compose.prod.yml up -d
```

---

### 📦 ¿Qué hace esta opción?

- No compila ni construye nada localmente.
- Descarga y ejecuta las imágenes Docker desde Docker Hub, específicamente:

  - `bulan506/authentication-service`
  - `bulan506/email-service`
  - `bulan506/eureka`
  - `bulan506/gateway`
  - `bulan506/ia-service`
  - `bulan506/question-service`

- Utiliza los secretos definidos en el archivo `.env`.
- Levanta todos los servicios necesarios para producción:

  - Kafka, Zookeeper, Redis
  - PostgreSQL para cada microservicio (autocontenidas)
  - Eureka, Gateway y microservicios

---

### 📁 Requisitos previos

- El archivo `.env` debe existir y contener:

  ```env
  JWT_SECRET=...
  GATEWAY_JWT_SECRET=...
  OPENAI_API_KEY=...
  SENDGRID_API_KEY=...
  POSTGRES_PASSWORD=vacalola
  ```

- Las imágenes deben haber sido previamente **construidas y pusheadas** con el pipeline de GitHub Actions o manualmente usando (esto lo hace ya el job de GitHub Action explicado en el siguiente paso):

  ```bash
  docker build -t bulan506/gateway:1.0 .
  docker push bulan506/gateway:1.0
  ```

- Las credenciales de Docker Hub ya estaban configuradas previamente en el repositorio.
  ```bash
   DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
   DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
  ```

---

### 🧪 Verificación post-despliegue

- **Eureka Dashboard:** [http://localhost:8761](http://localhost:8761)
- **Gateway API:** [http://localhost:8080](http://localhost:8080)

---

### 📌 Cuándo usar esta opción

- Para **ambientes de producción reales o staging controlado**
- Cuando ya validaste que las imágenes funcionan en preproducción

---

### 🧯 Rollback en producción

Si algo falla:

1. Parar los servicios:

   ```bash
   docker-compose -f docker-compose.prod.yml down
   ```

---

## 🤖 3. Automatización con GitHub Actions

### 📄 Archivo: `.github/workflows/ci-cd.yml`

Este archivo define un **pipeline CI/CD automático** que se ejecuta cada vez que se hace un `push` o `pull request` a la rama `main`.

---

### 🚦 Activación del Pipeline

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```

Esto asegura que el pipeline se active en dos escenarios:

- Cuando se hace un `push` directo a `main`
- Cuando se abre un `pull request` apuntando a `main`

---

### 🛠️ Job 1: `test-and-build`

Este job realiza **compilación y pruebas automáticas** para los microservicios definidos.

```yaml
strategy:
  matrix:
    service: [ia-service, question-service]
```

✅ Se usa una **matriz** para que este job se ejecute **una vez por cada servicio** listado (en este caso: `ia-service` y `question-service`).

#### 🔍 Pasos del job:

1. **Clona el código** del repositorio
2. **Configura Java 21** usando Temurin
3. Da permiso de ejecución al `gradlew` dentro de cada servicio
4. **Ejecuta los tests** con `./gradlew test`

Este job se asegura de que **cada servicio pase sus pruebas unitarias antes de crear imágenes**.

---

### 🐳 Job 2: `docker-build-and-push`

Este job solo se ejecuta **si el anterior (`test-and-build`) fue exitoso**. Se encarga de construir las imágenes y subirlas a Docker Hub.

```yaml
needs: test-and-build
```

#### 🔐 Requiere secretos configurados en el repositorio:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

#### 🔍 Pasos del job:

1. **Clona el código** del repositorio nuevamente
2. **Prepara Docker Buildx** para construir imágenes multiplataforma
3. **Hace login a Docker Hub**
4. **Itera sobre todos los servicios** y para cada uno:

   - Construye dos versiones de la imagen:

     - `:latest`
     - `:1.0` (versión definida en el script)

   - **Sube ambas imágenes** a Docker Hub

```bash
docker build -t usuario/servicio:latest -t usuario/servicio:1.0 ./servicio
docker push usuario/servicio:latest
docker push usuario/servicio:1.0
```

---

### 🐳 Etiquetas utilizadas en Docker Hub

- `:latest` → última versión disponible (útil para pruebas o entorno de staging)
- `:1.0` → versión fija que representa un release estable y reproducible

---

### ✅ Resultado final del pipeline

Al finalizar correctamente el pipeline:

1. Todos los servicios (`question-service`, `ia-service`) estarán **testeados**.
2. Sus respectivas imágenes estarán **construidas y publicadas** en Docker Hub bajo dos tags (`latest` y `1.0`).
3. Listas para ser usadas en el entorno de producción con `docker-compose.prod.yml`.

---

## 🧪 4. Post-Despliegue y Monitoreo

### ✅ Validaciones Post-Despliegue

- Verificar que Eureka muestre todos los servicios como UP.
- Probar endpoints del gateway.

### 🔎 Revisión de logs

Cada servicio muestra logs por consola:

```bash
docker logs <nombre_servicio> -f
```

---

### ⚠️ Rollback (Reversión)

Si un despliegue local falla:

1. Detener los servicios:

```bash
docker-compose -f docker-compose.prod.yml down
```

2. Volver a la imagen anterior (ej. :1.0):

```bash
docker run bulan506/gateway:1.0
```

---

## 📦 Archivos clave del proyecto

| Archivo                     | Descripción                           |
| --------------------------- | ------------------------------------- |
| .env                        | Variables de entorno sensibles        |
| compose-base.yml            | Servicios comunes (Kafka, Redis)      |
| docker-compose.yml          | Despliegue local (Simulacion)         |
| docker-compose.prod.yml     | Despliegue con imágenes en producción |
| run-all.sh                  | Arranque local con bootRun            |
| .github/workflows/ci-cd.yml | Pipeline de CI/CD                     |

---

## Notas Finales

- application-secret.yml, email-credentials.yml y otros **no deben subirse a Git**.

---
