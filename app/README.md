# Plaza Marketplace

Prototipo de una plataforma que ayuda a decidir en qué plaza comercial de
Panamá conviene abrir un negocio. Cruza el tipo de negocio que alguien
quiere abrir con el tenant mix, las anclas de tráfico, la competencia y el
carácter de cada plaza y su zona.

## Sitio en vivo

**https://plaza-marketplace.vercel.app** — protegido con código de acceso: `0010`

## Archivos

- `index.html` — el sitio completo (HTML, CSS y JavaScript en un solo
  archivo, con las fotos de las plazas incrustadas). Es el archivo que se
  despliega en Vercel.
- `src-con-placeholders.html` — el mismo sitio pero con marcadores
  (`%%nombre-de-plaza%%`) en lugar de las fotos ya incrustadas. Se usa como
  plantilla editable antes de inyectar las imágenes al hacer un build.
- `../data/plazas.json` — la base de datos de negocios reales por plaza
  (fuente de verdad). El array `PLAZAS` embebido en `index.html` y
  `src-con-placeholders.html` se genera/actualiza a partir de este archivo.
- `../editor-plazas.html` — herramienta local para investigar y editar los
  negocios de cada plaza (agregar, quitar, categorizar). Guarda en
  `localStorage` del navegador; no está conectada en vivo a `plazas.json` —
  los cambios se pasan a mano a `plazas.json` cuando se confirman.
- `../investigacion-plazas.md` — notas de investigación por plaza, con el
  estado de cada una (✅ lista, 🈳 falta info, 🔲 sin empezar).

## Estado

Prototipo funcional con 26 plazas reales de Panamá mapeadas. Los negocios
(`tenants`) son datos reales investigados por plaza — ver `data/plazas.json`
y `investigacion-plazas.md` para el detalle y qué falta confirmar. Los
locales y precios que muestra el sitio siguen siendo datos de ejemplo, no
reales. Ver el plan de negocio del proyecto para el detalle de qué falta
para el producto real.

## Desarrollo

El proyecto se despliega con [Vercel](https://vercel.com):

```
vercel --prod
```
