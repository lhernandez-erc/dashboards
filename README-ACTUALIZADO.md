# 📊 Dashboards Analíticos ERC Capital Corp

Repositorio de dashboards interactivos para análisis de datos empresariales de ERC Capital Corp.

## 🎯 Portal Principal

Accede al portal de dashboards con opciones de **Ver** (solo lectura) y **Editar** (carga de datos):

**🌐 [Portal de Dashboards](https://lhernandez-erc.github.io/dashboards/)**

---

## 📱 Dashboards Disponibles

### 1️⃣ Dashboard Presupuesto TI 2025

Análisis completo de ejecución presupuestaria del área de Tecnología de la Información.

**Versiones disponibles:**

| Tipo | URL | Descripción | Uso recomendado |
|------|-----|-------------|------------------|
| 👁️ **Ver** | [dashboard-presupuesto-ti-view.html](https://lhernandez-erc.github.io/dashboards/dashboard-presupuesto-ti-view.html) | Solo lectura con datos actualizados | Consultas, presentaciones, compartir con equipo |
| ✏️ **Editar** | [dashboard-presupuesto-ti-edit.html](https://lhernandez-erc.github.io/dashboards/dashboard-presupuesto-ti-edit.html) | Permite cargar nuevo Excel | Actualización de datos (solo administradores) |

**Características:**
- ✅ Seguimiento mensual de ejecución presupuestaria
- ✅ Análisis OPEX vs CAPEX
- ✅ Distribución por empresa y categoría
- ✅ KPIs en tiempo real
- ✅ Filtros interactivos por empresa, categoría y meses
- ✅ Meses ejecutados configurables para % de ejecución
- ✅ Exportación de versiones para compartir

---

### 2️⃣ Dashboard Renovación Enlaces UFINET

Análisis estratégico de ahorro y optimización de bandwidth en renovación de servicios de conectividad.

**Versiones disponibles:**

| Tipo | URL | Descripción | Uso recomendado |
|------|-----|-------------|------------------|
| 👁️ **Ver** | [dashboard-renovacion-ufinet-view.html](https://lhernandez-erc.github.io/dashboards/dashboard-renovacion-ufinet-view.html) | Solo lectura con datos actualizados | Análisis de ahorro, decisiones estratégicas |
| ✏️ **Editar** | [dashboard-renovacion-ufinet-edit.html](https://lhernandez-erc.github.io/dashboards/dashboard-renovacion-ufinet-edit.html) | Permite cargar nuevo Excel | Actualización de propuestas (solo administradores) |

**Características:**
- ✅ Comparativa de escenarios: 12 meses vs 24 meses
- ✅ Cálculo automático de ahorros mensuales y anuales
- ✅ Análisis de incremento de bandwidth
- ✅ Ahorro detallado por empresa y tipo de servicio
- ✅ ROI y recomendaciones estratégicas
- ✅ Filtros por empresa, servicio y bandwidth
- ✅ Comparativa lado a lado de ambos escenarios

---

## 🔄 ¿Cuál versión usar?

### 👁️ Versión VER (Solo Lectura)
**Úsala cuando:**
- Quieres consultar datos actualizados
- Necesitas hacer una presentación
- Vas a compartir con colaboradores que solo necesitan ver
- No tienes el archivo Excel a la mano
- Quieres acceso rápido sin cargar archivos

**Ventajas:**
- ✅ Carga instantánea (datos ya integrados)
- ✅ No requiere archivos Excel
- ✅ Ideal para compartir con el equipo
- ✅ Badge visual "🔒 SOLO LECTURA"

### ✏️ Versión EDITAR (Actualizable)
**Úsala cuando:**
- Necesitas actualizar los datos
- Tienes un archivo Excel nuevo
- Eres administrador del sistema
- Quieres exportar una nueva versión compartible

**Ventajas:**
- ✅ Permite cargar nuevos datos
- ✅ Función de exportar versión estática
- ✅ Control total sobre los datos
- ✅ Genera versiones para compartir

---

## 💻 Tecnologías

- **Frontend:** HTML5, CSS3, JavaScript (Vanilla)
- **Visualización:** Chart.js 4.4.0
- **Procesamiento de datos:** XLSX.js
- **Hosting:** GitHub Pages
- **Diseño:** Responsive Design (Mobile-first)

---

## 📱 Compatibilidad

- ✅ Chrome, Edge, Firefox, Safari (últimas versiones)
- ✅ Dispositivos móviles y tablets
- ✅ Exportación a Excel (versión EDITAR)
- ✅ Sin necesidad de instalación

---

## 🔒 Seguridad y Privacidad

- Los dashboards procesan datos localmente en el navegador
- No se envía información a servidores externos
- Los archivos Excel permanecen en el dispositivo del usuario (versión EDITAR)
- Las versiones VER tienen datos embebidos estáticamente
- Compatible con políticas de seguridad corporativa

---

## 📝 Flujo de Trabajo Recomendado

### Para Colaboradores (Usuarios Finales):
1. Accede al **Portal Principal**
2. Selecciona el dashboard que necesitas
3. Click en **"👁️ Ver Dashboard"**
4. Explora con los filtros interactivos
5. Analiza los datos y gráficos

### Para Administradores (Actualizadores de Datos):
1. Accede al **Portal Principal**
2. Selecciona el dashboard a actualizar
3. Click en **"✏️ Editar Dashboard"**
4. Carga tu archivo Excel actualizado
5. Verifica que los datos sean correctos
6. Click en **"📤 Exportar para Compartir"**
7. Sube la nueva versión VIEW a GitHub
8. Todos verán los datos actualizados automáticamente

---

## 🔄 Cómo Actualizar los Datos

### Método 1: Actualizar versión VIEW (Recomendado)
1. Abre la versión **EDITAR** del dashboard
2. Carga tu Excel actualizado
3. Click en **"Exportar para Compartir"**
4. Renombra el archivo descargado a `dashboard-XXX-view.html`
5. Sube a GitHub y reemplaza el archivo existente

### Método 2: Regenerar desde cero
1. Proporciona el Excel actualizado al equipo de TI
2. Se regenerará la versión VIEW con los nuevos datos
3. Se subirá automáticamente a GitHub

---

## 📞 Soporte

Para soporte técnico, nuevas funcionalidades o preguntas:
- 📧 Email: soporte-ti@erccapital.com
- 💬 Contacta al equipo de TI

---

## 📄 Estructura del Repositorio

```
dashboards/
├── index.html                              # Portal principal
├── dashboard-presupuesto-ti-view.html      # Presupuesto TI (solo lectura)
├── dashboard-presupuesto-ti-edit.html      # Presupuesto TI (editable)
├── dashboard-renovacion-ufinet-view.html   # UFINET (solo lectura)
├── dashboard-renovacion-ufinet-edit.html   # UFINET (editable)
├── README.md                               # Este archivo
└── INSTRUCCIONES.md                        # Guía de implementación
```

---

## ✅ Checklist de Verificación

- [x] Portal principal funcionando
- [x] Versiones VIEW con datos actualizados
- [x] Versiones EDIT funcionando correctamente
- [x] GitHub Pages activado
- [x] URLs accesibles
- [x] Filtros interactivos funcionando
- [x] Gráficos renderizando correctamente
- [x] Responsive design verificado

---

## 🎓 Notas Importantes

1. **Las versiones VIEW** contienen los datos al momento de su generación
2. **Para ver datos actualizados**, siempre regenera la versión VIEW
3. **Las versiones EDIT** siempre requieren cargar el Excel
4. **El Portal Principal** es la mejor forma de compartir con el equipo
5. **No compartas las versiones EDIT** a usuarios finales (solo VIEW)

---

## 📊 Estadísticas Actuales

**Última actualización:** Enero 2025

**Presupuesto TI 2025:**
- 71 proyectos activos
- 5 empresas
- 12 meses de seguimiento

**Renovación UFINET:**
- 27 enlaces
- 5 empresas
- 2 escenarios de análisis (12M y 24M)

---

**© 2025 ERC Capital Corp | Business Intelligence & Analytics**

*Para más información sobre GitHub Pages y actualización de dashboards, consulta [INSTRUCCIONES.md](INSTRUCCIONES.md)*
