# AI Skills Baseline

## Propósito y verificación
Usa este catálogo como mapa de selección; comprueba la disponibilidad en cada repositorio.
Identifica el tipo de tarea antes de seleccionar skills.
Comprueba que puedes leer el SKILL.md de cada skill pertinente en .claude/skills/ o en una ubicación expuesta por la herramienta.
Contrasta skills-lock.json si existe; no equipares una entrada del lock con una skill utilizable.
Informa skills activadas, skills ausentes e impacto concreto antes de editar.
Continúa con revisión manual y las capacidades verificadas cuando falte una skill.
No declares usada una skill cuyo contenido no hayas leído.
Respeta CLAUDE.md y la identidad del playbook por encima de preferencias internas de las skills.

## Mapa tarea → skill
| Tarea | Skill | Aplicación |
|---|---|---|
| Arquitectura, calidad, seguridad y rendimiento | code-auditor | Obligatoria para refactorizaciones importantes, dashboards empresariales y sistemas productivos |
| Requerimientos, roadmaps y desglose funcional | feature-planning | Obligatoria para nuevos módulos y cambios complejos |
| Comparar enfoques y resolver decisiones difíciles | ensemble-solving | Obligatoria para problemas difíciles, inconsistencias de negocio y reestructuraciones |
| Refactorización masiva y duplicidad | code-refactor | Seleccionar para reestructurar lógica |
| Documentación técnica, APIs y diseño técnico | technical-doc-creator | Genera documentación visual HTML; no sustituye los Markdown de continuidad |
| Documentar proyectos y código heredado | codebase-documenter | Seleccionar para documentación basada en código |
| Corregir fallos de pruebas | test-fixing | Seleccionar para estabilización |
| Aplicar comentarios de revisión | review-implementing | Seleccionar para correcciones de revisión |
| Inicializar proyectos | project-bootstrapper | Subordinar al bootstrap documental de CLAUDE.md |
| Dashboards, layouts ejecutivos, KPIs y gráficas | dashboard-creator | Principal para dashboards; usar code-auditor en la validación |
| Diagramas de arquitectura y datos | architecture-diagram-creator | Seleccionar para documentación visual de arquitectura |
| Flujos operativos y procesos | flowchart-creator | Verificar disponibilidad antes de usar |
| Cronogramas y planes de implementación | timeline-creator | Verificar disponibilidad antes de usar |
| Commit, push y convenciones de versiones | git-pushing | Usar únicamente para la operación solicitada explícitamente en ese momento |
| Metadatos e inventarios de archivos | file-operations | Verificar disponibilidad antes de usar |
| Trasladar código entre archivos | code-transfer | Verificar disponibilidad antes de usar |
| Automatizar análisis mediante ejecución local | code-execution | Revisar código y alcance antes de ejecutar |
| Analizar conversaciones previas | conversation-analyzer | Verificar disponibilidad antes de usar |
| Crear variantes comparables de un componente | prototype | Solo invocación explícita; no usar para arquitectura UX general |
| Afinar componentes e interacciones | emil-design-eng | Aplicar sin sustituir la identidad institucional |
| Gestos, movimiento físico y continuidad espacial | apple-design | Aplicar solo cuando la interacción lo requiera |
| Arquitectura UX, jerarquía, accesibilidad y pulido UI | impeccable | Seleccionar para evaluación y mejora de interfaz |
| Rediseñar una interfaz existente | redesign-existing-projects | Principal para rediseño |
| Auditar movimiento y planificar mejoras | improve-animations | Solo análisis y plan; no implementa |
| Implementar animaciones | animate | Usar después de estabilizar UX/UI |
| Revisar código de movimiento | review-animations | Solo invocación explícita; no sustituye una auditoría general |
| Diseñar landing pages y portafolios | design-taste-frontend | No usar para dashboards ni tablas de datos |
| Acabado visual de landing pages | high-end-visual-design | Subordinar tipografía, color y movimiento al playbook |

## Trabajo sin skill sustitutiva
Obtén reglas de negocio y cálculos financieros del modelo oficial confirmado; ninguna skill del mapa reemplaza esa definición.
Si falta una skill de flujos o cronogramas, informa que no hay cobertura especializada disponible y realiza la tarea manualmente sin inventar reemplazos.
Usa únicamente capacidades comprobadas de la herramienta para ejecutar el flujo de una skill.
Comprueba dependencias adicionales antes de delegar o ejecutar automatizaciones.

## Obligatoriedad por tipo de trabajo
Aplica las skills obligatorias del mapa cuando estén disponibles y sean compatibles con el alcance autorizado.
Para dashboards empresariales, realiza auditoría conceptual de arquitectura, KPIs, filtros, rendimiento, consistencia, riesgos y calidad con code-auditor.
Para decisiones difíciles, inconsistencias de negocio y reestructuraciones, compara enfoques con ensemble-solving.
Si una obligatoria está ausente, declara qué revisión especializada falta y realiza la comprobación manual equivalente sin bloquear el trabajo.
Respeta la invocación explícita exigida por prototype y review-animations; no actives sus flujos automáticamente.

## Instalación
Conserva este comando para instalar code-auditor desde la fuente del catálogo:
~~~sh
npx skills add mhattingpete/claude-skills-marketplace --skill code-auditor --agent claude-code
~~~
Para otra skill, usa su identificador exacto y una fuente comprobada en skills-lock.json o documentación del proveedor.
No atribuyas todas las skills a la fuente del ejemplo.
Para git-pushing sin fuente comprobada, informa [VERIFICAR: fuente y comando de instalación de git-pushing].
Si faltan Node.js, npx o acceso a la fuente, informa la limitación y continúa sin instalar.
No instales skills automáticamente como requisito para continuar la tarea.

## Riesgos propios de los flujos
Revisa el encadenamiento de feature-planning hacia plan-implementer y git-pushing antes de ejecutarlo; verifica esas dependencias por separado.
Mantén la autorización puntual de commit y push incluso si una skill propone automatizarlos.
Reserva ensemble-solving para decisiones de alto impacto; su flujo con tres subagentes puede multiplicar aproximadamente por cuatro el consumo de tokens.
Comprueba code-execution antes de usar la delegación de code-refactor para operaciones de diez o más archivos.
Revisa code-execution antes de ejecutarla; permite correr Python local y código arbitrario.
Adecua las salidas HTML de technical-doc-creator y architecture-diagram-creator al formato solicitado sin reemplazar los archivos de continuidad.
Verifica evaluaciones de seguridad de dependencias en la versión que se vaya a usar; no reutilices calificaciones históricas como garantía.

## Informe obligatorio
Enumera las skills activadas y el propósito de cada una.
Enumera las skills recomendadas ausentes o declara ninguna.
Describe el impacto de cada ausencia y la comprobación manual prevista.
Identifica dependencias o capacidades no verificadas sin presentarlas como disponibles.

Generado con IA (Claude — ERC AI Workspace) | Propiedad ERC Capital Corp | Requiere validación del responsable.
