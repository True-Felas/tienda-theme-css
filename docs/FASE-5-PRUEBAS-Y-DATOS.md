# ✅ FASE 5: Pruebas y Datos de Ejemplo

## Introducción

En esta fase final, añadiremos datos de prueba y verificaremos que todo el sistema funciona correctamente.

---

## 📋 Índice

1. [Añadir Categorías de Prueba](#1-añadir-categorías-de-prueba)
2. [Añadir Productos de Prueba](#2-añadir-productos-de-prueba)
3. [Probar el Flujo Completo](#3-probar-el-flujo-completo)
4. [Verificación de APIs](#4-verificación-de-apis)
5. [Checklist Final](#5-checklist-final)
6. [Solución de Problemas Comunes](#6-solución-de-problemas-comunes)

---

## 1. Añadir Categorías de Prueba

### Paso 1.1: Acceder al Objeto Categoría

1. Ve al **Menú de Aplicaciones** (☰)
2. Busca **"Categorías"** en la sección de objetos personalizados
3. O ve a **Panel de Control** → **Objetos** → **Categoría** → **Entradas**

### Paso 1.2: Crear Categorías

Haz clic en **"+"** y crea las siguientes categorías:

#### Categoría 1: Ordenadores
| Campo | Valor |
|-------|-------|
| Nombre | `Ordenadores` |
| Descripción | `Portátiles, sobremesa y todo en uno` |
| Activa | ✅ Sí |
| Imagen | (subir una imagen de ordenador) |

#### Categoría 2: Periféricos
| Campo | Valor |
|-------|-------|
| Nombre | `Periféricos` |
| Descripción | `Ratones, teclados, monitores y más` |
| Activa | ✅ Sí |

#### Categoría 3: Componentes
| Campo | Valor |
|-------|-------|
| Nombre | `Componentes` |
| Descripción | `Tarjetas gráficas, procesadores, memorias` |
| Activa | ✅ Sí |

#### Categoría 4: Smartphones
| Campo | Valor |
|-------|-------|
| Nombre | `Smartphones` |
| Descripción | `Móviles y accesorios` |
| Activa | ✅ Sí |

#### Categoría 5: Gaming
| Campo | Valor |
|-------|-------|
| Nombre | `Gaming` |
| Descripción | `Consolas, mandos y accesorios gaming` |
| Activa | ✅ Sí |

#### Categoría 6: Audio
| Campo | Valor |
|-------|-------|
| Nombre | `Audio` |
| Descripción | `Auriculares, altavoces y sistemas de sonido` |
| Activa | ✅ Sí |

---

## 2. Añadir Productos de Prueba

### Paso 2.1: Acceder al Objeto Producto

1. Busca **"Productos"** en el menú de aplicaciones
2. O ve a **Objetos** → **Producto** → **Entradas**

### Paso 2.2: Crear Productos

#### 📦 Productos de Ordenadores

**Producto 1:**
| Campo | Valor |
|-------|-------|
| Nombre | `Portátil Gaming Pro X15` |
| Descripción | `Portátil gaming de alto rendimiento con procesador Intel i7, 16GB RAM, SSD 512GB y tarjeta gráfica RTX 4060. Pantalla 15.6" Full HD 144Hz.` |
| Precio | `1299.99` |
| Stock | `15` |
| Destacado | ✅ Sí |
| Categoría | Ordenadores |
| Imagen | (subir imagen de portátil) |

**Producto 2:**
| Campo | Valor |
|-------|-------|
| Nombre | `PC Sobremesa WorkStation` |
| Descripción | `Ordenador de sobremesa para profesionales. AMD Ryzen 9, 32GB RAM, SSD 1TB. Ideal para diseño y desarrollo.` |
| Precio | `1899.00` |
| Stock | `8` |
| Destacado | ❌ No |
| Categoría | Ordenadores |

**Producto 3:**
| Campo | Valor |
|-------|-------|
| Nombre | `MacBook Air M2` |
| Descripción | `El portátil más delgado y ligero de Apple. Chip M2, 8GB RAM, 256GB SSD. Batería de hasta 18 horas.` |
| Precio | `1199.00` |
| Stock | `20` |
| Destacado | ✅ Sí |
| Categoría | Ordenadores |

#### 📦 Productos de Periféricos

**Producto 4:**
| Campo | Valor |
|-------|-------|
| Nombre | `Ratón Gaming RGB Pro` |
| Descripción | `Ratón gaming con sensor óptico de 16000 DPI, 8 botones programables e iluminación RGB personalizable.` |
| Precio | `59.99` |
| Stock | `50` |
| Destacado | ❌ No |
| Categoría | Periféricos |

**Producto 5:**
| Campo | Valor |
|-------|-------|
| Nombre | `Teclado Mecánico Cherry MX` |
| Descripción | `Teclado mecánico con switches Cherry MX Red. Layout español, retroiluminación LED, reposamuñecas incluido.` |
| Precio | `129.99` |
| Stock | `25` |
| Destacado | ✅ Sí |
| Categoría | Periféricos |

**Producto 6:**
| Campo | Valor |
|-------|-------|
| Nombre | `Monitor 27" 4K IPS` |
| Descripción | `Monitor profesional de 27 pulgadas con resolución 4K UHD. Panel IPS, 99% sRGB, HDR10, USB-C.` |
| Precio | `449.00` |
| Stock | `12` |
| Destacado | ❌ No |
| Categoría | Periféricos |

#### 📦 Productos de Componentes

**Producto 7:**
| Campo | Valor |
|-------|-------|
| Nombre | `NVIDIA RTX 4070 Ti` |
| Descripción | `Tarjeta gráfica de última generación para gaming 4K y creación de contenido. 12GB GDDR6X, Ray Tracing, DLSS 3.` |
| Precio | `799.99` |
| Stock | `5` |
| Destacado | ✅ Sí |
| Categoría | Componentes |

**Producto 8:**
| Campo | Valor |
|-------|-------|
| Nombre | `Intel Core i9-13900K` |
| Descripción | `Procesador de 13ª generación con 24 núcleos (8P+16E), hasta 5.8GHz. El más potente para gaming y productividad.` |
| Precio | `589.00` |
| Stock | `10` |
| Destacado | ❌ No |
| Categoría | Componentes |

**Producto 9:**
| Campo | Valor |
|-------|-------|
| Nombre | `RAM DDR5 32GB (2x16GB)` |
| Descripción | `Kit de memoria DDR5 de alto rendimiento. 6000MHz, CL36, RGB, optimizado para Intel y AMD.` |
| Precio | `159.99` |
| Stock | `30` |
| Destacado | ❌ No |
| Categoría | Componentes |

#### 📦 Productos de Gaming

**Producto 10:**
| Campo | Valor |
|-------|-------|
| Nombre | `PlayStation 5` |
| Descripción | `La consola de nueva generación de Sony. SSD ultrarrápido, 4K, Ray Tracing, mando DualSense con respuesta háptica.` |
| Precio | `549.99` |
| Stock | `3` |
| Destacado | ✅ Sí |
| Categoría | Gaming |

**Producto 11:**
| Campo | Valor |
|-------|-------|
| Nombre | `Xbox Series X` |
| Descripción | `La consola más potente de Xbox. 12 teraflops, SSD 1TB, 4K a 120fps, retrocompatibilidad total.` |
| Precio | `499.99` |
| Stock | `7` |
| Destacado | ❌ No |
| Categoría | Gaming |

**Producto 12:**
| Campo | Valor |
|-------|-------|
| Nombre | `Mando Pro Controller` |
| Descripción | `Mando inalámbrico profesional con gatillos analógicos, vibración HD, giroscopio y batería de 40 horas.` |
| Precio | `69.99` |
| Stock | `40` |
| Destacado | ❌ No |
| Categoría | Gaming |

#### 📦 Productos de Audio

**Producto 13:**
| Campo | Valor |
|-------|-------|
| Nombre | `Auriculares Sony WH-1000XM5` |
| Descripción | `Los mejores auriculares con cancelación de ruido. Audio Hi-Res, 30h de batería, llamadas cristalinas.` |
| Precio | `379.00` |
| Stock | `18` |
| Destacado | ✅ Sí |
| Categoría | Audio |

**Producto 14:**
| Campo | Valor |
|-------|-------|
| Nombre | `Altavoz Bluetooth Portátil` |
| Descripción | `Altavoz resistente al agua IPX7, 24h de batería, sonido 360°, emparejamiento estéreo.` |
| Precio | `89.99` |
| Stock | `35` |
| Destacado | ❌ No |
| Categoría | Audio |

#### 📦 Producto sin Stock (para probar estado)

**Producto 15:**
| Campo | Valor |
|-------|-------|
| Nombre | `Steam Deck OLED` |
| Descripción | `La consola portátil de Valve con pantalla OLED. Juega a tu biblioteca de Steam en cualquier lugar.` |
| Precio | `569.00` |
| Stock | `0` |
| Destacado | ✅ Sí |
| Categoría | Gaming |

---

## 3. Probar el Flujo Completo

### Test 1: Navegación Básica

1. **Ir a la página de inicio/catálogo**
   - ✅ ¿Se muestran todos los productos?
   - ✅ ¿Las tarjetas de producto tienen imagen, nombre y precio?
   - ✅ ¿Los productos destacados muestran el badge?
   - ✅ ¿Se muestra correctamente el stock?

2. **Probar el menú de categorías**
   - ✅ ¿Se despliega al hacer clic/hover?
   - ✅ ¿Se muestran todas las categorías activas?
   - ✅ ¿Al hacer clic en una categoría, se filtran los productos?

3. **Probar el ordenamiento**
   - ✅ ¿Funciona ordenar por precio ascendente?
   - ✅ ¿Funciona ordenar por precio descendente?
   - ✅ ¿Funciona ordenar por nombre?

### Test 2: Detalle de Producto

1. **Hacer clic en un producto**
   - ✅ ¿Se navega a /producto?id=X?
   - ✅ ¿Se muestra la imagen grande?
   - ✅ ¿Se muestra el nombre, precio y descripción?
   - ✅ ¿Se muestra el estado del stock correctamente?

2. **Probar producto sin stock**
   - ✅ ¿El botón "Añadir" está deshabilitado?
   - ✅ ¿Se muestra "Producto agotado"?

3. **Probar control de cantidad**
   - ✅ ¿Los botones +/- funcionan?
   - ✅ ¿No permite valores menores a 1?
   - ✅ ¿No permite valores mayores al stock?

### Test 3: Carrito de Compra

1. **Añadir producto al carrito**
   - ✅ ¿Aparece el toast "Producto añadido"?
   - ✅ ¿Se actualiza el contador en el icono?
   - ✅ ¿Al abrir el dropdown, aparece el producto?

2. **Añadir el mismo producto de nuevo**
   - ✅ ¿Se incrementa la cantidad en lugar de duplicar?

3. **Eliminar producto del carrito**
   - ✅ ¿El botón X elimina el producto?
   - ✅ ¿Se actualiza el contador?

4. **Ir a la cesta completa**
   - ✅ ¿El botón "Ver Cesta" lleva a /cesta?
   - ✅ ¿Se muestran todos los productos?
   - ✅ ¿Se calcula correctamente el subtotal y total?
   - ✅ ¿Funciona el control de cantidad?

### Test 4: Proceso de Compra

1. **Procesar el pago**
   - ✅ ¿Aparece confirmación al hacer clic en "Pagar"?
   - ✅ ¿Se crea el pedido correctamente?
   - ✅ ¿Se vacía la cesta?
   - ✅ ¿Se redirige a /pedidos?

### Test 5: Página de Pedidos

1. **Ver lista de pedidos**
   - ✅ ¿Se muestran los pedidos realizados?
   - ✅ ¿Aparece el número de pedido, fecha y total?
   - ✅ ¿Se muestra el estado (Pendiente)?
   - ✅ ¿Se muestran los productos del pedido?

2. **Clic en producto del pedido**
   - ✅ ¿Navega al detalle del producto?

---

## 4. Verificación de APIs

### Probar APIs REST

Abre el navegador o usa una herramienta como Postman para probar:

#### Categorías
```
GET http://localhost:8080/o/c/categorias
```
Respuesta esperada: Lista de categorías en JSON

#### Productos
```
GET http://localhost:8080/o/c/productos
```
Respuesta esperada: Lista de productos en JSON

#### Productos por categoría
```
GET http://localhost:8080/o/c/productos?filter=r_categoria_c_categoriaId eq {ID}
```

#### Cesta del usuario
```
GET http://localhost:8080/o/c/cestas?filter=activa eq true
```

#### Pedidos
```
GET http://localhost:8080/o/c/pedidos
```

### Verificar en la Consola del Navegador

1. Abre las **DevTools** (F12)
2. Ve a la pestaña **"Network"**
3. Navega por la tienda
4. Verifica que las llamadas a `/o/c/...` devuelven **200 OK**

Si hay errores **401** o **403**, revisa los permisos de los objetos.

---

## 5. Checklist Final

### Objetos Personalizados
- [ ] Categoría: creado, publicado, con datos
- [ ] Producto: creado, publicado, con datos, relación con Categoría
- [ ] Cesta: creado, publicado
- [ ] ItemCesta: creado, publicado, relaciones configuradas
- [ ] Pedido: creado, publicado, Picklist de estados
- [ ] ItemPedido: creado, publicado, relaciones configuradas
- [ ] Permisos configurados para APIs

### Client Extension
- [ ] tienda-theme-css compilado y desplegado
- [ ] Theme CSS aplicado a la Master Page

### Fragmentos
- [ ] tienda-navbar funcionando
- [ ] tienda-catalogo funcionando
- [ ] tienda-detalle-producto funcionando
- [ ] tienda-cesta-pagina funcionando
- [ ] tienda-pedidos funcionando
- [ ] tienda-footer funcionando

### Páginas
- [ ] Master Page creada y publicada
- [ ] Página Catálogo (/)
- [ ] Página Producto (/producto)
- [ ] Página Cesta (/cesta)
- [ ] Página Pedidos (/pedidos)

### Funcionalidades
- [ ] Ver catálogo de productos
- [ ] Filtrar por categoría
- [ ] Ver detalle de producto
- [ ] Añadir productos al carrito
- [ ] Ver carrito (dropdown)
- [ ] Ver carrito completo
- [ ] Modificar cantidades
- [ ] Eliminar productos
- [ ] Procesar pedido
- [ ] Ver historial de pedidos

---

## 6. Solución de Problemas Comunes

### Problema: Los productos no se cargan

**Causa posible:** Permisos de API
**Solución:**
1. Ve a **Panel de Control** → **Configuración del Sistema** → **Object**
2. Verifica que las APIs REST están habilitadas
3. Revisa los permisos del objeto Producto para el rol "Guest" o "User"

### Problema: Error 401 Unauthorized

**Causa:** El usuario no tiene permisos
**Solución:**
1. Inicia sesión en el portal
2. O configura permisos para usuarios "Guest"

### Problema: La cesta no se guarda

**Causa posible:** El objeto Cesta no tiene permisos de escritura
**Solución:**
1. Ve al objeto Cesta en Objetos
2. Configura permisos para "User": Ver, Añadir, Actualizar, Eliminar

### Problema: Los estilos no se aplican

**Causa:** Theme CSS no activado
**Solución:**
1. Ve a la configuración de la Master Page
2. Selecciona "Tienda Theme CSS" en Theme CSS Client Extension
3. Limpia la caché del navegador

### Problema: El dropdown no se cierra

**Causa:** Conflicto de eventos JavaScript
**Solución:**
1. Verifica que el JavaScript del fragmento no tiene errores (F12 → Console)
2. Asegúrate de que los IDs de elementos son únicos

### Problema: Las imágenes no se muestran

**Causa:** Rutas incorrectas o imágenes no subidas
**Solución:**
1. Verifica que las imágenes están subidas en los objetos
2. Verifica la URL de la imagen en la consola de red
3. Usa una imagen placeholder si falta: `/o/tienda-theme-css/static/img/placeholder.png`

### Problema: El precio muestra NaN

**Causa:** El campo precio está vacío o tiene formato incorrecto
**Solución:**
1. Verifica que todos los productos tienen precio
2. El precio debe ser un número decimal (ej: `99.99`)

---

## 🎉 ¡Felicidades!

Si has llegado hasta aquí y todos los tests pasan, ¡tu tienda online está funcionando!

### Próximos Pasos Sugeridos

1. **Personalizar el diseño:**
   - Modifica los colores en `_custom.scss`
   - Añade tu logo real
   - Ajusta tipografías

2. **Añadir más funcionalidades:**
   - Búsqueda de productos
   - Filtros avanzados (precio, características)
   - Favoritos/Wishlist
   - Reviews de productos

3. **Mejorar la seguridad:**
   - Autenticación de usuarios
   - Validación de stock antes de pedido
   - Integración con pasarela de pago real

4. **SEO y rendimiento:**
   - Meta tags dinámicos
   - Optimización de imágenes
   - Caché de datos

---

## 📚 Documentos de Referencia

- [FASE 1: Objetos Personalizados](./FASE-1-OBJETOS-PERSONALIZADOS.md)
- [FASE 2: Client Extension CSS](./FASE-2-CLIENT-EXTENSION-CSS.md)
- [FASE 3: Fragmentos](./FASE-3-FRAGMENTOS.md)
- [FASE 4: Master Page y Páginas](./FASE-4-MASTER-PAGE-Y-PAGINAS.md)
