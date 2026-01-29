# 📋 Tareas Pendientes - Amaya Aznar Photography

## 🔴 **CRÍTICO - Corregir antes del lanzamiento**

### 1. **Protección Email contra Spam**
- [ ] Implementar obfuscación del email en `contacto/index.html`
- [ ] Opciones:
  - CloudFlare Email Protection
  - JavaScript para ofuscar: `amayaaznar[at]gmail[dot]com`
  - Servicio como Formspree (formulario real sin exponer email)
- **Archivo:** `contacto/index.html`

### 2. **Galerías - Thumbnails no se visualizan**
- [ ] Investigar por qué los thumbnails de las galerías no cargan
- [ ] Verificar rutas de imágenes en páginas de galerías
- [ ] Posible problema: rutas relativas vs absolutas
- **Archivos afectados:**
  - `retratos_/index.html`
  - `bodas_/index.html`
  - `ninos_/index.html`
  - `composiciones_/index.html`
  - `corporativas_/index.html`
  - `reportaje_/index.html`
  - `estructuras_/index.html`
  - `encuentros/index.html`

### 3. **Navegación Modal en Galerías**
- [ ] Lightbox/modal funcional pero sin navegación entre fotos
- [ ] Verificar si falta JavaScript de FancyBox
- [ ] Revisar configuración de FancyBox para navegación anterior/siguiente
- **JavaScript:** `wp-content/themes/Modest/epanel/page_templates/js/fancybox/`

### 4. **Iconos del menú superior (Twitter, RSS, Facebook)**
- [ ] Iconos no se visualizan (posible problema de rutas)
- [ ] Verificar enlaces de iconos (probablemente vacíos o placeholder)
- [ ] **DECISIÓN PENDIENTE:** ¿Conservar o eliminar iconos?
  - Si conservar: añadir enlaces reales a redes sociales
  - Si eliminar: limpiar HTML en todas las páginas
- **Ubicación:** Header de todas las páginas
- **Archivos de iconos:** `wp-content/themes/Modest/images/twitter.png`, `facebook.png`, `rss.png`

### 5. **Página de Descargas**
- [ ] Links amontonados (problema de layout/CSS)
- [ ] Enlaces llevan a 404s
- [ ] **Opciones:**
  - Arreglar enlaces y layout
  - Eliminar página si no es necesaria
  - Convertir a página informativa
- **Archivo:** `descargas/index.html`

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
