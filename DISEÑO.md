# Lanzamiento de producto: brief de diseño

Plantilla `landing-producto` creada el 29/10/2026 a partir de `una-pagina` con `php artisan plantillas:nueva` y
rediseñada entera. Este fichero se queda en el repo: es lo que lee quien (persona o agente) la rediseñe después.

## Brief

- **Para quién**: marcas y artesanos que venden **un producto estrella** (sectores `producto`, `lanzamiento`, `marca`,
  `tienda-online`, `artesano-producto`). Quien entra quiere ver el producto en grande, saber cuánto cuesta, qué tiene
  de especial y cómo comprarlo, sin buscar.
- **Qué tiene que conseguir**: la compra (botón de cabecera con precio, sello en la portada, banda «Compra» con
  tienda online y WhatsApp). Secundario: escribir o pasar por el local.
- **Tono y estilo** (`impactante`): rotundo, gráfico y directo, como una página de lanzamiento de una marca de
  diseño. Sí: color pleno a sangre, el nombre del producto gigante, ficha técnica en monoespaciada. No: la caja
  centrada estrecha con tarjetas blancas, el hero centrado con imagen con halo de `una-pagina`, degradados.
- **Paleta de ejemplo**: primario `#19e0c5` (verde agua eléctrico, color de marca), acento `#0b7d70` (verde agua
  hondo, detalles sobre hueso), fondo `#0b0c0c` (negro), texto `#f2efe8` (hueso). Tres bandas: `.banda-negra`
  (fondo + texto), `.banda-hueso` (los mismos invertidos) y `.banda-color` (primario + la letra que mejor contraste,
  `--c-sobre-primario`, calculada en `Base.astro` entre fondo y texto). Líneas con `--linea` (currentColor al 18 %).
  Aguanta que el cliente cambie los cuatro, también un fondo claro.
- **Tipografía**: del sistema. Titulares en mayúsculas a 900 (`--fuente-titulos`: Franklin Gothic Heavy/Demi,
  Segoe UI Black, Helvetica Neue…), interletrado −0,02 em y altura de línea 0,92; hero de 2,6 a 6,75 rem; nombre del
  producto en hueco (`.hueco`, solo contorno) a casi todo el ancho. Antetítulos, botones, cabecera y ficha en
  monoespaciada (`--fuente-mono`) en mayúsculas espaciadas; antetítulo con una raya de color delante.
- **Forma**: esquinas rectas (radio 0), botones rectangulares de 48 px con flecha, bordes de 2 px, líneas finas;
  el único círculo es el sello del precio, girado.
- **Ritmo de bandas**: portada (foto a sangre + velo negro, nombre gigante) → cinta en color con los puntos fuertes →
  negra (características) → 50/50 foto a sangre | ficha en color → negra (galería, mosaico de borde a borde) → color
  (modelos) → hueso 50/50 con foto a sangre (cómo se usa) → negra (comparativa) → hueso (opiniones) → negra
  (preguntas) → color 50/50 con foto (compra) → partida hueso | negra (contacto) → pie negro con el nombre gigante
  en el color de marca.
- **Cabecera**: fija a todo el ancho; transparente sobre la portada y negra al bajar (script pequeño en línea; sin
  JavaScript, siempre negra). Botón «Comprar · precio». Menú móvil `details/summary` hasta 1100 px.

## Apartados

| id | Qué enseña | Lista propia |
|---|---|---|
| `hero` | Foto a sangre a 92 svh, titular, texto, dos botones, sello con `precio`/`precio_nota`, `producto` gigante hueco y cinta deslizante | `items` (titulo) |
| `caracteristicas` | Titular + texto; rejilla 1/2/4 columnas con número e icono; fila 50/50 a sangre foto de detalle + ficha técnica en color | `caracteristicas` (titulo, texto, icono), `ficha` (titulo, texto) |
| `galeria` | Mosaico de borde a borde sin márgenes (grande 2×2, pequeñas y anchas; sin huecos con cualquier número) | `galeria` (rutas) |
| `variantes` | Columnas pegadas con líneas sobre color pleno; el destacado en negro; precio gigante y botón | `variantes` (nombre, texto, precio, imagen, etiqueta, destacado, url) |
| `proceso` | 50/50: foto a sangre a la izquierda, pasos con números huecos a la derecha | `items` (titulo, texto) |
| `comparativa` | Tabla a todo el ancho; columna propia resaltada; «sí»/«no» como marca y aspa | `items` (titulo, propio, otros) |
| `opiniones` | Columnas altas con comilla enorme en el acento | `testimonios` (texto, autor, cargo) |
| `preguntas` | Titular fijo y acordeón en filas con «+» en cuadro de color | `preguntas` (pregunta, respuesta) |
| `compra` | 50/50 en color: titular, precio gigante, botones, nota y garantías; foto a sangre | `items` (titulo, icono) |
| `contacto` | Banda partida: contacto directo en hueso y formulario en negro | — |
| `texto` | Genérico: con foto, 50/50 a sangre; sin foto, titular y párrafos en dos columnas | `items` (titulo, texto, icono) |

## Fotos (`fotos.json`, 13)
Portada (cuchillo en diagonal sobre pizarra negra con mucho aire a la izquierda para el texto), detalle del filo,
seis de galería (cenital con perejil, mango de olivo, acero al rojo en la forja, tomate laminado, banco del taller,
estuche), tres modelos sobre fondo gris liso, manos picando cebolla (sin cara) y la de compra (cuchillo en vertical
sobre negro). Sin texto legible, sin logotipos, sin personas reconocibles.

## Qué no hacer
- Nada de secciones encajonadas en una columna estrecha ni tarjetas blancas flotando sobre gris.
- Nada de esquinas redondeadas ni degradados de colores: la fuerza está en el color pleno y el negro.
- Nada de cifras ni precios en los componentes: todo sale de `site.yaml`.
