# Plantilla «Lanzamiento de producto» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **impactante**.
Una sola página para presentar y vender **un producto**: color pleno de marca + negro, bandas a todo el ancho.
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores`. `primario` = color de marca (bandas de color pleno, botones, sello del precio, cinta); `acento` = detalles sobre las bandas claras (rayas, números, comillas); `fondo` = negro de las bandas oscuras, cabecera y pie; `texto` = letra sobre negro y fondo de las bandas claras («hueso»). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y calcula la letra que va sobre el primario y el acento (`--c-sobre-primario`, `--c-sobre-acento`), así que cualquier color de marca se lee.
- **Tipografías y aspecto general**: `src/styles/global.css` (variables `--fuente-texto`, `--fuente-titulos`, `--fuente-mono`; bandas `.banda-negra`, `.banda-hueso`, `.banda-color`; botones `.btn`/`.btn-sec`; cabecera y pie). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` y se referencian con ruta absoluta (`/fotos/hero.jpg`). Mientras una foto no exista, `Imagen.astro` pinta su respaldo de `public/placeholders/` (el de su nombre o el genérico). Las fotos de partida se generan desde `fotos.json`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial y nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `hero.astro`: foto a sangre, titular, sello con `precio` y `precio_nota`, botones, `producto` (nombre gigante y hueco; si falta, el del negocio) y la cinta con `items[].titulo`.
- `caracteristicas` → `caracteristicas.astro`: `caracteristicas[]` (titulo, texto, icono) en rejilla; `imagen` de detalle y `ficha[]` (titulo = dato, texto = valor) con `titulo_ficha` en fila 50/50 a sangre.
- `galeria` → `galeria.astro`: `galeria[]` en mosaico de borde a borde.
- `variantes` → `variantes.astro`: `variantes[]` (nombre, texto, precio, imagen, etiqueta, destacado, url) en columnas sobre color pleno; botón con el texto de `cta` y destino `url` del modelo, si no `cta.url`, si no WhatsApp.
- `proceso` → `proceso.astro`: «cómo se usa», `items[]` (titulo, texto) con números huecos y `imagen` a sangre.
- `comparativa` → `comparativa.astro`: tabla con `columna_propia`, `columna_otros` e `items[]` (titulo, propio, otros); «sí»/«no» salen como marca y aspa.
- `opiniones` → `opiniones.astro`: `testimonios[]` (texto, autor, cargo) en columnas.
- `preguntas` → `preguntas.astro`: acordeón `details/summary`; sin preguntas no se pinta.
- `compra` → `compra.astro`: titular, `precio` gigante, texto, `cta` (tienda online) y `cta_secundario` (WhatsApp), `nota`, `items[]` (titulo, icono) de garantías e `imagen` a sangre.
- `contacto` → `contacto.astro`: banda partida con el contacto directo y el formulario.
- `texto` → `texto.astro`: genérico para apartados nuevos (`tipo: texto`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, precios, fotos**: solo en `site.yaml`. Precios siempre entre comillas (`"149 €"`). Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista; máximo 24 elementos.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: un id propio en `site.yaml` con `tipo:` = el diseño de otra sección (o `texto`); `src/pages/index.astro` la recoge sola. Para un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(id)` y una de las bandas (`banda-negra`, `banda-hueso`, `banda-color`).
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida y respaldo), bandas a todo el ancho, 16 px de margen lateral del texto en móvil, sin scroll horizontal. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.variantes.variantes` → `/variantes/<slug>/` (variante).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/variantes/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
