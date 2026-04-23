# 🔍 Auditoría de Modelo Semántico — RPAUT084

**Fecha:** 2026-04-23  
**Tablas analizadas:** 19

## 📊 Scores

| Dimensión | Score | Estado | Hallazgos |
|---|---:|---|---:|
| 📐 **Estructural** | **47/100** | 🟠 Necesita trabajo | 10 |
| 📝 **Documentación** | **0/100** | 🔴 Requiere refactor | 190 |
| 🎯 **Global** (70/30) | **33/100** | 🔴 Requiere refactor | 200 |

> **Cómo leer esto:** El score estructural mide si el modelo funciona bien (relaciones, DAX, naming crítico). El score de documentación mide si está bien descrito (descriptions, folders, formats). Un modelo puede ser **estructuralmente perfecto pero mal documentado**, o viceversa.

---

## 📐 Análisis Estructural

### 🔴 Críticos

**SM-198** `DIM-FECHA-NOT-MARKED` — `tables/DimCalendario.tmdl`  
La tabla `DimCalendario` no está marcada como tabla de fechas (`dataCategory: Time`).  
**→** En Power BI Desktop: Vista de modelo → Seleccionar tabla → Mark as date table. Asegura que time intelligence funcione correctamente.

### ⚠️ Mejoras

- **NAMING-MEASURES-TABLE** — `tables/Medidas.tmdl`: Tabla `Medidas` no usa convención Promerica (prefijo `_` para auxiliares o `CG_` para calculation groups).
- **NAMING-MEASURES-TABLE** — `tables/Metricas.tmdl`: Tabla `Metricas` no usa convención Promerica (prefijo `_` para auxiliares o `CG_` para calculation groups).
- **NAMING-TABLE** — `tables/Parámetros.tmdl`: Tabla `Parámetros` con nombre genérico, no sigue prefijo Promerica.
- **NAMING-TABLE** — `tables/Tabla.tmdl`: Tabla `Tabla` con nombre genérico, no sigue prefijo Promerica.
- **DAX-USE-DIVIDE** — `tables/DimTipoProducto.tmdl:102`: Posible división sin `DIVIDE()`: `Source = Sql.Database("synw-modeling-prod-westus2-001-ondemand.sql.azuresynapse.`
- **MODEL-AUTO-DATETIME** — `model.tmdl`: Opción 'Auto Date/Time' habilitada (`__PBI_TimeIntelligenceEnabled = 1`). Esto genera tablas `LocalDateTable_*` ocultas por cada columna de fecha.

### ℹ️ Observaciones

- **NAMING-TABLE** — Tabla `⚙` no sigue convención FACT_/DIM_/BRIDGE_/PARAM_.
- **REL-AUTO-DETECTED** — 5 relaciones marcadas como `AutoDetected_*`.
- **REL-LOCAL-DATETABLE** — 4 referencias a `LocalDateTable_*` en relaciones.

---

## 📝 Análisis de Documentación

| Regla | Casos | Severidad | Impacto |
|---|---:|---|---|
| Medidas sin descripción | 67 | ℹ️ observación | Usuarios no saben qué calcula la medida |
| Medidas sin displayFolder | 65 | ℹ️ observación | Panel de campos desordenado |
| Medidas sin formatString | 35 | ⚠️ mejora | Visualizaciones inconsistentes |
| Tablas sin descripción | 14 | ⚠️ mejora | Difícil entender propósito de cada tabla |
| Estilo Fct/Dim en vez de FACT_/DIM_ | 9 | ℹ️ observación | Inconsistencia con convención Promerica |

---

## 📌 Plan de acción priorizado

### 🔴 Urgente (estructural)
1. **Marcar `DimCalendario` como tabla de fechas** — habilita time intelligence correctamente.
2. **Desactivar Auto Date/Time** en opciones del modelo — elimina 5 `LocalDateTable_*` auto-generadas.
3. **Revisar las 9 relaciones `AutoDetected_*`** — confirmar cardinalidad y dirección.

### 🟠 Importante (estructura)
4. **Renombrar tablas genéricas**: `Medidas` → `_Medidas`, `Parámetros` → `PARAM_Filtros`, `Tabla` → `_Auxiliar` o eliminar.
5. **Migrar estilo `Fct/Dim` → `FACT_/DIM_`** (opcional, alineación con convención institucional).

### 🟡 Mejora continua (documentación)
6. **Agregar `formatString` a las 35 medidas sin formato** — el `Model Documenter` (próximo agente) puede hacerlo de forma segura.
7. **Asignar `displayFolder` a las 65 medidas sin carpeta** — idem, automatizable sin riesgo.
8. **Generar descripciones (`///`) para medidas y tablas** — automatizable para el caso técnico; descripciones de negocio requieren validación humana.

---

## 🤖 Siguiente paso: Model Documenter

Los hallazgos de **documentación (190)** son candidatos ideales para automatizar.
Un próximo agente **Model Documenter** podrá:
- ✅ Agregar `formatString` inferido del `dataType` y contexto
- ✅ Asignar `displayFolder` según categoría detectada
- ✅ Generar descripciones técnicas con marca de "confianza baja/alta"
- ❌ NO modificar nombres (eso rompe DAX y PBIR)
- ❌ NO tocar lógica DAX ni relaciones

