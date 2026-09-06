# Instrucciones del repositorio
RAIZ_HTML: html/
RAIZ_DOCS: docs/

## Configuración
Usa rutas relativas al repositorio y separador "/"; nunca guardes rutas absolutas.
Al cambiar de equipo, edita únicamente RAIZ_HTML y RAIZ_DOCS si cambian las carpetas.
Interpreta toda referencia a html/ y docs/ en los tres estándares como RAIZ_HTML y RAIZ_DOCS.
Resuelve las rutas registradas desde la raíz del repositorio.
Importa los dos estándares con la sintaxis soportada por Claude Code:
@AI_DASHBOARD_PLAYBOOK.md
@AI_SKILLS_BASELINE.md
Declara ambos imports como excepción de carga automática al nivel 2; aplica sus secciones según la tarea.

## Verificación previa a cualquier tarea
1. Confirma AI_DASHBOARD_PLAYBOOK.md y AI_SKILLS_BASELINE.md junto a este archivo; si falta alguno, detente e indica su nombre.
2. Confirma RAIZ_HTML; si falta, no la crees: lista las carpetas del repositorio que realmente contengan .html y pregunta cuál usar.
3. Si no encuentras ningún .html, informa cero candidatos y pide la ubicación relativa de los originales; espera a que exista y sea confirmada.
4. Actualiza RAIZ_HTML con la respuesta verificada antes de continuar.
5. Registra si RAIZ_DOCS/INDEX.md existe ANTES de crear carpetas o archivos: ausente significa BOOTSTRAP; presente significa TRABAJO.
6. Si falta RAIZ_DOCS, créala con INDEX.md y _templates/ e informa la creación; conserva BOOTSTRAP para completar ese índice.
7. Si existe RAIZ_DOCS pero falta INDEX.md, ejecuta BOOTSTRAP; si solo falta _templates/, regénérala con los contratos de este archivo.
8. Verifica las skills del mapa del baseline mediante su SKILL.md accesible y contrasta skills-lock.json si existe; informa ausencias e impacto sin bloquear.
9. Si falta skills-lock.json o .claude/skills/, informa la ausencia; usa solo capacidades cuya disponibilidad puedas comprobar.
10. Pregunta por toda referencia ausente antes de sustituirla; exceptúa únicamente la creación documental y el bootstrap autorizados aquí.

## MODO BOOTSTRAP
Inventaría recursivamente todos los .html de RAIZ_HTML sin abrir su contenido.
Crea INDEX.md con columnas proyecto | archivo original | carpeta docs | estado | última sesión.
Registra un renglón por HTML, con estado sin-documentar y última sesión no registrada.
Conserva las carpetas de proyectos existentes y registra también las que carezcan de original, indicando original no localizado.
Deriva proyecto del nombre sin .html; conserva subcarpetas relativas para evitar colisiones.
Crea _templates/ con los cinco contratos de plantilla definidos abajo.
No documentes ningún proyecto durante BOOTSTRAP.
Informa N dashboards detectados y termina el bootstrap antes de atender una tarea de proyecto.

## Lectura por niveles
Nivel 0 automático: lee este archivo y los dos imports declarados.
Nivel 1 al nombrar proyecto: lee INDEX.md, después el YAML inicial de PROJECT_STATE.md y NEXT_TASKS.md de su carpeta.
Nivel 2 según tarea: consulta el playbook para diseño y el baseline para skills; lee ARCHITECTURE.md para estructura y PROJECT_CONTEXT.md para reglas de negocio.
Nivel 3 nunca automático: abre notas/, historial/ o el HTML completo solo si la tarea lo requiere explícitamente; busca primero fragmentos relevantes.
Si falta el YAML de un proyecto existente, informa formato legado y lee solo las secciones de estado vigente necesarias para resolver la fuente.
Si la petición es ambigua, muestra las coincidencias reales del índice y pide identificar proyecto y alcance antes de editar.
Si el proyecto no existe, informa la ausencia y pregunta si se desea crear o cuál es el proyecto correcto; no inventes su original.

## Reglas no negociables
1. Aplica la paleta institucional: marca #2C5273, #04B2D9, #99E2F2; canvas #F2F2F2, superficie #FFFFFF, texto #0D0D0D y colores semánticos del playbook.
2. Ordena cada pantalla TÍTULO → CONCLUSIÓN → KPI → GRÁFICO → INSIGHT → DETALLE.
3. Mantén todo texto en 12px o más y respeta los mínimos superiores de tipografía y proyección del playbook.
4. Ejecuta commit o push únicamente ante una petición explícita del usuario en ese momento para esa operación.
5. Edita únicamente el archivo de trabajo como fuente de verdad y promuévelo al original en RAIZ_HTML solo tras aprobación explícita de la promoción.
6. Asigna un solo agente escritor al archivo de trabajo, registra agente_activo y espera su liberación antes de transferirlo.
7. Al cerrar sesión, retira información obsoleta, actualiza estado y tareas abiertas, registra cambios y libera agente_activo.
8. Respeta los presupuestos como límites duros contando todas las líneas; comprime antes de agregar y rota CHANGELOG cuando corresponda.
9. Conserva funciones y compatibilidad dentro del alcance solicitado y verifica filtros, cálculos, KPIs, gráficas, tablas, rankings e insights sobre el mismo dataset.
10. Informa discrepancias entre documentación y código, usa el código para describir lo implementado y actualiza la documentación sin convertir defectos en reglas de negocio.

## Enrutamiento
| Si la tarea es | Lee | Usa la skill si está disponible |
|---|---|---|
| Crear dashboard | Playbook y baseline | dashboard-creator |
| Rediseñar dashboard | Playbook y baseline | redesign-existing-projects |
| Mejorar UX/UI | Playbook y baseline | impeccable; emil-design-eng para detalles |
| Planificar módulo o cambio complejo | Baseline y ARCHITECTURE.md | feature-planning |
| Auditar o refactorizar | Baseline y ARCHITECTURE.md | code-auditor; code-refactor para refactorización |
| Resolver problema difícil | Baseline y contexto pertinente | ensemble-solving |
| Documentar código existente | Baseline y fragmentos pertinentes | codebase-documenter |
| Corregir pruebas | Baseline y ARCHITECTURE.md | test-fixing |
| Auditar o implementar movimiento | Playbook y baseline | improve-animations para plan; animate para implementación |
| Prototipar variantes o revisar movimiento | Playbook y baseline | prototype o review-animations solo con invocación explícita |
| Diseñar landing | Playbook y baseline | design-taste-frontend; high-end-visual-design |
| Cambiar reglas de negocio | PROJECT_CONTEXT.md y modelo oficial localizado | Sin skill que sustituya la definición del responsable |

## Ritual antes de la primera edición
Emite el siguiente bloque con valores observados; usa "no registrado" cuando no haya evidencia y detente si falta una decisión necesaria.
Para bootstrap o mantenimiento global, indica proyecto "repositorio", estado observado y fuente documental; no atribuyas implementación a dashboards.
Formato obligatorio: ── Arranque ──
Leído: enumera los archivos realmente leídos.
Proyecto: nombre confirmado · Estado: estado observado · Última sesión: fecha documentada o no registrada.
Fuente de verdad: ruta verificada del archivo que editarás.
Ya implementado: hechos comprobados. Pendiente: tareas abiertas comprobadas.
Skills activadas: nombres. Skills ausentes: nombres e impacto, o ninguna.
Reglas aplicables a esta tarea: enumera las reglas concretas.
Plan: enumera los pasos previos a la edición.

## Estructura y presupuestos
Vincula html/<proyecto>.html ⇄ docs/<proyecto>/ usando las raíces configuradas.
| Recurso por proyecto | Máximo de líneas | Modo | Contenido |
|---|---:|---|---|
| PROJECT_STATE.md | 200 | sobrescribir | YAML de estado al inicio |
| NEXT_TASKS.md | 150 | sobrescribir | Solo tareas abiertas y aceptación |
| ARCHITECTURE.md | 400 | sobrescribir | Arquitectura vigente |
| PROJECT_CONTEXT.md | 150 | sobrescribir, casi inmutable | Objetivos y reglas aprobadas |
| CHANGELOG.md | 300 | agregar y rotar | Cambios y validación por sesión |
| trabajo/ | Un archivo de trabajo | editar | Fuente de verdad |
| notas/ | Libre | mantener | Lectura no obligatoria |
| historial/ | Libre | agregar | CHANGELOG rotado |
Crea documentación de proyecto solo al trabajar explícitamente en él, después de BOOTSTRAP.
Encabeza cada plantilla con un comentario HTML que indique presupuesto y modo; coloca inmediatamente después el YAML de PROJECT_STATE.md.
Define el YAML con proyecto, fuente_de_verdad, original, sincronizado_con_original, ultima_sesion, agente_activo, estado, implementado, en_progreso, no_implementado y bloqueos.
Inicializa valores desconocidos con null, listas con [], estado con sin-documentar y sincronizado_con_original con null hasta comparar archivos.
Incluye en NEXT_TASKS tarea, prioridad, aceptación y bloqueo; en ARCHITECTURE componentes, datos, dependencias y validación; en PROJECT_CONTEXT objetivo, audiencia, alcance y reglas aprobadas; en CHANGELOG fecha, cambio y validación.
Genera las cinco plantillas desde estos contratos si se copiaron únicamente los tres estándares; no dependas de archivos externos para arrancar.
Si no hay archivo de trabajo ni antecedentes de divergencia, copia el original verificado a trabajo/ conservando su nombre y registra la ruta antes de editar código.
Si hay varias copias o una fuente fuera de trabajo/, informa las rutas reales y acuerda su migración; no sobrescribas ni elijas por fecha de modificación.
Actualiza INDEX.md al cerrar una sesión de proyecto con estado y fecha sustentados.
Rota entradas completas antiguas de CHANGELOG a historial/CHANGELOG-AAAA-MM-DD-N.md usando fecha real y el primer N libre; conserva enlaces desde CHANGELOG.
Actualiza ARCHITECTURE cuando cambie la estructura y PROJECT_CONTEXT únicamente al cambiar objetivos o reglas aprobadas.
Valida desarrollos relevantes con code-auditor y usa ensemble-solving para decisiones difíciles; si faltan, informa el impacto y realiza la revisión manual equivalente.

## Casos borde y prioridad
Resuelve conflictos documentales con este orden: CLAUDE.md → AI_DASHBOARD_PLAYBOOK.md → AI_SKILLS_BASELINE.md → PROJECT_CONTEXT.md → PROJECT_STATE.md → NEXT_TASKS.md → ARCHITECTURE.md → CHANGELOG.md → notas e historial; informa qué instrucción prevalece.
Respeta las instrucciones explícitas vigentes del usuario y las restricciones superiores de la herramienta.
Ante documentación contra código, usa el código para el estado implementado e informa y corrige la documentación.
Ante referencia ausente no autorizada para creación, detén solo el trabajo dependiente y pregunta por la ubicación correcta.
Ante un archivo excedido, comprime lo vigente y retira lo obsoleto antes de agregar; conserva historial mediante la rotación indicada.
Ante un empate o contradicción no resuelta, pregunta antes de editar el recurso afectado.

Generado con IA (Claude — ERC AI Workspace) | Propiedad ERC Capital Corp | Requiere validación del responsable.
