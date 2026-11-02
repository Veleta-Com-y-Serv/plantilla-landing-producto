# Plantilla NoExpertise · Lanzamiento de producto

Web de una sola página para presentar y vender un producto: color pleno de marca + negro, portada a sangre con el
precio, características con ficha técnica, galería de borde a borde, modelos y precios, cómo se usa, comparativa,
opiniones, preguntas y compra directa (tienda online o WhatsApp).

- Sectores: producto, lanzamiento, marca, tienda-online, artesano-producto. Estilo: impactante. Plan mínimo: gratis.
- Secciones: hero, caracteristicas, galeria, variantes, proceso, comparativa, opiniones, preguntas, compra, contacto (y `texto` para apartados nuevos).
- Campos propios: `hero.producto`, `hero.precio`, `hero.precio_nota`; `caracteristicas.caracteristicas[]` (titulo, texto, icono), `caracteristicas.ficha[]` (titulo, texto) y `titulo_ficha`; `variantes.variantes[]` (nombre, texto, precio, imagen, etiqueta, destacado, url); `comparativa.columna_propia`, `columna_otros` e `items[]` (titulo, propio, otros); `compra.precio`, `compra.nota`.
- Ejemplo: Forja Tajo, cuchillos forjados a mano en Toledo (negocio ficticio).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; fotos de partida en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.variantes.variantes` con `detalle` tiene su página en `/variantes/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
