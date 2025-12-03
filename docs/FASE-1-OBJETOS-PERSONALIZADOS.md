# 🗄️ FASE 1: Crear los Objetos Personalizados (Custom Objects)

## Introducción

Los **Objetos Personalizados** de Liferay son la base de datos de nuestra tienda. Aquí almacenaremos todos los datos: productos, categorías, cestas de compra y pedidos.

---

## 📋 Índice de Objetos a Crear

1. [Categoría](#1-objeto-categoria)
2. [Producto](#2-objeto-producto)
3. [Cesta](#3-objeto-cesta)
4. [ItemCesta](#4-objeto-itemcesta)
5. [Pedido](#5-objeto-pedido)
6. [ItemPedido](#6-objeto-itempedido)
7. [Picklist para Estados](#7-crear-picklist-de-estados)

---

## 🚀 Acceder al Panel de Objetos

1. Inicia sesión como **Administrador** en tu portal Liferay
2. Ve al **Menú de Aplicaciones** (icono de cuadrícula ☰)
3. Navega a: **Panel de Control** → **Objetos** (o **Control Panel** → **Objects**)

![Acceso a Objetos](https://liferay.com/path-to-image)

---

## 1. Objeto: CATEGORIA

### Paso 1.1: Crear el Objeto

1. En la pantalla de Objetos, haz clic en el botón **"+"** (Añadir)
2. Rellena el formulario de creación:

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Categoría` |
| **Etiqueta Plural** | `Categorías` |
| **Nombre del Objeto** | `Categoria` (sin tilde, se genera automáticamente) |

3. Haz clic en **"Guardar"**

### Paso 1.2: Configurar el Objeto

1. Haz clic en el objeto **"Categoría"** que acabas de crear
2. Ve a la pestaña **"Detalles"**
3. Configura:

| Configuración | Valor |
|---------------|-------|
| **Alcance** | `Compañía` (Company) |
| **Tabla de Base de Datos** | Dejar por defecto |
| **Habilitar Comentarios** | ❌ No |
| **Habilitar Historial de Entrada** | ✅ Sí (opcional) |

### Paso 1.3: Añadir Campos

Ve a la pestaña **"Campos"** y añade los siguientes campos haciendo clic en **"+"**:

#### Campo 1: nombre
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Nombre` |
| **Nombre del Campo** | `nombre` |
| **Tipo** | `Texto` |
| **Obligatorio** | ✅ Sí |
| **Indexable como Texto** | ✅ Sí |

#### Campo 2: descripcion
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Descripción` |
| **Nombre del Campo** | `descripcion` |
| **Tipo** | `Texto Largo` (Long Text) |
| **Obligatorio** | ❌ No |

#### Campo 3: imagen
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Imagen` |
| **Nombre del Campo** | `imagen` |
| **Tipo** | `Attachment` (Archivo adjunto) |
| **Obligatorio** | ❌ No |

> 💡 **Nota**: El tipo "Attachment" permite subir imágenes o seleccionar de Documents and Media.

#### Campo 4: activa
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Activa` |
| **Nombre del Campo** | `activa` |
| **Tipo** | `Booleano` (Boolean) |
| **Obligatorio** | ✅ Sí |
| **Valor por defecto** | `true` |

### Paso 1.4: Publicar el Objeto

1. Una vez añadidos todos los campos, haz clic en **"Publicar"**
2. Confirma la publicación

> ⚠️ **IMPORTANTE**: Una vez publicado, no podrás cambiar ciertos aspectos del objeto. Asegúrate de que todos los campos están correctos antes de publicar.

---

## 2. Objeto: PRODUCTO

### Paso 2.1: Crear el Objeto

1. Haz clic en **"+"** para añadir nuevo objeto
2. Rellena:

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Producto` |
| **Etiqueta Plural** | `Productos` |
| **Nombre del Objeto** | `Producto` |

3. Guarda el objeto

### Paso 2.2: Configurar el Objeto

| Configuración | Valor |
|---------------|-------|
| **Alcance** | `Compañía` |

### Paso 2.3: Añadir Campos

#### Campo 1: nombre
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Nombre` |
| **Nombre del Campo** | `nombre` |
| **Tipo** | `Texto` |
| **Obligatorio** | ✅ Sí |
| **Indexable como Texto** | ✅ Sí |
| **Tamaño máximo** | `200` |

#### Campo 2: descripcion
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Descripción` |
| **Nombre del Campo** | `descripcion` |
| **Tipo** | `Texto Largo con HTML` (Rich Text) |
| **Obligatorio** | ✅ Sí |

#### Campo 3: precio
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Precio` |
| **Nombre del Campo** | `precio` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 4: imagen
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Imagen` |
| **Nombre del Campo** | `imagen` |
| **Tipo** | `Attachment` (Archivo adjunto) |
| **Obligatorio** | ✅ Sí |

> 💡 **Nota**: Selecciona "Attachment" para poder subir imágenes de productos.

#### Campo 5: stock
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Stock` |
| **Nombre del Campo** | `stock` |
| **Tipo** | `Entero` (Integer) |
| **Obligatorio** | ✅ Sí |
| **Valor por defecto** | `0` |

#### Campo 6: destacado
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Destacado` |
| **Nombre del Campo** | `destacado` |
| **Tipo** | `Booleano` |
| **Obligatorio** | ❌ No |
| **Valor por defecto** | `false` |

### Paso 2.4: Publicar el Objeto

Haz clic en **"Publicar"**

> ⚠️ **IMPORTANTE**: La relación con Categoría se crea DESDE el objeto Categoría, no aquí. Ve al siguiente paso.

### Paso 2.5: Crear Relación (desde Categoría)

1. Ve a **Panel de Control → Objetos → Categoria**
2. Ve a la pestaña **"Relaciones"**
3. Haz clic en **"+"**
4. Configura la relación:

| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Productos` |
| **Nombre** | `productos` |
| **Tipo** | `One to Many` |
| **One Record Of** | `Categoria` (el "uno") |
| **Many Records Of** | `Producto` (los "muchos") |
| **Enable Inheritance** | ❌ No marcar |

> 💡 **Explicación**: "Una categoría tiene muchos productos". Esto crea automáticamente un campo `r_productos_c_categoriaId` en Producto para vincularlos.

---

## 3. Objeto: CESTA

### Paso 3.1: Crear el Objeto

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Cesta` |
| **Etiqueta Plural** | `Cestas` |
| **Nombre del Objeto** | `Cesta` |

### Paso 3.2: Añadir Campos

#### Campo 1: total
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Total` |
| **Nombre del Campo** | `total` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ❌ No |
| **Valor por defecto** | `0` |

#### Campo 2: activa
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Activa` |
| **Nombre del Campo** | `activa` |
| **Tipo** | `Booleano` |
| **Obligatorio** | ✅ Sí |
| **Valor por defecto** | `true` |

> 💡 **Nota**: El campo `userId` se maneja automáticamente por Liferay a través del campo de auditoría `creator`. No necesitas crearlo manualmente.

### Paso 3.3: Publicar el Objeto

---

## 4. Objeto: ITEMCESTA

### Paso 4.1: Crear el Objeto

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Item de Cesta` |
| **Etiqueta Plural** | `Items de Cesta` |
| **Nombre del Objeto** | `ItemCesta` |

### Paso 4.2: Añadir Campos

#### Campo 1: cantidad
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Cantidad` |
| **Nombre del Campo** | `cantidad` |
| **Tipo** | `Entero` |
| **Obligatorio** | ✅ Sí |
| **Valor por defecto** | `1` |

#### Campo 2: precioUnitario
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Precio Unitario` |
| **Nombre del Campo** | `precioUnitario` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 3: subtotal
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Subtotal` |
| **Nombre del Campo** | `subtotal` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 4: nombreProducto (para caché/histórico)
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Nombre del Producto` |
| **Nombre del Campo** | `nombreProducto` |
| **Tipo** | `Texto` |
| **Obligatorio** | ❌ No |

#### Campo 5: imagenProducto (para caché/histórico)
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Imagen del Producto` |
| **Nombre del Campo** | `imagenProducto` |
| **Tipo** | `Texto` |
| **Obligatorio** | ❌ No |

### Paso 4.3: Publicar el Objeto

Haz clic en **"Publicar"**

> ⚠️ **NOTA SOBRE RELACIONES**: Las relaciones de ItemCesta se crean DESDE los objetos padre:
> - **Cesta → ItemCesta**: Se crea desde el objeto **Cesta**
> - **Producto → ItemCesta**: Se crea desde el objeto **Producto**
>
> Ver sección "Crear Todas las Relaciones" al final del documento.

---

## 5. Objeto: PEDIDO

### Paso 5.1: Crear el Objeto

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Pedido` |
| **Etiqueta Plural** | `Pedidos` |
| **Nombre del Objeto** | `Pedido` |

### Paso 5.2: Añadir Campos

#### Campo 1: numeroPedido
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Número de Pedido` |
| **Nombre del Campo** | `numeroPedido` |
| **Tipo** | `Texto` |
| **Obligatorio** | ✅ Sí |
| **Único** | ✅ Sí |

#### Campo 2: fechaPedido
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Fecha del Pedido` |
| **Nombre del Campo** | `fechaPedido` |
| **Tipo** | `Fecha` (Date) |
| **Obligatorio** | ✅ Sí |

#### Campo 3: total
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Total` |
| **Nombre del Campo** | `total` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 4: estado
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Estado` |
| **Nombre del Campo** | `estado` |
| **Tipo** | `Lista de Selección` (Picklist) |
| **Lista de Selección** | `EstadoPedido` (ver sección 7) |
| **Obligatorio** | ✅ Sí |

#### Campo 5: direccionEnvio
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Dirección de Envío` |
| **Nombre del Campo** | `direccionEnvio` |
| **Tipo** | `Texto Largo` |
| **Obligatorio** | ❌ No |

### Paso 5.3: Publicar el Objeto

---

## 6. Objeto: ITEMPEDIDO

### Paso 6.1: Crear el Objeto

| Campo | Valor |
|-------|-------|
| **Etiqueta** | `Item de Pedido` |
| **Etiqueta Plural** | `Items de Pedido` |
| **Nombre del Objeto** | `ItemPedido` |

### Paso 6.2: Añadir Campos

#### Campo 1: cantidad
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Cantidad` |
| **Nombre del Campo** | `cantidad` |
| **Tipo** | `Entero` |
| **Obligatorio** | ✅ Sí |

#### Campo 2: precioUnitario
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Precio Unitario` |
| **Nombre del Campo** | `precioUnitario` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 3: subtotal
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Subtotal` |
| **Nombre del Campo** | `subtotal` |
| **Tipo** | `Decimal` |
| **Obligatorio** | ✅ Sí |

#### Campo 4: nombreProducto
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Nombre del Producto` |
| **Nombre del Campo** | `nombreProducto` |
| **Tipo** | `Texto` |
| **Obligatorio** | ✅ Sí |

#### Campo 5: imagenProducto
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Imagen del Producto` |
| **Nombre del Campo** | `imagenProducto` |
| **Tipo** | `Texto` |
| **Obligatorio** | ❌ No |

### Paso 6.3: Publicar el Objeto

Haz clic en **"Publicar"**

> ⚠️ **NOTA SOBRE RELACIONES**: La relación de ItemPedido se crea DESDE el objeto padre:
> - **Pedido → ItemPedido**: Se crea desde el objeto **Pedido**
>
> Ver sección "Crear Todas las Relaciones" al final del documento.

---

## 8. CREAR TODAS LAS RELACIONES

> ⚠️ **IMPORTANTE**: Las relaciones One-to-Many SIEMPRE se crean desde el objeto "One" (el padre).

Una vez publicados todos los objetos, crea las siguientes relaciones:

### Relación 1: Categoría → Productos
**Ir a:** Panel de Control → Objetos → **Categoria** → Pestaña "Relaciones"

| Propiedad | Valor |
|-----------|-------|
| **Label** | `Productos` |
| **Name** | `productos` |
| **Type** | `One to Many` |
| **One Record Of** | `Categoria` |
| **Many Records Of** | `Producto` |

### Relación 2: Cesta → Items
**Ir a:** Panel de Control → Objetos → **Cesta** → Pestaña "Relaciones"

| Propiedad | Valor |
|-----------|-------|
| **Label** | `Items` |
| **Name** | `items` |
| **Type** | `One to Many` |
| **One Record Of** | `Cesta` |
| **Many Records Of** | `ItemCesta` |

### Relación 3: Producto → ItemsCesta
**Ir a:** Panel de Control → Objetos → **Producto** → Pestaña "Relaciones"

| Propiedad | Valor |
|-----------|-------|
| **Label** | `Items de Cesta` |
| **Name** | `itemsCesta` |
| **Type** | `One to Many` |
| **One Record Of** | `Producto` |
| **Many Records Of** | `ItemCesta` |

### Relación 4: Pedido → Items
**Ir a:** Panel de Control → Objetos → **Pedido** → Pestaña "Relaciones"

| Propiedad | Valor |
|-----------|-------|
| **Label** | `Items` |
| **Name** | `items` |
| **Type** | `One to Many` |
| **One Record Of** | `Pedido` |
| **Many Records Of** | `ItemPedido` |

#### Relación 2: Con Producto
| Propiedad | Valor |
|-----------|-------|
| **Etiqueta** | `Producto` |
| **Nombre** | `producto` |
| **Tipo** | `Uno a Muchos` |
| **Objeto Relacionado** | `Producto` |

### Paso 6.4: Publicar el Objeto

---

## 7. Crear Picklist de Estados

Antes de crear el objeto Pedido, necesitas crear la lista de selección para los estados.

### Paso 7.1: Acceder a Listas de Selección

1. Ve a **Panel de Control** → **Listas de Selección** (Picklists)
2. Haz clic en **"+"** para crear nueva

### Paso 7.2: Crear la Picklist

| Propiedad | Valor |
|-----------|-------|
| **Nombre** | `EstadoPedido` |

### Paso 7.3: Añadir Valores

Haz clic en **"+"** para cada valor:

| Clave | Nombre (Español) |
|-------|------------------|
| `pendiente` | Pendiente |
| `procesando` | Procesando |
| `enviado` | Enviado |
| `entregado` | Entregado |
| `cancelado` | Cancelado |

### Paso 7.4: Guardar

---

## 8. Configurar Permisos de API

Para que los fragmentos puedan acceder a los datos via API REST:

### Paso 8.1: Habilitar Headless API

1. Ve a **Panel de Control** → **Configuración del Sistema** → **Object**
2. Asegúrate de que **"Enable Object REST APIs"** está activado

### Paso 8.2: Configurar Permisos por Objeto

Para cada objeto creado:

1. Ve a **Objetos** → Selecciona el objeto
2. Ve a la pestaña **"Acciones"** o **"Permisos"**
3. Configura los permisos para el rol **"Guest"** y **"User"**:

**Para Categoría y Producto:**
- Guest: `Ver` (View)
- User: `Ver` (View)

**Para Cesta, ItemCesta, Pedido, ItemPedido:**
- Guest: Ninguno
- User: `Ver`, `Añadir`, `Actualizar`, `Eliminar`

---

## 9. Verificar la Creación

### Probar la API REST

Puedes probar que los objetos funcionan correctamente usando estas URLs:

```
GET http://localhost:8080/o/c/categorias
GET http://localhost:8080/o/c/productos
GET http://localhost:8080/o/c/cestas
GET http://localhost:8080/o/c/itemcestas
GET http://localhost:8080/o/c/pedidos
GET http://localhost:8080/o/c/itempedidos
```

### Añadir Datos de Prueba

1. Ve a **Panel de Control** → **Objetos**
2. En cada objeto, ve a la pestaña **"Entradas"** o accede desde el menú de aplicaciones
3. Añade algunos datos de prueba:

**Categorías de ejemplo:**
- Ordenadores
- Periféricos
- Componentes
- Móviles
- Gaming

**Productos de ejemplo:**
- Portátil Gaming XYZ - 999.99€ - Categoría: Ordenadores
- Ratón Inalámbrico - 29.99€ - Categoría: Periféricos
- Tarjeta Gráfica RTX - 599.99€ - Categoría: Componentes

---

## ✅ Checklist de Verificación

- [ ] Objeto Categoria creado y publicado
- [ ] Objeto Producto creado con relación a Categoria
- [ ] Objeto Cesta creado y publicado
- [ ] Objeto ItemCesta creado con relaciones
- [ ] Picklist EstadoPedido creada
- [ ] Objeto Pedido creado con campo de estado
- [ ] Objeto ItemPedido creado con relaciones
- [ ] Permisos configurados
- [ ] API REST funcionando
- [ ] Datos de prueba añadidos

---

## 🔗 Siguiente Fase

Una vez completada esta fase, continúa con:
→ **[FASE 2: Client Extension Theme CSS](./FASE-2-CLIENT-EXTENSION-CSS.md)**
