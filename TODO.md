# 📋 Tareas Pendientes - Amaya Aznar Photography

## 🔴 **CRÍTICO - Corregir antes del lanzamiento**

### 1. **Protección Email contra Spam** ⚠️ PENDIENTE
- [ ] Implementar obfuscación del email en `contacto/index.html`
- [ ] Opciones:
  - CloudFlare Email Protection
  - JavaScript para ofuscar: `amayaaznar[at]gmail[dot]com`
  - Servicio como Formspree (formulario real sin exponer email)
- **Archivo:** `contacto/index.html`

### 2. **Galerías - Thumbnails no se visualizan** ✅ RESUELTO
- [x] Investigar por qué los thumbnails de las galerías no cargan
- [x] Verificar rutas de imágenes en páginas de galerías
- [x] Arreglado: srcset con rutas relativas incorrectas
- **Solución:** Añadido prefijo `../` a todas las rutas en srcset
- **Commit:** 1ccead8

### 3. **Navegación Modal en Galerías** ✅ RESUELTO
- [x] Investigado código de FancyBox
- [x] Detectado problema: enlaces sin clase `fancybox` ni `rel="gallery"`
- [x] Añadido selector para galerías de WordPress Gutenberg (`.wp-block-image`)
- [x] JavaScript añade dinámicamente `rel="gallery"` a todos los enlaces
- [x] Habilitada navegación cíclica (última → primera imagen)
- **Solución:** Modificado `et-ptemplates-frontend.js` para agrupar imágenes
- **Commits:** a4c9ed9, 30720eb

### 4. **Iconos del menú superior (Twitter, RSS, Facebook)** ✅ RESUELTO
- [x] Iconos descargados y funcionando
- [ ] **DECISIÓN PENDIENTE:** ¿Conservar o eliminar iconos?
  - Twitter link: placeholder (`#`)
  - RSS link: funciona (comments/feed/)
  - Facebook link: placeholder (`#`)
- **Ubicación:** Header de todas las páginas
- **Archivos:** `wp-content/themes/Modest/images/*.png`
- **Commit:** 1ccead8

### 5. **Página de Descargas** ✅ RESUELTO
- [x] PDFs descargados (64MB)
- [x] Enlaces corregidos a rutas relativas
- [x] Layout mejorado con tarjetas individuales
- [x] Botón "Ver PDF" (abre en nueva pestaña)
- [x] Botón "Descargar" para descarga directa
- [x] Descripciones añadidas a cada portfolio
- **Archivos:** 4 PDFs en `wp-content/uploads/2023/03/`
- **Commits:** 1ccead8, a4c9ed9

---

## 🟡 **MEJORAS - Post-lanzamiento**

### 6. **Foto Portada**
- [x] La foto principal de portada SÍ se visualiza correctamente
- No requiere acción

### 7. **Optimización de Imágenes**
- [ ] Considerar conversión a WebP para mejorar rendimiento
- [ ] Implementar lazy loading
- [ ] Comprimir imágenes sin pérdida de calidad
- **Tamaño actual:** 129MB (1,352 imágenes)
- **Objetivo:** Reducir a ~80-100MB

### 8. **SEO**
- [ ] Añadir meta descriptions a todas las páginas
- [ ] Verificar titles de páginas
- [ ] Añadir sitemap.xml
- [ ] Configurar robots.txt
- [ ] Open Graph tags para redes sociales

### 9. **Analytics**
- [ ] Decidir si añadir Google Analytics o alternativa
- [ ] Configurar privacy-friendly analytics (Plausible, Fathom, etc.)

### 10. **Performance**
- [ ] Minificar CSS y JavaScript
- [ ] Implementar service worker para caché
- [ ] CDN para assets estáticos

---

## 🔧 **TÉCNICO**

### DNS Configuración (Cloudflare)
- [x] Eliminar registros de Cloudflare Tunnel
- [ ] Añadir 4 registros A de GitHub Pages (DNS only - nube gris)
- [ ] Añadir CNAME www → agraciag.github.io (DNS only - nube gris)
- [ ] Verificar propagación DNS (24-48h)
- [ ] Activar SSL en GitHub Pages (automático tras DNS)

### GitHub Repository
- [x] Repositorio creado: https://github.com/agraciag/amayaaznar.es
- [x] GitHub Pages activado
- [x] CNAME configurado
- [ ] Verificar que el sitio es accesible en https://amayaaznar.es

---

## 📝 **NOTAS**

- **Email actual:** amayaaznar@gmail.com
- **Dominio:** amayaaznar.es (DNS en Cloudflare)
- **Hosting:** GitHub Pages (gratis)
- **Tamaño:** 129MB / 1GB disponible (87% libre)
- **Tecnología:** HTML estático + CSS + JavaScript (FancyBox)
- **Tema original:** Modest (WordPress)

---

## 🎯 **PRIORIDAD DE TAREAS**

1. **ALTA:** Protección email (tarea #1)
2. **ALTA:** Arreglar thumbnails galerías (tarea #2)
3. **ALTA:** Navegación modal (tarea #3)
4. **MEDIA:** Decidir sobre iconos sociales (tarea #4)
5. **MEDIA:** Arreglar página descargas (tarea #5)
6. **BAJA:** Optimizaciones y mejoras post-lanzamiento

---

**Última actualización:** 2026-01-29
**Responsable:** agraciag + Claude
