# 🚀 GUÍA: Publicar Dashboards en GitHub Pages

## 📦 Archivos Preparados

He preparado 4 archivos para tu repositorio:

1. **index.html** - Página principal con enlaces a ambos dashboards
2. **dashboard-presupuesto-ti.html** - Dashboard de Presupuesto TI 2025
3. **dashboard-renovacion-ufinet.html** - Dashboard de Renovación UFINET
4. **README.md** - Documentación del repositorio

---

## 🔧 MÉTODO 1: Subir Archivos desde la Web (MÁS FÁCIL)

### Paso 1: Subir los archivos
1. En tu repositorio (donde estás ahora), haz click en **"Add file"** → **"Upload files"**
2. Arrastra los 4 archivos que te proporcioné
3. En el cuadro de "Commit changes" escribe: `Agregar dashboards iniciales`
4. Click en **"Commit changes"** (botón verde)

### Paso 2: Activar GitHub Pages
1. Ve a **Settings** (en la barra superior de tu repo)
2. En el menú izquierdo, busca y click en **"Pages"**
3. En "Source", selecciona: **"Deploy from a branch"**
4. En "Branch", selecciona: **main** (o master) y carpeta **"/ (root)"**
5. Click en **"Save"**
6. ¡Espera 1-2 minutos!

### Paso 3: Obtener tu URL
Después de 1-2 minutos, recarga la página de Settings → Pages

Verás un mensaje verde con tu URL:
```
Your site is live at https://lhernandez-erc.github.io/dashboards/
```

¡Esa es tu URL para compartir! 🎉

---

## 💻 MÉTODO 2: Usar Git desde la Terminal (AVANZADO)

Si tienes Git instalado en tu computadora:

```bash
# 1. Clonar el repositorio
git clone https://github.com/lhernandez-erc/dashboards.git
cd dashboards

# 2. Copiar los archivos preparados a la carpeta
# (Copia los 4 archivos que te di a esta carpeta)

# 3. Agregar y subir
git add .
git commit -m "Agregar dashboards iniciales"
git push origin main

# 4. Activar GitHub Pages desde Settings (igual que Método 1, Paso 2)
```

---

## 🌐 URLs Finales

Una vez activado GitHub Pages, tus dashboards estarán disponibles en:

### Portal Principal:
```
https://lhernandez-erc.github.io/dashboards/
```

### Dashboard Presupuesto TI:
```
https://lhernandez-erc.github.io/dashboards/dashboard-presupuesto-ti.html
```

### Dashboard Renovación UFINET:
```
https://lhernandez-erc.github.io/dashboards/dashboard-renovacion-ufinet.html
```

---

## 🔄 Cómo Actualizar los Dashboards

### Cuando necesites actualizar:

**Opción A - Desde la Web:**
1. Ve a tu repositorio en GitHub
2. Click en el archivo que quieres actualizar (ej: `dashboard-presupuesto-ti.html`)
3. Click en el icono del lápiz (✏️) arriba a la derecha
4. Reemplaza el contenido con la nueva versión
5. Click en **"Commit changes"**
6. Espera 1 minuto y la URL se actualizará automáticamente

**Opción B - Subir nuevo archivo:**
1. En tu repo, click **"Add file"** → **"Upload files"**
2. Sube el archivo actualizado (sobrescribirá el anterior)
3. Commit changes
4. GitHub Pages se actualiza automáticamente

---

## ✅ Checklist de Verificación

Después de seguir los pasos, verifica:

- [ ] Los 4 archivos están en tu repositorio
- [ ] GitHub Pages está activado en Settings
- [ ] La URL principal carga correctamente
- [ ] Ambos dashboards son accesibles desde sus URLs
- [ ] Los dashboards funcionan correctamente (prueba filtros, gráficos)

---

## 🎯 Compartir con tu Equipo

Una vez publicado, solo comparte la URL principal:

```
https://lhernandez-erc.github.io/dashboards/
```

**Ventajas:**
✅ URL profesional y fácil de recordar
✅ No necesitas enviar archivos HTML
✅ Actualizaciones instantáneas para todos
✅ Funciona en cualquier dispositivo
✅ Sin instalación requerida

---

## 🔒 Seguridad

**Nota Importante:**
- Tu repositorio es PÚBLICO, pero los archivos HTML solo contienen código
- Los datos se cargan desde el Excel del usuario localmente
- NO se suben datos sensibles al repositorio
- Las versiones "compartibles" tienen datos embebidos, úsalas con cuidado

**Si necesitas más privacidad:**
- Puedes hacer el repositorio PRIVADO en Settings → General → Danger Zone
- GitHub Pages seguirá funcionando con la URL
- Solo usuarios con acceso al repo podrán ver el código fuente

---

## 🆘 Solución de Problemas

### "La página no carga / Error 404"
- Verifica que GitHub Pages esté activado
- Espera 2-3 minutos después de subir archivos
- Verifica que el nombre del archivo sea exactamente igual en el index.html

### "Los dashboards no funcionan"
- Abre la consola del navegador (F12) y busca errores
- Verifica que los archivos se subieron completamente
- Prueba en modo incógnito / navegador diferente

### "Quiero cambiar la URL"
- Ve a Settings → Pages
- Puedes agregar un dominio personalizado (ej: dashboards.erccapital.com)
- Requiere configuración DNS adicional

---

## 📞 Soporte

Si tienes problemas, puedes:
1. Revisar la documentación de GitHub Pages: https://pages.github.com/
2. Contactar al equipo de TI de ERC
3. Consultar el README.md del repositorio

---

**¡Todo listo para publicar!** 🚀

Sigue el **MÉTODO 1** (es el más fácil) y en 5 minutos tendrás tus dashboards en línea.
