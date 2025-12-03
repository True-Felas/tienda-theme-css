# 🎨 FASE 2: Client Extension Theme CSS

## Introducción

La **Client Extension de Theme CSS** nos permite personalizar completamente el aspecto visual de nuestra tienda sin modificar el tema base de Liferay. Los estilos que hemos creado incluyen todos los componentes visuales de la tienda.

---

## 📋 Estado Actual

✅ **Esta fase ya está completada**. Los archivos han sido creados y desplegados.

### Archivos Creados

```
client-extensions/tienda-theme-css/
├── client-extension.yaml      # Configuración de la client extension
├── src/
│   ├── css/
│   │   ├── clay.scss          # Importación de Clay Atlas
│   │   ├── main.scss          # Archivo principal que importa _custom
│   │   └── _custom.scss       # Todos los estilos personalizados
│   └── img/
│       └── .gitkeep           # Placeholder para imágenes
└── docs/
    └── (documentación)
```

---

## 🔧 Estructura del client-extension.yaml

```yaml
assemble:
    - from: src/img
      into: static/img

tienda-theme-css:
    clayURL: css/clay.css
    mainURL: css/main.css
    name: Tienda Theme CSS
    type: themeCSS
```

### Explicación:

| Propiedad | Descripción |
|-----------|-------------|
| `assemble` | Define qué archivos se empaquetan y dónde |
| `clayURL` | Ruta al CSS de Clay (se genera desde clay.scss) |
| `mainURL` | Ruta al CSS principal (se genera desde main.scss) |
| `name` | Nombre visible en el panel de Liferay |
| `type` | Tipo de client extension (`themeCSS`) |

---

## 🎨 Variables CSS Disponibles

Todas las variables están definidas en `_custom.scss` y pueden usarse en los fragmentos:

### Colores Principales
```css
--tienda-primary: #0066cc;       /* Azul principal */
--tienda-primary-dark: #004499;  /* Azul oscuro */
--tienda-secondary: #ff6600;     /* Naranja (botones de acción) */
--tienda-success: #28a745;       /* Verde (stock, éxito) */
--tienda-danger: #dc3545;        /* Rojo (errores, eliminar) */
```

### Colores Neutros
```css
--tienda-white: #ffffff;
--tienda-gray-100: #f8f9fa;      /* Fondo claro */
--tienda-gray-200: #e9ecef;      /* Bordes suaves */
--tienda-gray-500: #adb5bd;      /* Texto secundario */
--tienda-gray-800: #343a40;      /* Texto principal */
--tienda-gray-900: #212529;      /* Texto oscuro */
```

### Espaciado
```css
--tienda-spacing-xs: 0.25rem;    /* 4px */
--tienda-spacing-sm: 0.5rem;     /* 8px */
--tienda-spacing-md: 1rem;       /* 16px */
--tienda-spacing-lg: 1.5rem;     /* 24px */
--tienda-spacing-xl: 2rem;       /* 32px */
--tienda-spacing-2xl: 3rem;      /* 48px */
```

### Bordes y Sombras
```css
--tienda-border-radius: 8px;
--tienda-border-radius-sm: 4px;
--tienda-border-radius-lg: 12px;
--tienda-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
--tienda-shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.2);
```

---

## 📦 Clases CSS Disponibles

### Header y Navbar
| Clase | Descripción |
|-------|-------------|
| `.tienda-header` | Contenedor del header |
| `.tienda-navbar` | Barra de navegación principal |
| `.tienda-logo` | Estilo del logo/nombre |
| `.tienda-nav-center` | Sección central del navbar |
| `.tienda-nav-right` | Sección derecha del navbar |

### Menú de Categorías
| Clase | Descripción |
|-------|-------------|
| `.tienda-categorias-wrapper` | Contenedor del dropdown |
| `.tienda-categorias-btn` | Botón que abre el menú |
| `.tienda-categorias-dropdown` | Panel desplegable |
| `.tienda-categoria-item` | Cada categoría en la lista |

### Cesta/Carrito
| Clase | Descripción |
|-------|-------------|
| `.tienda-cesta-wrapper` | Contenedor del dropdown de cesta |
| `.tienda-cesta-btn` | Botón del carrito |
| `.tienda-cesta-count` | Badge con número de items |
| `.tienda-cesta-dropdown` | Panel desplegable de la cesta |
| `.tienda-cesta-item` | Cada producto en la cesta |
| `.tienda-cesta-footer` | Pie con total y botón |
| `.tienda-cesta-ver-btn` | Botón "Ver Cesta" |

### Catálogo de Productos
| Clase | Descripción |
|-------|-------------|
| `.tienda-catalogo` | Sección del catálogo |
| `.tienda-catalogo-grid` | Grid de productos |
| `.tienda-producto-card` | Tarjeta de producto |
| `.tienda-producto-img-wrapper` | Contenedor de imagen |
| `.tienda-producto-badge` | Badge "Destacado" |
| `.tienda-producto-nombre` | Nombre del producto |
| `.tienda-producto-precio` | Precio del producto |
| `.tienda-producto-stock` | Indicador de stock |

### Detalle de Producto
| Clase | Descripción |
|-------|-------------|
| `.tienda-detalle` | Sección de detalle |
| `.tienda-detalle-grid` | Layout de 2 columnas |
| `.tienda-detalle-imagen` | Contenedor de imagen |
| `.tienda-detalle-nombre` | Título del producto |
| `.tienda-detalle-precio` | Precio grande |
| `.tienda-btn-anadir` | Botón "Añadir a Cesta" |
| `.tienda-cantidad-control` | Control +/- cantidad |

### Página de Cesta
| Clase | Descripción |
|-------|-------------|
| `.tienda-cesta-pagina` | Página completa de cesta |
| `.tienda-cesta-lista` | Lista de productos |
| `.tienda-cesta-resumen` | Panel de resumen |
| `.tienda-btn-pagar` | Botón de pagar |

### Pedidos
| Clase | Descripción |
|-------|-------------|
| `.tienda-pedidos` | Sección de pedidos |
| `.tienda-pedido-card` | Tarjeta de pedido |
| `.tienda-pedido-header` | Cabecera con info |
| `.tienda-pedido-estado` | Badge de estado |
| `.tienda-pedido-producto` | Producto en pedido |

### Footer
| Clase | Descripción |
|-------|-------------|
| `.tienda-footer` | Footer principal |
| `.tienda-footer-grid` | Grid de columnas |
| `.tienda-footer-links` | Lista de enlaces |

### Utilidades
| Clase | Descripción |
|-------|-------------|
| `.tienda-container` | Contenedor centrado |
| `.tienda-text-center` | Texto centrado |
| `.tienda-mt-*` | Margin top (sm, md, lg, xl) |
| `.tienda-mb-*` | Margin bottom (sm, md, lg, xl) |
| `.tienda-hidden` | Ocultar elemento |
| `.tienda-toast` | Notificación toast |

---

## 🚀 Compilar y Desplegar

### Comando para compilar:

```bash
cd client-extensions/tienda-theme-css
blade gw clean deploy
```

### Resultado esperado:
```
BUILD SUCCESSFUL in Xs
Files deployed to bundles/osgi/client-extensions
```

---

## ⚙️ Activar en Liferay

### Método 1: A nivel de Sitio

1. Ve a **Administración del Sitio** → **Configuración del Sitio**
2. Busca **"Look and Feel"** o **"Apariencia"**
3. En **"Theme CSS Client Extension"**, selecciona **"Tienda Theme CSS"**
4. Guarda los cambios

### Método 2: A nivel de Página

1. Ve a la página donde quieres aplicar los estilos
2. Haz clic en **"Configurar Página"** (icono de engranaje)
3. Ve a **"Look and Feel"** o **"Diseño"**
4. En **"Theme CSS Client Extension"**, selecciona **"Tienda Theme CSS"**
5. Guarda

### Método 3: En la Master Page

1. Ve a **Diseño del Sitio** → **Plantillas de Página**
2. Edita tu Master Page
3. En la configuración, aplica el Theme CSS

---

## 🔄 Modificar Estilos

Si necesitas modificar los estilos:

### Paso 1: Editar el archivo

Abre `src/css/_custom.scss` y realiza los cambios.

### Paso 2: Recompilar

```bash
blade gw clean deploy
```

### Paso 3: Refrescar el navegador

Los cambios se aplicarán automáticamente (puede requerir limpiar caché).

---

## 📝 Añadir Nuevos Estilos

Para añadir nuevos componentes:

1. Añade las clases CSS en `_custom.scss`
2. Sigue la nomenclatura: `.tienda-[componente]-[elemento]`
3. Usa las variables CSS definidas
4. Recompila con `blade gw clean deploy`

### Ejemplo:

```scss
.tienda-banner {
    background: linear-gradient(135deg, var(--tienda-primary), var(--tienda-primary-dark));
    color: var(--tienda-white);
    padding: var(--tienda-spacing-2xl);
    border-radius: var(--tienda-border-radius-lg);
    text-align: center;
    
    &-title {
        font-size: var(--tienda-font-size-3xl);
        margin-bottom: var(--tienda-spacing-md);
    }
}
```

---

## 🖼️ Añadir Imágenes

Para añadir imágenes estáticas:

1. Coloca las imágenes en `src/img/`
2. Referéncialas en CSS o HTML como:
   ```
   /o/tienda-theme-css/static/img/tu-imagen.png
   ```

---

## ✅ Checklist de Verificación

- [x] Archivos SCSS creados correctamente
- [x] client-extension.yaml configurado
- [x] Compilación exitosa (`blade gw deploy`)
- [ ] Theme CSS activado en el sitio
- [ ] Estilos visibles en el navegador

---

## 🐛 Solución de Problemas

### Error: "Entry is a duplicate"
**Solución**: No copies archivos CSS directamente. Deja que SCSS los genere.

### Los estilos no se ven
**Solución**: 
1. Verifica que el Theme CSS está activado
2. Limpia la caché del navegador
3. Verifica en Network que los CSS se cargan

### Error de compilación SCSS
**Solución**: Verifica la sintaxis SCSS. Los anidamientos deben usar `&`.

---

## 🔗 Siguiente Fase

Una vez completada esta fase, continúa con:
→ **[FASE 3: Fragmentos Personalizados](./FASE-3-FRAGMENTOS.md)**
