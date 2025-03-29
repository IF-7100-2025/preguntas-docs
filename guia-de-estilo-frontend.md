### - Principios Fundamentales

#### - Sobrecarga Mental Mínima
El código debe ser fácil de escanear y entender sin requerir comentarios excesivos o cambios frecuentes de contexto. Los desarrolladores deben poder predecir dónde se encuentran las cosas y cómo están estructuradas.

#### - Previsibilidad
Cada archivo y componente sigue una estructura consistente, minimizando la ambigüedad. Las convenciones de nombres, estructuras de carpetas y ubicaciones de funciones deben permanecer consistentes a lo largo de toda la base de código.

#### - Claridad por encima de Flexibilidad
Aunque la flexibilidad puede ser útil, la claridad es prioritaria. El objetivo no es admitir todas las posibles formas de escribir código, sino asegurar que el código sea uniforme y fácil de mantener.

#### - Separación de Responsabilidades
La lógica, la UI y la gestión del estado deben estar correctamente separadas para mejorar el mantenimiento. La lógica de negocio debe vivir en hooks o funciones de utilidad en lugar de en la capa de UI.

### - Convenciones de nomenclatura para archivos y componentes

- Los archivos de componentes deben utilizar **PascalCase** (por ejemplo, `UserCard.tsx`).
- Los hooks personalizados deben comenzar con el prefijo **use** seguido de una descripción clara de su función (por ejemplo, `useFetchData.ts`).
- Las clases que representan modelos de datos deben nombrarse de la siguiente manera: `purchases.models.ts`.
- Tanto las interface como los type deben respetar el formato **PascalCase** (por ejemplo, `interface Event`, `type Response`).
- Los services deben nombrarse de la siguiente manera: `events.service.ts`.

### - Convenciones para la declaración de métodos y variables

**Métodos**:
- Los métodos deben seguir la convención **camelCase** (por ejemplo, `handleClick`).
- Declarar los métodos como funciones flecha, por ejemplo: `const handleClick = () => {}`
- Los métodos deben ser pequeños y centrarse en una única tarea. Los nombres deben ser descriptivos y comenzar con un verbo (por ejemplo, `fetchData`, `handleSubmit`).

**Variables**:
- Las variables deben seguir la convención **camelCase** (por ejemplo, `userData`, `isLoading`).
- Las variables booleanas deben tener un prefijo como **is**, **has**, **can**, indicando un valor verdadero/falso (por ejemplo, `isAuthenticated`, `canEdit`).
- Para constantes que no cambian, usar **UPPER_SNAKE_CASE** (por ejemplo, `API_URL`).

**Funciones**:
- Las funciones deben seguir la convención **camelCase** (por ejemplo, `getUserInfo`).
- Las funciones que se usan dentro de los componentes deben declararse como funciones flecha (arrow functions) para mantener el contexto adecuado del `this`.

### - Separación de responsabilidades en el código
assets/: Contiene recursos estáticos como imágenes, fuentes, íconos y otros archivos multimedia. Esta carpeta se utiliza para almacenar todos los activos visuales o archivos no relacionados directamente con la lógica de la aplicación.

components/: Contiene los componentes reutilizables de la interfaz de usuario (UI), como botones, tarjetas, encabezados, etc. Los componentes deben ser autónomos y centrarse en la presentación de datos sin lógica de negocio compleja.

hooks/: Contiene los hooks personalizados que encapsulan la lógica reutilizable, como la gestión del estado, recuperación de datos o cualquier lógica que no esté directamente relacionada con la UI. Estos hooks permiten reutilizar la lógica en diferentes componentes.

models/: Contiene las definiciones de los modelos de datos y las interfaces que se usan a lo largo de la aplicación. Los archivos en esta carpeta definen los tipos y estructuras de datos que los componentes y servicios utilizarán.

pages/: Contiene los componentes de nivel superior o "páginas". Estos componentes pueden contener múltiples componentes más pequeños y se encargan de representar las vistas completas. Cada página generalmente tiene una ruta específica en la aplicación.

services/: Contiene servicios que interactúan con APIs externas, bases de datos o cualquier otra lógica de negocio fuera del alcance de los componentes y hooks. Estos servicios gestionan las peticiones y respuestas, y están destinados a ser reutilizados en múltiples partes de la aplicación.
## IDEs sugeridos y sus configuraciones óptimas

###  Visual Studio Code (VS Code)

**Visual Studio Code** es el IDE recomendado para el desarrollo frontend debido a su compatibilidad con tecnologías modernas como TypeScript, React, ESLint y Prettier.

###  Configuraciones óptimas del entorno de desarrollo

Para garantizar coherencia y compatibilidad entre los distintos miembros del equipo, se deben cumplir las siguientes configuraciones:

- **Uso de la misma versión de Node.js**  
  Todos los miembros del equipo deben trabajar con la **misma versión de Node.js** para evitar diferencias de comportamiento o errores inesperados.  
  Se recomienda utilizar herramientas como [nvm](https://github.com/nvm-sh/nvm) para gestionar versiones de Node.js fácilmente.

- **Gestor de paquetes consistente**  
 Todos los miembros deben usar el mismo  **npm** para evitar conflictos con los archivos de bloqueo (`package-lock.json` o `yarn.lock`). 

- **Configuración estándar del proyecto**  
  Una vez clonado el repositorio, cada miembro debe ejecutar:
  ```bash
  npm install
  ```

## Plugins esenciales para mejorar la productividad y calidad del código

###  ESLint

Herramienta para análisis de código estático. Detecta errores de estilo, convenciones inconsistentes y posibles bugs.

- Reglas personalizables.
- Integración con VS Code.
- Archivo `.eslintrc` en la raíz del proyecto define el estilo del equipo.

###  Prettier – Code Formatter

Formateador de código automático. Ayuda a mantener una apariencia uniforme en todos los archivos del proyecto.

- Se encarga de cuestiones como comillas, indentación, uso de punto y coma, saltos de línea, etc.
- Archivo `.prettierrc` con configuración personalizada.

## Guía de configuración de ambientes

### Pasos para configurar el entorno local

**Instalar Node.js**  
Asegurarse de que todos los miembros utilicen la misma versión.  
Se recomienda usar nvm para instalarla y gestionarla fácilmente.

**Clonar el repositorio y descargar dependencias**
```bash
git clone [url-del-repo]
cd [carpeta-del-proyecto]
npm install
```

**Instalar ESLint y Prettier (si no están en el proyecto aún)**
```bash
npm install --save-dev eslint prettier
```

**Verificar configuración compartida de VS Code**  
Comprobar que el proyecto incluya el archivo `.vscode/settings.json` y que cada integrante lo tenga habilitado.
