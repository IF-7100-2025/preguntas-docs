# Guía de Estilo de Código para la Base de Datos

Este documento define los estándares y convenciones a seguir para el diseño y desarrollo de la base de datos de la Plataforma Social de Aprendizaje. El objetivo es asegurar la consistencia, legibilidad y mantenibilidad del esquema de la base de datos y los scripts de migración.

## 1. Estándares de Nombramiento

La consistencia en los nombres facilita la comprensión y el mantenimiento de la base de datos. Se seguirán las siguientes convenciones:

### Convenciones para Nombres de Tablas

* Se utilizará el **plural** de la entidad representada.
* Se utilizará el formato **snake\_case** (palabras en minúsculas separadas por guiones bajos).
* Se evitarán abreviaturas ambiguas.

    **Ejemplos:**
    * `usuarios` en lugar de `usuario` o `tblUsuarios`
    * `preguntas` en lugar de `pregunta` o `tblPreguntas`
    * `categorias_pregunta` en lugar de `categoria_pregunta` o `tblCategoriasPregunta`

### Convenciones para Nombres de Columnas

* Se utilizará el **singular** de la propiedad representada.
* Se utilizará el formato **snake\_case**.
* Se utilizarán nombres **descriptivos y concisos**.
* Se evitarán abreviaturas ambiguas.
* Para las **claves foráneas**, se utilizará el nombre de la tabla referenciada seguido de `_id`.

    **Ejemplos:**
    * En la tabla `usuarios`: `id`, `nombre`, `apellido`, `email`, `fecha_registro`
    * En la tabla `preguntas`: `id`, `titulo`, `contenido`, `usuario_id`, `categoria_id`, `fecha_creacion`
    * En la tabla `respuestas`: `id`, `contenido`, `pregunta_id`, `usuario_id`, `fecha_creacion`

### Convenciones para Nombres de Vistas

* Se utilizará un prefijo `vw_` seguido de un nombre descriptivo.
* Se utilizará el formato **snake\_case**.

    **Ejemplos:**
    * `vw_preguntas_con_respuestas`
    * `vw_usuarios_con_calificaciones_promedio`

### Reglas para la Nomenclatura de Claves Primarias (PK)

* El nombre de la columna para la clave primaria será siempre `id`.
* El nombre de la restricción de clave primaria será `PK_<nombre_de_la_tabla>`.

    **Ejemplos:**
    * Para la tabla `usuarios`: Columna `id`, Restricción `PK_usuarios`
    * Para la tabla `preguntas`: Columna `id`, Restricción `PK_preguntas`

### Reglas para la Nomenclatura de Claves Foráneas (FK)

* El nombre de la columna será el nombre de la tabla referenciada seguido de `_id`.
* El nombre de la restricción de clave foránea será `FK_<nombre_de_la_tabla_actual>_<nombre_de_la_tabla_referenciada>`.

    **Ejemplos:**
    * En la tabla `preguntas` referenciando a la tabla `usuarios`: Columna `usuario_id`, Restricción `FK_preguntas_usuarios`
    * En la tabla `respuestas` referenciando a la tabla `preguntas`: Columna `pregunta_id`, Restricción `FK_respuestas_preguntas`

## 2. Guías para Declaraciones de Claves

La correcta definición de claves es fundamental para la integridad y el rendimiento de la base de datos.

### 2.1. Definición y Uso Adecuado de Claves Primarias (PK)

* Cada tabla debe tener una **clave primaria** para identificar de forma única cada registro.
* La clave primaria debe ser un **identificador único, estable y no nulo**.
* Se recomienda utilizar **identificadores enteros autoincrementales** como clave primaria.

    **Ejemplo (SQL):**

    ```sql
    CREATE TABLE usuarios (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nombre VARCHAR(255) NOT NULL,
        apellido VARCHAR(255) NOT NULL,
        email VARCHAR(255) UNIQUE NOT NULL,
        fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        CONSTRAINT PK_usuarios PRIMARY KEY (id)
    );
    ```

### 2.2. Reglas para la Declaración de Claves Foráneas (FK)

* Las **claves foráneas** se utilizarán para establecer relaciones entre tablas.
* Deben **referenciar la clave primaria** de la tabla padre.
* Es importante definir el **comportamiento de las claves foráneas** al eliminar o actualizar registros en la tabla padre (`ON DELETE`, `ON UPDATE`). Las opciones comunes son:
    * **CASCADE:** Propaga la operación (eliminar o actualizar) a la tabla hija.
    * **SET NULL:** Establece el valor de la clave foránea a `NULL` en la tabla hija. Requiere que la columna permita valores nulos.
    * **RESTRICT o NO ACTION:** Impide la operación en la tabla padre si existen registros relacionados en la tabla hija.
* Se recomienda **indexar las columnas de las claves foráneas** para mejorar el rendimiento de las consultas.

    **Ejemplo (SQL):**

    ```sql
    CREATE TABLE preguntas (
        id INT AUTO_INCREMENT PRIMARY KEY,
        titulo VARCHAR(255) NOT NULL,
        contenido TEXT,
        usuario_id INT NOT NULL,
        categoria_id INT NOT NULL,
        fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        CONSTRAINT PK_preguntas PRIMARY KEY (id),
        FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE,
        CONSTRAINT FK_preguntas_usuarios FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE,
        FOREIGN KEY (categoria_id) REFERENCES categorias_pregunta(id) ON DELETE RESTRICT,
        CONSTRAINT FK_preguntas_categorias_pregunta FOREIGN KEY (categoria_id) REFERENCES categorias_pregunta(id) ON DELETE RESTRICT
    );
    ```

### 2.3. Convenciones para la Definición de Claves Únicas (UK)

* Las **claves únicas** se utilizan para asegurar que los valores en una o más columnas sean únicos en una tabla.
* Se utilizará el nombre de la restricción `UK_<nombre_de_la_tabla>_<nombre_de_la_columna(s)>`.

    **Ejemplos:**

    * En la tabla `usuarios`, para asegurar que cada correo electrónico sea único:
        ```sql
        ALTER TABLE usuarios ADD CONSTRAINT UK_usuarios_email UNIQUE (email);
        ```
    * Si una combinación de columnas debe ser única:
        ```sql
        ALTER TABLE calificaciones_pregunta ADD CONSTRAINT UK_calificaciones_pregunta_usuario_pregunta UNIQUE (usuario_id, pregunta_id);
        ```

## 3. Creación de Scripts con Liquibase

Se utilizará Liquibase para la gestión de los cambios en el esquema de la base de datos. Esto permite un control de versiones eficiente y facilita la implementación y el rollback de los cambios.

### 3.1. Directrices para la Estructuración de Scripts de Migración

* Cada cambio en el esquema de la base de datos se realizará a través de un **archivo de migración (changelog)**.
* Los archivos de migración deben organizarse por **funcionalidad o release**. Se recomienda una estructura de directorios clara.

    **Ejemplo de estructura de directorios:**

    ```
    liquibase/
    ├── changelog-master.xml
    ├── 202303271000_crear_tabla_usuarios.xml
    ├── 202303271015_crear_tabla_preguntas.xml
    └── features/
        └── 202304051430_agregar_columna_descripcion_pregunta.xml
    ```

* Los nombres de los archivos de migración deben ser **descriptivos** e incluir una **marca de tiempo** para asegurar el orden de ejecución.

### 3.2. Uso de Convenciones en `changelogs` y `changesets`

* El archivo `changelog-master.xml` actuará como el **punto de entrada** y contendrá las referencias a todos los demás archivos de migración.
* Cada cambio específico se definirá dentro de un `<changeset>` en un archivo de migración.
* Cada `<changeset>` debe tener un **id único** y un **author**. Se recomienda utilizar un formato consistente para los IDs.
* Se incluirán **comentarios descriptivos** dentro de los `<changeset>` para explicar el propósito del cambio.

    **Ejemplo de changeset:**

    ```xml
    <changeSet id="crear-tabla-usuarios" author="tu_nombre">
        <comment>Crea la tabla de usuarios con sus columnas iniciales.</comment>
        <createTable tableName="usuarios">
            <column name="id" type="INT" autoIncrement="true">
                <constraints primaryKey="true" nullable="false" primaryKeyName="PK_usuarios"/>
            </column>
            <column name="nombre" type="VARCHAR(255)">
                <constraints nullable="false"/>
            </column>
            <column name="apellido" type="VARCHAR(255)">
                <constraints nullable="false"/>
            </column>
            <column name="email" type="VARCHAR(255)">
                <constraints nullable="false" unique="true" uniqueConstraintName="UK_usuarios_email"/>
            </column>
            <column name="fecha_registro" type="TIMESTAMP" defaultValueComputed="CURRENT_TIMESTAMP"/>
        </createTable>
    </changeSet>
    ```

### 3.3. Mejores Prácticas para Versionado y Rollback de Cambios

* Cada `<changeset>` debe incluir un `<rollback>` para **deshacer los cambios** realizados. Esto es crucial para poder revertir migraciones en caso de errores.
* Los scripts de **rollback deben ser probados** para asegurar su correcto funcionamiento.
* Se utilizará un **sistema de control de versiones (como Git)** para gestionar los archivos de migración.
* Antes de aplicar cualquier cambio en un entorno de producción, se realizará una **revisión exhaustiva** de los scripts de migración.

    **Ejemplo de changeset con rollback:**

    ```xml
    <changeSet id="agregar-columna-avatar-usuarios" author="tu_nombre">
        <comment>Agrega la columna avatar a la tabla de usuarios.</comment>
        <addColumn tableName="usuarios">
            <column name="avatar_url" type="VARCHAR(255)"/>
        </addColumn>
        <rollback>
            <dropColumn tableName="usuarios" columnName="avatar_url"/>
        </rollback>
    </changeSet>
    ```