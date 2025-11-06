# 🚀 GUÍA RÁPIDA: Subir Estructura Híbrida a GitHub

## 📦 Archivos que vas a subir (7 archivos)

✅ `index.html` - Portal principal con opciones Ver/Editar  
✅ `dashboard-presupuesto-ti-view.html` - Presupuesto TI (solo lectura) con datos  
✅ `dashboard-presupuesto-ti-edit.html` - Presupuesto TI (editable)  
✅ `dashboard-renovacion-ufinet-view.html` - UFINET (solo lectura) con datos  
✅ `dashboard-renovacion-ufinet-edit.html` - UFINET (editable)  
✅ `README.md` - Documentación actualizada  
✅ `INSTRUCCIONES.md` - Guía de uso  

---

## ⚡ PASO 1: Eliminar archivos antiguos

En tu repositorio de GitHub:

1. Ve a `https://github.com/lhernandez-erc/dashboards`
2. **Elimina estos archivos** (si existen):
   - `dashboards-github.zip` (ya no lo necesitas)
   - `dashboard-presupuesto-ti.html` (será reemplazado)
   - `dashboard-renovacion-ufinet.html` (será reemplazado)

**Cómo eliminar:**
- Click en el archivo
- Click en el icono de papelera (🗑️) arriba a la derecha
- Commit changes

---

## ⚡ PASO 2: Subir los nuevos archivos

### Opción A - Subir uno por uno (Más seguro):

1. En tu repositorio, click **"Add file"** → **"Upload files"**
2. Arrastra estos archivos en este orden:
   - `index.html` (sobrescribirá el anterior)
   - `README.md` (sobrescribirá el anterior)
   - `dashboard-presupuesto-ti-view.html` (nuevo)
   - `dashboard-presupuesto-ti-edit.html` (nuevo)
   - `dashboard-renovacion-ufinet-view.html` (nuevo)
   - `dashboard-renovacion-ufinet-edit.html` (nuevo)
3. Mensaje de commit: `Actualizar a estructura híbrida Ver/Editar`
4. Click **"Commit changes"**

### Opción B - Subir el ZIP completo:

1. Descarga el archivo: `dashboards-github-COMPLETO.zip`
2. Descomprímelo en tu computadora
3. Sube todos los archivos como en la Opción A

---

## ⚡ PASO 3: Verificar que funciona

**Espera 1-2 minutos** después de subir, luego verifica:

### ✅ Portal Principal:
```
https://lhernandez-erc.github.io/dashboards/
```
**Debe mostrar:**
- 🏠 Página elegante con 2 dashboards
- 💼 Tarjeta de Presupuesto TI con botones Ver/Editar
- 🌐 Tarjeta de UFINET con botones Ver/Editar
- 💡 Banner informativo explicando las diferencias

### ✅ Dashboard Presupuesto TI - VER:
```
https://lhernandez-erc.github.io/dashboards/dashboard-presupuesto-ti-view.html
```
**Debe mostrar:**
- 🔒 Badge "SOLO LECTURA" en el header
- 📊 Datos ya cargados (71 proyectos)
- 📈 Gráficos funcionando
- 🎛️ Filtros activos
- ❌ SIN sección de carga de Excel

### ✅ Dashboard Presupuesto TI - EDITAR:
```
https://lhernandez-erc.github.io/dashboards/dashboard-presupuesto-ti-edit.html
```
**Debe mostrar:**
- 📁 Sección de carga de Excel visible
- 📊 Dashboard vacío hasta cargar Excel
- 📤 Botón "Exportar para Compartir"

### ✅ Dashboard UFINET - VER:
```
https://lhernandez-erc.github.io/dashboards/dashboard-renovacion-ufinet-view.html
```
**Debe mostrar:**
- 🔒 Badge "SOLO LECTURA" en el header
- 📊 Datos ya cargados (27 enlaces)
- 📈 Gráficos funcionando
- 🎚️ Selector 12M/24M activo
- ❌ SIN sección de carga de Excel

### ✅ Dashboard UFINET - EDITAR:
```
https://lhernandez-erc.github.io/dashboards/dashboard-renovacion-ufinet-edit.html
```
**Debe mostrar:**
- 📁 Sección de carga de Excel visible
- 📊 Dashboard vacío hasta cargar Excel
- 📤 Botón "Exportar para Compartir"

---

## 🎯 Estructura Final en GitHub

Tu repositorio debe verse así:

```
lhernandez-erc/dashboards
├── 📄 README.md
├── 📄 INSTRUCCIONES.md  
├── 📄 index.html
├── 📄 dashboard-presupuesto-ti-view.html
├── 📄 dashboard-presupuesto-ti-edit.html
├── 📄 dashboard-renovacion-ufinet-view.html
└── 📄 dashboard-renovacion-ufinet-edit.html
```

**Total: 7 archivos**

---

## 💡 Para compartir con tu equipo

### Envía esta URL única:
```
https://lhernandez-erc.github.io/dashboards/
```

### En el email incluye:

```
Estimado equipo,

Les comparto el acceso a nuestros dashboards analíticos:

🌐 Portal: https://lhernandez-erc.github.io/dashboards/

Encontrarán dos dashboards disponibles:
📊 Presupuesto TI 2025
📊 Renovación Enlaces UFINET

Para cada uno hay dos opciones:
👁️ VER - Para consultar datos actualizados
✏️ EDITAR - Para administradores (requiere archivo Excel)

La mayoría solo necesitará usar la opción "VER".

Saludos,
[Tu nombre]
```

---

## 🔄 Cuando necesites actualizar los datos

### Para actualizar la versión VIEW:

1. Abre la versión **EDITAR**: 
   - `dashboard-XXX-edit.html`
2. Carga tu Excel actualizado
3. Verifica que todo se vea bien
4. Click en **"📤 Exportar para Compartir"**
5. El navegador descargará: `Dashboard_XXX_COMPARTIBLE.html`
6. **Renombra** el archivo a: `dashboard-XXX-view.html`
7. Ve a GitHub → tu repositorio
8. Click en el archivo antiguo `dashboard-XXX-view.html`
9. Click en **"Edit"** (icono de lápiz ✏️)
10. **"Delete file"** (icono de papelera)
11. Sube el nuevo archivo con el mismo nombre
12. Commit changes

**O más fácil:** Contáctame y te regenero la versión VIEW con los nuevos datos.

---

## ❓ Solución de Problemas

### "El portal principal no carga"
- Verifica que el archivo se llame exactamente `index.html`
- Espera 2-3 minutos después de subir
- Limpia la caché del navegador (Ctrl+F5)

### "Los botones no funcionan"
- Verifica que los nombres de archivo coincidan:
  - `dashboard-presupuesto-ti-view.html`
  - `dashboard-presupuesto-ti-edit.html`
  - `dashboard-renovacion-ufinet-view.html`
  - `dashboard-renovacion-ufinet-edit.html`

### "La versión VIEW no muestra datos"
- Verifica que subiste el archivo correcto (`-view.html`)
- Abre la consola del navegador (F12) y busca errores
- Contacta para regenerar el archivo

### "Error 404"
- Verifica que GitHub Pages esté activado
- Confirma que el nombre del archivo es exacto (minúsculas, guiones)

---

## ✅ Checklist Final

Antes de compartir con tu equipo, verifica:

- [ ] Los 7 archivos están en el repositorio
- [ ] GitHub Pages está activado
- [ ] El portal principal carga correctamente
- [ ] Los 4 dashboards son accesibles
- [ ] Las versiones VIEW muestran datos
- [ ] Las versiones EDIT permiten cargar Excel
- [ ] Los botones del portal funcionan
- [ ] Todo es responsive (prueba en móvil)

---

## 🎉 ¡Listo!

Una vez verificado todo, tu equipo podrá:
- ✅ Acceder desde cualquier dispositivo
- ✅ Ver datos actualizados sin archivos
- ✅ Usar filtros y análisis interactivos
- ✅ No necesitar instalaciones
- ✅ Compartir URLs fácilmente

---

**⏱️ Tiempo estimado de implementación: 10 minutos**

**¿Necesitas ayuda?** Consulta el README.md o contacta al equipo de TI.
