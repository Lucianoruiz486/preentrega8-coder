# Simulador de Ventas - Validador de Stock

Simulador en JavaScript para un negocio de indumentaria deportiva. Es la **Pre-Entrega 8 (Storage)**: el catálogo se guarda en `localStorage`, así que **los cambios siguen ahí después de recargar la página** (F5). Toda la interacción pasa por el DOM.

## Estructura del repositorio
```
preentrega8-coder/
├── index.html      # estructura de la página; enlaza el CSS y el JS (con defer)
├── README.md
├── css/
│   └── style.css   # estilos y layout
└── js/
    └── main.js     # clase Producto, storage, renderizado y eventos
```

## Cómo ejecutarlo
1. Descargá o cloná el repositorio.
2. Abrí `index.html` con doble clic. No hace falta instalar nada.

## Cómo comprobar la persistencia
1. Agregá un producto, vendé unidades o eliminá alguno.
2. Recargá la página con **F5**: los cambios siguen en pantalla.
3. Para ver los datos guardados: **F12 → pestaña Application → Local Storage → clave `productosStock`**.
4. **Restablecer catálogo** borra lo guardado y vuelve a los productos iniciales. **Vaciar catálogo** guarda una lista vacía.

## Cómo se sincroniza el estado
Cada acción (agregar, vender, descuento, eliminar, vaciar) sigue el mismo flujo: se actualiza el array, se guarda en `localStorage` con `JSON.stringify` y se vuelve a dibujar la vista. Al abrir la página, `cargarProductos()` lee lo guardado con `JSON.parse` y vuelve a crear cada objeto como `Producto` (porque `JSON.parse` devuelve objetos sin métodos).

## Criterios de la consigna y dónde se cumplen
| Criterio | Dónde está en `js/main.js` |
|---|---|
| Persistencia y recuperación (30%) | `guardarProductos()` (`setItem` + `JSON.stringify`) y `cargarProductos()` (`getItem` + `JSON.parse`); `removeItem` en `restablecerCatalogo()` |
| Actualización del estado en eventos (25%) | `agregarProducto()`, `venderUnidad()`, `aplicarDescuentoDiez()`, `eliminarProducto()` y `vaciarCatalogo()`: actualizan el array, guardan y vuelven a renderizar |
| Renderizado del DOM y eventos (20%) | `renderizarProductos()` con template strings e `innerHTML`; eventos `click`, `keydown`, `keyup` y `change` |
| Estructura del repositorio (10%) | `index.html` en la raíz, `css/style.css` y `js/main.js` enlazados |
| Operadores modernos y destructuring (15%) | **Ternario:** `venderUnidad()`. **`??`:** `cargarProductos()` (primera vez, sin nada guardado). **`?.`:** `actualizarVista()`. **Destructuring:** `cargarProductos()`, `obtenerNuevoId()` y el evento click de las tarjetas |
