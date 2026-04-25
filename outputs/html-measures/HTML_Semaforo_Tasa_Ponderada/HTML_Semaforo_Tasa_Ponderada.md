# HTML_Semaforo_Tasa_Ponderada

**Template:** Semáforo (template #7 de `html-dax-patterns`)
**Visual destino:** HTML Content (Daniel Marsh-Patrick)
**Generado:** 2026-04-25

## Propósito

Indicador visual con círculo de color y glow sutil que clasifica la Tasa
Ponderada en 3 estados según umbrales:
- **≤ 8%** → 🟢 Saludable (verde corporativo)
- **8.01% - 12%** → 🟠 Atención (naranja)
- **> 12%** → 🔴 Crítico (rojo)

## ⚠️ Importante: validar umbrales con negocio

Los umbrales (8%, 12%) son **valores de ejemplo** para mostrar la mecánica.
Cada banco/área tiene política propia sobre qué considera "saludable".

**Antes de usar en producción**, validá con el área correspondiente
(Riesgos, Tesorería, etc.) cuáles son los umbrales reales del banco.

## Medidas referenciadas

| Medida | Tabla | Uso |
|---|---|---|
| `[Tasa Ponderada]` | Medidas | Valor a clasificar |

## Parámetros customizables

| Parámetro | Valor actual | Cómo cambiar |
|---|---|---|
| Umbral OK | `0.08` | Modificar `_UmbralOk` |
| Umbral Atención | `0.12` | Modificar `_UmbralAtencion` |
| Labels | "Saludable" / "Atención" / "Crítico" | Modificar el `SWITCH(TRUE()...)` de `_Label` |
| Glow del círculo | `_Color & "55"` (33% opacidad hex) | `00`-`FF` para ajustar intensidad |

## Cómo usar

1. Ajustar los umbrales `_UmbralOk` y `_UmbralAtencion` según política del área
2. Copiar el `.dax` y agregar como medida en Power BI
3. Visual "HTML Content" → arrastrar la medida a Values

## Preview

Ver `HTML_Semaforo_Tasa_Ponderada.preview.html` con los 3 estados.
