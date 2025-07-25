
# Guía de Estándares de UI

## Introducción
Esta guía define los principios, componentes y patrones de diseño para garantizar coherencia visual y funcional en las interfaces de la aplicación, manteniendo flexibilidad para escalar el sistema.

---

## Principios Fundamentales
1. **Consistencia**: Mantener un diseño uniforme en toda la aplicación.  
2. **Accesibilidad**: Diseñar para todos los usuarios, incluyendo aquellos con discapacidades.  
3. **Simplicidad**: Evitar elementos innecesarios y priorizar la claridad.  
4. **Feedback**: Proveer retroalimentación visual y funcional en respuesta a las acciones del usuario.  

---

## Tipografía
- **Fuente principal**: Poppins como familia principal. Jerarquía clara (h1 > h2 > h3).
- **Escala**:

```css
:root {
  --text-xs: 0.75rem;   /* 12px - Notas */
  --text-sm: 0.875rem;  /* 14px - Texto secundario */
  --text-base: 1rem;    /* 16px - Cuerpo */
  --text-lg: 1.125rem;  /* 18px - Subtítulos */
  --text-xl: 1.5rem;    /* 24px - Títulos */
}
```

- **Espaciado**: 1.5 para párrafos, 1.2 para títulos.

---

## Colores

### Paleta principal

| Rol        | Hex      | Uso típico                       |
|------------|----------|----------------------------------|
| Primario   | #4361ee  | Botones principales, headers     |
| Secundario | #3f37c9  | Botones secundarios              |
| Acento     | #f72585  | Acciones destacadas              |
| Fondo      | #f5f7ff  | Fondo de la aplicación           |
| Texto      | #212529  | Contenido principal              |

### Estados

| Tipo        | Hex      | Ejemplo de uso            |
|-------------|----------|---------------------------|
| Éxito       | #4cc9f0  | Notificaciones positivas  |
| Error       | #ef233c  | Mensajes de validación    |
| Advertencia | #f8961e  | Alertas                   |

---

## Componentes

### Botones

- **Tipos**:

```css
.btn-primary {
  background: var(--primary);
  color: white;
  border-radius: 10px;
  padding: 12px 24px;
}
.btn-secondary {
  border: 2px solid var(--primary);
  background: transparent;
}
```

- **Estados**:
  - Hover: Oscurecer color de fondo 10%.
  - Active: Efecto de presión (scale: 0.98).

### Formularios

- **Campos de entrada**:

```css
.form-input {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 12px 16px;
  transition: all 0.3s ease;
}
.form-input:focus {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
}
```

- **Validación**:
  - Mensajes de error en `var(--danger)` con icono de alerta (opcional).

---

## Iconografía
- **Librería**: Font Awesome 6.  
- **Tamaños**: 16px (pequeño), 24px (estándar), 32px (grande).  
- **Alineación**: Centrado verticalmente con texto (`vertical-align: middle`).  

---

## Espaciado y Layout

- **Sistema 8px**:

```css
.element {
  margin-bottom: 16px; /* 2x base */
  padding: 24px;       /* 3x base */
}
```

- **Grid**: 12 columnas para escritorio, 4 para móvil.

---

## Accesibilidad
- **Enfoque**:
  - Contraste mínimo en texto.
  - Etiquetas `aria-label` para íconos decorativos.
  - Pruebas con Lighthouse (meta: >90 en Accessibility).

---

## Responsividad

- **Puntos de quiebre**:
  - Móvil: `0-768px`
  - Tablet: `769-1024px`
  - Escritorio: `1025px+`

- **Técnicas**:
  - Unidades relativas (`rem`, `%`)
  - Imágenes responsivas (`max-width: 100%`)

---

## Ejemplo de Implementación

```html
<!-- Botón primario con icono -->
<button class="btn btn-primary">
  <i class="fas fa-plus"></i> Crear prueba
</button>
```

```html
<!-- Tarjeta de pregunta -->
<div class="card">
  <h3>¿Cuál es la capital de Francia?</h3>
  <p>Categoría: Geografía</p>
</div>
```

---

## Conclusión

Seguir esta guía asegura una experiencia de usuario consistente y accesible.  
Actualiza este documento regularmente para reflejar cambios en los estándares.  
Para componentes no cubiertos:

- Reutilizar patrones existentes.
- Documentar nuevas decisiones.
- Validar con el equipo de diseño.
