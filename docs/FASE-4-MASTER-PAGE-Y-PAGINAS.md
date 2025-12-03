# 📄 FASE 4: Master Page y Páginas

## Introducción

La **Master Page** es una plantilla que define la estructura común de todas las páginas de la tienda (header, footer, áreas de contenido). Las páginas individuales heredan esta estructura.

---

## 📋 Índice

1. [Crear la Master Page](#1-crear-la-master-page)
2. [Crear Página de Catálogo](#2-crear-página-de-catálogo)
3. [Crear Página de Detalle de Producto](#3-crear-página-de-detalle-de-producto)
4. [Crear Página de Cesta](#4-crear-página-de-cesta)
5. [Crear Página de Pedidos](#5-crear-página-de-pedidos)
6. [Configurar Navegación](#6-configurar-navegación)

---

## 1. Crear la Master Page

### Paso 1.1: Acceder a Plantillas de Página

1. Ve a **Diseño del Sitio** → **Plantillas de Página**
2. Haz clic en la pestaña **"Plantillas de Página Maestra"** (Master Page Templates)
3. Haz clic en **"+"** para crear una nueva

### Paso 1.2: Configurar la Master Page

| Campo | Valor |
|-------|-------|
| **Nombre** | `Tienda Master Page` |
| **Descripción** | `Plantilla principal para la tienda online` |

### Paso 1.3: Diseñar la Estructura

Una vez creada, entra en modo edición y configura la estructura:

#### Estructura visual:
```
┌─────────────────────────────────────────────────┐
│           🔒 Drop Zone: Header                  │
│    [Aquí va el fragmento tienda-navbar]         │
├─────────────────────────────────────────────────┤
│                                                 │
│                                                 │
│           📝 Drop Zone: Contenido               │
│    [Aquí irá el contenido de cada página]       │
│                                                 │
│                                                 │
├─────────────────────────────────────────────────┤
│           🔒 Drop Zone: Footer                  │
│    [Aquí va el fragmento tienda-footer]         │
└─────────────────────────────────────────────────┘
```

### Paso 1.4: Añadir los Fragmentos

1. **En la zona superior (Header):**
   - Arrastra un **"Container"** (Contenedor)
   - Dentro del contenedor, arrastra el fragmento **"tienda-navbar"**
   - Configura el contenedor como **"Fixed"** (Fijo) si quieres que el header sea sticky

2. **En la zona central:**
   - Esta es el **"Drop Zone"** principal
   - NO añadas nada aquí - este es el espacio donde irá el contenido de cada página
   - Asegúrate de que está marcado como **"Editable"**

3. **En la zona inferior (Footer):**
   - Arrastra un **"Container"**
   - Dentro, arrastra el fragmento **"tienda-footer"**

### Paso 1.5: Configurar el Theme CSS

1. En el panel lateral, haz clic en **"Configuración de Página"** (icono de engranaje)
2. Ve a **"Look and Feel"** o **"Diseño"**
3. En **"Theme CSS Client Extension"**, selecciona **"Tienda Theme CSS"**
4. Guarda los cambios

### Paso 1.6: Configurar los Campos Editables

En el fragmento **tienda-navbar**, configura:

| Campo Editable | Valor Sugerido |
|----------------|----------------|
| Logo Text | `MiTienda` (o tu nombre de tienda) |
| Categorías Text | `Categorías` |
| Pedidos Text | `Mis Pedidos` |

En el fragmento **tienda-footer**, configura:

| Campo Editable | Valor Sugerido |
|----------------|----------------|
| Footer Title | `MiTienda` |
| Footer Desc | `Tu tienda de confianza...` |
| Footer Email | `info@tutienda.com` |
| Footer Phone | `+34 900 123 456` |
| Footer Copyright | `© 2024 MiTienda. Todos los derechos reservados.` |

### Paso 1.7: Publicar la Master Page

1. Revisa que todo esté correcto en la vista previa
2. Haz clic en **"Publicar"**

---

## 2. Crear Página de Catálogo

Esta será la página principal donde se muestran todos los productos.

### Paso 2.1: Crear la Página

1. Ve a **Diseño del Sitio** → **Páginas**
2. Haz clic en **"+"** para añadir página
3. Selecciona **"Página de Contenido"** (Content Page)

### Paso 2.2: Configurar la Página

| Campo | Valor |
|-------|-------|
| **Nombre** | `Catálogo` |
| **URL Amigable** | `catalogo` |
| **Master Page** | `Tienda Master Page` |

### Paso 2.3: Añadir el Contenido

1. En el área de contenido (Drop Zone central), arrastra el fragmento **"tienda-catalogo"**
2. Configura el campo editable del título si lo deseas:
   - `catalogo-title`: "Nuestros Productos" o "Catálogo"

### Paso 2.4: Publicar

Haz clic en **"Publicar"**

### Paso 2.5: Configurar como Página de Inicio (Opcional)

Si quieres que el catálogo sea la página principal:

1. Ve a **Diseño del Sitio** → **Páginas**
2. Haz clic en los tres puntos (⋮) junto a "Catálogo"
3. Selecciona **"Marcar como página de inicio"**

---

## 3. Crear Página de Detalle de Producto

### Paso 3.1: Crear la Página

1. En **Páginas**, haz clic en **"+"**
2. Selecciona **"Página de Contenido"**

### Paso 3.2: Configurar

| Campo | Valor |
|-------|-------|
| **Nombre** | `Producto` |
| **URL Amigable** | `producto` |
| **Master Page** | `Tienda Master Page` |

### Paso 3.3: Añadir el Contenido

1. Arrastra el fragmento **"tienda-detalle-producto"** al área de contenido

### Paso 3.4: Ocultar de la Navegación

Esta página no debe aparecer en el menú principal porque se accede a través del catálogo:

1. En la configuración de la página
2. Marca **"Ocultar de la navegación"** o desmarca "Mostrar en navegación"

### Paso 3.5: Publicar

---

## 4. Crear Página de Cesta

### Paso 4.1: Crear la Página

| Campo | Valor |
|-------|-------|
| **Nombre** | `Cesta` |
| **URL Amigable** | `cesta` |
| **Master Page** | `Tienda Master Page` |

### Paso 4.2: Añadir el Contenido

1. Arrastra el fragmento **"tienda-cesta-pagina"** al área de contenido

### Paso 4.3: Ocultar de la Navegación

Esta página se accede desde el icono del carrito, no del menú:

1. Marca **"Ocultar de la navegación"**

### Paso 4.4: Publicar

---

## 5. Crear Página de Pedidos

### Paso 5.1: Crear la Página

| Campo | Valor |
|-------|-------|
| **Nombre** | `Pedidos` |
| **URL Amigable** | `pedidos` |
| **Master Page** | `Tienda Master Page` |

### Paso 5.2: Añadir el Contenido

1. Arrastra el fragmento **"tienda-pedidos"** al área de contenido

### Paso 5.3: Configurar Visibilidad

Puedes decidir si mostrar en navegación o no:
- **Mostrar**: Si quieres que aparezca en un menú
- **Ocultar**: Si solo se accede desde el navbar (link "Mis Pedidos")

### Paso 5.4: Publicar

---

## 6. Configurar Navegación

### Paso 6.1: Verificar las URLs

Asegúrate de que las URLs coincidan con las configuradas en los fragmentos:

| Página | URL Esperada |
|--------|--------------|
| Inicio/Catálogo | `/catalogo` o `/` |
| Producto | `/producto?id=X` |
| Cesta | `/cesta` |
| Pedidos | `/pedidos` |

### Paso 6.2: Crear Menú de Navegación (Opcional)

Si quieres un menú adicional además del navbar:

1. Ve a **Diseño del Sitio** → **Navegación**
2. Crea un nuevo menú o edita uno existente
3. Añade las páginas que quieras mostrar

### Paso 6.3: Actualizar Links en los Fragmentos

Si tus URLs son diferentes, necesitas actualizar los fragmentos:

1. Ve a **Fragmentos** → **Tienda Fragmentos**
2. Edita cada fragmento y actualiza las URLs en el JavaScript

Por ejemplo, en `tienda-navbar`:
```javascript
// Cambiar estas líneas si tus URLs son diferentes
<a href="/catalogo" ...>  // Cambiar a tu URL de catálogo
<a href="/pedidos" ...>   // Cambiar a tu URL de pedidos
<a href="/cesta" ...>     // Cambiar a tu URL de cesta
```

---

## 📐 Estructura Final del Sitio

```
🏠 Sitio Web
│
├── 📄 Catálogo (/)
│   └── 🧩 tienda-catalogo
│
├── 📄 Producto (/producto)
│   └── 🧩 tienda-detalle-producto
│   └── [Oculta en navegación]
│
├── 📄 Cesta (/cesta)
│   └── 🧩 tienda-cesta-pagina
│   └── [Oculta en navegación]
│
└── 📄 Pedidos (/pedidos)
    └── 🧩 tienda-pedidos
```

Todas las páginas usan **Tienda Master Page** que incluye:
- Header con tienda-navbar
- Footer con tienda-footer
- Theme CSS: Tienda Theme CSS

---

## 🔧 Solución de Problemas

### El Theme CSS no se aplica
1. Verifica que la Client Extension está desplegada
2. Asegúrate de seleccionar "Tienda Theme CSS" en la configuración de la Master Page
3. Limpia la caché del navegador

### Los fragmentos no cargan datos
1. Verifica que los Objetos están publicados
2. Comprueba los permisos de API (ver FASE 1)
3. Abre la consola del navegador (F12) para ver errores

### Las URLs no funcionan
1. Verifica las URLs amigables de cada página
2. Asegúrate de que las páginas están publicadas
3. Comprueba que las URLs en los fragmentos coinciden

### El navbar no se ve sticky
1. Añade esta clase al contenedor del header en la Master Page:
```css
position: sticky;
top: 0;
z-index: 1020;
```

---

## ✅ Checklist de Verificación

- [ ] Master Page "Tienda Master Page" creada
- [ ] Fragmento navbar añadido al header
- [ ] Fragmento footer añadido al footer
- [ ] Theme CSS aplicado a la Master Page
- [ ] Página de Catálogo creada y publicada
- [ ] Página de Producto creada y publicada
- [ ] Página de Cesta creada y publicada
- [ ] Página de Pedidos creada y publicada
- [ ] Todas las páginas usan la Master Page
- [ ] URLs verificadas y funcionando
- [ ] Navegación probada entre páginas

---

## 🔗 Siguiente Fase

Una vez completada esta fase, continúa con:
→ **[FASE 5: Pruebas y Datos de Ejemplo](./FASE-5-PRUEBAS-Y-DATOS.md)**
