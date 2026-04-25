# HTML_Meta_Avance_VsTarget

**Template:** Comparativo vs Meta (template #3 de `html-dax-patterns`)
**Visual destino:** HTML Content (Daniel Marsh-Patrick)
**Generado:** 2026-04-25

## Propósito

Progress bar horizontal que muestra el avance hacia una meta, con cuatro niveles
de color según porcentaje cumplido:
- **≥ 100%** → verde corporativo (cumplió o superó)
- **80-99%** → verde brand (cerca de cumplir)
- **50-79%** → naranja (a medio camino, atención)
- **< 50%** → rojo (lejos de la meta)

## Medidas referenciadas

| Medida | Tabla | Uso |
|---|---|---|
| `[Valor Actual]` | Medidas | Numerador / progreso actual |
| `[Valor Meta]` | Medidas | Denominador / target |
| `[1_Complete_%]` | Medidas | Ratio actual/meta (ya calculado en el modelo) |

## Parámetros customizables

| Parámetro | Valor actual | Cómo cambiar |
|---|---|---|
| Umbrales de color | 100% / 80% / 50% | Modificar el `SWITCH(TRUE()...)` |
| Label "Avance vs Meta" | string | Cambiar texto en el header |
| Max-width | 320px | Ajustar según diseño |
| Color barra de fondo | `#F0F0F0` | Modificar valor en `<div style='height:8px; background:...'>` |

## Cómo usar en Power BI

1. Instalar visual "HTML Content" (Daniel Marsh-Patrick) si no lo tenés
2. Agregar la medida al modelo (copiar `.dax`)
3. Arrastrar la medida al campo `Values` del visual

## Preview

Ver `HTML_Meta_Avance_VsTarget.preview.html` para ver el progress bar en sus 4 estados.
