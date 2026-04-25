# 📊 Medidas HTML generadas

Catálogo de medidas DAX que devuelven HTML, listas para usar con el visual
**"HTML Content" (Daniel Marsh-Patrick)** en Power BI.

Generadas por el agente [`html-measure-generator`](../../.github/agents/html-measure-generator.agent.md).

---

## 🎴 Medidas disponibles

| Nombre | Template | Medidas que usa | Estado |
|---|---|---|---|
| [`HTML_Card_Saldo_YoY`](./HTML_Card_Saldo_YoY/) | KPI Card #1 | `[Saldo]`, `[1_YoY_%]` | ✅ Validada |
| [`HTML_Meta_Avance_VsTarget`](./HTML_Meta_Avance_VsTarget/) | Comparativo Meta #3 | `[Valor Actual]`, `[Valor Meta]`, `[1_Complete_%]` | ✅ Validada |
| [`HTML_Semaforo_Tasa_Ponderada`](./HTML_Semaforo_Tasa_Ponderada/) | Semáforo #7 | `[Tasa Ponderada]` | ✅ Validada |
| [`HTML_Grid_KPIs_Principales`](./HTML_Grid_KPIs_Principales/) | KPI Grid #2 | `[Saldo]`, `[Q Clientes]`, `[Q Cuentas]`, `[Tasa Ponderada]` | ✅ Validada |

## 📁 Estructura por medida

Cada medida vive en su propia carpeta con 3 archivos:

```
HTML_<NombreMedida>/
├── HTML_<NombreMedida>.dax           ← DAX listo para pegar en Power BI
├── HTML_<NombreMedida>.md             ← Documentación: propósito, parámetros, uso
└── HTML_<NombreMedida>.preview.html   ← Render visual con valores simulados
```

## 🚀 Cómo usar una medida

1. **Abrir el `.preview.html`** en el navegador → ver cómo se verá
2. **Si te gusta:** abrir el `.dax`, copiar todo el contenido
3. **En Power BI Desktop:**
   - Abrir el modelo
   - Click derecho en una tabla de medidas (o crear `_Medidas HTML`)
   - "Nueva medida" → pegar el contenido del `.dax`
4. **Visual "HTML Content":**
   - Si no lo tenés instalado: marketplace → buscar "HTML Content" by Daniel Marsh-Patrick
   - Agregar el visual a la página
   - Drag & drop de la medida al campo `Values`
5. **Validar** que el render coincide con el preview

## 🎨 Templates disponibles para nuevas medidas

El agente puede generar 8 templates distintos. Ver biblioteca completa en
[`html-dax-patterns/SKILL.md`](../../.github/skills/html-dax-patterns/SKILL.md):

1. **KPI Card** — valor + YoY con color condicional ✅ Probado
2. **KPI Grid** — 3-4 cards en flex grid ✅ Probado
3. **Comparativo Meta** — progress bar con % avance ✅ Probado
4. **Status Badge** — pastilla con color según umbral
5. **Mini Tabla** — tabla con formato condicional
6. **Gauge SVG** — semicírculo con %
7. **Semáforo** — círculo rojo/ámbar/verde ✅ Probado
8. **Card Cliente** — avatar con iniciales + segmento

## ✨ Generar una medida nueva

Desde Copilot Chat (cuando estés en VS Code):

```
/generate-html-measure
```

O directamente:

```
/generate-html-measure KPI card para Saldo con YoY del año anterior
```

El agente:
1. Detecta el template más adecuado
2. Valida que las medidas existan en el modelo
3. Genera los 3 archivos en `outputs/html-measures/<nombre>/`
4. Te avisa qué hacer

## 🎨 Paleta usada

Todas las medidas usan colores oficiales del **theme `Promerica1`**:

| Color | Hex | Uso |
|---|---|---|
| Verde corporativo | `#006338` | Positivo, OK, accent principal |
| Verde brand | `#61BF1A` | Cerca del objetivo |
| Azul corporativo | `#003E89` | Info, secundario |
| Cian | `#69C7C7` | Accent secundario |
| Naranja | `#C35A00` | Atención, alerta |
| Rojo | `#A20000` | Negativo, crítico |
| Gris neutro | `#A6A6A6` | Labels secundarios |

Ver detalles en [`promerica-brand/SKILL.md`](../../.github/skills/promerica-brand/SKILL.md).

---

**Última actualización:** 2026-04-25
**Mantenedor:** Equipo Data Science — Banco Promerica CR
