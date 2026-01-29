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
- [x] Investigado código de FancyBox - incompatible con jQuery 3.x
- [x] Detectado problema: FancyBox 1.3.4 usa APIs deprecadas (jQuery.browser, .live())
- [x] Solución: Reemplazado FancyBox con Lightbox2 (librería moderna)
- [x] Actualizado todos los HTML con `data-lightbox="gallery"`
- [x] Añadidos archivos Lightbox2: JS, CSS, imágenes (prev, next, close, loading)
- [x] Navegación con flechas prev/next funcionando correctamente
- [x] También corregido problema de contenido mixto (HTTP→HTTPS)
- **Commits:** a4c9ed9, 30720eb, b05d21b, e04e084

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
- [x] Añadir 4 registros A de GitHub Pages (DNS only - nube gris)
- [x] Añadir CNAME www → agraciag.github.io (DNS only - nube gris)
- [x] Verificar propagación DNS
- [x] SSL/HTTPS activado automáticamente en GitHub Pages

### GitHub Repository
- [x] Repositorio creado: https://github.com/agraciag/amayaaznar.es
- [x] GitHub Pages activado
- [x] CNAME configurado
- [x] Sitio accesible en https://amayaaznar.es
- [x] Corregido contenido mixto (Google Fonts HTTP→HTTPS)

---

## 📝 **NOTAS**

- **Email actual:** amayaaznar@gmail.com
- **Dominio:** amayaaznar.es (DNS en Cloudflare)
- **Hosting:** GitHub Pages (gratis)
- **Tamaño:** ~130MB / 1GB disponible (87% libre)
- **Tecnología:** HTML estático + CSS + JavaScript (jQuery 3.7.1 + Lightbox2)
- **Tema original:** Modest (WordPress)
- **HTTPS:** ✅ Activo con certificado válido

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
