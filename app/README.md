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

## Estado

Prototipo funcional con 25 plazas reales de Panamá mapeadas. Los negocios,
locales y precios que muestra son datos de ejemplo, no reales. Ver el plan
de negocio del proyecto para el detalle de qué falta para el producto real.

## Desarrollo

El proyecto se despliega con [Vercel](https://vercel.com):

```
vercel --prod
```
