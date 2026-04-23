---
description: "Documentar el modelo semántico a partir de los hallazgos del auditor (modo DRY-RUN)"
mode: agent
---

# Documentar modelo semántico

Ejecutá el agente **Model Documenter** en modo DRY-RUN (por defecto).

## Pasos

1. Verificá que exista `outputs/audit/semantic_model_findings.json`. Si no existe, primero ejecutá `/audit-semantic-model`.
2. Filtrá los hallazgos con `category: "documentacion"` y reglas permitidas:
   - `MEASURE-NO-FORMAT`
   - `MEASURE-NO-FOLDER`
   - `MEASURE-NO-DESCRIPTION`
   - `TABLE-DESCRIPTION`
3. Para cada archivo `.tmdl` con hallazgos:
   - Copiá el archivo a `outputs/documented/<archivo>.tmdl`
   - Aplicá los cambios a la copia
   - Generá `outputs/documented/<archivo>.diff`
4. Generá `outputs/documented/_summary.md` con el resumen.

## NO hacer

- NO modificar archivos originales en `powerbi-project/`
- NO tocar nombres, DAX, relaciones
- NO hacer commits git

## Output en chat

```
✅ Documentación propuesta (DRY-RUN)
   Archivos modificados: 10
   Total cambios: 150
   🟢 Alta confianza:  100
   🟡 Media confianza:  30
   🟠 Baja confianza:   20

📁 Revisá: outputs/documented/
   • _summary.md
   • Medidas.tmdl (35 cambios)
   • FctProductos.tmdl (8 cambios)
   • ...

Para aplicar cambios al modelo real, pedime "aplicá los cambios".
```
