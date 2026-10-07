# Fundación Social Country Club de Barranquilla · Sitio web

Carpeta lista para entregar al programador. Es un sitio estático (HTML + CSS + JS, sin dependencias ni compilación) aprobado como diseño con el cliente. Sirve como maqueta funcional de referencia para montar el sitio definitivo.

## Cómo verlo

Abrir `index.html` en el navegador, o servir la carpeta:

```bash
npx http-server . -p 5180 -c-1
```

y entrar a http://localhost:5180

## Estructura

```
website/
├── index.html        Todo el contenido (una sola página con rutas por #hash)
├── css/styles.css    Estilos
├── js/main.js        Navegación, animaciones, carruseles, filtros y formularios
└── assets/
    ├── fonts/        Axiforma (Regular, Medium, SemiBold, Bold, ExtraBold)
    ├── img/          Fotografías (WebP)
    ├── video/        hero-001.mp4, hero-002.mp4, hero-005.mp4
    ├── aliados/      Logos de aliados
    ├── pago/         Logos de medios de pago, sin fondo
    └── logo-*.png    Logo de la Fundación (color, blanco, color sobre oscuro, símbolo)
```

## Páginas (rutas)

Cada página es un bloque `<div data-page="…">` dentro de `index.html`. La función `route()` en `js/main.js` muestra el que corresponde al `#hash`.

| Ruta | Página |
|---|---|
| `#inicio` | Inicio |
| `#nosotros` | Quiénes somos |
| `#programas` | Nuestros programas (filtro lateral por bloque y línea) |
| `#impacto` | Nuestro impacto |
| `#apoya` | Sé parte |
| `#noticias` | Noticias (carrusel de destacadas + listado) |
| `#noticia`, `#noticia-emprendiendo`, `#noticia-vitrina`, `#noticia-vivienda`, `#noticia-auxilios`, `#noticia-aliados` | Detalle de cada noticia |
| `#contacto` | Contacto |

En el sitio definitivo conviene pasar cada ruta a una URL real (`/quienes-somos`, `/programas`, etc.) y las noticias a un gestor de contenidos.

## Marca

- Colores: azul `#1D4C65`, verde `#279A68`, naranja `#F6A233`, azul profundo `#0F2A38`, fondo `#FAF5F2`.
- Tipografía: Axiforma (Kastelov). **Es una fuente comercial: confirmar que la licencia de la Fundación cubre uso web antes de publicar.** Los archivos están en TTF; conviene convertirlos a WOFF2.
- El logo del header cambia según el fondo: color sobre fondo claro, versión con texto blanco sobre azul, blanco sobre video y sobre verde.

## Comportamientos a conservar

- **Color de fondo por sección:** cada `<section data-tone="light|sand|green|navy|deep">` cambia las variables de color del `body` al pasar por el centro de la pantalla (`updateTone()`).
- **Una sección por pantalla** en escritorio (`min-height:100svh`) con `scroll-snap` suave.
- **Textos que se encienden palabra por palabra** al hacer scroll, aparición de bloques (`.reveal`) y conteo animado de cifras (`[data-count]`).
- **Carruseles:** líneas de trabajo y fotos de impacto (Inicio), cifras con puntos y avance automático e historias en video vertical (Impacto), noticias destacadas (Noticias).
- **Programas:** los datos están en el arreglo `PROGRAMS` de `js/main.js`; las tarjetas se generan con `progCard()` y cada una despliega su ficha.
- Todo respeta la preferencia del sistema "reducir movimiento".

## Lo que hay que conectar o reemplazar antes de publicar

### Contenido de ejemplo (inventado para mostrar el diseño)

- **Cifras:** todas las de Inicio (+300, +165, +20) y de Nuestro impacto (+180, +120, +90, +40, +120, +5) son de ejemplo. Reales: 13 programas, 5 líneas de trabajo y 20 mujeres de Salgar.
- **Noticias:** los seis textos, sus citas, cifras, autor y tiempo de lectura son de ejemplo. Cada una lo indica con la línea "Contenido de ejemplo…".
- **Historias en video (Impacto):** títulos de ejemplo y videos reutilizados del hero.
- **Misión, visión y propósito:** se resumieron respecto al documento de la Fundación; validar con el cliente.
- **Datos para donar (Sé parte):** el número de cuenta y el NIT están en ceros a propósito. Reemplazar por los reales.
- **Fotografías:** imágenes de referencia generadas; reemplazar por fotos reales de la Fundación.

### Integraciones

- **Formularios** (Contacto y Sé parte): no envían datos. `wireForm()` en `js/main.js` solo muestra un aviso. Conectar a correo o CRM.
- **Mapa** (Contacto): `iframe` de Google Maps apuntando a "Country Club de Barranquilla". Confirmar la dirección exacta de la Fundación.
- **WhatsApp:** el botón flotante no tiene número real.
- **Redes sociales:** los íconos del footer y de Contacto apuntan a `#`.
- **Datos de contacto:** faltan teléfono, correo y horarios (se quitaron de la página hasta tenerlos).
- **Botón Donar:** lleva a Sé parte; no hay pasarela de pago. Los logos de medios de pago son informativos.
- **Logo de Banco Caja Social:** falta el archivo; los demás están en `assets/pago/`.

### Secciones y páginas ocultas (siguen en el HTML)

- Página **Historias** (`data-page="historias"`): fuera del menú y de las rutas.
- Inicio: banda final de llamado a la acción.
- Nuestro impacto: "Nuestros números" e "Impacto por línea" (sus datos pasaron al carrusel de cifras).

Se ocultan con el atributo `hidden`; basta quitarlo para volver a mostrarlas (y, en el caso de Historias, agregar `"historias"` al arreglo `PAGES`).

### Solo del prototipo (quitar en producción)

- La pastilla inferior izquierda "Prototipo · Datos pendientes" (`.protopill`).
- La librería de código QR que se carga desde cdnjs para la tarjeta de WhatsApp: decidir si se mantiene o se sirve localmente.

## Rendimiento

- `assets/video/hero-001.mp4` pesa 13 MB y `hero-005.mp4` 9 MB: comprimir y servir también en WebM.
- Las imágenes ya están en WebP a 1400–2200 px.
- Total de la carpeta: unos 31 MB, casi todo video.

## Historial

El diseño se iteró como prototipo en `../prototipo/` (versiones anteriores y archivo único). La referencia vigente es esta carpeta `website/`.
