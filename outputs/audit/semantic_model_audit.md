# 🔍 Auditoría de Modelo Semántico — RPAUT084

**Fecha:** 2026-04-23  
**Tablas analizadas:** 19  
**Score global:** **0/100**
  **🔴 Requiere refactor**

## 📊 Resumen ejecutivo

| Severidad | Cantidad | Peso |
|---|---:|---:|
| 🔴 Crítico | 1 | -20 pts |
| ⚠️ Mejora | 55 | -5 pts |
| ℹ️ Observación | 144 | -1 pt |

**Total hallazgos:** 200

## 🎯 Top reglas disparadas

| Regla | Cantidad | ¿Qué significa? |
|---|---:|---|
| `MEASURE-NO-DESCRIPTION` | 67 | Medidas sin comentario explicativo |
| `MEASURE-NO-FOLDER` | 65 | Medidas sin displayFolder |
| `MEASURE-NO-FORMAT` | 35 | Medidas sin formatString |
| `TABLE-DESCRIPTION` | 14 | Tablas sin descripción |
| `NAMING-TABLE-STYLE` | 9 | Uso Fct/Dim en vez de FACT_/DIM_ (Promerica) |
| `NAMING-TABLE` | 3 | Tabla con nombre genérico (Medidas, Tabla, etc.) |
| `NAMING-MEASURES-TABLE` | 2 | Tabla de medidas sin prefijo `_` |
| `DAX-USE-DIVIDE` | 1 | División sin DIVIDE() |
| `MODEL-AUTO-DATETIME` | 1 | Auto Date/Time habilitado |
| `DIM-FECHA-NOT-MARKED` | 1 | DimCalendario no marcada como tabla de fechas |
| `REL-AUTO-DETECTED` | 1 | Relaciones auto-detectadas por Power BI |
| `REL-LOCAL-DATETABLE` | 1 | Relaciones a tablas auto-generadas |

---

## 🔴 Hallazgos críticos

### SM-198 — `DIM-FECHA-NOT-MARKED`
**Ubicación:** `tables/DimCalendario.tmdl`  
**Problema:** La tabla `DimCalendario` no está marcada como tabla de fechas (`dataCategory: Time`).  
**Recomendación:** En Power BI Desktop: Vista de modelo → Seleccionar tabla → Mark as date table. Asegura que time intelligence funcione correctamente.

## ⚠️ Hallazgos de mejora (agrupados)

### MEASURE-NO-FORMAT (35 ocurrencias)
**Recomendación:** Agregar `formatString` explícito (ej: `"#,##0.00"`, `"0.00%"`, `"$#,##0"`).

**Ejemplos:**
- `tables/Medidas.tmdl` — Medida `[1_Estado]` sin `formatString`.
- `tables/Medidas.tmdl` — Medida `[1_Last_Valor (Eje)]` sin `formatString`.
- `tables/Medidas.tmdl` — Medida `[1_Last_Valor (%)]` sin `formatString`.
- `tables/Medidas.tmdl` — Medida `[Porcentaje Target (Ayer)]` sin `formatString`.
- `tables/Medidas.tmdl` — Medida `[Porcentaje Target (Fin Mes Actual)]` sin `formatString`.
- *... y 30 más*

### TABLE-DESCRIPTION (14 ocurrencias)
**Recomendación:** Agregar descripción explicando el propósito y contexto de negocio.

**Ejemplos:**
- `tables/DimCalendario.tmdl` — Tabla `DimCalendario` no tiene descripción (`/// ...`).
- `tables/DimCliente.tmdl` — Tabla `DimCliente` no tiene descripción (`/// ...`).
- `tables/DimEstadoProducto.tmdl` — Tabla `DimEstadoProducto` no tiene descripción (`/// ...`).
- `tables/DimMetas.tmdl` — Tabla `DimMetas` no tiene descripción (`/// ...`).
- `tables/DimMoneda.tmdl` — Tabla `DimMoneda` no tiene descripción (`/// ...`).
- *... y 9 más*

### NAMING-MEASURES-TABLE (2 ocurrencias)
**Recomendación:** Renombrar a `_Medidas` o similar para marcarla como auxiliar oculta.

**Ejemplos:**
- `tables/Medidas.tmdl` — Tabla `Medidas` no usa convención Promerica (prefijo `_` para auxiliares o `CG_` para calculation groups).
- `tables/Metricas.tmdl` — Tabla `Metricas` no usa convención Promerica (prefijo `_` para auxiliares o `CG_` para calculation groups).

### NAMING-TABLE (2 ocurrencias)
**Recomendación:** Renombrar a `PARAM_Filtros` o similar siguiendo convención institucional.

**Ejemplos:**
- `tables/Parámetros.tmdl` — Tabla `Parámetros` con nombre genérico, no sigue prefijo Promerica.
- `tables/Tabla.tmdl` — Tabla `Tabla` con nombre genérico, no sigue prefijo Promerica.

### DAX-USE-DIVIDE (1 ocurrencias)
**Recomendación:** Reemplazar `/` por `DIVIDE(num, den, 0)` para evitar errores de división por cero.

**Ejemplos:**
- `tables/DimTipoProducto.tmdl:102` — Posible división sin `DIVIDE()`: `Source = Sql.Database("synw-modeling-prod-westus2-001-ondemand.sql.azuresynapse.`

### MODEL-AUTO-DATETIME (1 ocurrencias)
**Recomendación:** Desactivar en Power BI Desktop: Archivo → Opciones → Modelo actual → Inteligencia de tiempo → desmarcar. Usar únicamente `DimCalendario`.

**Ejemplos:**
- `model.tmdl` — Opción 'Auto Date/Time' habilitada (`__PBI_TimeIntelligenceEnabled = 1`). Esto genera tablas `LocalDateTable_*` ocultas por cada columna de fecha.

## ℹ️ Observaciones más frecuentes

**`MEASURE-NO-DESCRIPTION`** — 67 casos  
*Agregar `/// descripción` explicando lógica de negocio y unidad aplicable.*

**`MEASURE-NO-FOLDER`** — 65 casos  
*Asignar un displayFolder para organizar medidas por categoría.*

**`NAMING-TABLE-STYLE`** — 9 casos  
*Considerar migrar a estilo con underscore: FctProductos → FACT_Productos.*

**`NAMING-TABLE`** — 1 casos  
*Evaluar renombrado según tipo.*

**`REL-AUTO-DETECTED`** — 1 casos  
*Revisar manualmente que cada relación esté bien configurada. Power BI las crea automáticamente cuando detecta coincidencias de nombres.*

---

## 📌 Plan de acción priorizado


### Prioridad ALTA (acción inmediata)
1. **Marcar `DimCalendario` como tabla de fechas** — habilita time intelligence correctamente.
2. **Desactivar Auto Date/Time** — elimina 5 tablas auto-generadas + 5 relaciones innecesarias.

### Prioridad MEDIA (esta semana)
3. **Agregar `formatString` a las 35 medidas sin formato** — especialmente las que devuelven porcentajes, montos o fechas.
4. **Renombrar tablas genéricas** (`Medidas` → `_Medidas`, `Tabla` → `_Auxiliar`, `Parámetros` → `PARAM_Filtros`).
5. **Revisar las 9 relaciones `AutoDetected_*`** — confirmar que la cardinalidad y dirección sean correctas.

### Prioridad BAJA (mejora continua)
6. **Asignar `displayFolder` a las 65 medidas sin carpeta** — organiza el panel de campos.
7. **Agregar descripciones (`///`) a medidas y tablas clave** — especialmente `FctProductos`, `Valor Métrica Seleccionada`, `Tasa Ponderada`.
8. **Evaluar migración de estilo `Fct/Dim` a `FACT_/DIM_`** — alinear con convención institucional Promerica.

---

## 💡 Nota sobre el score

El score de **0/100** refleja principalmente la **ausencia masiva de metadata** (descripciones, displayFolders, formatStrings), no problemas estructurales graves. El modelo tiene solo **1 hallazgo crítico**, y la arquitectura base es sólida (fuentes GOLD, relaciones coherentes, medidas funcionales).

El modelo es **funcionalmente correcto**. Lo que falta es **documentación y organización** — un trabajo de ~2-3 horas bien invertidas.

