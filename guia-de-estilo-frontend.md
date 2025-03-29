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
- Los nombres de las interfaces deben comenzar con **I** (por ejemplo, `IUser`).

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
