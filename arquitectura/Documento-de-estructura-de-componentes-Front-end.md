## Documento de Estructura de Componentes - Frontend
### Introducción
Este documento describe la estructura y organización de los componentes dentro del proyecto frontend de la Plataforma Social de Aprendizaje. Su objetivo es establecer un estándar para la creación, organización y uso de los componentes en la aplicación.

### Organización del proyecto
#### Tipos de componentes:


**Componentes de presentación (UI Components)**:
- Son reutilizables y se centran en la representación visual.
- No contienen lógica de negocio ni llamadas a API.
- Ejemplos: Botones, tarjetas, modales, listas.

    Ubicación: /src/components/

**Componentes Contenedores (Container Components)**:
- Gestionan el estado y la lógica de negocio.
- Se comunican con los servicios y hooks.
- Contienen componentes de presentación.

    Ubicación: /src/containers/

**Páginas (Pages)**:
- Representan las vistas principales de la aplicación.
- Componen la estructura de la navegación.
- Pueden contener múltiples contenedores y componentes.

    Ubicación: /src/pages/

#### Organización de archivos y carpetas

    /src
    ├── /assets         # Recursos estáticos (imágenes, fuentes)
    ├── /components     # Componentes reutilizables de UI
    ├── /containers     # Componentes con lógica de negocio
    ├── /pages          # Vistas principales
    ├── /services       # Llamadas a API y lógica de negocio
    ├── /hooks          # Hooks personalizados
    ├── /models         # Definición de tipos y modelos
    ├── /context        # Manejo de estado global
    ├── /routes         # Configuración de rutas


#### Comunicación entre componentes
**Props y Estado**:
- Props para pasar datos de padres a hijos.
- Estado local (useState) cuando sea necesario.
- Context API o Zustand para estado global.

#### Buenas prácticas
- Usar TypeScript para tipado seguro.
- Separar UI y lógica de negocio.
- Seguir la estructura de carpetas definida.
- Reutilizar componentes y hooks.
- Manejar errores y estado de carga correctamente.