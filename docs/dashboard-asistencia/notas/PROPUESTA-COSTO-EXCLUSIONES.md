# Propuesta de Negocio — Costo Perdido Total vs. Costo Perdido Controlable

> Generado con IA (Claude — ERC AI Workspace) | Propiedad ERC Capital Corp | Requiere validación del responsable.
> Fecha: 2026-09-04 | Fase 4 de "Implementación de Mejoras Post-Auditoría" — **solo análisis y propuesta, sin cambios de código.**

## Resumen Ejecutivo

Con datos reales (`ReporteUnificadoEne-Ago.xlsx`, ene-ago 2026, 57 colaboradores, validado por
partida doble entre `attendance_auditor.py` y el motor JS del dashboard — ver
`docs/dashboard-asistencia/auditor/README.md`), el KPI **"Costo Total Perdido" del Dashboard
Ejecutivo asciende a Q640,017.61**. De ese total, **Q260,970.00 (40.8%) proviene de solo 6
colaboradores** pertenecientes a 5 de las 7 categorías que el propio sistema ya identifica como
"operativas con horario controlado" en la función "Excluir del análisis" — pero que **los 4 KPIs
Ejecutivos nunca excluyen**, porque esa exclusión fue diseñada únicamente para los rankings
comparativos (Departamentos, Colaboradores), no para los KPIs.

**Esto no es un bug**: es el comportamiento documentado y decidido explícitamente en una sesión
anterior (ver `PROJECT_CONTEXT.md`, regla de negocio de Módulo 4). Pero con datos reales, la
magnitud (41% de un KPI que Gerencia interpreta como una sola cifra) es lo bastante significativa
como para requerir una decisión explícita, no asumida.

## Hallazgo (datos verificados)

| Categoría (una de las 7 de "Excluir del análisis") | Colaboradores | Costo Promedio aprox. |
|---|---|---|
| Socios | incluido en los 6 | ~Q42,000–43,700 |
| Seguridad | incluido en los 6 | ~Q42,000–43,700 |
| Visitas | incluido en los 6 | ~Q42,000–43,700 |
| Pilotos de seguridad | incluido en los 6 | ~Q42,000–43,700 |
| Gerencia General | incluido en los 6 | ~Q42,000–43,700 |

- Estas 5 categorías concentran **Q260,970.00 de los Q640,017.61 totales (40.8%)**.
- El siguiente departamento "regular" en la lista (Moore Díaz) tiene un costo promedio de
  Q18,449 — **menos de la mitad** que cualquiera de las 5 categorías anteriores.
- Las otras 2 categorías de "Excluir del análisis" (Contratista, Moore Díaz) **no** están entre las
  de mayor costo promedio en esta corrida — el hallazgo aplica específicamente a las 5 mencionadas,
  no a las 7 en bloque.

**Por qué ocurre:** estas 5 categorías corresponden a roles cuyo patrón de marcaje/horario no es
comparable al de un colaborador de oficina regular (ej. personal de seguridad con turnos rotativos,
socios sin obligación de marcaje, visitas sin relación laboral continua). El motor de cálculo no
distingue esto — aplica la misma jornada esperada (08:00-17:00) a todos por igual salvo que el
analista los excluya manualmente de los **rankings**, algo que nunca afecta los **KPIs**.

## Riesgo de interpretación ejecutiva

Si este archivo se presenta a Gerencia con la configuración por defecto (ninguna categoría
excluida, estado inicial del sistema), el KPI "Costo Total Perdido" — la cifra más visible del
Dashboard Ejecutivo — estaría dominado en más de un tercio por personas cuyo "costo perdido" no
representa una oportunidad real de recuperación operativa (no se les puede pedir que "cumplan
mejor su jornada de oficina" si su rol no es de oficina). Esto puede llevar a conclusiones
incorrectas sobre dónde está el verdadero costo de asistencia recuperable.

## Opciones evaluadas

### Opción A — Mantener la regla actual sin cambios
Los 4 KPIs siguen siendo un totalizador global sin distinción de categoría. Más simple, pero
mantiene el riesgo de interpretación descrito arriba.

### Opción B — Agregar una nota de advertencia junto al KPI (sin cambiar el número)
Ej.: "Incluye Q260,970 (41%) de categorías operativas con horario no comparable — ver detalle."
Cambio mínimo (una línea de UI), no altera ningún cálculo, da contexto inmediato a Gerencia sin
tocar la cifra oficial.

### Opción C — Mostrar dos cifras: "Costo Total" y "Costo Controlable"
- **Costo Total Perdido**: el cálculo actual, sin cambios (todos los colaboradores).
- **Costo Perdido Controlable**: el mismo cálculo, aplicando la exclusión de "Excluir del
  análisis" (igual que ya hacen los rankings hoy).
Requiere: exponer ambas cifras en el KPI (o un desglose secundario), y decidir cuál es la cifra
"principal" que ve Gerencia por defecto. Es el cambio de mayor alcance de las 3 opciones, pero es
el único que responde directamente a la pregunta de negocio real ("¿cuánto de esto puedo
recuperar?").

## Recomendación

Se recomienda la **Opción C**, con la Opción B como paso intermedio de bajo riesgo si se prefiere
no tocar la lógica de KPIs todavía: mostrar "Costo Total Perdido" (cifra oficial sin cambios) como
KPI principal, y agregar "Costo Perdido Controlable" (aplicando "Excluir del análisis") como una
segunda cifra de contexto, sin reemplazar ni recalcular el KPI existente — visualmente subordinada,
igual que "Oportunidad de Recuperación" ya convive hoy junto a los 4 KPIs principales sin ser uno
de ellos. Esto:

- No modifica ninguna fórmula ya validada por `attendance_auditor.py`.
- No rompe compatibilidad con el archivo ejecutivo ya generado ni con el filtro "Excluir del
  análisis" existente (reutiliza exactamente su lógica, `estaExcluidoDeRanking()`).
- Da a Gerencia el contexto que hoy falta, sin decisiones automáticas sobre qué excluir.

## Próximos pasos (pendientes de aprobación explícita del responsable)

1. Confirmar cuál opción (A/B/C) se implementa — **no se implementa ninguna hasta esta
   aprobación**, por instrucción explícita de esta fase.
2. Si se aprueba B o C: definir el texto/etiqueta exacto que verá Gerencia.
3. Si se aprueba C: definir si "Costo Perdido Controlable" también debe reflejarse en "Impacto
   sobre Nómina" y "Oportunidad de Recuperación" (misma pregunta de fondo, mismo tipo de sesgo).

## Referencias

- `docs/dashboard-asistencia/auditor/README.md` — hallazgo original y cifras completas.
- `docs/dashboard-asistencia/auditor/attendance_auditor.py` — fuente de los cálculos.
- `PROJECT_CONTEXT.md` — regla de negocio actual de "Excluir del análisis" y su alcance.
- `NEXT_TASKS.md`, Alta prioridad #3 — pendiente de decisión formal, ahora documentado aquí.
