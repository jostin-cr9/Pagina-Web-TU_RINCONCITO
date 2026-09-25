# Cambios: barra lateral de la intranet

La navegación de la intranet se mostraba como una lista de enlaces sin estilo arriba de la página.
Esto pasaba porque todas las páginas cargan `css/style.css` y `js/script.js`, pero esos archivos no existen en el repositorio,
así que las clases `sidebar`, `topbar`, `intranet-main`, etc. no tenían ningún estilo.

Se rehízo la barra lateral y el encabezado usando **solo clases de Bootstrap 5.3** (sin CSS propio ni JavaScript adicional):

- **En computadora:** barra lateral oscura fija a la izquierda, que se mantiene visible al hacer scroll. La página actual se marca en azul y "Cerrar sesión" queda al final, en rojo.
- **En celular:** la barra se oculta y se abre con el botón ☰ como menú deslizable (componente *offcanvas* de Bootstrap).

## Páginas modificadas

Se modificaron las 9 páginas de la intranet, siempre en las mismas 3 zonas. `index.html` y `login.html` no se tocaron.

| Página | 1. Barra lateral | 2. Encabezado y `<main>` | 3. Cierre agregado |
|---|---|---|---|
| `dashboard.html` | líneas 11–39 | 41–51 | línea 144 |
| `productos.html` | 11–39 | 41–51 | 164 |
| `inventario.html` | 11–39 | 41–51 | 142 |
| `movimientos.html` | 11–39 | 41–51 | 148 |
| `ventas.html` | 11–39 | 41–51 | 116 |
| `cliente.html` | 10–38 | 40–50 | 109 |
| `proveedores.html` | 11–39 | 41–51 | 121 |
| `reportes.html` | 11–39 | 41–51 | 90 |
| `usuarios.html` | 10–38 | 40–50 | 88 |

En `cliente.html` y `usuarios.html` los números van una línea antes porque esas páginas no tienen el `<link>` a `style.css` en el `<head>`.

## Qué cambió en cada zona

### 1. Barra lateral

- `<body class="intranet">` pasó a ser `<body class="bg-body-tertiary">`.
- Se agregó un contenedor `<div class="row g-0 min-vh-100 ...">` que divide la página en dos columnas: menú y contenido.
- `<aside class="sidebar">` se reemplazó por una columna oscura (`col-lg-3 col-xl-2 bg-dark`) con un `offcanvas-lg` dentro:
  fijo a la izquierda en computadora y menú deslizable en celular.
- El logo "TU RINCONCITO / Intranet de bodega" va en el `offcanvas-header`, junto a un botón ✕ que solo aparece en celular.
- Los enlaces usan `nav nav-pills flex-column`. La página actual se marca con `active`.
- "Cerrar sesión" quedó separado al final del menú, en rojo (`link-danger`).
- Se quitó `<div class="overlay-sidebar">`, porque Bootstrap ya pone su propio fondo oscuro detrás del menú en celular.
- **Enlace corregido:** `clientes.html` → `cliente.html` (el archivo que existe realmente).

### 2. Encabezado y `<main>`

- `<div class="intranet-main">` pasó a ser `<div class="col-lg-9 col-xl-10">`.
- `<header class="topbar">` ahora usa solo clases de Bootstrap: fondo blanco, borde inferior y fijo arriba (`sticky-top`).
- El botón ☰ abre el menú con `data-bs-toggle="offcanvas"`, así que no depende de `script.js`.
- El título `<h1>` ahora tiene `class="h4 mb-0"`.
- `<main class="content">` pasó a ser `<main class="p-3 p-md-4">`.

### 3. Cierre

- Se agregó un `</div>` después del `</main>` y su `</div>`, para cerrar el contenedor nuevo.

## Lo que no se tocó

- El contenido de cada página: tablas, tarjetas, formularios y modales.
- Los `<link>` a `css/style.css` y los `<script>` a `js/script.js`.

## Pendiente

Algunos elementos usan clases que venían de `style.css` y hoy no tienen estilo: `btn-verde`, `stat-card`, `reporte-card`.
Por ejemplo, el botón "Nuevo producto" se ve sin color. Se pueden cambiar por clases de Bootstrap como `btn-success`.
