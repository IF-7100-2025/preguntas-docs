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
git clone https://github.com/IF-7100-2025/preguntas-backend.git
cd preguntas-backend
```

## Dos opciones para lanzar el proyecto

Aquí se explica que puedes elegir entre:

1. **Usar IntelliJ IDEA (IDE gráfico)**:

   - Abres el proyecto en IntelliJ
   - Ejecutas cada módulo (Eureka y Gateway) directamente desde el IDE
   - Ideal para desarrollo/debugging

2. **Usar terminal/comandos**:
   - Ejecutas los servicios manualmente mediante comandos Gradle
   - Necesitas una terminal para cada servicio
   - Más directo pero menos visual

Ambos métodos son válidos y producen el mismo resultado final.

#### Terminal 1: Servidor Eureka (Dashboard de servicios)

```bash
cd eureka/
./gradlew bootRun
```

**Verificación:**  
🔹 Espera hasta ver el mensaje `Started EurekaServerApplication`  
🔹 Accede al dashboard en [http://localhost:8761](http://localhost:8761)

#### Terminal 2: Gateway (Puerta de enlace)

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

| Servicio | URL                                            |
| -------- | ---------------------------------------------- |
| Eureka   | [http://localhost:8761](http://localhost:8761) |
| Gateway  | [http://localhost:8080](http://localhost:8080) |

---

## 📌 Notas adicionales

- ✅ Verifica que tienes **Java** y **Gradle** correctamente instalados
- 🐞 Si encuentras errores:
  - Confirma que cada servicio se registró correctamente en Eureka
  - Revisa los logs de cada servicio para identificar problemas
- ⏱ Los tiempos de inicio pueden variar según tu hardware

---

> **Tip:** Mantén todas las terminales visibles para monitorear fácilmente los logs de cada servicio.
