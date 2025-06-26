# Guía de Estilo de Código para la Base de Datos - Versión Actualizada

## 1. Estándares de Nombramiento

### 1.1 Convenciones para Nombres de Tablas
* **Singular** para entidades (ej: `user`, `quiz`, `question`)
* Formato **snake_case**
* Prohibido abreviaturas ambiguas
* **Excepciones documentadas**: Tablas de unión mantienen nombres compuestos (ej: `quiz_question`)

### 1.2 Convenciones para Identificadores
#### Claves Primarias (PK):
* **Tipo**: UUID (versión 4 o 7 según requisitos)
* **Nombre de columna**: 
  - `id` para tablas principales (ej: `user.id`)
  - `id_<tabla>` para tablas de unión (ej: `quiz_question.id_quiz`)

#### Claves Foráneas (FK):
* **Estructura**: `<tabla_referenciada>_id` (con tipo UUID)
* **Correcciones identificadas**:
  - `created_by` → `user_id`
  - `id_user` → `user_id`
  - `id_question` → `question_id`

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
| Columna          | Tipo Recomendado       | Ejemplo Real              |
|------------------|------------------------|---------------------------|
| Identificadores  | UUID                   | `id UUID PRIMARY KEY`     |
| Fechas          | TIMESTAMPTZ           | `created_at TIMESTAMPTZ`  |
| Imágenes/URLs   | TEXT                  | `profile_image TEXT`      |
| Estados         | VARCHAR(20)           | `status VARCHAR(20)`      |

### 2.2 Casos Especiales Documentados
* **Auth Service**: Mantiene `id_user` por legado (requiere migración planificada)
* **AI Service**: Usa `double precision[]` para embeddings

## 3. Convenciones para Relaciones

### 3.1 Relaciones Many-to-Many
* **Nomenclatura**: `<tabla1>_<tabla2>`
* **Claves**: Usar compuesto de ambas FK como PK
```sql
CREATE TABLE question_category (
    question_id UUID REFERENCES question(id),
    category_id INT REFERENCES category(id),
    PRIMARY KEY (question_id, category_id)
);
```

### 3.2 Políticas de Integridad
* **ON DELETE**: 
  - `CASCADE` para dependencias fuertes (ej: respuestas→preguntas)
  - `RESTRICT` para datos maestros (ej: categorías→preguntas)

## 4. Guía de Migración para Inconsistencias

### 4.1 Cambios Prioritarios
1. **Normalización de PKs**:
   ```sql
   ALTER TABLE auth.users RENAME COLUMN id_user TO id;
   ```

2. **Estandarización de FKs**:
   ```sql
   ALTER TABLE quiz RENAME COLUMN created_by TO user_id;
   ```

### 4.2 Plan de Transición
| Tabla          | Cambio Requerido                  | Prioridad |
|----------------|-----------------------------------|-----------|
| quiz          | `created_by` → `user_id`         | Alta      |
| question      | `created_by` → `user_id`         | Alta      |
| auth.users    | `id_user` → `id`                 | Media     |

## 5. Documentación de Excepciones

### 5.1 Excepciones Aprobadas
1. **Auth Service**:
   - Mantiene temporalmente `id_user` por dependencias externas
   - Plan de migración a implementar en Q3 2025

2. **AI Service**:
   - Usa `category_embedding` con array de precisión doble
   - Requiere extensión PostgreSQL `vector`

### 5.2 Plantilla para Nuevas Excepciones
```markdown
**Tabla**: [nombre_tabla]  
**Razón**: [justificación técnica/business]  
**Periodo**: [fecha_inicio] - [fecha_fin_estimada]  
**Owner**: [team/responsable]  
```

## 6. Ejemplo Completo con UUID v7
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

## 7. Checklist de Implementación
- [ ] Todos los IDs son UUID
- [ ] Nombres de tablas en singular
- [ ] FKs siguen formato `<tabla>_id`
- [ ] Tablas de unión usan PK compuesta
- [ ] Excepciones documentadas
- [ ] Tipos de datos alineados con dominio