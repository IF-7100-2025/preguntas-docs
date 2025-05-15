**Sede del Atlántico**
**Recinto de Paraíso**
**IF-7100 Ingeniería de Software**
**Laboratorio: ADR y Fitness function**
**Profesor MSc. Leonardo Camacho Navarro**

**Plataforma de aprendizaje grupo: _Conti_**

---

## Práctica: ADR y Fitness Functions en el Proyecto Final

---

### ✳️ Características arquitectónicas seleccionadas:

1. **Usabilidad**
2. **Seguridad**
3. **Responsividad**

---

## 📄 ADR-001: Uso de componentes UI consistentes y accesibles

**Estado:** Aprobado

### Contexto

La experiencia del usuario es esencial para que el sistema sea fácil de entender y usar. Los usuarios deben poder navegar sin necesidad de capacitación, especialmente en interfaces orientadas a tareas frecuentes como registro, búsqueda y gestión de contenido.

### Decisión

Se decidió usar una biblioteca de componentes UI como **Ant Design** con principios de diseño accesible (alto contraste, tabulación, íconos descriptivos, etc.) y diseño intuitivo.

### Alternativas consideradas

- Material UI: elegante, pero con curva de aprendizaje mayor.
- Bootstrap: útil, pero menos moderno visualmente.
- UI personalizada: muy flexible, pero requiere más tiempo de desarrollo.

### Consecuencias

✅ Mejora la experiencia de usuario desde el primer uso.
✅ Aumenta la accesibilidad para personas con limitaciones visuales o motoras.
❌ Dependencia de una biblioteca externa.

### Fecha

13/05/2025

---

## 📄 ADR-002: Autenticación mediante tokens JWT con verificación de rol

**Estado:** Aprobado

### Contexto

Es necesario proteger los recursos del sistema mediante control de acceso por roles. Se requiere que solo usuarios autenticados y autorizados accedan a recursos sensibles.

### Decisión

Se implementará autenticación mediante **JWT** (JSON Web Tokens), donde cada solicitud incluirá un token que será verificado por el backend para validar la identidad del usuario y sus permisos.

### Alternativas consideradas

- Autenticación basada en sesiones: no escalable y requiere mantener estado.
- OAuth2: más robusto, pero complejo para el alcance actual del proyecto.

### Consecuencias

✅ Mejora la seguridad y escalabilidad del sistema.
✅ Permite integración con microservicios sin compartir sesión.
❌ Es necesario proteger adecuadamente el almacenamiento del token en el cliente.

### Fecha

13/05/2025

---

## 📄 ADR-003: Diseño responsivo adaptable a múltiples dispositivos

**Estado:** Aprobado

### Contexto

Los usuarios acceden desde diferentes dispositivos (PC, móviles). Se necesita que la interfaz se adapte a distintas resoluciones para mantener la funcionalidad y legibilidad.

### Decisión

Se adoptó una estrategia de diseño **responsivo** usando unidades relativas (%, rem), media queries de CSS y un sistema de grillas para adaptar la vista a diferentes tamaños de pantalla.

### Alternativas consideradas

- Aplicación separada para móviles: costosa y difícil de mantener.
- Interfaz fija: sencilla, pero inadecuada para usuarios móviles.

### Consecuencias

✅ Mejor experiencia móvil.
✅ Aumento en la cobertura de usuarios.
❌ Necesidad de validar visualmente múltiples dispositivos.

### Fecha

13/05/2025

---

## ✅ Fitness Function 1: Test de tareas clave por usuarios

### Característica arquitectónica:

**Usabilidad**

### Propósito:

Evaluar si los usuarios pueden completar las tareas principales del sistema sin ayuda externa.

### Criterio de éxito:

Al menos el **85% de los usuarios** debe completar las tareas sin asistencia en un entorno de prueba.

### Método de validación:

Pruebas de usabilidad con 5 usuarios. Se mide si pueden registrarse, iniciar sesión, y realizar una acción clave (ej: enviar reporte) sin intervención.

### Frecuencia de ejecución:

Cada iteración importante del frontend (al menos cada sprint).

---

## ✅ Fitness Function 2: Pruebas de acceso no autorizado

### Característica arquitectónica:

**Seguridad**

### Propósito:

Garantizar que los endpoints protegidos rechacen accesos sin autorización o con permisos incorrectos.

### Criterio de éxito:

**100% de los endpoints protegidos** deben rechazar accesos indebidos durante las pruebas automatizadas.

### Método de validación:

Test automatizados con Postman o Jest enviando tokens inválidos, sin token o de otro rol.

### Frecuencia de ejecución:

En cada commit al repositorio principal (pipeline de integración continua).

---

## ✅ Fitness Function 3: Adaptabilidad de interfaz en distintos dispositivos

### Característica arquitectónica:

**Responsividad**

### Propósito:

Verificar que la interfaz se vea correctamente en distintos tamaños de pantalla (móvil, tablet, escritorio).

### Criterio de éxito:

Todos los componentes deben mantener legibilidad, alineación y funcionalidad en al menos **tres tamaños de pantalla**: 360px, 768px y 1280px.

### Método de validación:

Pruebas visuales con herramientas como Chrome DevTools (modo responsivo) o Lighthouse.

### Frecuencia de ejecución:

En cada despliegue del frontend y antes de entregas de proyecto.
