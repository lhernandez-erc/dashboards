# CLAUDE GLOBAL

## Objetivo

Mantener memoria persistente entre sesiones, evitar pérdida de contexto y asegurar documentación consistente en todos los proyectos.

## Documentos Globales Obligatorios

Antes de trabajar sobre cualquier proyecto, siempre leer en este orden:

1. CLAUDE_GLOBAL.md
2. AI_SKILLS_BASELINE.md
3. AI_DASHBOARD_PLAYBOOK.md

Prioridad (en caso de conflicto entre documentos):

1. CLAUDE_GLOBAL.md
2. AI_SKILLS_BASELINE.md
3. AI_DASHBOARD_PLAYBOOK.md
4. Documentación local del proyecto (`docs/<nombre-proyecto>/`)

Roles de cada documento:

**CLAUDE_GLOBAL.md**

- Define el proceso de trabajo.
- Define la gestión documental.
- Define la memoria del proyecto.
- Define la estructura de carpetas.
- Define el flujo de actualización.

**AI_SKILLS_BASELINE.md**

- Define el catálogo de skills disponibles en el entorno de Claude Code.
- Define cuándo debe utilizarse cada skill (auditoría, planeación de features, dashboards,
  diagramas, documentación técnica, refactorización, etc.).
- Exige verificar, antes de iniciar cualquier análisis/implementación/auditoría/rediseño, si una
  skill recomendada para esa tarea está instalada — y si no lo está, informarlo explícitamente
  (con su impacto) antes de continuar, en vez de asumir que sí está disponible.

**AI_DASHBOARD_PLAYBOOK.md**

- Define UX.
- Define UI.
- Define Branding.
- Define Diseño Ejecutivo.
- Define Visualización de Datos.
- Define Accesibilidad.
- Define Identidad Corporativa ERC Capital Corp.
- Define estándares de dashboards.

Las decisiones de diseño, experiencia de usuario, visualización y branding deberán seguir siempre AI_DASHBOARD_PLAYBOOK.md.

## Gobernanza de Skills

Antes de iniciar cualquier tarea:

1. Leer AI_SKILLS_BASELINE.md.
2. Identificar el tipo de trabajo solicitado.
3. Determinar qué skills son aplicables.
4. Verificar cuáles están disponibles.
5. Informar explícitamente las skills recomendadas que no estén instaladas.
6. Explicar el impacto potencial de la ausencia de dichas skills.
7. Priorizar el uso de skills especializadas antes de proponer implementaciones complejas.

La selección de skills forma parte obligatoria del análisis inicial de cualquier proyecto.

## Auditoría Obligatoria

Antes de cerrar cualquier desarrollo relevante:

Realizar validación conceptual utilizando:

- code-auditor
- ensemble-solving

Validar:

- Arquitectura
- KPIs
- Filtros
- Performance
- Consistencia
- Riesgos
- Calidad general

Ninguna tarea debe considerarse finalizada hasta completar esta validación.

## Regla Principal

Antes de realizar cualquier modificación en un proyecto:

1. Identificar el archivo principal indicado por el usuario.
2. Considerar dicho archivo como la fuente de verdad de la sesión.
3. Localizar la documentación asociada al proyecto.
4. Si la documentación no existe, crearla automáticamente.
5. Si existe, leerla completamente antes de analizar o modificar código.
6. Actualizar la documentación al finalizar cualquier cambio.

## Estructura de Documentación por Proyecto

Cada proyecto deberá tener una carpeta de documentación independiente:

docs/<nombre-proyecto>/

con los siguientes archivos:

- PROJECT_CONTEXT.md
- ARCHITECTURE.md
- PROJECT_STATE.md
- CHANGELOG.md
- NEXT_TASKS.md

## Área de Trabajo (Workspace)

Antes de realizar modificaciones:

1. Identificar el archivo principal indicado por el usuario.

2. Crear o actualizar una copia de trabajo dentro de:

docs/<nombre-proyecto>/

Ejemplo:

Archivo original:

dashboard-asistencia.html

Archivo de trabajo:

docs/dashboard-asistencia/dashboard-asistencia-working.html

3. Todos los cambios deberán realizarse sobre el archivo de trabajo.

4. El archivo original permanecerá intacto como respaldo.

5. Toda la documentación del proyecto deberá reflejar el estado del archivo de trabajo.

6. Cuando el usuario indique que los cambios fueron aprobados, el archivo de trabajo podrá reemplazar al archivo original.

7. Registrar en CHANGELOG.md:
   - Fecha
   - Archivo trabajado
   - Versión modificada
   - Cambios realizados

## Creación Automática

Si la carpeta de documentación del proyecto no existe:

1. Analizar el código real.
2. Analizar HTML.
3. Analizar CSS.
4. Analizar JavaScript.
5. Analizar estructura de directorios.
6. Identificar reglas de negocio.
7. Crear automáticamente toda la documentación requerida.

La documentación debe basarse en información real encontrada en el proyecto.

No generar documentación genérica.

## Archivo Fuente de Verdad

El archivo principal indicado por el usuario será considerado la fuente oficial de la sesión.

Ejemplo:

"Trabajar sobre dashboard-asistencia-copia.html"

En ese caso:

- dashboard-asistencia-copia.html es la fuente de verdad.
- Otros archivos sólo son referencia histórica.
- La documentación debe reflejar el estado de dashboard-asistencia-copia.html.

## Procedimiento Obligatorio

### Paso 1

Identificar proyecto.

### Paso 2

Buscar documentación existente.

### Paso 3

Leer:

- PROJECT_CONTEXT.md
- ARCHITECTURE.md
- PROJECT_STATE.md
- CHANGELOG.md
- NEXT_TASKS.md

Generar un resumen del estado actual del proyecto antes de realizar cambios.

### Paso 3.5 — Validación de Skills

Antes de realizar cualquier cambio:

- Identificar skills relevantes para la tarea.
- Identificar skills opcionales.
- Identificar skills faltantes.
- Evaluar riesgos asociados.

Documentar siempre:

Skills relevantes detectadas:
- Skill A
- Skill B
- Skill C

Skills recomendadas ausentes:
- Ninguna

o

Skills recomendadas ausentes:
- Nombre de la skill

Impacto:
- Explicación del riesgo o limitación.

No iniciar cambios importantes sin completar esta validación.

### Paso 4

Analizar estructura actual del código.

### Paso 5

Ejecutar cambios solicitados.

### Paso 6

Actualizar:

- PROJECT_STATE.md
- CHANGELOG.md
- NEXT_TASKS.md (pendientes, bloqueos y próximas actividades)

### Paso 7

- Actualizar ARCHITECTURE.md cuando existan cambios técnicos o estructurales.
- Actualizar PROJECT_CONTEXT.md únicamente cuando cambien objetivos, reglas de negocio o
  requerimientos funcionales.

### Paso 8 — Cierre de sesión

Antes de dar por concluida una sesión de trabajo:

1. Revisar todos los cambios realizados.
2. Actualizar la documentación correspondiente (Pasos 6 y 7).
3. Verificar que la documentación refleje el estado real del proyecto.
4. Registrar pendientes, riesgos o tareas futuras en NEXT_TASKS.md.
5. Confirmar que código y documentación están sincronizados.
6. Ejecutar la Auditoría Obligatoria (ver sección arriba: code-auditor + ensemble-solving) para
   desarrollos relevantes — arquitectura, KPIs, filtros, performance, consistencia, riesgos y
   calidad general.

No considerar una tarea como finalizada hasta completar estos pasos.

## Restricciones

- No eliminar funcionalidades existentes.
- No romper compatibilidad.
- No modificar módulos fuera del alcance solicitado.
- Reutilizar código existente.
- Evitar duplicaciones.
- Identificar riesgos antes de modificar.
- No asumir contexto basado únicamente en conversaciones anteriores. La documentación almacenada
  en el proyecto (`docs/<nombre-proyecto>/`) tiene prioridad sobre el contexto del chat — si hay
  conflicto entre lo recordado de la conversación y lo que dice la documentación en disco, la
  documentación en disco gana.

## Manejo de Inconsistencias

Si existe una diferencia entre documentación y código:

1. Informar la inconsistencia.
2. Tomar el código como fuente de verdad.
3. Actualizar documentación.
4. Continuar el trabajo.

## Registro de Estado

Toda tarea deberá dejar actualizado:

- Estado del proyecto.
- Cambios realizados.
- Funciones agregadas.
- Funciones modificadas.
- Riesgos identificados.
- Próximos pasos sugeridos.

Este archivo debe ser consultado antes de trabajar sobre cualquier proyecto nuevo o existente.

## Regla Final Obligatoria

Resumen consolidado del procedimiento completo (detalle en las secciones de arriba) — antes de
iniciar cualquier proyecto:

1. Leer CLAUDE_GLOBAL.md.
2. Leer AI_SKILLS_BASELINE.md.
3. Leer AI_DASHBOARD_PLAYBOOK.md.
4. Leer documentación local del proyecto.
5. Identificar skills aplicables.
6. Informar skills faltantes.
7. Generar plan de trabajo.
8. Ejecutar cambios.
9. Actualizar documentación.
10. Ejecutar auditoría final usando:
    - code-auditor
    - ensemble-solving

Ningún proyecto debe considerarse completo si documentación, código, dashboards y auditoría final
no están alineados.
