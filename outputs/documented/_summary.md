# 📝 Propuesta de documentación (DRY-RUN)

**Archivos modificados:** 14  
**Total cambios:** 181

## Distribución por confianza

| Confianza | Cantidad | Acción sugerida |
|---|---:|---|
| 🟢 Alta | 108 | Aplicar sin revisar |
| 🟡 Media | 54 | Revisar antes de aplicar |
| 🟠 Baja | 19 | Requiere input del negocio |

## Desglose por archivo

| Archivo | Cambios | 🟢 Alta | 🟡 Media | 🟠 Baja |
|---|---:|---:|---:|---:|
| `Medidas.tmdl` | 65 | 51 | 8 | 6 |
| `⚙ Medidas.tmdl` | 59 | 39 | 10 | 10 |
| `Parámetros.tmdl` | 46 | 17 | 27 | 2 |
| `DimCalendario.tmdl` | 1 | 0 | 1 | 0 |
| `DimCliente.tmdl` | 1 | 0 | 1 | 0 |
| `DimEstadoProducto.tmdl` | 1 | 0 | 1 | 0 |
| `DimMetas.tmdl` | 1 | 0 | 1 | 0 |
| `DimMoneda.tmdl` | 1 | 0 | 1 | 0 |
| `DimProducto.tmdl` | 1 | 0 | 1 | 0 |
| `DimPromotor.tmdl` | 1 | 0 | 1 | 0 |
| `DimTipoProducto.tmdl` | 1 | 0 | 1 | 0 |
| `FctProductos.tmdl` | 1 | 0 | 1 | 0 |
| `Metricas.tmdl` | 1 | 1 | 0 | 0 |
| `Tabla.tmdl` | 1 | 0 | 0 | 1 |

## ⚠️ Cambios que requieren revisión (confianza baja)

### `Medidas.tmdl` (6 bajos)
- **description** en `[TieneDatos]`: `[TODO: validar descripción con negocio]`
- **description** en `[1_YTD_Delta_SinFormato]`: `[TODO: validar descripción con negocio]`
- **description** en `[1_YoY_Delta_SinFormato]`: `[TODO: validar descripción con negocio]`
- **description** en `[1_MoM_Delta_SinFormato]`: `[TODO: validar descripción con negocio]`
- **description** en `[1_Target_Valor_FinMes]`: `[TODO: validar descripción con negocio]`
- **formatString** en `[1_Estado]`: `"#,##0.00"`

### `Parámetros.tmdl` (2 bajos)
- **description** en `[Titulo Medida]`: `[TODO: validar descripción con negocio]`
- **description** en `[Titulo Reporte (Panel)]`: `[TODO: validar descripción con negocio]`

### `Tabla.tmdl` (1 bajos)
- **table_description** en `[<tabla Tabla>]`: `Tabla Tabla. [TODO: validar descripción con negocio]`

### `⚙ Medidas.tmdl` (10 bajos)
- **formatString** en `[Valor Métrica Seleccionada (txt)]`: `"#,##0.00"`
- **displayFolder** en `[Valor Métrica Seleccionada (txt)]`: `Sin categorizar`
- **description** en `[Valor Meta]`: `[TODO: validar descripción con negocio]`
- **formatString** en `[Valor MoM (txt)]`: `"#,##0.00"`
- **description** en `[Título Medida]`: `[TODO: validar descripción con negocio]`
- **formatString** en `[Título Medida]`: `"#,##0.00"`
- **displayFolder** en `[Título Medida]`: `Sin categorizar`
- **description** en `[Valor Actual]`: `[TODO: validar descripción con negocio]`
- **description** en `[Valor Métrica Seleccionada]`: `[TODO: validar descripción con negocio]`
- **displayFolder** en `[Valor Métrica Seleccionada]`: `Sin categorizar`

## 📋 Instrucciones para aplicar

1. Revisá los `.diff` en `outputs/documented/` contra los originales.
2. Ajustá manualmente los `[TODO]` con contexto de negocio real.
3. Cuando estés conforme, pedile al agente **Model Documenter**: _"aplicá los cambios"_.
4. El agente creará un backup automático antes de modificar el modelo original.

## 🛡️ Garantías
- ✅ Archivos originales intactos en `powerbi-project/`
- ✅ Solo se agregaron `description`, `displayFolder`, `formatString`
- ✅ NO se renombró nada ni se modificó DAX
- ✅ NO se tocaron relaciones ni particiones