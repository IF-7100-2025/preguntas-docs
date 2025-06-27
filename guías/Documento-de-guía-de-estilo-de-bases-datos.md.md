

# Guía de Estilo de Código para la Base de Datos - Versión Actualizada

## 1. Estándares de Nombramiento

### 1.1 Convenciones para Nombres de Tablas

* **Singular** para entidades (ej: `user`, `quiz`, `question`)
* Formato **snake\_case**
* Prohibido abreviaturas ambiguas
* **Excepciones documentadas**: Tablas de unión mantienen nombres compuestos (ej: `quiz_question`)

### 1.2 Convenciones para Identificadores

#### Claves Primarias (PK):

* **Tipo**: UUID (versión 4 o 7 según requisitos)
* **Nombre de columna**:

  * `id` para tablas principales (ej: `user.id`)
  * `id_<tabla>` para tablas de unión (ej: `quiz_question.id_quiz`)

#### Claves Foráneas (FK):

* **Estructura**: `<tabla_referenciada>_id` (con tipo UUID)
* **Correcciones identificadas**:

  * `created_by` → `user_id`
  * `id_user` → `user_id`
  * `id_question` → `question_id`

### 1.3 Ejemplo de Implementación Correcta

```sql
-- Tabla principal
CREATE TABLE user (
    id UUID DEFAULT uuid_generate_v4() PRIMARY KEY,
    username VARCHAR(50) NOT NULL
);

-- Tabla de unión
CREATE TABLE quiz_question (
    id_quiz UUID REFERENCES quiz(id),
    id_question UUID REFERENCES question(id),
    PRIMARY KEY (id_quiz, id_question)
);
```

## 2. Estándares de Tipos de Datos

### 2.1 Tipos Específicos por Dominio

| Columna         | Tipo Recomendado | Ejemplo Real             |
| --------------- | ---------------- | ------------------------ |
| Identificadores | UUID             | `id UUID PRIMARY KEY`    |
| Fechas          | TIMESTAMPTZ      | `created_at TIMESTAMPTZ` |
| Imágenes/URLs   | TEXT             | `profile_image TEXT`     |
| Estados         | VARCHAR(20)      | `status VARCHAR(20)`     |

### 2.2 Casos Especiales Documentados

* **Auth Service**: Mantiene `id_user` por legado (requiere migración planificada)
* **AI Service**: Usa `double precision[]` para embeddings


## 3. Creación de Scripts con Liquibase

Se utilizará **Liquibase con archivos `.yml`** para la gestión de cambios en el esquema de la base de datos. Esto permite un control de versiones estructurado, seguro y fácilmente reversible.

### 3.1 Directrices para la Estructuración de Scripts de Migración

* Cada cambio en el esquema de la base de datos se define en un archivo **YAML (`.yml`)** llamado **changelog**.

* Los archivos deben organizarse por **funcionalidad o versión**, en una estructura clara.

  **Ejemplo de estructura de directorios:**

  ```
  liquibase/
  ├── changelog-master.yml
  ├── 20230601_crear_tabla_user.yml
  ├── 20230601_crear_tabla_question.yml
  └── features/
      └── 20230605_agregar_columna_status_question.yml
  ```

* El nombre de cada archivo debe incluir una **marca de tiempo** y una **descripción clara** del cambio.

### 3.2 Uso de Convenciones en `changelogs` y `changesets`

* El archivo `changelog-master.yml` actuará como el **punto de entrada** e incluirá los demás archivos con la instrucción `include`.

  **Ejemplo de `changelog-master.yml`:**

  ```yaml
  databaseChangeLog:
    - include:
        file: 20230601_crear_tabla_user.yml
    - include:
        file: 20230601_crear_tabla_question.yml
    - include:
        file: features/20230605_agregar_columna_status_question.yml
  ```

* Cada archivo `.yml` debe contener al menos un bloque `changeSet` con:

  * `id`: identificador único del cambio
  * `author`: nombre del autor del cambio
  * `changes`: lista de operaciones realizadas
  * `comment`: (opcional) descripción del propósito del cambio

  **Ejemplo de archivo `.yml` para crear tabla:**

  ```yaml
  databaseChangeLog:
    - changeSet:
        id: crear-tabla-usuarios
        author: tu_nombre
        comment: Crea la tabla de usuarios con sus columnas iniciales.
        changes:
          - createTable:
              tableName: user
              columns:
                - column:
                    name: id
                    type: UUID
                    constraints:
                      primaryKey: true
                      nullable: false
                - column:
                    name: username
                    type: VARCHAR(50)
                    constraints:
                      nullable: false
                - column:
                    name: email
                    type: VARCHAR(100)
                    constraints:
                      nullable: false
                      unique: true
                - column:
                    name: created_at
                    type: TIMESTAMPTZ
                    defaultValueComputed: CURRENT_TIMESTAMP
  ```

### 3.3 Mejores Prácticas para Rollback y Control de Versiones

* Cada `changeSet` debe incluir una sección `rollback` para revertir el cambio si es necesario.

  **Ejemplo con rollback:**

  ```yaml
  databaseChangeLog:
    - changeSet:
        id: agregar-columna-avatar
        author: tu_nombre
        comment: Agrega la columna avatar_url a la tabla user.
        changes:
          - addColumn:
              tableName: user
              columns:
                - column:
                    name: avatar_url
                    type: VARCHAR(255)
        rollback:
          - dropColumn:
              tableName: user
              columnName: avatar_url
  ```

* Los archivos `.yml` deben almacenarse en un sistema de control de versiones (como **Git**).

* Todos los cambios deben pasar por **revisión de código**, especialmente si afectan entornos productivos.

* Ejecutar migraciones en entornos de staging antes de aplicarlas en producción.


## 4. Convenciones para Relaciones

### 4.1 Relaciones Many-to-Many

* **Nomenclatura**: `<tabla1>_<tabla2>`
* **PK compuesta** con ambas FK

```sql
CREATE TABLE question_category (
    question_id UUID REFERENCES question(id),
    category_id INT REFERENCES category(id),
    PRIMARY KEY (question_id, category_id)
);
```

### 4.2 Políticas de Integridad

* **ON DELETE**:

  * `CASCADE`: Relaciones fuertes (e.g., respuestas → preguntas)
  * `RESTRICT`: Datos maestros (e.g., categorías → preguntas)

## 5. Guía de Migración para Inconsistencias

### 5.1 Cambios Prioritarios

```sql
-- Renombrar claves primarias
ALTER TABLE auth.users RENAME COLUMN id_user TO id;

-- Renombrar claves foráneas
ALTER TABLE quiz RENAME COLUMN created_by TO user_id;
```

### 5.2 Plan de Transición

| Tabla      | Cambio Requerido         | Prioridad |
| ---------- | ------------------------ | --------- |
| quiz       | `created_by` → `user_id` | Alta      |
| question   | `created_by` → `user_id` | Alta      |
| auth.users | `id_user` → `id`         | Media     |

## 6. Documentación de Excepciones

### 6.1 Excepciones Aprobadas

1. **Auth Service**:

   * Conserva `id_user` por dependencias externas
   * Migración programada para Q3 2025

2. **AI Service**:

   * Usa `category_embedding` (array `double precision`)
   * Requiere extensión PostgreSQL `vector`

### 6.2 Plantilla para Nuevas Excepciones

```markdown
**Tabla**: [nombre_tabla]  
**Razón**: [justificación técnica/business]  
**Periodo**: [fecha_inicio] - [fecha_fin_estimada]  
**Owner**: [team/responsable]  
```

## 7. Ejemplo Completo con UUID v7

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

CREATE TABLE question (
    id UUID DEFAULT uuid_generate_v7() PRIMARY KEY,
    text TEXT NOT NULL,
    user_id UUID NOT NULL REFERENCES user(id),
    created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE quiz_question (
    id_quiz UUID REFERENCES quiz(id),
    id_question UUID REFERENCES question(id),
    position INT,
    PRIMARY KEY (id_quiz, id_question)
);
```

## 8. Checklist de Implementación

* [ ] Todos los IDs son UUID
* [ ] Nombres de tablas en singular
* [ ] FKs siguen formato `<tabla>_id`
* [ ] Tablas de unión usan PK compuesta
* [ ] Excepciones documentadas
* [ ] Tipos de datos alineados con dominio
* [ ] Cambios gestionados con Liquibase
* [ ] Rollbacks definidos en todos los changesets

---
