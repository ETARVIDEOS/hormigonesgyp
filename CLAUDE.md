# Hormigones G&P — Guía de desarrollo

## Stack
Sitio estático HTML + CSS + JS vanilla. Sin frameworks.  
Deploy: GitHub → Netlify (dominio: hormigonesgyp.cl)  
Server local: `npx serve -l 3456 .` (ver `.claude/launch.json`)

## Archivos base

| Archivo | Rol |
|---------|-----|
| `index.html` | One-page principal con todas las secciones |
| `style.css` | Hoja de estilos global — no duplicar reglas aquí definidas |
| `robots.txt` | LLM crawlability (GPTBot, Claude-Web, CCBot, etc.) |
| `sitemap.xml` | Sitemap para SEO y LLMs |
| `assets/logo.png` | Logo G&P (rojo/gris circular) |
| `assets/img/` | Fotos reales de obra (camiones mixer) |
| `assets/multimedia/` | Videos MP4 del cliente |

---

## Paleta de colores de marca

| Variable | Valor | Uso |
|----------|-------|-----|
| `--red` | `#DC2626` | Color primario, CTAs, acentos |
| `--red-dark` | `#B91C1C` | Hover del rojo |
| `--yellow` | `#F59E0B` | Accent, botón nav CTA, highlights |
| `--yellow-dk` | `#D97706` | Hover del amarillo |
| `--dark` | `#1f2937` | Texto principal, fondo header |
| `--dark-2` | `#374151` | Fondos oscuros secundarios |
| `--gray` | `#6B7280` | Texto secundario |
| `--light` | `#F3F4F6` | Fondos de secciones claras |
| `--white` | `#ffffff` | Fondos de tarjetas |

---

## Información de la empresa

- **Nombre:** Hormigones G&P
- **Ubicación:** Maule, Región del Maule, Chile
- **Cobertura:** Linares a Camarico (NO zonas costeras: Cauquenes, Pelluhue, Chanco)
- **Comunas:** San Clemente, Colbún, Pencahue, Pelarco, San Rafael, Linares, Camarico y aledañas
- **Horario:** Lunes a Sábado — coordinamos según las necesidades del cliente
- **Experiencia:** Más de 25 años en el rubro
- **Compromiso:** "Entregar productos de excelencia con un servicio cercano y confiable a la comunidad"

---

## Contacto

- **WhatsApp:** `+56981578903` → URL: `https://wa.me/56981578903`
- **Llamados:** `+56996747681`
- **Email:** `contacto@hormigonesgyp.cl`

> Todos los botones "Cotizar" y "Contactar" abren WhatsApp.  
> Excepción: botón "Enviar correo" en la CTA band → `mailto:`

---

## Secciones del sitio (en orden)

1. `#inicio` — Hero con video de fondo + typing effect
2. Stats — Banda roja con contadores (25+ años, 500+ proyectos, 15+ comunas) — **3 ítems, grid 3 columnas**
3. `#servicios` — 5 tarjetas: Premezclado, Bombeo, Cobertura, Asesoría, Cierres Perimetrales — **5.° ítem centrado en desktop (grid-column: 2/4), reseteado en tablet/mobile**
4. `#nosotros` — Split layout foto + texto + lista de valores
5. `#galeria` — Grid de fotos y videos (fondo oscuro)
6. `#cobertura` — Mapa Google Maps + lista de comunas
7. Horario — Banda oscura: Horario · WhatsApp · Llamados · Email — **4 ítems, grid 4 columnas desktop / 2 tablet / 1 mobile**
8. `#contacto` — CTA band roja → WhatsApp + email
9. Footer — 4 columnas: marca, empresa, servicios, contacto

---

## Hero — Video de fondo

**Actualmente:** Video local `assets/multimedia/video-01.mp4`  
**Para cambiar a YouTube:** En `index.html` busca `OPCIÓN A` en el hero y reemplaza `YOUTUBE_ID` con el ID del video de YouTube. Luego comenta/elimina `OPCIÓN B`.

```html
<!-- Ejemplo con ID de YouTube -->
<iframe src="https://www.youtube.com/embed/ABC123xyz?autoplay=1&mute=1&loop=1&playlist=ABC123xyz&controls=0&showinfo=0&rel=0&iv_load_policy=3&modestbranding=1" ...>
```

---

## CSS global — Convenciones clave

| Selector | Descripción |
|----------|-------------|
| `.btn--red` | Botón rojo primario |
| `.btn--yellow` | Botón amarillo CTA |
| `.btn--wsp` | Botón verde WhatsApp |
| `.section--dark` | Sección fondo oscuro (`#1f2937`) |
| `.section--light` | Sección fondo gris claro |
| `.section--red` | Sección fondo rojo |
| `.service-card` | Tarjeta de servicio con borde y hover |
| `.gallery-item` | Item de galería (foto o video) |
| `.gallery-item--wide` | Ocupa 2 columnas del grid |
| `.wsp-float` | Botón WhatsApp flotante fijo |
| `.section__tag` | Etiqueta pequeña encima del título |

---

## Animaciones de entrada (IntersectionObserver)

Agregar clase al elemento HTML y se activa al hacer scroll:

| Clase | Efecto |
|-------|--------|
| `fade-in` | Aparece (solo opacidad) |
| `slide-up` | Sube desde abajo |
| `slide-left` | Entra desde la izquierda |
| `slide-right` | Entra desde la derecha |
| `zoom-in` | Zoom desde escala 0.94 |
| `delay-1` a `delay-5` | Retraso de 0.1s a 0.5s |

---

## Script obligatorio en todos los HTML

```html
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
<script>
  lucide.createIcons();
  const observer = new IntersectionObserver((entries, obs) => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); } });
  }, { threshold: 0.12 });
  document.querySelectorAll('.fade-in,.slide-up,.slide-left,.slide-right,.zoom-in').forEach(el => observer.observe(el));
</script>
```

---

## Fase 2 — Deploy (pendiente aprobación diseño)

1. `git init` en `C:\Proyectos\HORMIGONES GYP`
2. Crear repo en GitHub (público o privado)
3. Conectar Netlify al repo → auto-deploy en push a `main`
4. Configurar dominio `hormigonesgyp.cl` en Netlify DNS
5. Lark webhook para notificaciones de contacto (3 correos — pendiente datos)

---

## Checklist para nuevas páginas/cambios

- [ ] Paleta respeta variables CSS de `style.css`
- [ ] Botones de contacto apuntan a WhatsApp correcto (+56981578903)
- [ ] robots.txt y sitemap.xml actualizados si se agregan páginas
- [ ] Animaciones de entrada en secciones nuevas
- [ ] Responsive mobile verificado (375px · 768px · 1024px)
- [ ] `lucide.createIcons()` ejecutado al final
- [ ] `html` y `body` tienen `overflow-x: hidden`
- [ ] Grids con columnas = número de ítems reales
- [ ] `grid-column` con span reseteado en todas las media queries
- [ ] Ningún `right/bottom` negativo sin `overflow:hidden` en el padre

---

## Lecciones aprendidas — Responsive mobile

Errores ocurridos en este proyecto y cómo evitarlos:

| Error | Síntoma | Fix |
|-------|---------|-----|
| `html` sin `overflow-x:hidden` | Página se desplaza a la derecha en mobile | Agregar a `html` Y `body` |
| Grid con más columnas que ítems | Espacio vacío a la derecha | `repeat(N_items, 1fr)` siempre |
| `grid-column: X/Y` sin reset en media query | Cards no apilan, se salen del contenedor | Agregar `grid-column: auto` en cada breakpoint |
| `right: -20px` sin `overflow:hidden` en el padre | Elemento desborda el viewport | Agregar `overflow:hidden` al contenedor |
| Grid con N columnas pero N+1 ítems | Ítem solitario en nueva fila desalineado | Actualizar el grid al agregar/quitar ítems |
