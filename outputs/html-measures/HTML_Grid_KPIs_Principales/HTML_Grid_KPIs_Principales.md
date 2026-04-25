# HTML_Grid_KPIs_Principales

**Template:** KPI Grid (template #2 de `html-dax-patterns`)
**Visual destino:** HTML Content (Daniel Marsh-Patrick)
**Generado:** 2026-04-25

## Propósito

Grilla horizontal con 4 KPIs principales para el header de un dashboard.
Cada card tiene un accent de color distinto para diferenciar visualmente
las métricas, manteniendo la paleta Promerica.

## Layout

- **Flex container** que acomoda las cards horizontalmente
- **Wrap automático** si no hay espacio (responsive)
- **min-width: 140px** por card → en pantallas chicas se apilan
- **gap: 12px** entre cards

## Medidas referenciadas

| # | Medida | Tabla | Color accent |
|---|---|---|---|
| 1 | `[Saldo]` | ⚙ Medidas | Verde corporativo `#006338` |
| 2 | `[Q Clientes]` | Medidas | Azul corporativo `#003E89` |
| 3 | `[Q Cuentas]` | Medidas | Verde brand `#61BF1A` |
| 4 | `[Tasa Ponderada]` | Medidas | Cian `#69C7C7` |

## Customización

Para cambiar las medidas o colores:
- Modificar las 4 `VAR` al inicio (`_Saldo`, `_Clientes`, etc.)
- Modificar los colores `_Verde`, `_Azul`, `_VerdeLima`, `_Cian`
- Cambiar los labels en cada `text-transform:uppercase`
- Ajustar `min-width: 140px` si las cards quedan apretadas

## ⚠️ Consideración importante

Este template usa **una sola medida HTML** que renderiza 4 cards. Para
algunos casos puede ser preferible **4 medidas separadas** (1 por card)
y agregar 4 visuales independientes — eso te da:
- ✅ Más flexibilidad para reordenar visualmente
- ✅ Drill-through individual por KPI
- ❌ Más medidas para mantener
- ❌ Más visuales en la página

Decidí según el caso de uso. Para un header consolidado de dashboard,
una sola medida es más práctica. Para drill independiente, separar.

## Cómo usar

1. Copiar el `.dax` y pegar como nueva medida
2. Visual "HTML Content" → arrastrar la medida al campo `Values`
3. Estirar el visual horizontalmente para que las 4 cards quepan
