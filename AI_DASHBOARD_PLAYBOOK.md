# AI Dashboard Playbook

Versión: 2.0

Este documento es la fuente de verdad para el diseño, rediseño, implementación y evolución de todos los dashboards de este repositorio.

Toda decisión de UX, UI, visualización de datos, accesibilidad, arquitectura de información y presentación ejecutiva debe seguir estas reglas.

Nota de versión (2.0): se incorpora la identidad visual oficial de ERC Capital Corp como estándar de marca obligatorio. Toda referencia previa a una paleta genérica queda sustituida por la paleta institucional definida en "Identidad Corporativa ERC Capital Corp" y "Sistema Visual Oficial". Ninguna sección, regla ni criterio de la versión 1.0 fue eliminado.

---

# Visión

Los dashboards de este repositorio NO son:

- Sistemas administrativos
- Herramientas de captura de datos
- Hojas de cálculo visuales
- Reportes operativos tradicionales

Los dashboards de este repositorio SON:

- Herramientas para toma de decisiones
- Productos analíticos
- Sistemas de visualización ejecutiva
- Instrumentos de gestión
- Presentaciones operativas y estratégicas

---

# Identidad Corporativa ERC Capital Corp

La identidad visual de ERC Capital Corp es el estándar corporativo obligatorio para todos los dashboards de este repositorio. No es una opción de estilo: es un requisito al mismo nivel que la accesibilidad o la jerarquía visual.

## Significado de la paleta

El azul institucional (Primary) transmite solidez, estabilidad financiera y autoridad — es el color con el que ERC Capital Corp debe asociarse en cualquier pantalla, con o sin logotipo visible.

El cian de marca (Secondary) transmite acción, foco y modernidad tecnológica — es el color reservado para lo que el usuario debe notar primero: acciones, elementos activos, focos de atención.

El cian claro (Supporting) transmite apoyo y contexto sin competir con la información principal — es el color de los fondos que informan pero no distraen.

El canvas neutro y el texto casi negro transmiten precisión y seriedad ejecutiva, evitando cualquier lectura "genérica" o "de plantilla".

## Principios de marca

- Todo dashboard debe ser identificable como un producto de ERC Capital Corp incluso si se oculta el logotipo, únicamente por su color, tipografía, jerarquía y estilo gráfico.
- La marca se expresa con disciplina, no con saturación: el azul institucional domina la estructura: el cian de acento se usa con moderación, reservado para lo que realmente merece atención.
- Ningún dashboard puede introducir una identidad visual paralela o alternativa a la de ERC Capital Corp.

## Consistencia visual

Todos los dashboards, sin excepción, comparten la misma paleta, la misma tipografía y el mismo sistema de jerarquía. Un usuario que pase de un dashboard a otro dentro del repositorio nunca debe sentir que cambió de producto o de proveedor.

## Experiencia corporativa

Los dashboards deben sentirse como productos propios de ERC Capital Corp.

NO como interfaces genéricas.

NO como sistemas de terceros.

NO como dashboards sin branding.

---

# Regla de Branding

Todo dashboard creado para ERC Capital Corp debe verse como un producto corporativo propio.

La marca debe ser reconocible mediante:

- color
- tipografía
- jerarquía
- estilo gráfico

aunque el logotipo no esté visible.

Esta regla aplica sin excepción a dashboards ejecutivos, analíticos y operativos, y prevalece sobre cualquier preferencia estética individual de quien implementa.

---

# Audiencias Objetivo

## Nivel Ejecutivo

- CEO
- CFO
- COO
- Junta Directiva
- Comité Ejecutivo

Objetivo:

Tomar decisiones.

Tiempo de comprensión:

Menos de 10 segundos por pantalla.

---

## Nivel Gerencial

- Directores
- Gerentes
- Recursos Humanos
- Finanzas
- Operaciones

Objetivo:

Entender tendencias y riesgos.

---

## Nivel Analítico

- Analistas
- Coordinadores
- Supervisores

Objetivo:

Explorar detalles y validar información.

---

# Regla Suprema

Toda pantalla debe responder obligatoriamente:

1. ¿Qué está pasando?
2. ¿Es bueno o malo?
3. ¿Por qué importa?
4. ¿Qué debería hacerse?

Si una pantalla no responde estas preguntas, debe ser rediseñada.

---

# Tipos de Dashboard

## Executive Dashboard

Orientado a:

- Junta
- CEO
- Gerencia

Características:

- Máximo 4 KPIs principales
- Un gráfico dominante
- Una conclusión principal
- Una implicación clara

---

## Analytical Dashboard

Orientado a:

- Analistas
- Coordinadores

Características:

- Más filtros
- Más exploración
- Más profundidad

---

## Operational Dashboard

Orientado a:

- Operaciones
- Monitoreo

Características:

- Estado en tiempo real
- Alertas
- Seguimiento

---

# Jerarquía Visual Obligatoria

Toda pantalla debe seguir este orden:

TÍTULO

↓

CONCLUSIÓN

↓

KPIs

↓

GRÁFICO PRINCIPAL

↓

INSIGHT

↓

DETALLE

Nunca alterar este orden.

---

# Principios de Diseño

## Una conclusión por pantalla

Cada vista debe comunicar una idea principal.

Evitar:

- 10 conclusiones compitiendo
- 20 KPIs con el mismo peso
- múltiples focos visuales

---

## Comparabilidad antes que decoración

Priorizar:

- interpretación
- comparación
- tendencias

sobre elementos decorativos.

---

## Espacio en blanco

El espacio vacío es una herramienta de comunicación.

Nunca intentar llenar todas las áreas disponibles.

---

## Menos es más

Eliminar:

- textos innecesarios
- etiquetas redundantes
- tarjetas sin propósito
- gráficos decorativos

---

# Sistema de KPIs

## Máximo recomendado

Dashboard ejecutivo:

- 3 a 4 KPIs principales

Dashboard analítico:

- 6 a 8 KPIs

---

## Estructura KPI

Debe incluir:

- Etiqueta
- Valor principal
- Variación
- Estado
- Contexto

---

## Prioridad visual

1. KPI crítico
2. KPI principal
3. KPI secundario
4. KPI auxiliar

No dar el mismo peso visual a todos.

---

# Estándar Financiero

## Valores negativos

Siempre usar:

Color:

#B91C1C

Peso:

600+

Ejemplos:

-100

-$100

-Q100

-5%

(100)

($100)

(Q100)

Todos deben mostrarse en rojo.

---

## Valores positivos

Color:

#15803D

Peso:

600+

Ejemplos:

+100

+$100

+5%

Q100

---

## Valores neutros

Color:

#4B5563

(Corresponde al token oficial `--text-secondary`; ver "Tokens CSS Oficiales".)

Peso:

500

---

## Indicadores visuales

Positivo:

▲

Negativo:

▼

Neutro:

●

Nunca depender únicamente del color.

---

# Sistema de Gráficos

## Gráficos preferidos

- Bar Charts
- Horizontal Bars
- Trend Charts
- Variance Charts
- Bullet Charts
- Waterfalls
- Heatmaps
- Sparklines

---

## Usar con moderación

- Donuts
- Gauge Charts

---

## Evitar

- 3D Charts
- Pie Charts múltiples
- Visualizaciones decorativas
- Gráficos difíciles de comparar

---

# Consistencia de Gráficos

Todos los gráficos del proyecto deben compartir:

- Tipografía
- Paleta
- Leyendas
- Tamaños
- Espaciados
- Sistema visual

Nunca permitir que una slide parezca pertenecer a otro producto.

---

# Diseño para Proyección

Estos dashboards podrán proyectarse en:

- Televisores
- Salones
- Gerencia
- Junta Directiva

Por lo tanto:

## Tamaños mínimos

Título:

40px+

Subtítulo:

20px+

KPI:

24px+

Texto:

14px+

Caption:

12px mínimo

Nunca menor a 12px.

---

## Visibilidad

Los KPIs principales:

- Deben verse sin scroll
- Deben estar visibles en el primer viewport

---

# Responsive

Desktop:

1920x1080

Laptop:

1366x768

Tablet:

768px

Mobile:

390px

---

## Regla importante

No reducir tipografía para hacer que todo quepa.

Si es necesario:

Usar scroll vertical.

---

# Accesibilidad

Cumplir WCAG 2.2.

Obligatorio:

- Contraste AA
- Focus visible
- Navegación por teclado
- Reduced Motion
- Roles ARIA
- Labels accesibles

---

# Sistema Visual

## Colores

La paleta genérica queda reemplazada por la identidad visual oficial de ERC Capital Corp. Ver "Identidad Corporativa ERC Capital Corp" y "Sistema Visual Oficial" para el detalle completo de roles y uso, y "Tokens CSS Oficiales" para los valores de implementación.

Resumen:

Primary Brand:

#2C5273

Secondary Brand:

#04B2D9

Supporting Brand:

#99E2F2

Canvas:

#F2F2F2

Surface:

#FFFFFF

Text:

#0D0D0D

Colores funcionales (no de marca — ver "Colores Semánticos"):

Success:

#15803D

Warning:

#CA8A04

Danger:

#B91C1C

Border:

#D9E2E8

---

## Tipografía

IBM Plex Sans

IBM Plex Mono

---

## Radios

8px

12px

16px

---

## Sombras

Muy sutiles.

Preferir:

0 1px 3px rgba(0,0,0,.08)

ó

0 4px 12px rgba(0,0,0,.05)

---

# Sistema Visual Oficial

Esta es la paleta institucional obligatoria. Reemplaza cualquier paleta genérica usada en versiones anteriores de dashboards de este repositorio.

## Primary Brand

#2C5273

Uso:

- navegación
- encabezados
- títulos
- métricas principales
- elementos institucionales

---

## Secondary Brand

#04B2D9

Uso:

- acciones
- elementos destacados
- focos visuales
- indicadores activos

---

## Supporting Brand

#99E2F2

Uso:

- fondos informativos
- paneles secundarios
- apoyo visual

---

## Canvas

#F2F2F2

Uso:

- fondo general
- layouts
- áreas de trabajo

---

## Text

#0D0D0D

Uso:

- texto principal
- tablas
- información crítica

---

# Colores Semánticos

Success, Warning y Danger se mantienen sin cambio de valor:

Success:

#15803D

Warning:

#CA8A04

Danger:

#B91C1C

Pero deben quedar aclarados:

NO son colores de marca.

Son colores funcionales.

Solamente se utilizan para comunicar:

- éxito
- advertencia
- riesgo
- estados

Nunca deben usarse para navegación, encabezados, branding ni ningún elemento institucional — ese uso corresponde exclusivamente a Primary Brand, Secondary Brand y Supporting Brand.

---

# Dashboards Financieros

Todas las visualizaciones financieras (gráficas, series, comparativos) deben utilizar exclusivamente esta asignación de color:

Serie Principal:

#2C5273

Serie Secundaria:

#04B2D9

Serie Terciaria:

#99E2F2

Positivo:

#15803D

Negativo:

#B91C1C

Advertencia:

#CA8A04

Prohibido:

- colores aleatorios
- colores automáticos de librerías
- paletas por defecto de Plotly
- paletas por defecto de Chart.js

Toda librería de gráficos usada en un dashboard de este repositorio debe configurarse explícitamente con esta paleta antes de renderizar cualquier serie. Ninguna gráfica se publica con la paleta por defecto de su librería.

---

# Tokens CSS Oficiales

Estos son los tokens de implementación oficiales. Sustituyen cualquier token de color genérico usado en versiones anteriores.

```css
:root {

  --brand-primary: #2C5273;
  --brand-secondary: #04B2D9;
  --brand-support: #99E2F2;

  --canvas: #F2F2F2;
  --surface: #FFFFFF;

  --text-primary: #0D0D0D;
  --text-secondary: #4B5563;

  --success: #15803D;
  --warning: #CA8A04;
  --danger: #B91C1C;

  --border: #D9E2E8;

}
```

---

# Regla de Gráficos

Todos los gráficos de todos los dashboards deben compartir:

- la misma paleta
- la misma tipografía
- la misma escala visual
- la misma jerarquía
- la misma filosofía de diseño

El usuario nunca debe sentir que una gráfica fue tomada de otra aplicación.

Esta regla es la extensión, aplicada a gráficos, de "Consistencia de Gráficos" y de la "Identidad Corporativa ERC Capital Corp": ambas exigen que ningún componente visual delate un origen distinto al del resto del producto.

---

# Regla de Consistencia

Todo componente nuevo debe derivarse del sistema visual institucional.

Antes de introducir un nuevo color debe justificarse:

- funcionalidad
- accesibilidad
- visualización de datos

Nunca por motivos decorativos.

Un color que no pueda justificarse por una de estas tres razones no se introduce, sin excepción.

---

# Dashboard Storytelling

Toda pantalla debe seguir:

Dato

↓

Significado

↓

Riesgo

↓

Acción

Nunca mostrar números sin contexto.

---

# Errores Comunes

Prohibido:

- KPIs escondidos
- KPIs debajo del viewport
- Gráficos inconsistentes
- Cards sin propósito
- Hover en elementos no clicables
- Exceso de donuts
- Microtexto ilegible
- Scroll horizontal
- Dashboard tipo Excel
- Dashboard tipo sistema administrativo

---

# Uso de Skills

Consulta AI_SKILLS_BASELINE.md para verificar disponibilidad, alcance e impacto de ausencias.

| Tarea | Skill principal | Complemento según alcance |
|---|---|---|
| Proyecto nuevo de dashboard | dashboard-creator | feature-planning para módulos o cambios complejos; code-auditor para validación |
| Rediseño de dashboard | redesign-existing-projects | impeccable para UX/UI; emil-design-eng para detalles |
| Mejora visual | impeccable | emil-design-eng para componentes |
| Arquitectura UX | impeccable | feature-planning para desglose funcional |
| Variantes de un componente | prototype | Solo con invocación explícita |
| Gestos y movimiento físico | apple-design | Solo cuando la interacción lo requiera |
| Auditoría y plan de animaciones | improve-animations | No implementa cambios |
| Implementación de animaciones | animate | review-animations solo con invocación explícita |
| Landing pages | design-taste-frontend | high-end-visual-design |
| Reglas de negocio y cálculos financieros | Sin skill sustitutiva | Usar el modelo oficial confirmado |

Aplica las skills de animaciones solo después de estabilizar UX/UI.
No uses las skills de landing pages como skill principal para dashboards.
Mantén las reglas institucionales por encima de las preferencias visuales de cualquier skill.

---

# Checklist Final

Antes de publicar cualquier dashboard verificar:

[ ] Se entiende en menos de 10 segundos

[ ] Tiene una conclusión principal

[ ] Los KPIs críticos son visibles

[ ] No existen elementos decorativos innecesarios

[ ] Los negativos son rojos

[ ] Los positivos son verdes

[ ] No hay texto menor a 12px

[ ] Los gráficos son consistentes

[ ] Funciona en proyector

[ ] Cumple accesibilidad

[ ] Sigue la jerarquía definida

[ ] Parece un producto ejecutivo

[ ] No parece una hoja de cálculo

[ ] No parece un sistema administrativo

[ ] Mantiene consistencia visual con el resto del repositorio

[ ] Usa exclusivamente la paleta institucional de ERC Capital Corp (Primary Brand, Secondary Brand, Supporting Brand, Canvas, Text)

[ ] Es reconocible como producto de ERC Capital Corp aun sin mostrar el logotipo

[ ] Ninguna gráfica usa la paleta por defecto de su librería

[ ] Cumple el Dashboard Validation Standard (ver sección siguiente) — trazabilidad completa del dato y consistencia matemática entre KPIs, gráficas, tablas y rankings

---

# Dashboard Validation Standard

Todo dashboard debe validar obligatoriamente la trazabilidad completa del dato:

Filtro
↓
Dataset
↓
Cálculos
↓
KPIs
↓
Gráficas
↓
Tablas
↓
Rankings
↓
Insights

Todos los elementos deben utilizar exactamente el mismo conjunto de datos.

No pueden existir diferencias de:

- Filtros.
- Agregaciones.
- Períodos.
- Departamentos.
- Fórmulas.

---

## Regla de Consistencia Matemática

Si existe cualquier discrepancia entre:

- KPI
- Tabla
- Gráfica
- Ranking
- Insight

Se considera un defecto crítico.

Debe corregirse antes de considerar el dashboard terminado.

---

## Validación de Filtros

Todos los dashboards deben validar:

### Filtro de Período

Si se selecciona:

"Todos los meses"

Todos los KPIs y tablas deben mostrar acumulados.

Las gráficas deben mostrar el detalle del mismo conjunto de datos.

La suma de la gráfica debe coincidir con los KPIs.

---

### Filtro de Departamento

Todos los cálculos deben limitarse exclusivamente al departamento seleccionado.

No deben existir componentes ignorando filtros.

---

### Consistencia Global

KPIs, tablas, rankings, gráficas y análisis deben responder exactamente al mismo contexto de filtros.

---

Generado con IA (Claude — ERC AI Workspace) | Propiedad ERC Capital Corp | Requiere validación del responsable.
