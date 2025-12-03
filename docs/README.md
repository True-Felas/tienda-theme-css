# 🛒 Guía Completa: Tienda Online con Liferay

## Descripción del Proyecto

Este proyecto implementa una **tienda online completa** utilizando las capacidades nativas de Liferay:
- **Objetos Personalizados** para el modelo de datos
- **Client Extensions** para los estilos CSS
- **Fragmentos** para los componentes de UI
- **Master Pages** para la estructura de páginas

---

## 📋 Índice de Fases

| Fase | Descripción | Estado |
|------|-------------|--------|
| [FASE 1](./FASE-1-OBJETOS-PERSONALIZADOS.md) | Crear Objetos Personalizados | 📝 Por hacer |
| [FASE 2](./FASE-2-CLIENT-EXTENSION-CSS.md) | Client Extension Theme CSS | ✅ Completado |
| [FASE 3](./FASE-3-FRAGMENTOS.md) | Fragmentos Personalizados | 📝 Por hacer |
| [FASE 4](./FASE-4-MASTER-PAGE-Y-PAGINAS.md) | Master Page y Páginas | 📝 Por hacer |
| [FASE 5](./FASE-5-PRUEBAS-Y-DATOS.md) | Pruebas y Datos de Ejemplo | 📝 Por hacer |

---

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │   Navbar    │  │  Catálogo   │  │   Footer    │          │
│  │ (Fragmento) │  │ (Fragmento) │  │ (Fragmento) │          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │  Detalle    │  │    Cesta    │  │   Pedidos   │          │
│  │ (Fragmento) │  │ (Fragmento) │  │ (Fragmento) │          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
├─────────────────────────────────────────────────────────────┤
│                    CAPA DE ESTILOS                          │
│              ┌──────────────────────┐                       │
│              │  Theme CSS Client    │                       │
│              │     Extension        │                       │
│              └──────────────────────┘                       │
├─────────────────────────────────────────────────────────────┤
│                    CAPA DE DATOS                            │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐               │
│  │ Categoría │  │ Producto  │  │   Cesta   │               │
│  │  (Objeto) │  │  (Objeto) │  │  (Objeto) │               │
│  └───────────┘  └───────────┘  └───────────┘               │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐               │
│  │ItemCesta  │  │  Pedido   │  │ItemPedido │               │
│  │  (Objeto) │  │  (Objeto) │  │  (Objeto) │               │
│  └───────────┘  └───────────┘  └───────────┘               │
├─────────────────────────────────────────────────────────────┤
│                      API REST                               │
│         /o/c/categorias  /o/c/productos  /o/c/cestas       │
│         /o/c/itemcestas  /o/c/pedidos    /o/c/itempedidos  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 Inicio Rápido

### Requisitos Previos

- Liferay DXP/Portal 7.4+ en funcionamiento
- Acceso de Administrador
- Blade CLI instalado (para compilar client extensions)

### Paso 1: Desplegar el Theme CSS

```bash
cd client-extensions/tienda-theme-css
blade gw clean deploy
```

### Paso 2: Crear los Objetos

Sigue la [FASE 1](./FASE-1-OBJETOS-PERSONALIZADOS.md) para crear:
- Categoría
- Producto
- Cesta
- ItemCesta
- Pedido
- ItemPedido

### Paso 3: Crear los Fragmentos

Sigue la [FASE 3](./FASE-3-FRAGMENTOS.md) para crear los 6 fragmentos en el portal.

### Paso 4: Crear las Páginas

Sigue la [FASE 4](./FASE-4-MASTER-PAGE-Y-PAGINAS.md) para:
- Crear la Master Page
- Crear las páginas del sitio
- Configurar la navegación

### Paso 5: Añadir Datos y Probar

Sigue la [FASE 5](./FASE-5-PRUEBAS-Y-DATOS.md) para:
- Añadir categorías de ejemplo
- Añadir productos de ejemplo
- Probar todas las funcionalidades

---

## 📁 Estructura de Archivos

```
tienda-theme-css/
├── client-extension.yaml       # Configuración de la client extension
├── src/
│   ├── css/
│   │   ├── clay.scss           # Importa Clay Atlas
│   │   ├── main.scss           # Archivo principal
│   │   └── _custom.scss        # Estilos personalizados
│   └── img/
│       └── placeholder.png     # Imagen por defecto
└── docs/
    ├── README.md               # Este archivo
    ├── FASE-1-OBJETOS-PERSONALIZADOS.md
    ├── FASE-2-CLIENT-EXTENSION-CSS.md
    ├── FASE-3-FRAGMENTOS.md
    ├── FASE-4-MASTER-PAGE-Y-PAGINAS.md
    └── FASE-5-PRUEBAS-Y-DATOS.md
```

---

## 🎨 Personalización

### Cambiar Colores

Edita las variables en `src/css/_custom.scss`:

```scss
:root {
    --tienda-primary: #0066cc;      // Color principal
    --tienda-secondary: #ff6600;    // Color de acción
    --tienda-success: #28a745;      // Color de éxito
    --tienda-danger: #dc3545;       // Color de error
}
```

Luego recompila:
```bash
blade gw clean deploy
```

### Cambiar el Logo

En el fragmento `tienda-navbar`, edita el campo editable "Logo Text" o reemplázalo por una imagen.

### Añadir Nuevas Páginas

1. Crea una nueva página usando la Master Page existente
2. Añade los fragmentos necesarios
3. Configura la URL amigable

---

## 🔧 Comandos Útiles

```bash
# Compilar y desplegar el theme CSS
cd client-extensions/tienda-theme-css
blade gw clean deploy

# Ver logs de Liferay
tail -f bundles/logs/liferay.*.xml

# Limpiar caché de Liferay
# En la UI: Panel de Control → Servidor → Limpiar Caché
```

---

## ❓ FAQ

### ¿Puedo usar este proyecto en Liferay CE?
Sí, los Objetos Personalizados y Client Extensions están disponibles en Liferay 7.4 CE.

### ¿Cómo añado autenticación?
Los objetos ya están vinculados al usuario actual a través del campo `creator`. Para restringir acceso, configura los permisos de los objetos.

### ¿Puedo integrar con un sistema de pagos real?
Sí, puedes extender el fragmento de la cesta para integrar con Stripe, PayPal, etc. usando sus SDKs de JavaScript.

### ¿Cómo añado más campos a los productos?
1. Ve a Panel de Control → Objetos → Producto
2. Añade los campos que necesites
3. Actualiza el fragmento para mostrarlos

---

## 📞 Soporte

Si tienes problemas:
1. Revisa la sección de "Solución de Problemas" en cada fase
2. Consulta la consola del navegador (F12) para errores JavaScript
3. Revisa los logs de Liferay

---

## 📄 Licencia

Este proyecto es de uso educativo y puede ser modificado libremente.

---

**Versión:** 1.0  
**Última actualización:** Diciembre 2025  
**Compatibilidad:** Liferay 7.4+
