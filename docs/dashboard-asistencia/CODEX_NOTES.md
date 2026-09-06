# Notas de continuidad de Codex

## Cierre documental — 2026-09-06

Estado vigente: ronda Codex 37 completada. El resumen inicial antiguo y entradas anteriores
se conservan como historial; prevalecen las rondas finales y el cierre de PROJECT_STATE.md.
Se actualizaron PROJECT_CONTEXT.md, PROJECT_STATE.md, NEXT_TASKS.md, ARCHITECTURE.md y CHANGELOG.md.
Inventario con rutas completas y hashes: SESSION_CLOSE_INVENTORY.md. No se modificó código en
este cierre, ni .gitignore, ni se hizo stage/commit/publicación. Documentación principal antes de
este cierre estaba rezagada; ahora incorpora la divergencia Codex y los cuatro pendientes solicitados.


**Estado vigente:** corrección de especificidad del Pendiente A implementada únicamente en la
copia Codex y comprobada en Chrome. Tamaños correctos en escritorio y en la media query móvil;
se detectaron limitaciones de layout en anchos reducidos y montos extremos, documentadas en la
entrada de implementación al final. El diagnóstico inicial se conserva como historial.

## 2026-09-05 — Copia independiente y diagnóstico del Pendiente A

### Alcance y fuente de trabajo

Por instrucción expresa del responsable, se creó `dashboard-asistencia-working-codex.html`
como copia binaria exacta de `dashboard-asistencia-working.html`, ambos en esta carpeta.
La separación solicitada se materializó en el archivo de trabajo independiente; no se creó una
rama de Git ni se hizo commit o publicación.

**Desde esta instrucción, Codex debe trabajar exclusivamente sobre
`docs/dashboard-asistencia/dashboard-asistencia-working-codex.html` para cambios de la aplicación.
No modificar `dashboard-asistencia-working.html` nunca más.** Esta instrucción sustituye para
Codex las referencias anteriores al working original como destino de edición. Las notas de
continuidad de Codex se registran en este documento.

- Tamaño de cada HTML: **574,892 bytes**.
- Comparación byte por byte: **idénticos**.
- SHA-256 de ambos: `B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
- No se modificó el contenido de ninguno de los dos HTML durante el diagnóstico.
- No se implementó ninguna corrección ni se modificó funcionalidad, fórmulas, filtros o datos.
- No se trabajó en el Pendiente B.

### Resultado

**La hipótesis principal de NEXT_TASKS.md queda confirmada en Chrome real:** las clases
`.valor-monetario-sm` y `.valor-monetario-xs` pueden reemplazar el tamaño tipográfico de la franja
porque se aplican sobre el MISMO elemento que `.veredicto-cifra-principal` o
`.veredicto-cifra-secundaria`, tienen igual especificidad y están declaradas después.

Con los montos de prueba de once caracteres, ambas cifras terminan en **13.12px**, no en 64/56px.
La apreciación anterior de «aproximadamente 20px» era un reporte visual; no es el valor computado
obtenido en esta prueba. Fila 1 sí conserva sus **30px**, porque su selector incluye un ID.

### Ubicación exacta del código involucrado

Referencias al archivo **dashboard-asistencia-working-codex.html**, con la numeración vigente al
crear la copia y el hash anterior. Los enlaces son relativos a esta carpeta; los rangos se
indican como texto para facilitar la búsqueda.

| Líneas | Código / responsabilidad |
|---|---|
| 4633–7647 | `construirHTMLEjecutivo(datos)`: función que genera el documento ejecutivo independiente. |
| 4647–4656 | Inicio del template literal, documento, viewport, fuentes, dependencia Chart.js y estilos. |
| 4707 | Tokens: `--txt-cifra-franja:4rem`, `--txt-cifra-franja-sec:3.5rem`, `--txt-cifra-fila1:1.875rem`. |
| 4713–4714 | Reset y `body`: no establecen un tamaño tipográfico base distinto del predeterminado. |
| 5041 | `#kpisEjecutivosFila1 .kpi-value`: aplica el token de 30px con especificidad (1,1,0). |
| 5093–5094 | `.veredicto-cifras` y `.veredicto-bloque`: contenedores flex, sin `font-size` propio. El padre de cada cifra mide 16px en la prueba. |
| 5096–5103 | Selectores principal/secundario: tamaño mediante tokens, pesos 800/700, interlineado 1.05 y colores rojo/ámbar. Especificidad (0,1,0). |
| 5120–5125 | Media query hasta 640px: disposición vertical y tamaños 2.6rem/2.2rem. |
| 5214–5216 | `.valor-monetario` conserva `nowrap`; `-sm` aplica `0.82em` y `-xs`, `0.65em`, con especificidad (0,1,0). Estas últimas declaraciones ganan por orden. |
| 5221 | `.valor-centavos { font-size:0.72em; }`: reducción adicional en un elemento hijo. |
| 5828–5833 | `claseValorLongitud(texto)`: más de 14 caracteres → `-xs`; más de 10 → `-sm`; en otro caso sin modificador. |
| 6788–6794 | Formateo monetario y `cifraFranjaSpan()`: concatena clase de franja, `valor-monetario` y el modificador de longitud en un solo span. |
| 6795–6809 | Ramas sin costo y con pérdida completamente regularizada: también utilizan el helper de la franja. |
| 6843–6849 | Rama de dos cifras: principal «Pérdida confirmada» y secundaria «Exposición máxima», ambas creadas por el helper. |
| 6925–6929 | Montos de Fila 1: reciben modificadores de longitud, pero el selector con ID protege su tamaño de 30px. |

### Cadena causal

1. El formateador produce un monto como `Q 152,198.65` (espacio no separable, longitud 11).
2. `claseValorLongitud()` devuelve `valor-monetario-sm` porque la longitud supera 10.
3. `cifraFranjaSpan()` coloca esa clase junto a `veredicto-cifra-principal` en el mismo span.
4. Ambas reglas tienen especificidad (0,1,0); gana `-sm`, por aparecer después en la hoja.
5. Para `font-size`, `0.82em` se resuelve respecto al tamaño COMPUTADO DEL PADRE: 16px.
   El resultado es **16 × 0.82 = 13.12px**. No multiplica 64px: esa declaración perdió la cascada.
6. Los centavos son un span hijo y multiplican el resultado: **13.12 × 0.72 = 9.4464px**.

Con `-xs`, la misma causa da **16 × 0.65 = 10.4px**. Un monto corto que no activa ninguno de
estos modificadores no sufre esta colisión. Esto explica por qué una prueba de «Período limpio»
con `Q0.00` puede aparentar que el tamaño de la franja funciona correctamente.

### CSS esperado frente al realmente aplicado

Con raíz de 16px, que fue la medida real en Chrome:

| Elemento / viewport | Esperado según la declaración de franja | Computado con monto largo `-sm` |
|---|---|---|
| Principal, ancho >640px | `4rem` = **64px** | `0.82em` = **13.12px** |
| Secundaria, ancho >640px | `3.5rem` = **56px** | `0.82em` = **13.12px** |
| Principal, ancho ≤640px | `2.6rem` = **41.6px** | **13.12px** |
| Secundaria, ancho ≤640px | `2.2rem` = **35.2px** | **13.12px** |
| Cifra de Fila 1 | `1.875rem` = **30px** | **30px** |
| Centavos de la principal, escritorio | 72% de 64px = **46.08px** | **9.4464px** |
| Centavos de la secundaria, escritorio | 72% de 56px = **40.32px** | **9.4464px** |

Los tamaños móviles existentes son una excepción explícita en el CSS a la banda de proyección
56–64px. Corregir el pendiente no debe borrarlos inadvertidamente; exigir también esa banda en
móvil sería una decisión adicional de diseño.

Otras propiedades medidas y conservadas en la franja: `font-weight` 800/700, `white-space:nowrap`,
color principal `rgb(185, 28, 28)` y secundario `rgb(202, 138, 4)`. El `line-height` efectivo de
ambas cifras es 13.776px, consecuencia de 13.12px × 1.05. El defecto no elimina los tokens ni los
colores: sustituye la declaración ganadora de `font-size`.

### Verificación realizada y límites

- Se leyó únicamente la copia Codex para extraer la función generadora real.
- Se evaluó `construirHTMLEjecutivo()` en Node con su cuerpo literal completo, sin aproximar su
  salida por búsqueda de marcadores internos. Se proporcionaron datos sintéticos con la estructura
  necesaria y montos de longitud representativa, sin nombres ni salarios personales reales.
- Se comprobó sintaxis del script administrativo completo y del script del HTML efectivamente
  generado mediante `vm.Script`. Ambos pasaron.
- Se abrió ese HTML generado, sin cambios de CSS/JS, mediante `file://` en **Chrome headless
  152.0.7977.76**, con perfil temporal independiente. Es el motor real de navegador, no un DOM simulado.
- Se consultaron `getComputedStyle()` y las reglas coincidentes de la hoja CSS a anchos
  **1920, 1366, 768 y 390px**, altura 1080px, escala de dispositivo 1. En los cuatro casos:
  raíz/padre 16px, principal/secundaria 13.12px y Fila 1 30px.
- Control causal en el DOM temporal a 390px, sin editar archivos: el mismo span principal pasó
  de **41.6px sin modificador** a **13.12px con `-sm`** y **10.4px con `-xs`**. Se restauró la
  clase original al finalizar el control. No se inyectó ni implementó el CSS propuesto.
- Se inspeccionó una captura del documento a **1366×768**: la franja presenta cifras menores que
  Fila 1, reproduciendo visualmente el síntoma. No hubo excepciones JavaScript registradas por CDP.
- No se cargó un Excel real, no se validaron cálculos financieros ni el flujo administrativo
  completo. El objetivo exclusivo fue aislar la cascada de la franja. Tampoco se certificó
  legibilidad a distancia de proyección, otros navegadores ni el layout posterior a una corrección.
- El diagnóstico necesitó ejecución fuera del sandbox para conectar con el Chrome local; la
  conexión restringida devolvía `ECONNREFUSED`. La medición exitosa se realizó después de la
  autorización. Se cerró la instancia conectada al terminar.

Artefactos auxiliares, fuera del proyecto, en el directorio temporal
`C:/Users/LEANDR~1/AppData/Local/Temp/codex-asistencia-pendiente-a/`:
`diagnose.cjs` (procedimiento reproducible), `ejecutivo-diagnostico.html` (salida real del
generador con datos sintéticos), `resultado.json` (mediciones y reglas) y `antes-1366.png`
(captura inspeccionada). Son temporales y pueden desaparecer; los resultados necesarios para
continuidad quedan registrados aquí. No se reemplazó el ejemplo ejecutivo existente del proyecto.

### Propuesta de corrección — NO implementada

**Recomendación: dar prioridad explícita al tamaño propio de la franja mediante selectores
acotados al componente**, calificando ambas reglas con `.veredicto-cifras`:
`.veredicto-cifras .veredicto-cifra-principal` y
`.veredicto-cifras .veredicto-cifra-secundaria`. Su especificidad (0,2,0) vence a los modificadores
genéricos (0,1,0) sin depender del orden de declaración ni utilizar `!important`.

El mismo ajuste de especificidad debe aplicarse a las DOS reglas de tamaño dentro de la media
query de 640px. De lo contrario, las reglas desktop más específicas anularían accidentalmente
los tamaños móviles. Mantener los valores de tokens, pesos, colores, centavos y `nowrap`.

Alternativa igualmente acotada: dejar de añadir los modificadores `-sm/-xs` en
`cifraFranjaSpan()` exclusivamente, conservando `valor-monetario`. Evita la colisión y respeta
automáticamente la media query existente, pero cambia la construcción del HTML y la política
de reducción por longitud del helper. Se prefiere la solución CSS para mantener el cambio en
presentación. No combinar ambas estrategias sin necesidad.

No se recomienda aumentar los tokens (seguirían perdiendo la cascada), cambiar el tamaño del
padre (alteraría otros textos), eliminar globalmente `-sm/-xs` (afectaría tablas y tarjetas),
ni limitarse a mover las reglas al final de la hoja (solución dependiente del orden).

### Riesgos y condiciones para una futura implementación

1. **Desbordamiento al recuperar el tamaño:** `nowrap`, dos montos lado a lado, separación de
   56px, padding y columna lateral de 240px pueden dejar de caber con montos largos, especialmente
   en tablet y laptop. La corrección de cascada no certifica automáticamente el layout final.
2. **Regresión móvil por especificidad:** deben actualizarse las reglas base y las móviles de
   forma coherente, preservando la disposición vertical. Probar el límite 640/641px.
3. **Jerarquía frente a adaptación monetaria:** al proteger la franja, sus modificadores de
   longitud dejarán de reducir el tamaño. Verificar cantidades cortas, `-sm` y `-xs`, sin abreviar
   dinero ni recortar cifras. Si no caben, evaluar distribución/espacio antes de volver a reducir
   por debajo de la jerarquía exigida.
4. **Centavos y altura:** crecerán proporcionalmente con el monto y cambiará la altura de línea;
   revisar separación de etiquetas, cifras, divisor y textos de contexto.
5. **Plantilla anidada:** aunque el cambio sea CSS del ejecutivo, un escape/backtick incorrecto
   puede romper el script administrativo completo. Mantener las precauciones de ARCHITECTURE.md.
6. **Alcance compartido:** no modificar las clases monetarias globales ni los estilos del
   administrativo para resolver un problema exclusivo de la franja ejecutiva.
7. **Validación futura mínima:** ambas capas de sintaxis, generación real, funcionamiento de las
   tres zonas de carga, estilos computados, captura visual, estados limpio/regularizado/mixto,
   filtros de mes y departamento, viewports desktop/laptop/tablet/móvil y montos largos.
   Comprobar con fuentes cargadas, zoom y configuración de proyección habituales.

**Estado al cerrar:** Pendiente A diagnosticado y causa reproducida; corrección solamente
propuesta. La copia Codex continúa idéntica al original. El siguiente paso requiere la instrucción
del responsable para implementar, conforme a la restricción de este turno de diagnóstico exclusivo.

## 2026-09-05 — Implementación autorizada del Pendiente A

### Cambio aplicado

El responsable autorizó corregir la especificidad únicamente en
`dashboard-asistencia-working-codex.html`, verificar antes/después en Chrome y revisar responsive.
Se modificaron **cuatro líneas**, sin agregar reglas ni cambiar valores:

- Línea 5096: selector principal calificado con `.veredicto-cifras`.
- Línea 5101: selector secundario calificado con `.veredicto-cifras`.
- Líneas 5123 y 5124: la misma calificación en ambos selectores dentro de
  `@media (max-width:640px)`.

Los selectores resultantes son `.veredicto-cifras .veredicto-cifra-principal` y
`.veredicto-cifras .veredicto-cifra-secundaria`, con especificidad (0,2,0), superior al (0,1,0)
de `.valor-monetario-sm` y `.valor-monetario-xs`. Las reglas móviles conservan la misma
especificidad que las base y ganan por orden cuando su condición es verdadera.
No se utilizó `!important`.

Tokens, tamaños móviles, colores, pesos, centavos, formato monetario, funciones JavaScript,
cálculos y Pendiente B permanecen sin cambios. No se modificó el working original.

### Evidencia de Chrome: antes y después

Chrome headless **152.0.7977.76**, motor real, perfil temporal, raíz de 16px, escala de dispositivo
1. El HTML se generó ejecutando la función real completa de cada versión, con el mismo objeto
sintético de prueba. Se esperó `document.fonts.ready`; IBM Plex Sans disponible en las mediciones
de layout. Las cifras de referencia son de longitud representativa, no una validación financiera.

La medición previa se repitió antes de editar la copia y confirmó el diagnóstico. Después del
cambio se volvió a generar y abrir el ejecutivo para medirlo: no se inyectó una hoja CSS de prueba
ni se parcheó el DOM para obtener los valores de esta tabla.

| Ancho de viewport | Principal antes | Principal después | Secundaria antes | Secundaria después | Dirección de las cifras después |
|---|---|---|---|---|---|
| 1920px | 13.12px | **64px** | 13.12px | **56px** | horizontal |
| 1366px | 13.12px | **64px** | 13.12px | **56px** | horizontal |
| 768px | 13.12px | **64px** | 13.12px | **56px** | horizontal |
| 641px | 13.12px | **64px** | 13.12px | **56px** | horizontal |
| 640px | 13.12px | **41.6px** | 13.12px | **35.2px** | vertical |
| 390px | 13.12px | **41.6px** | 13.12px | **35.2px** | vertical |

Las filas 641/640px comprueban explícitamente el límite responsive: la corrección base no anula
la media query móvil. Los valores anteriores de esos dos anchos se completaron en una segunda
corrida leyendo el original intacto como referencia, sin editarlo. Altura de viewport de las
mediciones comparativas: 1080px. Fila 1 permanece en **30px en todos los anchos**.

Centavos después: **46.08px / 40.32px** en escritorio y **29.952px / 25.344px** en móvil
(principal/secundaria). Pesos 800/700 y colores rojo/ámbar conservados. Interlineados de escritorio
67.2px/58.8px, coherentes con `line-height:1.05`.

Controles adicionales de render a 1366px:

- Montos cortos sin modificador: 64px/56px.
- Montos con `-sm`: antes 13.12px/13.12px; después 64px/56px.
- Montos con `-xs`: antes 10.4px/10.4px; después 64px/56px.
- Estado completamente regularizado: principal de 64px, sin segunda cifra.
- Estado limpio: principal de 64px, sin segunda cifra.
- Control temporal de clases a 390px: principal de 41.6px tanto sin modificador como con `-sm`
  o `-xs`; se restauraron las clases al terminar. Estos controles auxiliares no alteran archivos.

Se inspeccionaron las capturas posteriores de escritorio y móvil. En escritorio, con los montos
representativos, la franja recupera la jerarquía dominante y las dos cifras caben.

### Revisión responsive: limitaciones reales detectadas

**Las reglas tipográficas responsive funcionan; el layout completo NO queda validado como
libre de desbordamiento.** Se conserva el cambio limitado de cuatro selectores solicitado,
documentando los resultados sin presentar el responsive como resuelto.

| Ancho | Ancho disponible para cifras | Contenido antes (`scrollWidth`) | Contenido después (`scrollWidth`) | Resultado |
|---|---|---|---|---|
| 1920px | 1023px | 1023px | 1023px | Sin desbordamiento de la franja con montos representativos. |
| 1366px | 974px | 974px | 974px | Sin desbordamiento de la franja con montos representativos. |
| 768px | 376px | 376px | 818px | Restaurar 64/56px expone falta de espacio para dos cifras en horizontal. |
| 641px | 249px | 281px | 818px | Desbordamiento interno previo que aumenta al restaurar tamaños. |
| 640px | 248px | 248px | 248px | La disposición vertical permite que estos montos quepan. |
| 390px | 0px | 87px | 242px | La columna lateral fija consume el espacio; defecto estructural previo, agravado visualmente por las cifras mayores. |

La comparación se completó con la versión original en Chrome para evitar atribuir todos los
defectos a esta edición. Ancho total del documento antes/después a 768px: **988/1138px**, frente
a 753px de área visible (scrollbar descontado). A 390px: **549/562px**, frente a 375px visibles.
El scroll horizontal ya existía en esos dos anchos; la corrección lo incrementa. A 641px, el
ancho del documento pasa de 626 a 1138px: hay una regresión de desbordamiento de página en ese caso.

Montos extremos que activan `-xs` a 1366px: el contenido de la franja pasa de 974 a **1069px**
para un contenedor de 974px al recuperar los tamaños. Es un caso adicional de falta de espacio,
no un fallo de especificidad.

Seguimiento recomendado, distinto del Pendiente B: ajustar la distribución de la franja y de la
barra lateral en anchos reducidos, conservando los tamaños requeridos, sin abreviar ni recortar
dinero. En esta entrega no se cambiaron breakpoints, flex, anchos o padding: la autorización fue
para la corrección de especificidad y la revisión responsive. **La corrección tipográfica está
verificada; no se declara listo para producción el layout tablet/móvil ni montos extremos.**

### Verificación de integridad y regresión funcional

- Script administrativo completo: sintaxis válida mediante `vm.Script`.
- Generador real evaluado y script de su HTML resultante: sintaxis válida mediante `vm.Script`.
- Chrome ejecutó el ejecutivo y el administrativo de la copia Codex sin excepciones JavaScript
  registradas por CDP.
- En el administrativo real, cada zona (`uploadZone`, `uploadZoneSalarios`, `uploadZonePermisos`)
  registra un listener `dragover` y uno `drop`.
- Soltar un archivo sintético `prueba-pendiente-a.xlsx` en Asistencia cambió el estado a
  `Cargado: prueba-pendiente-a.xlsx` y habilitó Procesar (`disabled:true` → `false`). No se pulsó
  Procesar sobre ese archivo ficticio; no se afirma haber validado parseo de Excel ni salarios.
- Comparación original/copia: exactamente cuatro líneas reemplazadas, las cuatro de selectores
  descritas arriba. No se agregaron caracteres de escape ni backticks.
- SHA-256 del original, antes y después:
  `B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
- SHA-256 de la copia corregida:
  `8027CD00851C2F999E109F9B8EDF404207C904C0EDE80DF14F02833A7DDA754C`.

Evidencia auxiliar en el mismo directorio temporal del diagnóstico:
`resultado-antes-fix.json` (medición inmediatamente previa), `resultado-despues-fix.json`
(validación posterior completa), `resultado-before-completo.json` (comparación responsive de
referencia), `despues-1366.png`, `despues-390.png` y capturas equivalentes para los otros anchos.
Las cifras y limitaciones relevantes quedan persistidas en esta nota, independientemente de la
duración de esos archivos temporales.

**Estado final:** especificidad del Pendiente A corregida y tamaños confirmados; limitaciones de
layout documentadas. Working original intacto. Pendiente B sin intervención.

---

## Pendiente B — implementación inicial Codex (2026-09-05)

Esta sección actualiza el estado histórico anterior: Pendiente B tiene una implementación
inicial autorizada, exclusivamente en `dashboard-asistencia-working-codex.html`.
No se modificó el working original. Las capturas y el informe son evidencia auxiliar.

### Decisiones de diseño

- Escritorio: dos líneas por mes. Primera: mes y tres columnas monetarias alineadas
  (pérdida confirmada, sujeto a regularización y total). Segunda: barra horizontal apilada
  y porcentaje permanente sobre la nómina mensual.
- Rojo y ámbar identifican los dos componentes de la barra; total monetario neutro y en
  negrita. Los rótulos y montos permiten interpretar la composición sin depender del color.
- Montos completos con Q y centavos, cifras tabulares; tamaño computado de los importes
  22px en escritorio y 20px en contenedores estrechos. Mes 22px, porcentaje 20px,
  etiquetas 16px y pista de 26px. Centavos subordinados a 0.8em.
- Escala compartida 0/25/50/75/100%, con guías alineadas. La pista gris representa el 100%
  de la nómina de CADA mes, no un denominador monetario común. La nota visible explica
  esta distinción y que total incluye importes aún sujetos a regularización.
- Los segmentos usan proporciones sin redondear a píxeles y sin separación aditiva;
  un separador interior de 1px no aumenta la longitud de la barra.
- Si algún costo supera el 100%, se amplía la escala de TODOS los meses al siguiente
  múltiplo de 25%; el gris sigue terminando en 100%. No se recorta ni se normaliza el costo.
- Sin nómina positiva: “No calculable / Sin nómina positiva”, conservando los montos,
  sin dibujar proporciones. Un costo cero con nómina positiva sí muestra 0.0%.
- Se conservan el orden recibido, el mínimo de dos meses, los filtros, las exclusiones y
  la nota de regularización existente. No se modificó ninguna fórmula de negocio.
- Tooltip complementario con nómina exacta, disponible con ratón o foco de teclado;
  Escape lo cierra. Los valores principales siempre están visibles.
- Responsive por ancho del componente: debajo de 700px se repiten etiquetas por mes;
  debajo de 360px los montos se apilan. La tarjeta tiene un mínimo de 320px para impedir
  que el layout lateral reduzca la gráfica a unos pocos píxeles. Esto conserva lectura,
  pero aumenta el ancho desplazable de la página móvil; no resuelve su estructura global.

Código involucrado: estilos `.tendencia-card` y `.composicion-*`, nota explicativa del
componente y funciones `construirBarraComposicion`, `actualizarGraficoTendencia`,
`mostrarComposicionTooltip`, `posicionarComposicionTooltip` y `ocultarComposicionTooltip`.

### Validación real en Chrome

Chrome **152.0.7977.76**, ejecución headless por CDP, escala de dispositivo 1. Se evaluó
el generador real y se abrió su HTML resultante. Se inspeccionaron visualmente las cuatro
capturas finales. Datos exclusivamente sintéticos: un colaborador de prueba, nómina mensual
Q1,000,000.00, enero–agosto; exposición mensual 19/24/22/36/28/31/23/26%.
Estas capturas no representan resultados reales del archivo Excel del proyecto.

| Viewport | Ancho gráfico / scroll interno | Alto aproximado de fila | Observación |
|---|---|---|---|
| 1920×1080 | 1044 / 1044px | 108px | Ocho meses completos y aclaración de escala visibles al desplazar la sección arriba. |
| 1366×768 | 995 / 995px | 108px | Cinco meses completos y parte del sexto; se necesita scroll vertical para los restantes. |
| 768×1024 | 397 / 397px | 199px | Etiquetas repetidas y porcentaje debajo; cuatro meses completos. Persiste scroll horizontal de página. |
| 390×844 | 272 / 272px | 257px | Montos apilados legibles al desplazar la página hacia el gráfico; no constituye un layout móvil resuelto. |

En 768px el documento mide 1138px de ancho, igual al problema ya registrado tras Pendiente A.
En 390px mide 604px (antes 562px): el mínimo de tarjeta introduce 42px adicionales de
ancho desplazable. La captura móvil está desplazada horizontalmente por `scrollIntoView`;
no debe interpretarse como prueba de que todo el dashboard cabe en pantalla.

Controles de proporción y estados, ejecutados sobre el componente en Chrome:

- Q200 sobre Q1,000 frente a Q200 sobre Q2,000: 20.0% y 10.0%; cada segmento pasa de 10% a 5%.
- Q0 sobre Q1,000: 0.0%, sin segmentos de color.
- Q30 sin nómina: No calculable, sin segmentos, con los tres montos visibles.
- Q1,300 sobre Q1,000: 130.0%; escala común extendida a 150%; segmentos 53.3333% y
  33.3333% del ancho total, equivalentes a 80% y 50% de nómina. Otro mes conserva 30.0%.
- Un solo mes: mensaje de mínimo dos meses y ninguna barra.
- Foco de teclado: tooltip visible con Q1,000,000.00; dentro del viewport probado.
  Escape cambia su display a none.
- Sin excepciones JavaScript registradas en el ejecutivo ni en el administrativo.
- Sintaxis válida del script administrativo completo y del script ejecutivo REAL generado
  mediante `vm.Script`. Se preservaron los escapes del template literal.
- Las tres zonas administrativas conservan sus listeners dragover/drop. Soltar un archivo
  sintético habilita Procesar. No se probó procesamiento Excel con ese archivo ficticio.
- Comparación con respaldo inmediatamente anterior: prefijo administrativo anterior al
  generador y todo el bloque posterior al componente (KPIs, recálculo, filtros, tablas y
  exportación) idénticos. Se conserva la corrección de especificidad del Pendiente A.
  No se afirma una validación integral de filtros ni del modelo salarial con datos reales.

### Evidencia persistida

- [Captura 1920×1080](codex-evidence/pendiente-b-1920.png)
- [Captura 1366×768](codex-evidence/pendiente-b-1366.png)
- [Captura 768×1024](codex-evidence/pendiente-b-768.png)
- [Captura 390×844](codex-evidence/pendiente-b-390.png)
- [Mediciones y controles en JSON](codex-evidence/pendiente-b-validation.json)

SHA-256 original confirmado intacto:
`B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
SHA-256 Codex tras esta implementación:
`E2F37161D8F23DE43B37D8F61211201C1074E04799E4DCD37DF13FBC89D150DB`.

### Observaciones de legibilidad y límites

La comparación de extremos de barra y porcentajes es inmediata en escritorio; los montos
alineados permiten comparar el impacto absoluto aun cuando cambie la nómina. La longitud
conserva su significado real y no amplifica artificialmente las diferencias.

La lectura a distancia debe comprobarse con el proyector y la sala reales: una captura
no verifica contraste bajo luz ambiental ni distancia del público. La versión inicial
favorece 1080p con la sección situada arriba. En 768p se necesita scroll; no hay modo de
presentación ni paginación de meses. Los valores muy grandes pueden envolver líneas;
la tipografía prioriza conservar el importe completo. La comparación del componente ámbar
es menos directa porque comienza donde termina el rojo; su columna monetaria sirve de apoyo.

Pendientes de revisión posteriores: prueba en sala con datos reales y eventual tratamiento
separado del layout global tablet/móvil. No se presenta el responsive completo como resuelto.

---

## Ronda 26 — ajustes visuales de franja, gráfica y tarjetas

Implementación limitada a `construirHTMLEjecutivo()` en la copia Codex. Esta entrada sustituye
las decisiones visuales previas incompatibles con el encargo 26. No se cambió el working original,
la interfaz administrativa, las fórmulas, los filtros, el orden de secciones ni el contenido KPI.

### 26.1 — causa reportada antes de editar y medición real

La causa histórica sigue siendo la cascada: `.valor-monetario-sm` y `-xs`, declaradas después
con la misma especificidad que los selectores originales, sustituyen el tamaño de la cifra.
Sus valores 0.82em y 0.65em se calculan sobre el padre de 16px: 13.12px y 10.4px. Los centavos
son hijos separados y no reducen la parte entera. La base rem no era menor de 16px.

La copia Codex YA tenía la solución del Pendiente A: selectores calificados con
`.veredicto-cifras`. Se conservó, sin añadir otra corrección ni !important.
Se reportó la causa al usuario antes de pasar a 26.2.

Chrome 152.0.7977.76, viewport 1366px, misma muestra sintética en ambos generadores:

| Elemento | Working original, font-size computado | Codex, font-size computado | Caja renderizada Codex (alto) |
|---|---|---|---|
| Cifra principal de franja | 13.12px | 64px | 67.1875px |
| Cifra secundaria de franja | 13.12px | 56px | 58.796875px |
| Cada cifra de Fila 1 | 30px | 30px | 30px |

Se usaron `getComputedStyle` y `getBoundingClientRect`, no solo lectura del CSS.
1920/1366/768px: franja 64/56px. 640/390px: 41.6/35.2px. Fila 1: 30px en todos esos anchos.
La franja conserva la mayor escala tipográfica. Se mantienen las limitaciones anteriores de
layout tablet/móvil; estas mediciones no certifican que los montos extremos quepan en toda pantalla.

### 26.2 — una fila por mes en escritorio

- Mes a la izquierda, pista gris a escala real, rojo y después ámbar, altura 24px y radio 4px.
- Separador blanco interior de 2px, sin sumar longitud al costo. Es una separación visual
  dentro de la geometría proporcional; un gap aditivo distorsionaría la escala solicitada.
- Retícula CSS compartida mediante subgrid: todas las barras tienen igual origen y ancho;
  las columnas monetarias también comparten ancho incluso si cambia la longitud del importe.
- Tres importes completos: Confirmada en rojo, Por regularizar en ámbar y Total neutro.
  Porcentaje neutro en una cuarta columna. Tipografía tabular de 18px; centavos a 0.8em.
- Debajo de 900px de ancho de tarjeta se oculta la columna de porcentaje y su valor queda
  disponible en el tooltip existente, mediante ratón o foco. No se añadió una interacción.
- Debajo de 700px de tarjeta la barra pasa a una segunda línea, conservando las tres cifras
  juntas y sin partir dinero. En anchos aún menores hay desplazamiento horizontal local;
  no se recortan montos para aparentar que caben.
- Se repuso el cuadro gris de Nómina analizada: leyenda de tres cuadros. Se conservaron
  literalmente la nota al pie vigente de Codex y la nota dinámica de regularización.
- Se conserva la condición de visibilidad de todos los meses y el tratamiento preexistente
  de nómina ausente, costo cero y valores superiores al 100%. No se tocó su aritmética.
- Alto de cada fila en escritorio: 49px frente a aproximadamente 108px de la versión Codex anterior.

### 26.3 — acabado de las ocho tarjetas

- Padding de 20px uniforme, espacios entre tarjetas y filas de 16px.
- Títulos con altura de referencia común, posibilidad de envolver texto sin ellipsis;
  cifras conservadas sin saltos de línea y con su jerarquía original 30/24/22px.
- Igual altura dentro de cada fila, alineación superior consistente de título/cifra/contexto.
- Acentos de estado uniformes de 3px; tarjetas sin estado mantienen solo borde fino de 1px.
- Borde fino y sin sombra de reposo. No se modificaron acciones, tooltips ni eventos KPI.
- Fila 3 conserva dos tarjetas y su orden, ahora en las primeras dos columnas de la retícula
  de tres para cumplir la alineación vertical; queda libre la tercera posición. Se sustituye
  así el reparto previo en dos mitades, incompatible con columnas alineadas entre las tres filas.
- Sparklines: 32px de alto, mismo margen y opacidad, mismo trazo gris secundario en las tres;
  los colores semánticos de las cifras y los datos de los trazos se conservan.

Medición a 1366px: columnas x=284/637/990px y ancho 337px en las tres filas (Fila 3 usa
las dos primeras). Altos iguales por fila: 168.796875 / 122.796875 / 120.796875px.
El espacio sin contexto en Nómina analizada se mantiene para igualar la altura con su compañera;
no se inventó una línea de contenido para rellenarlo.

### Verificación por etapa y regresión

Después de 26.1, 26.2, 26.3 y el ajuste final de retícula se extrajeron los scripts a archivos
JavaScript y se ejecutó `node --check` sobre AMBOS: administrativo completo y ejecutivo realmente
generado mediante `construirHTMLEjecutivo(datos)`. Todos pasaron. Sin excepciones JavaScript en Chrome.

Cinco combinaciones verificadas, con muestra sintética de ocho meses y DOS departamentos:

| Combinación | Gráfica visible | Sparklines Fila 1 | Badges Fila 1 |
|---|---|---|---|
| Todos los meses + todos los departamentos | Sí | 3 | 0 |
| Agosto + todos los departamentos | No | 0 | 1 |
| Todos los meses + Pruebas | Sí | 3 | 0 |
| Agosto + Pruebas | No | 0 | 1 |
| Enero + Pruebas, sin mes anterior | No | 0 | 0 |

La quinta combinación verifica específicamente el límite de primer mes. No se presenta esta
matriz como prueba exhaustiva de todas las exclusiones y estados posibles.

- Comparación automática contra respaldo previo a ronda 26: los ocho valores KPI y los
  agregados mensuales son idénticos en las cinco combinaciones. El segundo departamento
  permite que el filtro departamental cambie efectivamente los resultados.
- Se extrajeron los TRES importes del texto renderizado de cada fila y se verificó que
  Confirmada + Por regularizar = Total, con tolerancia de un centavo por formato monetario.
- Administrativo: listeners dragover/drop presentes en las tres zonas. Archivo de asistencia
  Excel sintético válido creado con la librería existente; drop, clic en Procesar, 2 registros
  leídos, 2 procesados y resultados visibles. No se usaron datos personales ni se guardó el Excel.
- No se afirma haber validado integralmente salarios, permisos o un archivo real de producción.
- Comparación textual: todo el código fuera del generador es idéntico al respaldo inicial.
  Todo el bloque posterior al componente de composición, incluidos KPIs y recálculo, es idéntico.
- Sin nuevas dependencias. Sin backticks ni escapes de comilla problemáticos añadidos al template.

### Evidencia

- [Franja y tarjetas finales, 1366px](codex-evidence/26-final-kpis-1366.png)
- [Gráfica final, 1366px](codex-evidence/26-final-grafica-1366.png)
- [Franja y tarjetas finales, 1920px](codex-evidence/26-final-kpis-1920.png)
- [Gráfica final, 1920px](codex-evidence/26-final-grafica-1920.png)
- [Medición del original](codex-evidence/26-original.json)
- [Verificación de 26.1](codex-evidence/26-26-1.json)
- [Verificación de 26.2](codex-evidence/26-26-2.json)
- [Verificación de 26.3](codex-evidence/26-26-3.json)
- [Respaldo anterior, prueba de dos departamentos](codex-evidence/26-regresion-antes.json)
- [Validación final](codex-evidence/26-final.json)
- [Aserciones de integridad, igualdad y sumas](codex-evidence/26-integridad.json)

Las capturas finales usan datos sintéticos, no resultados del Excel real del proyecto.
La gráfica completa y sus dos notas caben holgadamente en la captura de escritorio al situar
la sección arriba. Se revisó visualmente el espaciado; total y porcentaje tienen columnas
separadas (12px de gap mínimo). En sala aún hace falta comprobar la lectura de las cifras
monetarias de 18px con la distancia y el proyector reales. La franja es el foco tipográfico.

SHA-256 original intacto:
`B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
SHA-256 Codex final:
`283DE0A7CA4D4EBAC6F5BBD86F56F9C744EB5D136E2C9375FF7C7639C8963CD2`.

---

## Ronda 27 — composición vertical con escala de 40%

Se reemplazó únicamente la gráfica dentro de `construirHTMLEjecutivo()` en la copia Codex.
La instrucción de mostrar tres importes por mes en pantalla queda anulada por este encargo.
Franja, tarjetas, tablas, orden de secciones y código administrativo no se modificaron.

### Presentación

- Barras verticales de 32px de ancho y 220px de alto, fondo gris tenue, esquinas de 6px.
- Referencia visible: “40% de nómina”. El alto del segmento se obtiene como porcentaje
  real dividido entre 40, sin modificar importes ni denominadores del recálculo.
- Rojo desde la base, ámbar encima, separación visual interior de 2px; no añade altura a
  la proporción. Se mantiene un origen común para las ocho barras.
- Un solo porcentaje sobre cada barra, mes debajo; sin columnas monetarias en pantalla.
- Tooltip por ratón/foco: nómina, confirmada, por regularizar, total y porcentaje.
  Conserva el cierre por Escape y al abandonar la barra.
- Leyenda de tres cuadros y nota de regularización conservadas. Nota de escala actualizada
  para explicar el 40% y que total no equivale íntegramente a pérdida confirmada.
- En un filtro con valores superiores al 40%, se conserva la defensa de escala común
  ampliable: el tope aumenta al siguiente múltiplo de 10 y se rotula explícitamente.
  Para la serie solicitada el tope es exactamente 40%. La excepción evita cortar datos
  departamentales que pudieran superar ese rango. Está explicada en la nota visible.
- Sin nómina positiva se muestra N/D, con explicación accesible y porcentaje no calculable
  en tooltip. No se añade un porcentaje ficticio.
- En espacio reducido se conserva la fila cronológica de barras con desplazamiento local;
  no se cambia el layout de otras secciones ni se declara resuelto el responsive global.

### Verificación y alcance de los datos

Chrome 152.0.7977.76. `node --check` pasó sobre el script administrativo completo y el script
REAL producido por el generador. No se registraron excepciones JavaScript.

**Los valores de negocio reales no estaban disponibles como ejecutivo de ocho meses.**
El `dashboard-asistencia-ejecutivo.html` guardado es un ejemplo antiguo de dos meses.
La verificación de esta ronda usa una prueba controlada, no una auditoría del cálculo salarial
real: nómina sintética total Q1,500,000 por mes, dos departamentos, componente confirmado
constante de 8% y componente pendiente construido para reproducir la serie indicada por el usuario.
Estos valores viven solamente en el arnés de prueba; NO se fijaron en el HTML de la aplicación.

| Mes | Etiqueta comprobada en Chrome | Altura total esperada sobre pista de 220px |
|---|---|---|
| Ene | 22.6% | 124.30px |
| Feb | 19.5% | 107.25px |
| Mar | 26.4% | 145.20px |
| Abr | 25.8% | 141.90px |
| May | 24.1% | 132.55px |
| Jun | 26.0% | 143.00px |
| Jul | 34.5% | 189.75px |
| Ago | 30.3% | 166.65px |

Se verificaron las alturas geométricas con tolerancia de 0.05px por subpíxeles. Febrero
ocupa 48.75% de la pista y julio 86.25%. Cada tooltip contiene cuatro importes Q y porcentaje;
se comprobó confirmada + por regularizar = total. Tooltip visible al recibir foco y oculto
tras Escape, dentro del viewport de escritorio probado.

Cinco combinaciones conservadas de la ronda 26:
1. Todos los meses / todos los departamentos.
2. Agosto / todos los departamentos.
3. Todos los meses / Pruebas.
4. Agosto / Pruebas.
5. Enero / Pruebas (primer mes, sin anterior).

En las cinco combinaciones se compararon valores KPI y agregados mensuales contra el respaldo
inmediatamente anterior: idénticos. La gráfica solo está visible en los casos 1 y 3.
La equivalencia antes/después demuestra conservación del cálculo para la muestra; no demuestra
por sí sola que los archivos reales y sus exclusiones produzcan la serie indicada.

Se repitió la carga de un Excel sintético válido: 2 filas leídas, 2 procesadas, resultados visibles.
La franja mantiene 64/56px en escritorio y las cifras de Fila 1, 30px.

Una comparación textual, excluyendo exclusivamente el CSS de composición, el renderizador
correspondiente y su nota al pie, confirma que TODO el resto del archivo es idéntico al respaldo.
Sin dependencias añadidas, sin backticks ni escapes de comilla problemáticos añadidos al template.

### Evidencia y legibilidad

- [Gráfica final, 1366px](codex-evidence/27-final-grafica-1366.png)
- [Gráfica final, 1920px](codex-evidence/27-final-grafica-1920.png)
- [Validación anterior con la misma muestra](codex-evidence/27-antes.json)
- [Chrome: porcentajes, geometría, tooltips y filtros](codex-evidence/27-final.json)
- [Aserciones de integridad y proporciones](codex-evidence/27-integridad.json)

La captura final es sintética. Visualmente permite distinguir el máximo en julio, una base roja
estable y la variación ámbar sin leer montos. Esto verifica la capacidad del diseño con dicha
muestra, no constituye un hallazgo nuevo sobre los registros reales.

Original intacto, SHA-256:
`B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
Copia Codex tras ronda 27:
`CCB75B8342F56485A429A48A763731C6BCAD8D25E79DC202CEE9777FA2B82F7B`.

---

## Ronda 28 — chips de contexto y textos de la gráfica

Cambios limitados a los cuatro elementos solicitados, dentro del generador ejecutivo de
`dashboard-asistencia-working-codex.html`. El working original permanece intacto.

- Contexto: chips informativos de período y departamento, alineados a la izquierda con el
  borde exterior de franja y tarjetas. Fondo tenue, borde 1px, radio 8px, texto 13px/400 gris
  secundario, separación 8px. Se retira el conteo de colaboradores evaluados de esta línea.
- Exclusiones: se conserva exactamente el cálculo existente del conteo en el filtro activo.
  El chip solo se crea cuando ese conteo es mayor de cero; singular/plural según corresponda.
  Los textos se insertan mediante textContent, sin interpretar nombres de departamento como HTML.
- Porcentajes de barras: 22px/700/color primario → 20px/500/#525B66.
- Nota gráfica reemplazada literalmente por: “El total combina pérdida confirmada y monto
  sujeto a regularización.” La explicación extensa se elimina, como permite el encargo;
  se conserva el rótulo dinámico del tope de escala.
- Nota de regularización: gris secundario, peso 400 y tamaño existente pequeño de 12.48px.
  “provisionales” pasa a minúscula. El porcentaje y la condición de advertencia no cambian.

### Validación

Chrome 152.0.7977.76. Node --check satisfactorio sobre ambos scripts: administrativo completo
y ejecutivo realmente generado. Sin excepciones JavaScript. Se conservaron los resultados
numéricos KPI y los agregados mensuales en la comparación automática antes/después.

Cinco combinaciones, cada una probada con una exclusión individual activa y después sin ella:

| Período | Departamento | Primeros dos chips |
|---|---|---|
| Todos | Todos | Enero a agosto 2026 · Todos los departamentos |
| Agosto | Todos | Agosto 2026 · Todos los departamentos |
| Todos | Pruebas | Enero a agosto 2026 · Pruebas |
| Agosto | Pruebas | Agosto 2026 · Pruebas |
| Enero | Pruebas | Enero 2026 · Pruebas |

En las diez comprobaciones: tres chips al excluir al colaborador de prueba (“1 exclusión”)
y dos chips al retirar la exclusión. Sin texto de colaboradores evaluados en el contexto.
Se usaron dos colaboradores/departamentos y ocho meses sintéticos; las capturas no representan
los datos reales ni la serie controlada de porcentajes de la ronda 27.

Medición a 1366px: contexto/chip inicia en x=284px, igual que el borde exterior de franja y
primera tarjeta. Porcentajes de gráfica: 20px/500, rgb(82,91,102). Fila 1: 30px/700.
Franja: 64px/800 y 56px/700. Nota de regularización: 12.48px/400, rgb(75,85,99).
Se inspeccionaron las capturas: las barras conservan protagonismo y los porcentajes quedan
subordinados a las cifras KPI/franja. La lectura a distancia física depende de la sala/proyector.

La comparación textual excluyendo solamente estos cuatro elementos y su render de contexto
confirma que todo el resto del HTML es idéntico al respaldo previo. Sin cambios de cálculo,
estructura de la gráfica, franja, tarjetas, tablas, interacción ni dependencias externas.
La carga/procesamiento administrativo de un Excel sintético volvió a pasar: 2 filas leídas,
2 procesadas y resultados visibles.

Evidencia:
- [Chips y jerarquía tipográfica, 1366px](codex-evidence/28-final-kpis-1366.png)
- [Gráfica y notas suavizadas, 1366px](codex-evidence/28-final-grafica-1366.png)
- [Mediciones anteriores](codex-evidence/28-antes.json)
- [Mediciones finales y filtros](codex-evidence/28-final.json)
- [Aserciones de alcance e integridad](codex-evidence/28-integridad.json)

SHA-256 original: `B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC`.
SHA-256 copia Codex: `C88377ECC552E9C91F3C85E9290A4DBA4477F9D8D15EE4BF94E01A48DEA122BA`.

## Ronda 29 — Gráfica, perfil condicional y chips de filtro (2026-09-05)

Alcance: únicamente construirHTMLEjecutivo() de dashboard-asistencia-working-codex.html.
Comparación con el respaldo previo: el contenido anterior y posterior al generador es idéntico.
No se modificó dashboard-asistencia-working.html ni se añadieron dependencias.

### 29.1 — Escala y paleta

La escala inicial/común pasa de 40% a 50% de la nómina. Se conserva la ampliación automática
existente si un dato supera ese límite, con el tope efectivo rotulado; no se recortan datos.
Los cálculos de nómina, confirmada, regularización, total y porcentaje permanecen intactos.
Colores compartidos por segmentos/fondo y leyenda, medidos mediante getComputedStyle en Chrome:

| Elemento | HEX | RGB computado |
| --- | --- | --- |
| Fondo neutro con matiz verdoso | #E5E9E5 | 229, 233, 229 |
| Pérdida confirmada | #B66A68 | 182, 106, 104 |
| Sujeto a regularización | #C3A05D | 195, 160, 93 |

Se conservan barras de 32px, separación de 2px, porcentajes, tooltips y visibilidad exclusivamente
con todos los meses. Las barras pueden envolver a otra línea en pantallas estrechas, evitando
el ancho mínimo anterior de 640px. No se modificó su contenido ni orden.

### 29.2 — Perfil del departamento

La reformulación es viable: perfilDepto() ya entrega acción y composición. Las tablas
 departamentales que repiten el perfil se ocultan cuando se selecciona un departamento.
Con todos los departamentos, Mayor exposición mantiene contenido y comportamiento anteriores.
Con un departamento, la misma posición contiene Perfil del departamento, su acción y composición;
no repite días ni nombre del departamento. Se reutiliza perfilDepto() sin modificar umbrales,
porcentajes ni cálculos. Se permite envolver el texto de la acción.

Caso sintético validado: Control de jornada / Predominio Déficit, 76%.
También se comprobó el perfil mixto; se conserva su desglose ausencia/déficit.

### 29.3 — Filtros desde chips

Se eliminó el elemento aside del ejecutivo y su lógica de apertura/cierre. El contenido recupera
los 240px del panel y los 20px de separación: a 1366px, su margen izquierdo pasa de 284px a 24px.
Los chips son botones persistentes y conservan el foco al recalcular. Se mantienen los mismos
lectores mesActivo()/dptoActivo() y el flujo de recalcularDashboard(); el estado se almacena en
inputs ocultos, sin elementos select nativos.

- Período: lista propia generada desde los meses disponibles; no se fijan nueve meses en código.
- Departamento: búsqueda y lista propias con roles combobox/listbox/option y selección activa.
- Exclusiones: las mismas categorías, acciones de seleccionar/limpiar y exclusiones individuales.
  Con cero exclusiones se mantiene el chip «Exclusiones» para poder abrir el control; esta decisión
  sustituye expresamente el ocultamiento de la ronda 28 por el nuevo requisito de acceso desde chips.
- Desplegables debajo del chip, con margen mínimo de 12px respecto al área útil del navegador;
  consideran también el espacio de la barra de desplazamiento. Scroll vertical para listas largas.
- Cierre con clic fuera, Escape o salida del foco. Flechas para navegar; Enter para confirmar;
  Escape devuelve el foco al chip. El período también admite Inicio/Fin.
- Se conserva la persistencia por pestaña. En Análisis por Colaborador solo se muestra el chip
  de período, como correspondía al comportamiento previo de los filtros.
- Ajuste responsive mínimo: los bloques de cifras de la franja pueden envolver sin reducir sus
  tamaños existentes. No cambia la jerarquía ni el contenido de los KPIs.

### Validación

node --check pasó sobre el script completo y el script ejecutivo realmente generado tras cada
punto (29.1, 29.2 y 29.3), y nuevamente después de los ajustes de borde/texto/teclado.

Chrome sin errores de ejecución. Cinco combinaciones verificadas desde los chips:
todos/todos; agosto/todos; todos/Pruebas; agosto/Pruebas; enero/Pruebas.
La comparación antes/después confirma igualdad de todos los datos de la gráfica, de los otros
siete KPIs y de las condiciones de visibilidad. La tarjeta condicional es la única excepción
intencional de contenido KPI.

Prueba ampliada con datos sintéticos: nueve meses más Todos los meses; 21 departamentos más
Todos los departamentos; búsqueda de «internacionales»; siete categorías de exclusión.
Resultado de exclusiones: 7 → ninguna («Exclusiones») → 1 → 7 mediante sus controles.
Se confirmó «Control de jornada / Predominio Déficit, 76%», sin días repetidos.
La navegación mediante eventos de teclado de Chrome confirmó selección de mes con flechas/Enter
y desplazamiento hasta la última opción de departamento sin recorte. Escape, clic fuera y
restauración de filtros al volver de Análisis por Colaborador también pasaron.

Resoluciones: 1920×1080 y 1366×768; adicionalmente 1046×768 para simular una barra lateral del
navegador de 320px, y 390×768. Los desplegables quedan dentro del viewport y su scrollWidth es
igual a clientWidth, sin desplazamiento horizontal. **La barra lateral real del navegador no se
abrió: el caso se validó por reducción equivalente del viewport en Chrome headless.**
Se hicieron mediciones adicionales del dashboard a 768px y 640px.

La inspección de capturas confirma una paleta discreta y diferenciable y chips alineados con el
contenido. Los porcentajes conservan 20px/500 frente a 30px en Fila 1 y 64px/56px en la franja
(desktop). La lectura física desde el fondo de una sala no se simuló.
Los datos son sintéticos: las capturas no representan resultados reales de nómina.

La carga administrativa de Excel sigue funcionando: dos filas leídas y procesadas, resultados
visibles; los tres receptores de archivos conservan sus manejadores de carga.

Evidencia:
- [Gráfica al 50%, 1366px](codex-evidence/29-final-grafica-1366.png)
- [Departamento desplegado, 1366px](codex-evidence/29-stress-chip-1366-1.png)
- [Viewport reducido equivalente a barra lateral](codex-evidence/29-stress-chip-1046-1.png)
- [Lista larga a 390px](codex-evidence/29-stress-chip-390-1.png)
- [Antes](codex-evidence/29-antes.json) y [después](codex-evidence/29-final.json)
- [Regresión de los cinco filtros](codex-evidence/29-regresion.json)
- [Límites, filtros y navegación](codex-evidence/29-ui.json)
- [Nueve meses, 21 departamentos y exclusiones](codex-evidence/29-stress-controls.json)
- [Teclado de Chrome y colores computados](codex-evidence/29-teclado-colores.json)

SHA-256 original, sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 30 — Visibilidad condicional, franja por estado y chips (2026-09-05)

Alcance: cambios exclusivamente dentro de construirHTMLEjecutivo() en la copia Codex.
El resto del archivo es idéntico al respaldo anterior a esta ronda. Archivo original intacto.
No se alteraron fórmulas, importes, agregaciones, perfiles calculados ni datos de la gráfica.

### 30.1 — Franja por estado

El estado visual usa diasSinRespaldoTotal y perdidaCierta, ya calculados:

| Estado | Acento | Fondo | Cifra principal |
| --- | --- | --- | --- |
| Días sin respaldo > 0 | #B66A68 | #F8EEEE | #9B5553 |
| Sin días pendientes y pérdida >= Q0.01 | #C3A05D | #F7F3E9 | gris del texto secundario |
| Sin días pendientes y sin pérdida | #7F9B87 | #EFF4EF | #55745D |

Se aplica un atributo data-estado al resultado de la franja, independiente de las ramas que
construyen su contenido. Se conservan cifras, textos y tamaños. Los días pendientes tienen
prioridad visual incluso si el costo es cero. Se validaron los tres estados en Chrome.

### 30.2 y 30.3 — Tarjetas condicionales y retícula

Se omiten del DOM Sujeto a regularización cuando su importe redondeado a centavos es Q0.00;
Colaboradores afectados cuando su conteo es cero; Oportunidad recuperable cuando sinBrecha
ya calculado es verdadero. Se elimina la tarjeta Perfil del departamento. Mayor exposición
se conserva solamente con todos los departamentos, con su contenido anterior.

Siempre se construyen Pérdida por déficit, Días sin respaldo, Balance de horas y Nómina analizada.
La visibilidad de Días sin respaldo no depende de tener un valor positivo.

Un contenedor CSS Grid común permite redistribuir las tarjetas manteniendo el orden de sus
filas de origen. Los contenedores de esas filas usan display:contents para conservar las reglas
tipográficas originales. Distribución a partir de 768px:

| Tarjetas visibles | Filas completas |
| --- | --- |
| 4 | 2+2 |
| 5 | 3+2 |
| 6 | 3+3 |
| 7 | 3+2+2 |
| 8 | 3+3+2 |

Cada fila ocupa todo el ancho disponible, con separación de 16px y altura uniforme dentro de
la fila. En pantallas inferiores a 768px se utiliza una sola columna, sin posiciones vacías.

### 30.4 y 30.5 — Etiquetas y acabado de chips

Los meses individuales y rangos del mismo año omiten el año. Un rango que cruza años conserva
ambos: se verificó «Enero 2025 a agosto 2026». Al elegir agosto vuelve a mostrarse «Agosto»,
porque ese filtro ya no abarca varios años.

Fondo rgba(255,255,255,.56), borde rgba(90,105,100,.13), backdrop-filter:blur(10px), hover tenue.
La flecha rota 180 grados. El desplegable entra en 200ms y cierra en 110ms con 4px de
 desplazamiento máximo y curva cubic-bezier(.2,.8,.2,1). Implementación exclusivamente CSS,
mediante transiciones discretas de display y @starting-style; sin temporizadores ni dependencias.
En navegadores que no admitan transiciones discretas, el control conserva apertura/cierre
inmediatos. prefers-reduced-motion desactiva las transiciones y el desplazamiento.

### Caso Agosto / Tecnología de la Información

No se encontró un ejecutivo guardado con el estado real descrito. El archivo ejecutivo de ejemplo
contiene dos colaboradores ficticios y enero/febrero. Se construyó un caso sintético que reproduce
Q95.07 de pérdida, cero días sin respaldo y sin brecha recuperable; **la captura no certifica los
restantes valores de nómina, balance ni acumulado del caso real**.

Resultado validado:
- Franja ámbar suave (#F7F3E9), acento #C3A05D, cifra principal gris; sin alarma roja/rosada.
- Primera fila: Pérdida por déficit Q95.07 y Días sin respaldo 0 días.
- Segunda fila: Balance de horas y Nómina analizada.
- Ocultas: Sujeto a regularización, Colaboradores afectados, Oportunidad recuperable y la tarjeta
  departamental. La oportunidad solo se oculta si efectivamente no hay brecha según el cálculo
  existente; regularización al 100% por sí sola no determina ese cálculo.
- Retícula 2+2 completa en escritorio, una columna en móvil.

### Evidencia de validación

node --check pasó sobre el script del working completo y el script ejecutivo generado después
de cada punto: 30.1, 30.2, 30.3, 30.4 y 30.5.

Chrome: cinco filtros (todos/todos; agosto/todos; todos/TI; agosto/TI; enero/TI), cada uno a
1920×1080, 1366×768, 1046×768 y 390×768: 20 escenarios, sin errores de ejecución.
Se midieron posiciones para confirmar filas completas de borde a borde, separación de 16px,
orden y ausencia de huecos. Días sin respaldo permaneció visible en todos, incluido cero.
La comparación con el respaldo confirma igualdad de los datos calculados de la gráfica y de
cada valor KPI conservado en los 20 escenarios. El archivo fuera del generador es idéntico.

Se volvió a probar la navegación por flechas/Enter y la visibilidad de la última opción en una
lista de 21 departamentos. Escala de gráfica 50% y colores de ronda 29 confirmados por estilo
computado. No reaparece el panel lateral ni se introducen selects nativos.

Transiciones medidas en Chrome: durante apertura, opacidad intermedia 0.858; durante cierre,
0.169 y display:block temporal; al finalizar, display:none. Duraciones computadas 0.2s y 0.11s.
Con movimiento reducido: 0s. Desenfoque computado: blur(10px).

- [Agosto/TI, 1366px — caso sintético](codex-evidence/30-agosto-ti-1366.png)
- [Todos los meses/departamentos](codex-evidence/30-todos-1366.png)
- [Agosto/TI, 390px](codex-evidence/30-agosto-ti-390.png)
- [Mediciones anteriores](codex-evidence/30-antes.json)
- [20 escenarios y transiciones](codex-evidence/30-final.json)
- [Integridad y regresión de cálculos](codex-evidence/30-integridad.json)
- [Teclado y conservación de la gráfica](codex-evidence/30-teclado-colores.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 31 — Tabla documental, franja concisa y chips perceptibles (2026-09-05)

Cambios exclusivamente en construirHTMLEjecutivo() de dashboard-asistencia-working-codex.html.
El archivo original permanece intacto y todo el contenido fuera del generador es idéntico al
respaldo previo. Sin nuevas dependencias. Único cambio de criterio: inclusión en la tabla (31.1).

### 31.1 — Tabla de regularización pendiente

Ahora incluye solo diasSinRespaldo > 0 del conjunto filtrado por mes, departamento y exclusiones.
Se elimina costo > 0 como condición alternativa. Mantiene orden descendente por días sin respaldo.
El subtítulo pasa a «Ordenados por días sin respaldo». Cuando no hay registros se vacía tbody y
se oculta el bloque completo, sin encabezado, acordeón ni mensaje de tabla vacía visibles.

Se procesó ReporteUnificadoEne-Ago.xlsx con el working: 6,582 filas, 57 colaboradores, ocho meses;
rango detectado 05/01/2026–31/08/2026. El ejecutivo inicia con las categorías de exclusión marcadas:
8 personas excluidas y 49 evaluadas en todos los meses. No se cargó un archivo adicional de
salarios/permisos para esta prueba. Estos resultados corresponden al Excel disponible y al
procesamiento actual; no certifican modificaciones de otra sesión que no estén en ese archivo.
A diferencia de la prueba anterior, este procesamiento reproduce el caso observado de Agosto/TI:
Q95.07, cero días pendientes y acumulado de dos días en un colaborador.

| Filtro | Antes | Después | Entran | Salen |
| --- | ---: | ---: | ---: | ---: |
| Enero–agosto / todos | 49 | 48 | 0 | 1 |
| Agosto / todos | 43 | 39 | 0 | 4 |
| Enero–agosto / TI | 2 | 1 | 0 | 1 |
| Agosto / TI | 2 | 0 | 0 | 2 |
| Enero / TI | 1 | 0 | 0 | 1 |

**Consecuencia sobre información de costo, reportada antes de cerrar la implementación:**
Agosto/TI deja de mostrar dos filas con Q95.07 de pérdida documentada. Enero/TI deja de mostrar
una fila con Q684.41. Es correcto para este título: esas personas no tienen días por documentar
en esos meses. Los importes permanecen en franja/KPIs; desaparece su detalle individual en ESTA
tabla. Una tabla separada por costo queda como decisión de producto pendiente, no implementada.

### 31.2 — Una sola línea descriptiva

Se retiraron la proporción de colaboradores y las frases de «mejoró/empeoró» del veredicto mensual,
incluida su construcción de texto. Se conserva el porcentaje monetario existente, redondeado como
antes: «N% del total está pendiente de documentar.» No se atribuye ninguna causa a las variaciones.
La línea se omite cuando no hay monto pendiente. En Agosto/TI quedan Q95.07 y «Período regularizado
al 100%». Se conserva el color por estado y toda la visibilidad condicional de las tarjetas.

### 31.3 — Superficies y movimiento

- Reposo: #ECEBE7, ligeramente más oscuro que la página #F7F6F3.
- Hover: #E2E1DC.
- Desplegable abierto: #D8DCD6.
- Borde transparente; se conserva el contorno de foco por accesibilidad.
- backdrop-filter eliminado; Chrome confirma valor computado none.
- Curva cubic-bezier(.4,0,.2,1), apertura 200ms y cierre 110ms.
- prefers-reduced-motion mantiene duración 0s.

Medición de transición ejecutada, mediante transitionend y muestreo por fotograma:
apertura elapsedTime=0.2s (evento observado a 218ms); cierre elapsedTime=0.11s (evento a 123ms).
Opacidad durante apertura: ~24% a 51ms, ~46% a 68ms, ~65% a 85ms y ~86% a 118ms.
La curva anterior llegaba a ~86% a 76ms: el comienzo ahora es perceptiblemente más gradual.

### Verificación

node --check pasó sobre ambos scripts (working completo y ejecutivo generado) tras cada punto,
31.1, 31.2 y 31.3, y durante la validación final.

Cinco combinaciones de filtro operadas desde los chips en Chrome a 1366×768, 1046×768 y 390×768:
15 escenarios con el Excel disponible y 15 adicionales sintéticos. Sin errores de ejecución.
La tabla muestra exactamente el número de colaboradores con días sin respaldo positivos; Agosto/TI
no muestra bloque y tiene cero filas. La franja contiene como máximo una línea descriptiva y ninguna
cuando el importe pendiente es cero. Capturas inspeccionadas en todos/todos y Agosto/TI.

Comparación antes/después con el mismo snapshot real: datos de gráfica y valores de todas las
 tarjetas idénticos en los 15 escenarios. Se preservan escala al 50%, paleta suave, retícula
condicional, chips sin panel lateral y sus manejadores de teclado.

Evidencia:
- [Agosto/TI: tabla ausente y franja regularizada](codex-evidence/31-real-agosto-ti.png)
- [Todos los meses/departamentos: franja concisa](codex-evidence/31-real-todos.png)
- [Conteos antes con el Excel disponible](codex-evidence/31-real-antes.json)
- [Conteos y filtros después](codex-evidence/31-real-final.json)
- [Pruebas sintéticas adicionales](codex-evidence/31-sintetico-final.json)
- [Estilos efectivos y tiempos de transición](codex-evidence/31-chips-transiciones.json)
- [Integridad del original y regresión de cálculos](codex-evidence/31-integridad.json)

SHA-256 original: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC (sin cambios).

## Ronda 32 — Fusión de colaboradores, semáforo condicional y tablas (2026-09-05)

Alcance: solo construirHTMLEjecutivo() en la copia Codex. Archivo original intacto; contenido
fuera del generador idéntico al respaldo previo. Sin dependencias ni cambios de cálculo.

### 32.1 — Una tabla de colaboradores

Se eliminó el bloque duplicado y su renderizador. Se conserva un solo acordeón, inicialmente
colapsado, con el título «Colaboradores afectados: N colaboradores, N días» y subtítulo
«Ordenados por días sin respaldo». Sigue incluyendo únicamente diasSinRespaldo > 0 del filtro
activo, sin límite de registros y con la misma ordenación descendente.

Columnas: Nombre, Departamento, Balance de horas, Costo, Sujeto a regularización, Días sin respaldo,
Acumulado (solo con un mes seleccionado), Excluir del análisis. Los meses afectados están en gris
bajo el nombre, dentro de la misma celda y fila, sin prefijo. Sujeto a regularización reutiliza
exactamente deudaAusenciaBruta × costoPorMinuto del renderizador retirado.

Limitación de ancho reportada antes de implementar: ocho columnas no tienen lectura cómoda a
1046px o menos. No se omitió ninguna. Hasta 1100px se muestran registros apilados con etiquetas
por campo, ampliando el patrón móvil existente. Por encima de ese ancho hay tabla convencional
con encabezado fijo; en la vista apilada cada registro identifica sus campos y no hay encabezado
horizontal. Ambas conservan scroll vertical y todos los valores, sin truncamiento ni scroll
horizontal. El bloque completo se oculta cuando no hay días pendientes y tbody queda vacío.

### 32.2 — Cumplimiento como KPI con departamento filtrado

Se conserva el cálculo existente de deptosSemaforo, sin cambiar su promedio ni umbrales:
verde >=95%, ámbar >=80%, rojo por debajo de 80%. Con todos los departamentos sigue visible
la sección comparativa. Con uno seleccionado se oculta la sección y se añade el KPI al final
del grupo de prioridad de Fila 2. La retícula común se redistribuye con las reglas de ronda 30.
Porcentaje y color salen del mismo objeto que alimentaba la fila del semáforo.

Caso real del Excel disponible: Agosto / Transnorte → 75.9%, 2 colaboradores, estado rojo.
Sin registros para un departamento se muestra «—» y cero colaboradores, sin inventar un porcentaje.

### 32.3 — Filas completas y cabecera departamental

El límite fijo de 400px no correspondía a un número entero de filas y el desplazamiento podía
terminar en cualquier punto de una fila. Se sustituye por altura medida: cabecera más un número
entero de filas de altura uniforme para cada tabla. Se recalcula al abrir, cambiar datos/vista
y redimensionar. Cabecera sticky como grupo, fondo opaco y border-collapse:separate evitan
artefactos de superposición/bordes de las celdas sticky independientes.

Scroll snap vertical al inicio de fila, descontando la altura de cabecera, hace que el reposo
coincida con filas completas. Durante el movimiento continuo las filas naturalmente atraviesan
los bordes; la comprobación de filas completas se realiza al detenerse. En móvil las tablas
 departamentales usan los registros apilados existentes y el desplazamiento vertical de la página,
sin limitar a 400px un registro alto.

Medición a 1366px después de solicitar scrollTop=137:
- Pérdida confirmada: ajuste a 126px; cabecera 36px; filas 63px; área 414px.
- Exposición sujeta: ajuste a 141px; cabecera 36px; filas 47px; área 412px.
En ambos casos, la primera fila visible empieza justo debajo de la cabecera y la última termina
en el borde inferior del área. Las filas anteriores quedan detrás del encabezado opaco.

### 32.4 — Numeración sin partir

La columna de 30px con padding horizontal de 24px dejaba espacio insuficiente para dos dígitos.
Pasa a 48px con padding de 8px por lado y white-space:nowrap. El ancho total sigue siendo 100%;
las demás columnas absorben el ajuste. La regla no fuerza nowrap en los separadores colspan.
Se corrigió también el desbordamiento móvil del separador «Departamentos con menos de 3
colaboradores», detectado durante la validación. No se oculta contenido para disimular overflow.

### Validación y evidencia

node --check pasó sobre el working completo y sobre el ejecutivo realmente generado tras cada
punto (32.1, 32.2, 32.3, 32.4) y después de los ajustes responsive.

Datos: snapshot producido en la ronda 31 desde ReporteUnificadoEne-Ago.xlsx, sin archivos
adicionales de salarios/permisos; 57 colaboradores, 49 evaluados con las exclusiones iniciales.

Cinco filtros: todos/todos, agosto/todos, todos/TI, agosto/TI, enero/TI. Probados a 1920×1080,
1366×768, 1046×768 y 390×768: 20 escenarios sin errores ni desbordamiento horizontal de celdas
visibles o contenedores de tabla. Acumulado solo aparece con mes específico. Solo hay un tbody
de colaboradores en esta sección. El semáforo vuelve a sección al quitar el filtro de departamento.
La tabla muestra 48 colaboradores en todos/todos y 39 en agosto/todos; Agosto/TI queda sin tabla.
Acción Excluir del análisis comprobada desde la tabla fusionada: 48 → 47 filas, restaurable.

Comparación antes/después de los cinco filtros: mismos valores de los KPIs previos, mismo texto
calculado del semáforo y mismos datos de gráfica. La cifra del KPI nuevo es la ya existente del
semáforo. Sin cambios de costos, días, cumplimiento ni agregaciones.

- [Tabla fusionada, todos los meses](codex-evidence/32-todos.png)
- [Tabla fusionada con Acumulado, agosto](codex-evidence/32-mes.png)
- [Agosto/TI: KPI y tabla ausente](codex-evidence/32-agosto-ti.png)
- [Transnorte: 75.9% y dos colaboradores](codex-evidence/32-transnorte.png)
- [Tablas departamentales después de desplazar](codex-evidence/32-departamentos-scroll.png)
- [20 escenarios, anchos y filas](codex-evidence/32-validacion.json)
- [Integridad y regresión](codex-evidence/32-integridad.json)
- [Valores anteriores](codex-evidence/32-regresion-antes.json) y [finales](codex-evidence/32-regresion-final.json)
- [Exclusión y KPI Transnorte](codex-evidence/32-interacciones.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 33 — Redundancias y fondo verde salvia (2026-09-05)

Alcance: solo construirHTMLEjecutivo() de la copia Codex. Original intacto y contenido fuera del
generador idéntico al respaldo anterior. No se modificaron cálculos ni dependencias.

### Cambios

33.1: retirada la tarjeta Pérdida por déficit y su sparkline. La etiqueta de franja ahora dice
«Pérdida por déficit de jornada». Su badge mensual se traslada junto a la cifra, fuera del span
que anima el importe, conservando valor, color y condiciones de aparición. No aparece con todos
los meses o sin base válida de comparación, igual que antes. Se ajustó el índice de la tarjeta
Sujeto a regularización para mantener su ocultación cuando vale cero. Retícula redistribuida.

33.2: retirados del HTML la nota de regularización documental y el texto explicativo de composición.
Los cálculos existentes de regularización quedan intactos. Aclaración reportada: regularización
documental y cumplimiento de jornada son métricas distintas, aunque sus porcentajes puedan ser
parecidos. La retirada de la nota no implica equipararlas.

33.3: retirados los subtítulos de orden de las tablas del Resumen Ejecutivo. No se altera ningún
criterio de inclusión ni ordenamiento.

33.4: retirada la nota «Período regularizado al 100%» y la nota secundaria del estado sin costo.
Los estados sin pendiente quedan con etiqueta, cifra y, cuando corresponde, el badge trasladado.
Se conserva el color por estado. Los estados con exposición pendiente conservan la única línea
porcentual introducida en la ronda 31.

33.5: fondo de barras y muestra de leyenda pasan a **#D6DFD2**, verde salvia grisáceo, muy
 desaturado. Medido en Chrome: rgb(214,223,210). Se mantienen #B66A68 para confirmada y #C3A05D
para sujeto a regularización. El fondo conserva la referencia de escala al 50% de nómina;
no se interpreta como indicador de aprobación ni se convierte en una métrica de cumplimiento.

### Verificación

node --check sobre el working completo y el script ejecutivo generado pasó después de cada
punto: 33.1, 33.2, 33.3, 33.4 y 33.5.

Chrome con el snapshot del Excel local procesado en ronda 31. Cinco filtros habituales:
todos/todos, agosto/todos, todos/TI, agosto/TI y enero/TI; más todos/FRP como caso solicitado.
Probados a 1920×1080, 1366×768, 1046×768 y 390×768: 24 escenarios, sin errores de ejecución.

Importes principales confirmados, sin tarjetas monetarias que los dupliquen:
- Agosto/TI: Q95.07. Badge ▼16.2% ahora en la franja. Retícula 2+2.
- Enero–agosto/FRP: Q19,507.08. Sin badge mensual. Retícula 3+2+2.
- Enero–agosto/todos: Q152,198.65. Sin badge mensual. Retícula 3+2+2.

Los demás filtros también pasan la comprobación de ausencia de duplicación. Todas las filas
ocupan el ancho completo, sin huecos; a 390px se conserva una columna. No quedan nodos de notas
de gráfica, subtítulos de orden ni notas de franja. Máximo un badge, siempre en la franja.
La comparación antes/después confirma los mismos importes de franja, textos de badge, valores
de todas las tarjetas conservadas y datos de gráfica en los 24 escenarios.

Evidencia:
- [Agosto/TI y badge trasladado](codex-evidence/33-agosto-ti.png)
- [Enero–agosto/FRP](codex-evidence/33-frp.png)
- [Enero–agosto/todos](codex-evidence/33-todos.png)
- [Gráfica limpia con fondo salvia](codex-evidence/33-grafica.png)
- [Mediciones anteriores](codex-evidence/33-antes.json)
- [24 escenarios finales y colores computados](codex-evidence/33-final.json)
- [Integridad y regresión](codex-evidence/33-integridad.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 34 — Tooltip y barras departamentales (2026-09-06)

Alcance: solo construirHTMLEjecutivo() de la copia Codex. Original intacto; todo el contenido
fuera del generador es idéntico al respaldo de ronda 33. Sin cambios de cálculo ni dependencias.

### 34.1 — Nómina separada de la suma

El tooltip contiene el mes y tres filas: Confirmada, Por regularizar y Total. Se conserva la línea
divisoria antes de Total. La nómina sale de ese bloque y pasa a un pie con margen superior de
12px: «Sobre una nómina de Q… · …%». Estilo efectivo en Chrome: 13px, peso 400 y gris #4B5563,
frente a 16px en los componentes. Se conservan valores, centavos pequeños y el caso No calculable.

Ejemplo real verificado en enero: Q19,725.57 + Q17,346.53 = Q37,072.10. El pie muestra
«Sobre una nómina de Q164,093.48 · 22.6%». La nómina ya no aparece como una fila sumable.

### 34.2 — Tabla compacta y barras de 200px

La columna monetaria tiene 224px incluyendo padding, con barra útil de 200px. Antes se midieron
570.31px de barra a 1920px de viewport. El contenido de cada tabla se agrupa a la izquierda en
un área de máximo 760px: numeración 48px, nombre flexible, métrica 224px y días 152px. Se conservan
los límites exteriores de las tarjetas; el espacio libre queda después del conjunto, no entre
el departamento y sus importes. En móvil se conserva la presentación apilada y las barras de 200px
caben dentro del registro. Los porcentajes inline de relleno no cambian: solo su longitud física.

### Filas cortadas, cabecera y numeración: diagnóstico separado

Acortar la barra por sí solo NO resuelve estos tres problemas. La copia de ronda 33 ya tenía
las correcciones independientes de ronda 32: ancho y nowrap de numeración, encabezado de grupo
sticky, altura medida de filas y ajuste de scroll a filas completas. En el respaldo previo no
se reprodujeron filas partidas al reposo en las posiciones verificadas; no puede atribuirse la
captura reportada a una causa adicional concreta sin disponer de ese estado del navegador.

Se mantuvieron esas correcciones y se reforzó la medición cuando termina de cargar la tipografía
(document.fonts.ready), además de apertura, recálculo y resize. Esto evita conservar alturas
medidas con la fuente provisional. El nuevo ancho vuelve a medirse antes de establecer el área
visible. En móvil la tabla departamental usa registros apilados y scroll de página.

Prueba final: al inicio, tras solicitar scrollTop=137 y al final del scroll, las filas visibles
quedan completas al detenerse, debajo del encabezado opaco y hasta el límite inferior. Durante
el arrastre continuo es normal que una fila atraviese el borde; el ajuste se produce al reposo.
Los números de posición se midieron con Range.getClientRects(): una sola línea, sin overflow.

### Validación

node --check pasó sobre el working completo y el ejecutivo realmente generado después de 34.1
y 34.2, y nuevamente al ejecutar el arnés de Chrome.

Datos: snapshot del Excel local procesado en ronda 31. Cinco filtros: todos/todos, agosto/todos,
todos/TI, agosto/TI y enero/TI. Cuatro tamaños: 1920×1080, 1366×768, 1046×768 y 390×768.
20 escenarios sin errores. Ambas tablas departamentales se mantienen ocultas con departamento
filtrado. En los casos visibles no hay scroll horizontal, números partidos ni filas cortadas al
reposo. Encabezado fijo en escritorio y etiquetas por campo en la presentación móvil.

El tooltip no desborda, tiene exactamente tres filas monetarias en el bloque principal y el pie
de nómina separado. Las barras miden 200px en ambas tablas a los cuatro anchos. Comparación
antes/después: KPIs, datos de gráfica, valores/textos departamentales y porcentajes de las barras
idénticos en los 20 escenarios. Se conserva la escala del 50% y el fondo salvia #D6DFD2.

- [Tooltip con nómina al pie](codex-evidence/34-tooltip.png)
- [Tablas compactas después de desplazar](codex-evidence/34-tablas.png)
- [Mediciones anteriores](codex-evidence/34-antes.json)
- [20 escenarios finales y tres posiciones de scroll](codex-evidence/34-final.json)
- [Integridad y regresión de valores](codex-evidence/34-integridad.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 35 — Exclusiones reversibles, propagación y acabado (2026-09-06)

Alcance: solo construirHTMLEjecutivo() en la copia Codex. Original intacto y contenido fuera
del generador idéntico al respaldo previo. No se alteraron fórmulas, cálculos ni dependencias.

### 35.1 — Exclusiones individuales visibles y reversibles

El desplegable ahora separa Categorías excluidas y Colaboradores excluidos. Cada persona excluida
aparece por nombre con una casilla marcada; desmarcarla la reincorpora al análisis y recalcula.
Los nombres se insertan mediante textNode, sin concatenarlos como HTML ni como argumentos inline.
Las casillas individuales tienen una clase distinta para no mezclarse con categoriasActivas().

Se muestran tanto las exclusiones de esta sesión como las embebidas desde el administrativo,
sin duplicar personas. Reincorporar o Limpiar modifica solo el estado del ejecutivo en memoria,
no el archivo administrativo ni los datos guardados en él. Limpiar exclusiones desmarca todas
las categorías, vacía las exclusiones de sesión y restablece también las individuales embebidas.
Si otra categoría sigue excluyendo a esa persona, quitar solo su exclusión individual no anula
esa categoría: se conserva la combinación de filtros.

Se conserva navegación por teclado; al desaparecer una casilla, el foco pasa a otra casilla
individual o al chip, evitando perder el punto de interacción.
El contador del chip cuenta personas excluidas en el filtro, no número de categorías.

### 35.2 — Auditoría de propagación, valor por valor

No se confirmó el defecto sospechado. pctDependiente se calcula dentro de renderKpisEjecutivos()
en cada recalcularDashboard(), usando costoTotal y costoSujetoRegularizacion del conjunto filtrado.
No se cambió la fórmula. El redondeo a entero puede mantener el texto visible igual cuando la
variación es pequeña; eso no significa que el valor no se haya recalculado.

Caso de prueba real: Claudia Pamela Toledo Pineda, Fundación Rios Por La Paz, elegida por su
impacto significativo en costo, documentación y cumplimiento. Datos del Excel local procesado
en ronda 31, con las categorías iniciales activas. Se probaron todos/todos, agosto/todos,
todos/FRP y agosto/FRP. La reincorporación mediante su casilla restauró exactamente cada snapshot.

| Elemento | Antes → después de excluir | Resultado |
| --- | --- | --- |
| Franja: déficit, todos/todos | Q152,198.65 → Q134,433.46 | Se actualiza |
| Franja: exposición, todos/todos | Q376,636.11 → Q354,067.27 | Se actualiza |
| Porcentaje pendiente, todos/todos | 60% → 62% | Se actualiza |
| Porcentaje pendiente, agosto/todos | 61% → 65% | Se actualiza |
| Días sin respaldo, todos/todos | 841 → 823 | Se actualiza |
| Sujeto a regularización, todos/todos | Q224,437.46 → Q219,633.81 | Se actualiza |
| Balance de horas, todos/todos | 4562.5 h → 4029.9 h | Se actualiza |
| Colaboradores afectados, todos/todos | 48 → 47 | Se actualiza |
| Nómina analizada, todos/todos | Q1,428,813.96 → Q1,396,795.72 | Se actualiza |
| Oportunidad recuperable, todos/todos | Q114,772.27 → Q98,188.69 | Se actualiza |
| Mayor exposición, todos/todos | 172 días → 172 días | Correcto: el departamento líder no cambia |
| Dos sparklines restantes | Cambian los puntos de ambas series | Se actualizan |
| Badge, agosto/todos | ▲10.7% → ▲8.2% | Se actualiza |
| Cumplimiento, todos/FRP | 77.0% → 96.4% | Se actualiza |
| Cumplimiento, agosto/FRP | 70.9% → 92.9% | Se actualiza |
| Tabla de pérdida departamental | Cambia la fila de FRP | Se actualiza |
| Tabla de exposición departamental | Cambia la fila de FRP | Se actualiza |
| Tabla de colaboradores | Se elimina la persona seleccionada | Se actualiza |
| Chip de exclusiones, todos/todos | 8 → 9 | Se actualiza |
| Chips de período y departamento | Conservan la selección activa | Correcto: no cambió ese filtro |

Gráfica: se actualizan montos, nómina, segmentos y los ocho porcentajes.
Antes: 22.6, 19.5, 26.4, 25.8, 24.1, 26.0, 34.5, 30.3%.
Después: 21.5, 18.5, 25.4, 24.4, 22.8, 25.4, 33.7, 29.2%.
Con mes específico la gráfica y sparklines siguen ocultos por diseño; el badge ocupa su función
mensual. Las tablas departamentales siguen ocultas con departamento específico. Al volver a
todos los meses/departamentos se calculan con las exclusiones vigentes, sin valores visibles obsoletos.
En todos/FRP la oportunidad recuperable desaparece al quedar sin brecha, como exige la ronda 30.
No se encontró ningún componente visible con propagación defectuosa en estas pruebas.

### 35.3 — Barra de 100px

Ambas barras departamentales pasan de 200px a 100px útiles, conservando su proporción de relleno.
No se estrecha otra vez la tabla ni la columna de cifras: el ancho disponible se mantiene para
importes, promedio/total y cantidad de colaboradores. La barra queda como apoyo compacto bajo
la cifra. Ancho computado verificado: 100px en ambas tablas a los cuatro anchos.

### 35.4 — Colores finales

- Página: #FFFFFF.
- Tarjetas: #FFFFFF; borde fino #D8DFE5, medido en Chrome. Se conservan acentos de estado.
- Chips en reposo: #F0F1EE; borde #E2E5DF.
- Chips en hover: #E5E8E1; borde #D6DBD1.
- Chip abierto: #D8DED2; borde #CBD3C3.

Las tarjetas/tablas mantienen su delimitación por borde y espaciado sobre blanco. No se añaden
sombras ni dependencias. Se conservan las superficies de estado de la franja y el fondo salvia
de las barras de composición.

### 35.5 — Chip de período

Con todos los meses muestra «Todos los meses». Con mes específico conserva «Agosto», «Enero», etc.
La interfaz no permite subconjuntos arbitrarios de meses; no se introduce esa interacción.

### Validación y evidencia

node --check sobre working completo y ejecutivo generado pasó tras 35.1, auditoría 35.2,
35.3, 35.4 y 35.5. Chrome sin errores de ejecución.
Cinco filtros habituales (todos/todos, agosto/todos, todos/TI, agosto/TI, enero/TI) a 1920×1080,
1366×768, 1046×768 y 390×768: 20 escenarios. Barras de 100px, tooltip y geometría de scroll
conservados; desplegable dentro del viewport y sin overflow horizontal. Validación adicional
con exclusión/reincorporación real en cuatro escenarios y prueba de Limpiar sobre exclusiones
embebidas: categorías=0, sesión=0 e individuales embebidas=0 después de limpiar.

La comparación con la ronda 34, antes de excluir personas, confirma los mismos KPIs, gráfica,
valores departamentales y porcentajes de relleno en los 20 escenarios.

- [Desplegable con categorías y colaboradora excluida](codex-evidence/35-exclusiones.png)
- [Tablas con barras de 100px y fondo blanco](codex-evidence/35-tablas.png)
- [Auditoría completa antes/excluida/restaurada](codex-evidence/35-propagacion.json)
- [20 escenarios finales, colores y tamaños](codex-evidence/35-final.json)
- [Integridad y regresión](codex-evidence/35-integridad.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 36 — Ranking único, ancho completo y rangos (2026-09-06)

Cambios exclusivamente dentro de construirHTMLEjecutivo() de la copia Codex. Original intacto.
Sin cambios en importes, promedios, costos ni agregaciones.

### 36.1 — Sin umbral de plantilla

Retirado el tbody secundario y el separador de departamentos con menos de tres colaboradores.
La vista Promedio aplica el orden descendente existente a todos los departamentos con pérdida,
y numera 1…N sin interrupciones. La vista Total conserva su orden descendente por total.
Los mismos importes y promedios alimentan ambas vistas; la barra se referencia al máximo de
la lista unificada. Se retira también la atenuación por muestra pequeña y el texto del tooltip
que describía la separación eliminada. Se mantiene la cantidad de colaboradores por fila.

Top 5, enero–agosto / todos, con el Excel local y exclusiones iniciales:

| Posición | Departamento | Promedio por colaborador | Colaboradores |
| --- | --- | ---: | ---: |
| 1 | Operación de sedes | Q10,060.99 | 1 |
| 2 | Legal | Q9,952.57 | 3 |
| 3 | Fundación Rios Por La Paz | Q9,753.54 | 2 |
| 4 | Transacciones de Mercado Ambiental | Q6,096.30 | 3 |
| 5 | Transnorte | Q4,832.02 | 2 |

Ambas vistas contienen 15 departamentos en este filtro. Sin secciones internas ni subtítulos.

### 36.2 — Ancho del 100%

Se elimina el máximo de 760px del área de scroll de ambas tablas departamentales. Las tablas
ocupan todo el ancho útil del contenedor, descontando únicamente la barra de desplazamiento
vertical. Se mantiene la columna monetaria de 224px y la de días de 152px; el nombre recibe
el ancho adicional. Barras de progreso fijas de 100px, sin crecimiento al ampliar el viewport.
La presentación móvil apilada conserva todos los campos.

### 36.3 — Rangos homogéneos

Barrido del generador: **cuatro construcciones con el conector «a» corregidas**:
1. Contexto: rango mensual dentro de un mismo año.
2. Contexto: rango mensual entre años distintos.
3. Rango de las tarjetas (abreviaturas Ene a Ago), compartido por Acumulado y Colaboradores afectados.
4. Intervalo de fechas generado para el pie de página.

Son tres construcciones de rangos mensuales más el intervalo del pie; no cuatro textos literales
idénticos. Las ocurrencias gramaticales de «a» ajenas a rangos no se modifican.

El formato común produce «Enero - Agosto», nombres completos con inicial mayúscula y guion.
El chip reemplaza «Todos los meses» por el rango real. Con mes específico muestra «Agosto», sin
rango; también se expande la abreviatura de la tarjeta Colaboradores afectados. El pie «Período
analizado» refleja ahora el filtro activo. La línea Acumulado conserva deliberadamente el rango
completo del archivo, con el nuevo formato. Tooltips y encabezados no generan otro rango mensual
con «a». Las etiquetas individuales abreviadas de barras y las listas de meses no son rangos y
se conservan.

Se verificó cruce de años: «Diciembre 2025 - Enero 2026», manteniendo la distinción entre años.

### Verificación

node --check pasó sobre working completo y script ejecutivo generado tras 36.1, 36.2 y 36.3,
y de nuevo tras ajustar el texto del encabezado.

Cinco filtros: todos/todos, agosto/todos, todos/TI, agosto/TI y enero/TI. A 1920×1080, 1366×768,
1046×768 y 390×768: 20 escenarios sin errores. Ambas tablas ocupan el 100% de su área útil,
sin scroll horizontal; barras de 100px. Se mantiene la comprobación de filas completas al reposo
en inicio, posición intermedia y final, así como numeración en una línea.

Numeración continua comprobada y vista Total verificada descendente en los 15 departamentos.
Rangos probados para un mes, mismo año y años distintos. Comparación con ronda 35: datos mensuales
de composición idénticos en los 20 escenarios; el contenido fuera del generador permanece idéntico.

- [Tablas al ancho completo y ranking unificado](codex-evidence/36-tablas.png)
- [20 escenarios y ranking resultante](codex-evidence/36-final.json)
- [Vista Total y formatos de rango](codex-evidence/36-vistas-rangos.json)
- [Integridad y regresión](codex-evidence/36-integridad.json)

SHA-256 original sin cambios: B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

## Ronda 37 final — pie único de composición (2026-09-06)

Se añadió bajo las barras, centrado y separado 24px del eje de meses, un único texto:
«26.4% de la nómina del período está comprometida.»

El porcentaje se obtiene al renderizar la composición mediante suma de los totales mensuales / suma
 de las nóminas mensuales × 100. Se reutilizan los datos ya filtrados por departamento y exclusiones;
no se modifican cálculos existentes. Con nómina cero no se genera una razón indeterminada.

Enero - Agosto / todos, con las exclusiones predeterminadas del dataset real:
- Total: Q376,636.11.
- Nómina: Q1,428,813.96.
- Razón: 26.360052501166788%, presentada como **26.4%**.
- Promedio aritmético de porcentajes mensuales sin redondear: 26.130796683694207% (26.1%).
  No se usa ese promedio ni el 6.7% del ejemplo.

Tipografía computada: 16px en escritorio, menor que los porcentajes de barras (20px), peso 400,
gris neutro #4B5563. A 390px se usa 12px y se aprovechan 16px del margen interno a cada lado
únicamente para este pie; así conserva una línea sin modificar las barras ni generar scroll horizontal.

Verificación: node --check pasó sobre ambos scripts (working completo y ejecutivo generado),
también después del ajuste móvil. Chrome: todos/todos, agosto/todos, todos/TI, agosto/TI y enero/TI
a 1920×1080, 1366×768, 1046×768 y 390×768: 20 escenarios sin errores de ejecución ni desborde
horizontal. El texto coincide con la razón entre sumas en cada caso visible; se oculta junto con
la gráfica al seleccionar un mes. Una línea renderizada en todos los casos visibles.

El contenido fuera de construirHTMLEjecutivo() es idéntico al respaldo previo a esta ronda.
Original intacto: SHA-256 B54A3161586F2533FB44312FDAFAFFF1952583DD7E440637BE7A62E3D073FAEC.

Evidencia:
- [Validación de 20 escenarios y valores calculados](codex-evidence/37-validacion.json)
- [Gráfica y pie en Chrome a 1366px](codex-evidence/37-grafica-1366.png)
