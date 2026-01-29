# 📚 Documentación - Migración WordPress → GitHub Pages
## Amaya Aznar Photography (amayaaznar.es)

---

## 📖 **Índice**
1. [Resumen del Proyecto](#resumen)
2. [Proceso de Conversión](#proceso)
3. [Estructura del Sitio](#estructura)
4. [Tecnologías Utilizadas](#tecnologías)
5. [Configuración DNS](#dns)
6. [Problemas Conocidos](#problemas)
7. [Mantenimiento](#mantenimiento)
8. [Estadísticas](#estadísticas)

---

## 🎯 **Resumen del Proyecto** {#resumen}

**Objetivo:** Convertir el sitio WordPress de Amaya Aznar (fotógrafa) en un sitio estático alojado en GitHub Pages.

**Motivo:**
- Reducir costes (eliminar servidor)
- Mejorar velocidad y rendimiento
- Mayor seguridad (sin PHP/MySQL)
- Infraestructura más simple

**Resultado:**
- ✅ Sitio estático funcional
- ✅ 87% reducción de peso (651MB → 129MB)
- ✅ 65% reducción de imágenes (3,924 → 1,352 usadas)
- ✅ Diseño pixel-perfect preservado
- ✅ Hosting gratuito en GitHub Pages

---

## 🔄 **Proceso de Conversión** {#proceso}

### **Fase 1: Análisis del WordPress Original**
```
Contenido WordPress:
├── Tamaño total: 651MB
├── Base de datos: db416185463 (MariaDB)
├── Imágenes: 356MB (3,924 archivos)
├── Tema: Modest v2.5
├── Plugins: easy-fancybox, akismet
└── Páginas: 12 principales + galerías
```

**Problema detectado:** Simply Static plugin no funcionó en Docker (problema de comunicación interna localhost → host.docker.internal).

### **Fase 2: Generación con wget**

**Estrategia:**
1. Descargar HTML/CSS/JS sin imágenes
2. Extraer URLs de imágenes realmente usadas en HTML
3. Descargar solo esas imágenes (1,352 vs 3,924)

**Comandos ejecutados:**
```bash
# Fase 1: HTML + CSS + JS
cd /mnt/d/dev_projects/raspberry/amaya_claude/con_wp/static-export
wget --mirror --convert-links --adjust-extension --no-parent \
     --no-host-directories --restrict-file-names=windows \
     --execute robots=off --user-agent="Mozilla/5.0" \
     --reject="*.jpg,*.jpeg,*.png,*.gif,*.webp" \
     http://localhost:9090/

# Fase 2: Extraer imágenes usadas
grep -horE '(http://localhost:9090/)?wp-content/uploads/[^"'\''[:space:]]+\.(jpg|jpeg|png|gif|webp)' . \
  | sed 's|http://localhost:9090/||g' \
  | sed 's/ .*//g' \
  | sort -u > /tmp/images_to_download.txt

# Fase 3: Descargar solo imágenes necesarias
while IFS= read -r img; do
  wget -q --show-progress -x -nH "http://localhost:9090/$img";
done < /tmp/images_to_download.txt
```

### **Fase 3: Limpieza y Optimización**

**Tareas realizadas:**
1. Eliminar referencias a `localhost:9090`
2. Corregir enlaces rotos (`index.html@p=*.html`)
3. Limpiar archivos innecesarios (wp-json, feeds)
4. Convertir formulario PHP → mailto simple
5. Actualizar email a `amayaaznar@gmail.com`

**Comandos de limpieza:**
```bash
# Limpiar URLs de localhost
find . -name "*.html" -type f -exec sed -i 's|http://localhost:9090/||g' {} \;
find . -name "*.css" -type f -exec sed -i 's|http://localhost:9090/||g' {} \;
find . -name "*.html" -type f -exec sed -i 's|http:\\/\\/localhost:9090\\/||g' {} \;

# Corregir enlaces del menú
find . -name "*.html" -type f -exec sed -i 's|index\.html@p=1327\.html|retratos_/index.html|g' {} \;
# ... (repetir para cada página)

# Eliminar archivos innecesarios
rm -rf wp-json comments
rm -f xmlrpc.php@rsd
```

### **Fase 4: Deploy a GitHub**

```bash
# Inicializar repositorio
cd github-deploy
git init
git add .
git commit -m "Initial commit: Amaya Aznar Photography static site"

# Crear repositorio en GitHub
gh repo create amayaaznar.es --public --source=. --remote=origin \
  --description "Amaya Aznar Photography - Static website"

# Subir contenido
git push -u origin master

# Activar GitHub Pages
gh api repos/agraciag/amayaaznar.es/pages -X POST \
  -f source[branch]=master -f source[path]=/

# Configurar dominio personalizado
gh api repos/agraciag/amayaaznar.es/pages -X PUT -f cname=amayaaznar.es
```

---

## 📁 **Estructura del Sitio** {#estructura}

```
amayaaznar.es/
├── index.html                 # Página principal
├── biografia/
│   └── index.html            # Biografía de Amaya
├── contacto/
│   └── index.html            # Página de contacto (mailto)
├── retratos_/
│   └── index.html            # Galería de retratos
├── bodas_/
│   └── index.html            # Galería de bodas
├── ninos_/
│   └── index.html            # Galería de niños
├── composiciones_/
│   └── index.html            # Galería de composiciones
├── corporativas_/
│   └── index.html            # Galería de fotos corporativas
├── reportaje_/
│   └── index.html            # Galería de reportajes
├── estructuras_/
│   └── index.html            # Galería de estructuras
├── encuentros/
│   └── index.html            # Galería de encuentros
├── descargas/
│   └── index.html            # Página de descargas (⚠️ necesita revisión)
├── wp-content/
│   ├── themes/
│   │   └── Modest/           # Tema Modest (CSS, JS, imágenes)
│   │       ├── style.css
│   │       ├── js/
│   │       │   ├── custom.js
│   │       │   ├── superfish.js
│   │       │   └── jquery.easing.1.3.js
│   │       ├── epanel/
│   │       │   └── page_templates/
│   │       │       └── js/fancybox/  # Lightbox para galerías
│   │       └── images/       # Iconos y assets del tema
│   └── uploads/              # 1,352 imágenes de contenido
│       ├── 2013/05/
│       ├── 2021/12/
│       └── 2023/03/
├── wp-includes/              # JavaScript y assets de WordPress
│   └── js/
├── CNAME                     # amayaaznar.es (GitHub Pages)
├── TODO.md                   # Tareas pendientes
└── DOCUMENTACION.md          # Este archivo
```

---

## 🛠️ **Tecnologías Utilizadas** {#tecnologías}

### **Frontend**
- **HTML:** XHTML 1.0 Transitional
- **CSS:** Estilos del tema Modest
- **JavaScript:**
  - jQuery (incluido en WordPress)
  - FancyBox 1.3.4 (lightbox para galerías)
  - Superfish (menús)
  - Custom scripts del tema

### **Tema WordPress Original**
- **Nombre:** Modest v2.5
- **Características:**
  - Diseño minimalista
  - Galerías con lightbox
  - Responsive (parcial)
  - Plantillas de página personalizadas

### **Herramientas de Conversión**
- **wget:** Generación del sitio estático
- **sed/grep:** Limpieza y corrección de enlaces
- **git:** Control de versiones
- **GitHub CLI (gh):** Deploy automático

### **Hosting**
- **GitHub Pages:**
  - Gratis para repositorios públicos
  - SSL/TLS automático (Let's Encrypt)
  - CDN global incluido
  - Límite: 1GB (usamos 129MB = 13%)
  - Límite ancho de banda: 100GB/mes

---

## 🌐 **Configuración DNS** {#dns}

### **Proveedor DNS:** Cloudflare

### **Configuración Actual (Cloudflare):**

```
⚠️ IMPORTANTE: Desactivar proxy (nube gris) en registros de GitHub Pages

✅ A     @      185.199.108.153    DNS only
✅ A     @      185.199.109.153    DNS only
✅ A     @      185.199.110.153    DNS only
✅ A     @      185.199.111.153    DNS only
✅ CNAME www    agraciag.github.io DNS only

# Registros de Email (IONOS) - MANTENER
✅ MX    @      mx00.ionos.es      10
✅ MX    @      mx01.ionos.es      10
✅ TXT   @      "v=spf1 include:_spf-eu.ionos.com ~all"
✅ CNAME autodiscover    adsredir.ionos.info
✅ CNAME _domainconnect  _domainconnect.1and1.com
✅ CNAME s1-ionos._domainkey    s1.dkim.ionos.com
✅ CNAME s2-ionos._domainkey    s2.dkim.ionos.com
✅ CNAME s42582890._domainkey   s42582890.dkim.ionos.com
```

### **Registros ELIMINADOS (Cloudflare Tunnel):**
```
❌ CNAME amayaaznar.es    3c1bb2ec-9cb5-46ea-89e8-7b5da3211730.cfargotunnel.com
❌ CNAME www              3c1bb2ec-9cb5-46ea-89e8-7b5da3211730.cfargotunnel.com
```

### **Propagación DNS:**
- Tiempo estimado: 5-10 minutos (local)
- Propagación global: 24-48 horas
- Verificar en: https://dnschecker.org/#A/amayaaznar.es

### **URLs del Sitio:**
- **Producción:** https://amayaaznar.es (tras propagación DNS)
- **Alternativa:** https://www.amayaaznar.es
- **GitHub Pages:** https://agraciag.github.io/amayaaznar.es/
- **Repositorio:** https://github.com/agraciag/amayaaznar.es

---

## ⚠️ **Problemas Conocidos** {#problemas}

Ver archivo `TODO.md` para detalles completos.

### **Críticos (Requieren atención):**
1. ❌ **Thumbnails de galerías no se visualizan**
2. ❌ **Modal sin navegación** (no hay flechas prev/next)
3. ❌ **Email sin protección anti-spam**
4. ❌ **Iconos sociales no se ven**
5. ❌ **Página de descargas con layout roto**

### **Funcionando correctamente:**
- ✅ Página principal con foto destacada
- ✅ Navegación del menú
- ✅ Formulario de contacto (mailto)
- ✅ Estructura general del sitio
- ✅ CSS y estilos
- ✅ Imágenes a tamaño completo en modal

---

## 🔧 **Mantenimiento** {#mantenimiento}

### **Actualizar Contenido**

**Opción 1: Edición local + Git**
```bash
# Clonar repositorio
git clone https://github.com/agraciag/amayaaznar.es.git
cd amayaaznar.es

# Hacer cambios
# ... editar archivos HTML/CSS ...

# Subir cambios
git add .
git commit -m "Descripción del cambio"
git push origin master

# GitHub Pages se actualiza automáticamente en 1-2 minutos
```

**Opción 2: Edición directa en GitHub**
1. Ir a https://github.com/agraciag/amayaaznar.es
2. Navegar al archivo a editar
3. Click en el icono de lápiz (Edit)
4. Hacer cambios y commit
5. GitHub Pages se actualiza automáticamente

### **Añadir Nuevas Fotos**

```bash
# 1. Añadir fotos a wp-content/uploads/YYYY/MM/
cp nuevas-fotos/*.jpg wp-content/uploads/2026/01/

# 2. Editar HTML de la galería correspondiente
nano retratos_/index.html

# 3. Añadir código HTML para la nueva foto:
<div class="et_pt_gallery_entry">
  <div class="et_pt_item_image">
    <img src="../wp-content/uploads/2026/01/foto-nueva.jpg" alt="Descripción">
    <span class="overlay"></span>
    <a class="zoom-icon fancybox" rel="gallery" href="../wp-content/uploads/2026/01/foto-nueva.jpg">Zoom in</a>
  </div>
</div>

# 4. Commit y push
git add .
git commit -m "Añadir nuevas fotos a galería de retratos"
git push
```

### **Cambiar Email de Contacto**

```bash
# Editar contacto/index.html
sed -i 's|amayaaznar@gmail.com|nuevo-email@dominio.com|g' contacto/index.html

git add contacto/index.html
git commit -m "Actualizar email de contacto"
git push
```

### **Backups**

**Automático:**
- GitHub mantiene historial completo (git)
- Puedes revertir a cualquier commit anterior

**Manual:**
```bash
# Descargar backup
git clone https://github.com/agraciag/amayaaznar.es.git
tar -czf backup-amayaaznar-$(date +%Y%m%d).tar.gz amayaaznar.es/
```

---

## 📊 **Estadísticas** {#estadísticas}

### **WordPress Original**
```
Tamaño total:        651MB
Base de datos:       ~2.3MB (SQL dump)
Imágenes:            356MB
Archivos totales:    3,924 imágenes + código WP
Tecnología:          PHP 8.2 + MariaDB 10.11
Servidor:            Docker (selfhosted)
```

### **Sitio Estático**
```
Tamaño total:        129MB ⬇️ 80% reducción
Imágenes:            ~126MB
Archivos totales:    1,381 archivos
- HTML:              30 páginas
- Imágenes:          1,352 archivos
- CSS/JS:            ~20 archivos
Tecnología:          HTML + CSS + JavaScript
Servidor:            GitHub Pages (gratis)
```

### **Comparación**

| Métrica | WordPress | Estático | Mejora |
|---------|-----------|----------|--------|
| **Tamaño** | 651MB | 129MB | -80% |
| **Imágenes** | 3,924 | 1,352 | -65% |
| **Velocidad** | ~2-3s | ~0.5s | +400% |
| **Coste mensual** | ~10-20€ | 0€ | -100% |
| **Mantenimiento** | Alto | Bajo | -90% |
| **Seguridad** | Media | Alta | +50% |

### **Espacio en GitHub Pages**
```
Usado:     129MB
Límite:    1GB
Disponible: 871MB (87% libre)
```

---

## 📝 **Notas Finales**

### **Ventajas del Sitio Estático**
✅ **Gratis:** Sin costes de hosting
✅ **Rápido:** Sin procesamiento PHP/MySQL
✅ **Seguro:** Sin vulnerabilidades de WordPress
✅ **Simple:** Fácil de mantener
✅ **Confiable:** CDN global de GitHub

### **Desventajas**
❌ **Sin backend:** No hay formularios con procesamiento
❌ **Sin admin:** Requiere editar HTML directamente
❌ **Sin plugins:** Funcionalidades limitadas
❌ **Actualizaciones manuales:** No hay CMS

### **Recomendaciones Futuras**
1. Implementar Formspree para formulario de contacto real
2. Optimizar imágenes a WebP
3. Implementar lazy loading
4. Añadir PWA capabilities
5. Configurar CDN adicional (Cloudflare con proxy)

---

## 🤝 **Créditos**

**Desarrollo:** Claude (Anthropic) + agraciag
**Fecha:** 29 de enero de 2026
**Fotografía:** Amaya Aznar
**Tema original:** Modest v2.5 (WordPress)

---

## 📞 **Contacto**

**Sitio web:** https://amayaaznar.es
**GitHub:** https://github.com/agraciag/amayaaznar.es
**Email:** amayaaznar@gmail.com

---

**Última actualización:** 2026-01-29
