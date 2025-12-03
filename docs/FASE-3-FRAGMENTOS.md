# 🧩 FASE 3: Fragmentos Personalizados

## Introducción

Los **Fragmentos** son componentes reutilizables que combinan HTML, CSS y JavaScript. Crearemos los fragmentos necesarios para construir nuestra tienda.

---

## 📋 Índice de Fragmentos

1. [Navbar Principal](#fragmento-1-navbar-principal)
2. [Catálogo de Productos](#fragmento-2-catálogo-de-productos)
3. [Detalle de Producto](#fragmento-3-detalle-de-producto)
4. [Página de Cesta](#fragmento-4-página-de-cesta)
5. [Lista de Pedidos](#fragmento-5-lista-de-pedidos)
6. [Footer](#fragmento-6-footer)

---

## 🚀 Crear el Conjunto de Fragmentos

### Paso 1: Acceder a Fragmentos

1. Ve a **Diseño del Sitio** → **Fragmentos**
2. Haz clic en **"+"** para crear un nuevo **Conjunto de Fragmentos**

### Paso 2: Configurar el Conjunto

| Campo | Valor |
|-------|-------|
| **Nombre** | `Tienda Fragmentos` |
| **Descripción** | `Fragmentos personalizados para la tienda online` |

### Paso 3: Guardar

---

## Fragmento 1: NAVBAR PRINCIPAL

Este fragmento contiene el header completo con logo, menú de categorías, y carrito.

### Paso 1: Crear el Fragmento

1. Dentro del conjunto "Tienda Fragmentos", haz clic en **"+"**
2. Selecciona **"Fragmento Básico"**
3. Nombre: `tienda-navbar`

### Paso 2: Código HTML

```html
<div class="tienda-header">
    <nav class="tienda-navbar">
        <!-- Logo -->
        <a href="/" class="tienda-logo">
            <span data-lfr-editable-id="logo-text" data-lfr-editable-type="rich-text">MiTienda</span>
        </a>
        
        <!-- Centro: Menú de categorías y búsqueda -->
        <div class="tienda-nav-center">
            <!-- Dropdown de Categorías -->
            <div class="tienda-categorias-wrapper" id="categoriasWrapper">
                <button class="tienda-categorias-btn" id="btnCategorias">
                    <span class="icon-bars">☰</span>
                    <span>Categorías</span>
                </button>
                <div class="tienda-categorias-dropdown" id="categoriasDropdown">
                    <div id="categorias-lista">
                        <div class="tienda-cesta-empty">
                            <p>Cargando categorías...</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Búsqueda -->
            <div class="tienda-busqueda">
                <input type="text" 
                       placeholder="Buscar productos..." 
                       class="tienda-busqueda-input" 
                       id="busquedaInput">
            </div>
        </div>
        
        <!-- Derecha: Pedidos y Cesta -->
        <div class="tienda-nav-right">
            <!-- Link a Pedidos -->
            <a href="/pedidos" class="tienda-pedidos-link">
                <span>📦</span>
                <span>Mis Pedidos</span>
            </a>
            
            <!-- Dropdown de Cesta -->
            <div class="tienda-cesta-wrapper" id="cestaWrapper">
                <button class="tienda-cesta-btn" id="btnCesta">
                    <span class="icon-cart">🛒</span>
                    <span class="tienda-cesta-count" id="cestaCount">0</span>
                </button>
                <div class="tienda-cesta-dropdown" id="cestaDropdown">
                    <div class="tienda-cesta-header">
                        <span>Mi Cesta</span>
                    </div>
                    <div class="tienda-cesta-items" id="cestaItems">
                        <div class="tienda-cesta-empty">
                            <div class="tienda-cesta-empty-icon">🛒</div>
                            <p>Tu cesta está vacía</p>
                        </div>
                    </div>
                    <div class="tienda-cesta-footer">
                        <div class="tienda-cesta-total">
                            <span class="tienda-cesta-total-label">Total:</span>
                            <span class="tienda-cesta-total-value" id="cestaTotal">0,00 €</span>
                        </div>
                        <a href="/cesta" class="tienda-cesta-ver-btn">
                            Ver Cesta Completa
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</div>
```

### Paso 3: Código JavaScript

```javascript
(function() {
    // ==========================================
    // CONFIGURACIÓN Y VARIABLES GLOBALES
    // ==========================================
    const CATEGORIAS_API = '/o/c/categorias';
    const CESTAS_API = '/o/c/cestas';
    const ITEMS_CESTA_API = '/o/c/itemcestas';
    const PRODUCTOS_API = '/o/c/productos';
    
    let cestaItems = [];
    let cestaId = null;
    
    // ==========================================
    // FUNCIONES DE UTILIDAD
    // ==========================================
    function formatearPrecio(precio) {
        return new Intl.NumberFormat('es-ES', {
            style: 'currency',
            currency: 'EUR'
        }).format(precio || 0);
    }
    
    function mostrarToast(mensaje, esError = false) {
        // Eliminar toast existente
        const existente = document.querySelector('.tienda-toast');
        if (existente) existente.remove();
        
        const toast = document.createElement('div');
        toast.className = 'tienda-toast' + (esError ? ' error' : '');
        toast.textContent = mensaje;
        document.body.appendChild(toast);
        
        setTimeout(() => toast.remove(), 3000);
    }
    
    // ==========================================
    // TOGGLE DROPDOWNS
    // ==========================================
    function initDropdowns() {
        const btnCategorias = document.getElementById('btnCategorias');
        const btnCesta = document.getElementById('btnCesta');
        const categoriasDropdown = document.getElementById('categoriasDropdown');
        const cestaDropdown = document.getElementById('cestaDropdown');
        
        // Toggle categorías
        if (btnCategorias) {
            btnCategorias.addEventListener('click', function(e) {
                e.stopPropagation();
                categoriasDropdown.classList.toggle('active');
                cestaDropdown.classList.remove('active');
            });
        }
        
        // Toggle cesta
        if (btnCesta) {
            btnCesta.addEventListener('click', function(e) {
                e.stopPropagation();
                cestaDropdown.classList.toggle('active');
                categoriasDropdown.classList.remove('active');
            });
        }
        
        // Cerrar al hacer clic fuera
        document.addEventListener('click', function(e) {
            if (!e.target.closest('.tienda-categorias-wrapper')) {
                categoriasDropdown.classList.remove('active');
            }
            if (!e.target.closest('.tienda-cesta-wrapper')) {
                cestaDropdown.classList.remove('active');
            }
        });
    }
    
    // ==========================================
    // CARGAR CATEGORÍAS
    // ==========================================
    async function cargarCategorias() {
        const container = document.getElementById('categorias-lista');
        if (!container) return;
        
        try {
            const response = await fetch(CATEGORIAS_API + '?pageSize=50&filter=activa eq true', {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                const categorias = data.items || [];
                
                if (categorias.length === 0) {
                    container.innerHTML = '<div class="tienda-cesta-empty"><p>No hay categorías</p></div>';
                    return;
                }
                
                container.innerHTML = categorias.map(cat => `
                    <a href="/catalogo?categoria=${cat.id}" class="tienda-categoria-item">
                        ${cat.imagen ? `<img src="${cat.imagen}" alt="${cat.nombre}">` : '<span>📁</span>'}
                        <span>${cat.nombre}</span>
                    </a>
                `).join('');
            }
        } catch (error) {
            console.error('Error al cargar categorías:', error);
            container.innerHTML = '<div class="tienda-cesta-empty"><p>Error al cargar</p></div>';
        }
    }
    
    // ==========================================
    // CARGAR CESTA
    // ==========================================
    async function cargarCesta() {
        try {
            // Obtener la cesta activa del usuario
            const response = await fetch(CESTAS_API + '?filter=activa eq true&pageSize=1', {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                
                if (data.items && data.items.length > 0) {
                    cestaId = data.items[0].id;
                    await cargarItemsCesta(cestaId);
                } else {
                    actualizarVistaCesta([]);
                }
            }
        } catch (error) {
            console.error('Error al cargar cesta:', error);
        }
    }
    
    async function cargarItemsCesta(id) {
        try {
            const response = await fetch(`${ITEMS_CESTA_API}?filter=r_cesta_c_cestaId eq ${id}`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                cestaItems = data.items || [];
                actualizarVistaCesta(cestaItems);
            }
        } catch (error) {
            console.error('Error al cargar items:', error);
        }
    }
    
    function actualizarVistaCesta(items) {
        const container = document.getElementById('cestaItems');
        const countElement = document.getElementById('cestaCount');
        const totalElement = document.getElementById('cestaTotal');
        
        if (!container) return;
        
        // Actualizar contador
        const totalItems = items.reduce((sum, item) => sum + (item.cantidad || 0), 0);
        if (countElement) countElement.textContent = totalItems;
        
        if (items.length === 0) {
            container.innerHTML = `
                <div class="tienda-cesta-empty">
                    <div class="tienda-cesta-empty-icon">🛒</div>
                    <p>Tu cesta está vacía</p>
                </div>
            `;
            if (totalElement) totalElement.textContent = '0,00 €';
            return;
        }
        
        // Renderizar items
        container.innerHTML = items.map(item => `
            <div class="tienda-cesta-item">
                <img src="${item.imagenProducto || '/o/tienda-theme-css/static/img/placeholder.png'}" 
                     alt="${item.nombreProducto || 'Producto'}" 
                     class="tienda-cesta-item-img"
                     onerror="this.src='/o/tienda-theme-css/static/img/placeholder.png'">
                <div class="tienda-cesta-item-info">
                    <div class="tienda-cesta-item-name">${item.nombreProducto || 'Producto'}</div>
                    <div class="tienda-cesta-item-qty">Cantidad: ${item.cantidad}</div>
                    <div class="tienda-cesta-item-price">${formatearPrecio(item.precioUnitario)}</div>
                </div>
                <button class="tienda-cesta-item-remove" onclick="window.tiendaEliminarItem(${item.id})">✕</button>
            </div>
        `).join('');
        
        // Calcular y mostrar total
        const total = items.reduce((sum, item) => sum + (item.subtotal || 0), 0);
        if (totalElement) totalElement.textContent = formatearPrecio(total);
    }
    
    // ==========================================
    // FUNCIONES GLOBALES (para otros fragmentos)
    // ==========================================
    
    // Eliminar item de la cesta
    window.tiendaEliminarItem = async function(itemId) {
        try {
            const response = await fetch(`${ITEMS_CESTA_API}/${itemId}`, {
                method: 'DELETE',
                headers: { 'Content-Type': 'application/json' }
            });
            
            if (response.ok) {
                cestaItems = cestaItems.filter(item => item.id !== itemId);
                actualizarVistaCesta(cestaItems);
                mostrarToast('Producto eliminado');
            }
        } catch (error) {
            console.error('Error:', error);
            mostrarToast('Error al eliminar', true);
        }
    };
    
    // Añadir producto a la cesta
    window.tiendaAnadirACesta = async function(productoId, cantidad = 1) {
        try {
            // Obtener datos del producto
            const prodResponse = await fetch(`${PRODUCTOS_API}/${productoId}`);
            if (!prodResponse.ok) throw new Error('Producto no encontrado');
            const producto = await prodResponse.json();
            
            // Obtener o crear cesta
            if (!cestaId) {
                const createResponse = await fetch(CESTAS_API, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ activa: true, total: 0 })
                });
                const nuevaCesta = await createResponse.json();
                cestaId = nuevaCesta.id;
            }
            
            // Verificar si el producto ya está en la cesta
            const itemExistente = cestaItems.find(item => 
                item.r_producto_c_productoId === productoId
            );
            
            if (itemExistente) {
                // Actualizar cantidad
                const nuevaCantidad = itemExistente.cantidad + cantidad;
                await fetch(`${ITEMS_CESTA_API}/${itemExistente.id}`, {
                    method: 'PATCH',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        cantidad: nuevaCantidad,
                        subtotal: nuevaCantidad * producto.precio
                    })
                });
            } else {
                // Crear nuevo item
                await fetch(ITEMS_CESTA_API, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        r_cesta_c_cestaId: cestaId,
                        r_producto_c_productoId: productoId,
                        cantidad: cantidad,
                        precioUnitario: producto.precio,
                        subtotal: cantidad * producto.precio,
                        nombreProducto: producto.nombre,
                        imagenProducto: producto.imagen
                    })
                });
            }
            
            // Recargar cesta
            await cargarCesta();
            mostrarToast('¡Producto añadido a la cesta!');
            
        } catch (error) {
            console.error('Error:', error);
            mostrarToast('Error al añadir producto', true);
        }
    };
    
    // Recargar cesta (para otros fragmentos)
    window.tiendaRecargarCesta = cargarCesta;
    
    // ==========================================
    // BÚSQUEDA
    // ==========================================
    function initBusqueda() {
        const input = document.getElementById('busquedaInput');
        if (!input) return;
        
        input.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                const query = this.value.trim();
                if (query) {
                    window.location.href = `/catalogo?buscar=${encodeURIComponent(query)}`;
                }
            }
        });
    }
    
    // ==========================================
    // INICIALIZACIÓN
    // ==========================================
    function init() {
        initDropdowns();
        initBusqueda();
        cargarCategorias();
        cargarCesta();
    }
    
    // Ejecutar cuando el DOM esté listo
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
})();
```

### Paso 4: CSS (Dejar vacío)

Los estilos ya están en la Client Extension CSS.

### Paso 5: Configuración

En la pestaña **"Configuración"**, añade campos editables si lo deseas (opcional).

### Paso 6: Publicar

---

## Fragmento 2: CATÁLOGO DE PRODUCTOS

### Crear el Fragmento

Nombre: `tienda-catalogo`

### HTML

```html
<section class="tienda-catalogo">
    <div class="tienda-catalogo-container">
        <div class="tienda-catalogo-header">
            <h1 class="tienda-catalogo-title" 
                data-lfr-editable-id="catalogo-title" 
                data-lfr-editable-type="text">
                Nuestros Productos
            </h1>
            <div class="tienda-catalogo-filters">
                <select id="ordenar" class="tienda-select">
                    <option value="">Ordenar por...</option>
                    <option value="precio-asc">Precio: menor a mayor</option>
                    <option value="precio-desc">Precio: mayor a menor</option>
                    <option value="nombre">Nombre A-Z</option>
                </select>
            </div>
        </div>
        
        <div class="tienda-catalogo-grid" id="productosGrid">
            <div class="tienda-text-center tienda-mt-xl">
                <p>Cargando productos...</p>
            </div>
        </div>
        
        <div class="tienda-paginacion" id="paginacion"></div>
    </div>
</section>
```

### JavaScript

```javascript
(function() {
    const PRODUCTOS_API = '/o/c/productos';
    const CATEGORIAS_API = '/o/c/categorias';
    
    let productosActuales = [];
    let categoriaFiltro = null;
    let busquedaFiltro = null;
    let paginaActual = 1;
    const productosPorPagina = 12;
    
    // Obtener parámetros de URL
    function obtenerParametrosURL() {
        const params = new URLSearchParams(window.location.search);
        categoriaFiltro = params.get('categoria');
        busquedaFiltro = params.get('buscar');
    }
    
    // Formatear precio
    function formatearPrecio(precio) {
        return new Intl.NumberFormat('es-ES', {
            style: 'currency',
            currency: 'EUR'
        }).format(precio || 0);
    }
    
    // Cargar productos
    async function cargarProductos(pagina = 1) {
        const container = document.getElementById('productosGrid');
        if (!container) return;
        
        try {
            paginaActual = pagina;
            let url = `${PRODUCTOS_API}?page=${pagina}&pageSize=${productosPorPagina}`;
            
            // Filtrar por categoría
            if (categoriaFiltro) {
                url += `&filter=r_categoria_c_categoriaId eq ${categoriaFiltro}`;
            }
            
            // Filtrar por búsqueda
            if (busquedaFiltro) {
                url += `&search=${encodeURIComponent(busquedaFiltro)}`;
            }
            
            const response = await fetch(url, {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                productosActuales = data.items || [];
                renderizarProductos(productosActuales);
                renderizarPaginacion(data.totalCount || 0);
                
                // Actualizar título si hay filtro
                if (categoriaFiltro) {
                    actualizarTituloCategoria();
                } else if (busquedaFiltro) {
                    const titulo = document.querySelector('.tienda-catalogo-title');
                    if (titulo) titulo.textContent = `Resultados para "${busquedaFiltro}"`;
                }
            }
        } catch (error) {
            console.error('Error:', error);
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl" style="grid-column: 1 / -1;">
                    <p>Error al cargar productos</p>
                    <button onclick="location.reload()" class="tienda-btn-anadir" style="margin-top: 16px;">
                        Reintentar
                    </button>
                </div>
            `;
        }
    }
    
    async function actualizarTituloCategoria() {
        try {
            const response = await fetch(`${CATEGORIAS_API}/${categoriaFiltro}`);
            if (response.ok) {
                const categoria = await response.json();
                const titulo = document.querySelector('.tienda-catalogo-title');
                if (titulo) titulo.textContent = categoria.nombre;
            }
        } catch (error) {
            console.error('Error:', error);
        }
    }
    
    function renderizarProductos(productos) {
        const container = document.getElementById('productosGrid');
        
        if (productos.length === 0) {
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl" style="grid-column: 1 / -1;">
                    <div style="font-size: 3rem; margin-bottom: 16px;">🔍</div>
                    <h3>No se encontraron productos</h3>
                    <p style="color: var(--tienda-gray-500);">Prueba con otros filtros o categorías</p>
                    <a href="/catalogo" class="tienda-btn-anadir" style="display: inline-block; margin-top: 16px;">
                        Ver todos los productos
                    </a>
                </div>
            `;
            return;
        }
        
        container.innerHTML = productos.map(producto => `
            <article class="tienda-producto-card" onclick="window.location.href='/producto?id=${producto.id}'">
                <div class="tienda-producto-img-wrapper">
                    ${producto.destacado ? '<span class="tienda-producto-badge">Destacado</span>' : ''}
                    <img src="${producto.imagen || '/o/tienda-theme-css/static/img/placeholder.png'}" 
                         alt="${producto.nombre}" 
                         class="tienda-producto-img"
                         onerror="this.src='/o/tienda-theme-css/static/img/placeholder.png'">
                </div>
                <div class="tienda-producto-info">
                    <p class="tienda-producto-categoria">${producto.categoriaNombre || 'General'}</p>
                    <h3 class="tienda-producto-nombre">${producto.nombre}</h3>
                    <div class="tienda-producto-precio-wrapper">
                        <span class="tienda-producto-precio">${formatearPrecio(producto.precio)}</span>
                        <span class="tienda-producto-stock ${producto.stock > 0 ? '' : 'sin-stock'}">
                            ${producto.stock > 0 ? 'En stock' : 'Agotado'}
                        </span>
                    </div>
                </div>
            </article>
        `).join('');
    }
    
    function renderizarPaginacion(total) {
        const container = document.getElementById('paginacion');
        if (!container) return;
        
        const totalPaginas = Math.ceil(total / productosPorPagina);
        
        if (totalPaginas <= 1) {
            container.innerHTML = '';
            return;
        }
        
        let html = '<div class="tienda-paginacion-btns">';
        
        if (paginaActual > 1) {
            html += `<button onclick="window.tiendaCargarPagina(${paginaActual - 1})" class="tienda-paginacion-btn">← Anterior</button>`;
        }
        
        for (let i = 1; i <= totalPaginas; i++) {
            if (i === paginaActual) {
                html += `<span class="tienda-paginacion-actual">${i}</span>`;
            } else {
                html += `<button onclick="window.tiendaCargarPagina(${i})" class="tienda-paginacion-btn">${i}</button>`;
            }
        }
        
        if (paginaActual < totalPaginas) {
            html += `<button onclick="window.tiendaCargarPagina(${paginaActual + 1})" class="tienda-paginacion-btn">Siguiente →</button>`;
        }
        
        html += '</div>';
        container.innerHTML = html;
    }
    
    // Función global para paginación
    window.tiendaCargarPagina = cargarProductos;
    
    // Ordenar
    function initOrdenar() {
        const select = document.getElementById('ordenar');
        if (!select) return;
        
        select.addEventListener('change', function() {
            const orden = this.value;
            let productosOrdenados = [...productosActuales];
            
            switch(orden) {
                case 'precio-asc':
                    productosOrdenados.sort((a, b) => a.precio - b.precio);
                    break;
                case 'precio-desc':
                    productosOrdenados.sort((a, b) => b.precio - a.precio);
                    break;
                case 'nombre':
                    productosOrdenados.sort((a, b) => a.nombre.localeCompare(b.nombre));
                    break;
                default:
                    return;
            }
            
            renderizarProductos(productosOrdenados);
        });
    }
    
    // Inicialización
    function init() {
        obtenerParametrosURL();
        initOrdenar();
        cargarProductos();
    }
    
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
})();
```

---

## Fragmento 3: DETALLE DE PRODUCTO

### Crear el Fragmento

Nombre: `tienda-detalle-producto`

### HTML

```html
<section class="tienda-detalle">
    <div class="tienda-detalle-container">
        <div id="productoDetalle">
            <div class="tienda-text-center tienda-mt-xl">
                <p>Cargando producto...</p>
            </div>
        </div>
    </div>
</section>
```

### JavaScript

```javascript
(function() {
    const PRODUCTOS_API = '/o/c/productos';
    let productoActual = null;
    
    function obtenerIdProducto() {
        const params = new URLSearchParams(window.location.search);
        return params.get('id');
    }
    
    function formatearPrecio(precio) {
        return new Intl.NumberFormat('es-ES', {
            style: 'currency',
            currency: 'EUR'
        }).format(precio || 0);
    }
    
    async function cargarProducto() {
        const container = document.getElementById('productoDetalle');
        const productoId = obtenerIdProducto();
        
        if (!productoId) {
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl">
                    <div style="font-size: 3rem; margin-bottom: 16px;">❓</div>
                    <h2>Producto no encontrado</h2>
                    <a href="/catalogo" class="tienda-btn-anadir" style="display: inline-block; margin-top: 20px;">
                        Volver al catálogo
                    </a>
                </div>
            `;
            return;
        }
        
        try {
            const response = await fetch(`${PRODUCTOS_API}/${productoId}`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                productoActual = await response.json();
                renderizarProducto(productoActual);
            } else {
                throw new Error('Producto no encontrado');
            }
        } catch (error) {
            console.error('Error:', error);
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl">
                    <div style="font-size: 3rem; margin-bottom: 16px;">😕</div>
                    <h2>Error al cargar el producto</h2>
                    <a href="/catalogo" class="tienda-btn-anadir" style="display: inline-block; margin-top: 20px;">
                        Volver al catálogo
                    </a>
                </div>
            `;
        }
    }
    
    function renderizarProducto(producto) {
        const container = document.getElementById('productoDetalle');
        
        container.innerHTML = `
            <div class="tienda-detalle-grid">
                <!-- Imagen -->
                <div class="tienda-detalle-imagen">
                    <img src="${producto.imagen || '/o/tienda-theme-css/static/img/placeholder.png'}" 
                         alt="${producto.nombre}"
                         onerror="this.src='/o/tienda-theme-css/static/img/placeholder.png'">
                </div>
                
                <!-- Info -->
                <div class="tienda-detalle-info">
                    <div class="tienda-detalle-breadcrumb">
                        <a href="/">Inicio</a>
                        <span>/</span>
                        <a href="/catalogo">Catálogo</a>
                        ${producto.r_categoria_c_categoriaId ? `
                            <span>/</span>
                            <a href="/catalogo?categoria=${producto.r_categoria_c_categoriaId}">
                                ${producto.categoriaNombre || 'Categoría'}
                            </a>
                        ` : ''}
                    </div>
                    
                    <h1 class="tienda-detalle-nombre">${producto.nombre}</h1>
                    
                    <div class="tienda-detalle-precio">${formatearPrecio(producto.precio)}</div>
                    
                    <div class="tienda-detalle-stock ${producto.stock > 0 ? '' : 'sin-stock'}">
                        ${producto.stock > 0 
                            ? `✓ En stock (${producto.stock} disponibles)` 
                            : '✕ Producto agotado'}
                    </div>
                    
                    <div class="tienda-detalle-descripcion">
                        ${producto.descripcion || 'Sin descripción disponible.'}
                    </div>
                    
                    ${producto.stock > 0 ? `
                        <div class="tienda-detalle-cantidad">
                            <span class="tienda-cantidad-label">Cantidad:</span>
                            <div class="tienda-cantidad-control">
                                <button class="tienda-cantidad-btn" onclick="cambiarCantidad(-1)">−</button>
                                <input type="number" id="cantidadInput" class="tienda-cantidad-input" 
                                       value="1" min="1" max="${producto.stock}">
                                <button class="tienda-cantidad-btn" onclick="cambiarCantidad(1)">+</button>
                            </div>
                        </div>
                        
                        <div class="tienda-detalle-acciones">
                            <button class="tienda-btn-anadir" onclick="anadirACesta()">
                                🛒 Añadir a la Cesta
                            </button>
                        </div>
                    ` : `
                        <div class="tienda-detalle-acciones">
                            <button class="tienda-btn-anadir" disabled>
                                Producto no disponible
                            </button>
                        </div>
                    `}
                </div>
            </div>
        `;
    }
    
    // Funciones globales para los botones
    window.cambiarCantidad = function(delta) {
        const input = document.getElementById('cantidadInput');
        if (!input || !productoActual) return;
        
        let valor = parseInt(input.value) || 1;
        valor = Math.max(1, Math.min(productoActual.stock, valor + delta));
        input.value = valor;
    };
    
    window.anadirACesta = function() {
        if (!productoActual) return;
        
        const cantidad = parseInt(document.getElementById('cantidadInput').value) || 1;
        
        if (typeof window.tiendaAnadirACesta === 'function') {
            window.tiendaAnadirACesta(productoActual.id, cantidad);
        } else {
            alert('Error: La función del carrito no está disponible. Recarga la página.');
        }
    };
    
    // Inicialización
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', cargarProducto);
    } else {
        cargarProducto();
    }
})();
```

---

## Fragmento 4: PÁGINA DE CESTA

### Crear el Fragmento

Nombre: `tienda-cesta-pagina`

### HTML

```html
<section class="tienda-cesta-pagina">
    <div class="tienda-cesta-pagina-container">
        <h1 class="tienda-cesta-pagina-title">Tu Cesta de Compra</h1>
        <div id="cestaContenido">
            <div class="tienda-text-center tienda-mt-xl">
                <p>Cargando cesta...</p>
            </div>
        </div>
    </div>
</section>
```

### JavaScript

```javascript
(function() {
    const CESTAS_API = '/o/c/cestas';
    const ITEMS_API = '/o/c/itemcestas';
    const PEDIDOS_API = '/o/c/pedidos';
    const ITEMS_PEDIDO_API = '/o/c/itempedidos';
    
    let cestaActual = null;
    let itemsCesta = [];
    
    function formatearPrecio(precio) {
        return new Intl.NumberFormat('es-ES', {
            style: 'currency',
            currency: 'EUR'
        }).format(precio || 0);
    }
    
    async function cargarCestaCompleta() {
        const container = document.getElementById('cestaContenido');
        
        try {
            const response = await fetch(CESTAS_API + '?filter=activa eq true&pageSize=1', {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                
                if (data.items && data.items.length > 0) {
                    cestaActual = data.items[0];
                    await cargarItemsCesta(cestaActual.id);
                } else {
                    renderizarCestaVacia();
                }
            }
        } catch (error) {
            console.error('Error:', error);
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl">
                    <p>Error al cargar la cesta</p>
                    <button onclick="location.reload()" class="tienda-btn-anadir" style="margin-top: 16px;">
                        Reintentar
                    </button>
                </div>
            `;
        }
    }
    
    async function cargarItemsCesta(cestaId) {
        try {
            const response = await fetch(`${ITEMS_API}?filter=r_cesta_c_cestaId eq ${cestaId}`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                itemsCesta = data.items || [];
                
                if (itemsCesta.length > 0) {
                    renderizarCesta();
                } else {
                    renderizarCestaVacia();
                }
            }
        } catch (error) {
            console.error('Error:', error);
        }
    }
    
    function renderizarCesta() {
        const container = document.getElementById('cestaContenido');
        const subtotal = itemsCesta.reduce((sum, item) => sum + (item.subtotal || 0), 0);
        const envio = subtotal > 50 ? 0 : 4.99;
        const total = subtotal + envio;
        
        container.innerHTML = `
            <div class="tienda-cesta-pagina-grid">
                <div class="tienda-cesta-lista">
                    <div class="tienda-cesta-lista-header">
                        <span>Producto</span>
                        <span>Precio</span>
                        <span>Cantidad</span>
                        <span>Subtotal</span>
                        <span></span>
                    </div>
                    ${itemsCesta.map(item => `
                        <div class="tienda-cesta-lista-item">
                            <div class="tienda-cesta-lista-producto">
                                <img src="${item.imagenProducto || '/o/tienda-theme-css/static/img/placeholder.png'}" 
                                     alt="${item.nombreProducto}" 
                                     class="tienda-cesta-lista-img">
                                <div class="tienda-cesta-lista-nombre">
                                    <a href="/producto?id=${item.r_producto_c_productoId}">${item.nombreProducto || 'Producto'}</a>
                                </div>
                            </div>
                            <div class="tienda-cesta-lista-precio">${formatearPrecio(item.precioUnitario)}</div>
                            <div class="tienda-cesta-lista-cantidad">
                                <div class="tienda-cantidad-control">
                                    <button class="tienda-cantidad-btn" onclick="cambiarCantidadItem(${item.id}, -1)">−</button>
                                    <input type="number" value="${item.cantidad}" min="1" 
                                           class="tienda-cantidad-input" 
                                           onchange="actualizarCantidadItem(${item.id}, this.value)"
                                           data-precio="${item.precioUnitario}">
                                    <button class="tienda-cantidad-btn" onclick="cambiarCantidadItem(${item.id}, 1)">+</button>
                                </div>
                            </div>
                            <div class="tienda-cesta-lista-subtotal">${formatearPrecio(item.subtotal)}</div>
                            <button class="tienda-cesta-lista-eliminar" onclick="eliminarItem(${item.id})">
                                🗑️
                            </button>
                        </div>
                    `).join('')}
                </div>
                
                <div class="tienda-cesta-resumen">
                    <h2 class="tienda-cesta-resumen-title">Resumen del Pedido</h2>
                    
                    <div class="tienda-cesta-resumen-linea">
                        <span>Subtotal (${itemsCesta.length} productos)</span>
                        <span>${formatearPrecio(subtotal)}</span>
                    </div>
                    
                    <div class="tienda-cesta-resumen-linea">
                        <span>Envío</span>
                        <span>${envio === 0 ? 'Gratis' : formatearPrecio(envio)}</span>
                    </div>
                    
                    ${subtotal < 50 && subtotal > 0 ? `
                        <div class="tienda-cesta-resumen-linea" style="color: var(--tienda-success); font-size: 0.875rem;">
                            <span>¡Añade ${formatearPrecio(50 - subtotal)} más para envío gratis!</span>
                        </div>
                    ` : ''}
                    
                    <div class="tienda-cesta-resumen-total">
                        <span>Total</span>
                        <span class="tienda-cesta-resumen-total-valor">${formatearPrecio(total)}</span>
                    </div>
                    
                    <button class="tienda-btn-pagar" onclick="procesarPago()">
                        💳 Proceder al Pago
                    </button>
                    
                    <a href="/catalogo" style="display: block; text-align: center; margin-top: 16px; color: var(--tienda-primary);">
                        ← Seguir comprando
                    </a>
                </div>
            </div>
        `;
    }
    
    function renderizarCestaVacia() {
        const container = document.getElementById('cestaContenido');
        container.innerHTML = `
            <div class="tienda-text-center tienda-mt-xl">
                <div style="font-size: 4rem; margin-bottom: 20px;">🛒</div>
                <h2>Tu cesta está vacía</h2>
                <p style="color: var(--tienda-gray-500); margin-bottom: 20px;">
                    ¡Añade algunos productos para empezar!
                </p>
                <a href="/catalogo" class="tienda-btn-anadir" style="display: inline-block;">
                    Ver Catálogo
                </a>
            </div>
        `;
    }
    
    // Funciones globales
    window.cambiarCantidadItem = async function(itemId, delta) {
        const item = itemsCesta.find(i => i.id === itemId);
        if (!item) return;
        
        const nuevaCantidad = Math.max(1, item.cantidad + delta);
        await actualizarCantidadItem(itemId, nuevaCantidad);
    };
    
    window.actualizarCantidadItem = async function(itemId, cantidad) {
        const item = itemsCesta.find(i => i.id === itemId);
        if (!item) return;
        
        cantidad = Math.max(1, parseInt(cantidad) || 1);
        
        try {
            await fetch(`${ITEMS_API}/${itemId}`, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    cantidad: cantidad,
                    subtotal: cantidad * item.precioUnitario
                })
            });
            
            await cargarCestaCompleta();
            if (typeof window.tiendaRecargarCesta === 'function') {
                window.tiendaRecargarCesta();
            }
        } catch (error) {
            console.error('Error:', error);
        }
    };
    
    window.eliminarItem = async function(itemId) {
        if (!confirm('¿Eliminar este producto?')) return;
        
        try {
            await fetch(`${ITEMS_API}/${itemId}`, { method: 'DELETE' });
            await cargarCestaCompleta();
            if (typeof window.tiendaRecargarCesta === 'function') {
                window.tiendaRecargarCesta();
            }
        } catch (error) {
            console.error('Error:', error);
        }
    };
    
    window.procesarPago = async function() {
        if (!confirm('¿Confirmar pedido?')) return;
        
        try {
            const subtotal = itemsCesta.reduce((sum, item) => sum + (item.subtotal || 0), 0);
            const envio = subtotal > 50 ? 0 : 4.99;
            const total = subtotal + envio;
            const numeroPedido = 'PED-' + Date.now();
            
            // Crear pedido
            const pedidoResponse = await fetch(PEDIDOS_API, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    numeroPedido: numeroPedido,
                    fechaPedido: new Date().toISOString().split('T')[0],
                    total: total,
                    estado: { key: 'pendiente' }
                })
            });
            
            if (pedidoResponse.ok) {
                const pedido = await pedidoResponse.json();
                
                // Crear items del pedido
                for (const item of itemsCesta) {
                    await fetch(ITEMS_PEDIDO_API, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            r_pedido_c_pedidoId: pedido.id,
                            r_producto_c_productoId: item.r_producto_c_productoId,
                            cantidad: item.cantidad,
                            precioUnitario: item.precioUnitario,
                            subtotal: item.subtotal,
                            nombreProducto: item.nombreProducto,
                            imagenProducto: item.imagenProducto
                        })
                    });
                }
                
                // Vaciar cesta
                for (const item of itemsCesta) {
                    await fetch(`${ITEMS_API}/${item.id}`, { method: 'DELETE' });
                }
                
                await fetch(`${CESTAS_API}/${cestaActual.id}`, {
                    method: 'PATCH',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ activa: false })
                });
                
                alert('¡Pedido realizado con éxito!\nNúmero: ' + numeroPedido);
                window.location.href = '/pedidos';
            }
        } catch (error) {
            console.error('Error:', error);
            alert('Error al procesar el pedido. Por favor, intenta de nuevo.');
        }
    };
    
    // Inicialización
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', cargarCestaCompleta);
    } else {
        cargarCestaCompleta();
    }
})();
```

---

## Fragmento 5: LISTA DE PEDIDOS

### Crear el Fragmento

Nombre: `tienda-pedidos`

### HTML

```html
<section class="tienda-pedidos">
    <div class="tienda-pedidos-container">
        <h1 class="tienda-pedidos-title">Mis Pedidos</h1>
        <div class="tienda-pedidos-lista" id="pedidosLista">
            <div class="tienda-text-center tienda-mt-xl">
                <p>Cargando pedidos...</p>
            </div>
        </div>
    </div>
</section>
```

### JavaScript

```javascript
(function() {
    const PEDIDOS_API = '/o/c/pedidos';
    const ITEMS_PEDIDO_API = '/o/c/itempedidos';
    
    function formatearPrecio(precio) {
        return new Intl.NumberFormat('es-ES', {
            style: 'currency',
            currency: 'EUR'
        }).format(precio || 0);
    }
    
    function formatearFecha(fecha) {
        if (!fecha) return '-';
        return new Date(fecha).toLocaleDateString('es-ES', {
            year: 'numeric',
            month: 'long',
            day: 'numeric'
        });
    }
    
    function obtenerTextoEstado(estado) {
        if (!estado) return 'Desconocido';
        const key = estado.key || estado;
        const estados = {
            'pendiente': 'Pendiente',
            'procesando': 'Procesando',
            'enviado': 'Enviado',
            'entregado': 'Entregado',
            'cancelado': 'Cancelado'
        };
        return estados[key] || key;
    }
    
    function obtenerClaseEstado(estado) {
        if (!estado) return '';
        return estado.key || estado;
    }
    
    async function cargarPedidos() {
        const container = document.getElementById('pedidosLista');
        
        try {
            const response = await fetch(PEDIDOS_API + '?sort=dateCreated:desc', {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                const pedidos = data.items || [];
                
                if (pedidos.length > 0) {
                    // Cargar items de cada pedido
                    for (let pedido of pedidos) {
                        pedido.items = await cargarItemsPedido(pedido.id);
                    }
                    renderizarPedidos(pedidos);
                } else {
                    renderizarSinPedidos();
                }
            }
        } catch (error) {
            console.error('Error:', error);
            container.innerHTML = `
                <div class="tienda-text-center tienda-mt-xl">
                    <p>Error al cargar los pedidos</p>
                    <button onclick="location.reload()" class="tienda-btn-anadir" style="margin-top: 16px;">
                        Reintentar
                    </button>
                </div>
            `;
        }
    }
    
    async function cargarItemsPedido(pedidoId) {
        try {
            const response = await fetch(`${ITEMS_PEDIDO_API}?filter=r_pedido_c_pedidoId eq ${pedidoId}`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                return data.items || [];
            }
            return [];
        } catch (error) {
            return [];
        }
    }
    
    function renderizarPedidos(pedidos) {
        const container = document.getElementById('pedidosLista');
        
        container.innerHTML = pedidos.map(pedido => `
            <div class="tienda-pedido-card">
                <div class="tienda-pedido-header">
                    <div class="tienda-pedido-info">
                        <div class="tienda-pedido-info-item">
                            <span class="tienda-pedido-info-label">Nº Pedido</span>
                            <span class="tienda-pedido-info-value">${pedido.numeroPedido}</span>
                        </div>
                        <div class="tienda-pedido-info-item">
                            <span class="tienda-pedido-info-label">Fecha</span>
                            <span class="tienda-pedido-info-value">${formatearFecha(pedido.fechaPedido)}</span>
                        </div>
                        <div class="tienda-pedido-info-item">
                            <span class="tienda-pedido-info-label">Total</span>
                            <span class="tienda-pedido-info-value">${formatearPrecio(pedido.total)}</span>
                        </div>
                    </div>
                    <span class="tienda-pedido-estado ${obtenerClaseEstado(pedido.estado)}">
                        ${obtenerTextoEstado(pedido.estado)}
                    </span>
                </div>
                
                <div class="tienda-pedido-productos">
                    ${pedido.items.map(item => `
                        <div class="tienda-pedido-producto" onclick="window.location.href='/producto?id=${item.r_producto_c_productoId}'">
                            <img src="${item.imagenProducto || '/o/tienda-theme-css/static/img/placeholder.png'}" 
                                 alt="${item.nombreProducto}" 
                                 class="tienda-pedido-producto-img">
                            <div class="tienda-pedido-producto-info">
                                <div class="tienda-pedido-producto-nombre">${item.nombreProducto}</div>
                                <div class="tienda-pedido-producto-detalles">
                                    Cantidad: ${item.cantidad} × ${formatearPrecio(item.precioUnitario)}
                                </div>
                            </div>
                            <div class="tienda-pedido-producto-precio">${formatearPrecio(item.subtotal)}</div>
                        </div>
                    `).join('')}
                </div>
            </div>
        `).join('');
    }
    
    function renderizarSinPedidos() {
        const container = document.getElementById('pedidosLista');
        container.innerHTML = `
            <div class="tienda-text-center tienda-mt-xl">
                <div style="font-size: 4rem; margin-bottom: 20px;">📦</div>
                <h2>No tienes pedidos</h2>
                <p style="color: var(--tienda-gray-500); margin-bottom: 20px;">
                    ¡Haz tu primera compra ahora!
                </p>
                <a href="/catalogo" class="tienda-btn-anadir" style="display: inline-block;">
                    Ver Catálogo
                </a>
            </div>
        `;
    }
    
    // Inicialización
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', cargarPedidos);
    } else {
        cargarPedidos();
    }
})();
```

---

## Fragmento 6: FOOTER

### Crear el Fragmento

Nombre: `tienda-footer`

### HTML

```html
<footer class="tienda-footer">
    <div class="tienda-footer-container">
        <div class="tienda-footer-grid">
            <div class="tienda-footer-col">
                <h4 class="tienda-footer-col-title" 
                    data-lfr-editable-id="footer-title" 
                    data-lfr-editable-type="text">
                    MiTienda
                </h4>
                <p data-lfr-editable-id="footer-desc" 
                   data-lfr-editable-type="rich-text">
                    Tu tienda de confianza para los mejores productos tecnológicos.
                </p>
            </div>
            
            <div class="tienda-footer-col">
                <h4 class="tienda-footer-col-title">Categorías</h4>
                <ul class="tienda-footer-links" id="footerCategorias">
                    <li>Cargando...</li>
                </ul>
            </div>
            
            <div class="tienda-footer-col">
                <h4 class="tienda-footer-col-title">Mi Cuenta</h4>
                <ul class="tienda-footer-links">
                    <li><a href="/pedidos">Mis Pedidos</a></li>
                    <li><a href="/cesta">Mi Cesta</a></li>
                    <li><a href="/catalogo">Catálogo</a></li>
                </ul>
            </div>
            
            <div class="tienda-footer-col">
                <h4 class="tienda-footer-col-title">Contacto</h4>
                <ul class="tienda-footer-links">
                    <li data-lfr-editable-id="footer-email" data-lfr-editable-type="text">
                        info@mitienda.com
                    </li>
                    <li data-lfr-editable-id="footer-phone" data-lfr-editable-type="text">
                        +34 900 123 456
                    </li>
                </ul>
            </div>
        </div>
        
        <div class="tienda-footer-bottom">
            <p data-lfr-editable-id="footer-copyright" data-lfr-editable-type="text">
                © 2024 MiTienda. Todos los derechos reservados.
            </p>
        </div>
    </div>
</footer>
```

### JavaScript

```javascript
(function() {
    async function cargarCategoriasFooter() {
        const container = document.getElementById('footerCategorias');
        if (!container) return;
        
        try {
            const response = await fetch('/o/c/categorias?pageSize=5&filter=activa eq true', {
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                }
            });
            
            if (response.ok) {
                const data = await response.json();
                const categorias = data.items || [];
                
                if (categorias.length > 0) {
                    container.innerHTML = categorias.map(cat => `
                        <li><a href="/catalogo?categoria=${cat.id}">${cat.nombre}</a></li>
                    `).join('');
                } else {
                    container.innerHTML = '<li><a href="/catalogo">Ver catálogo</a></li>';
                }
            }
        } catch (error) {
            container.innerHTML = '<li><a href="/catalogo">Ver catálogo</a></li>';
        }
    }
    
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', cargarCategoriasFooter);
    } else {
        cargarCategoriasFooter();
    }
})();
```

---

## ✅ Checklist de Verificación

- [ ] Conjunto "Tienda Fragmentos" creado
- [ ] Fragmento tienda-navbar creado y publicado
- [ ] Fragmento tienda-catalogo creado y publicado
- [ ] Fragmento tienda-detalle-producto creado y publicado
- [ ] Fragmento tienda-cesta-pagina creado y publicado
- [ ] Fragmento tienda-pedidos creado y publicado
- [ ] Fragmento tienda-footer creado y publicado
- [ ] Todos los fragmentos probados en vista previa

---

## 🔗 Siguiente Fase

Una vez completada esta fase, continúa con:
→ **[FASE 4: Master Page y Páginas](./FASE-4-MASTER-PAGE-Y-PAGINAS.md)**
