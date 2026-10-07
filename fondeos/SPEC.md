# Fondeos — Spec Técnica

Material de capacitación interactiva sobre cuentas de fondeo, para la organización de Johnny Bravo (@johnnyfxec). Vive en `johnnyfxec.com/fondeos/` dentro del repo `johnnyfxec.github.io`.

Este documento es la fuente de verdad técnica antes de escribir el HTML final. Se actualiza a medida que se cierran decisiones (contenido, preguntas, mecanismo de reveal) — no se regenera completo, se edita por comando según el protocolo FYR.

---

## Objetivo del material

Página standalone, formato "presentación" (poco texto, títulos/subtítulos, links de apoyo), navegable pantalla por pantalla como diapositivas. Pensada para durar en el tiempo (a diferencia de los PDFs usados antes), y para ser recorrida **en vivo** durante una capacitación grupal, con preguntas que la audiencia responde por WhatsApp fuera de la página (no hay botón de WhatsApp embebido — el teléfono de Johnny no va público en el HTML).

---

## Repo y ubicación

- Repo: `~/johnnyfxec.github.io` (clonado en Termux, remote `https://github.com/johnnyfxec/johnnyfxec.github.io`)
- Carpeta nueva: `fondeos/`
- Archivo final: `fondeos/index.html` (mismo patrón que `qdla/manual.html`)
- Esta spec: `fondeos/SPEC.md`
- Publica en `johnnyfxec.com/fondeos/` vía el `CNAME` ya existente del repo — sin pasos de configuración adicionales.

---

## Mecanismo de navegación — extraído de `latam.luis-velez.com`

Fuente: `~/Lanzamientos-Luis/Latam/index.html` (repo `luis-velez86/LandingPageLatam`, clonado en `~/Lanzamientos-Luis/Latam`).

### CSS base del deck

```css
.deck{
  position:fixed;
  top:0;left:0;
  width:100%;
  will-change:transform;
  transition:transform 0.8s cubic-bezier(0.76,0,0.24,1);
}

.card{
  position:relative;
  width:100%;height:100vh;height:100dvh;
  overflow:hidden;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
}
```

### Rail de progreso (puntitos laterales)

```css
.rail{
  position:fixed;
  right:18px;top:50%;
  transform:translateY(-50%);
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:6px;
  z-index:200;
}

.rail-dot{
  width:5px;height:5px;
  border-radius:50%;
  background:rgba(138,155,181,0.25);
  border:1px solid rgba(138,155,181,0.4);
  cursor:pointer;
  transition:all 0.35s ease;
}

.rail-dot.active{
  background:var(--gold);
  border-color:var(--gold);
  box-shadow:0 0 8px rgba(201,168,76,0.5);
  height:18px;
  border-radius:3px;
}

.rail-dot.done{
  background:var(--emerald-bright);
  border-color:var(--emerald-bright);
}
```

> Nota: en fondeos, adaptar `.rail-dot.done` a la paleta de la guía (dorado `--c-gold` en vez de esmeralda) — no hay concepto de "video completado" acá, pero puede usarse para marcar "card ya vista".

### HTML — estructura del deck

```html
<nav class="rail" id="rail">
  <div class="rail-dot active" data-card="0"></div>
  <div class="rail-dot" data-card="1"></div>
  <!-- un rail-dot por card -->
</nav>

<div class="deck" id="deck">
  <div class="card" id="card-0"> ... </div>
  <div class="card" id="card-1"> ... </div>
  <!-- una card por pantalla -->
</div>
```

### JS — navegación (wheel + touch + rail click)

```js
var cur = 0, moving = false;

function goTo(n) {
  if (moving || n === cur) return;
  moving = true; cur = n;
  document.getElementById('deck').style.transform = 'translateY(calc(-'+n+' * 100dvh))';
  updateRail(n);
  setTimeout(function(){ moving=false; }, 850);
}

function updateRail(n) {
  document.querySelectorAll('.rail-dot').forEach(function(d,i){
    d.classList.remove('active','done');
    if(i<n) d.classList.add('done');
    if(i===n) d.classList.add('active');
  });
}

document.querySelectorAll('.rail-dot').forEach(function(d){
  d.addEventListener('click', function(){ goTo(parseInt(this.dataset.card)); });
});

window.addEventListener('wheel',function(e){
  if(moving) return;
  if(e.deltaY>30) goTo(Math.min(cur+1, TOTAL_CARDS-1));
  else if(e.deltaY<-30) goTo(Math.max(cur-1,0));
},{passive:true});

var ty0=0;
window.addEventListener('touchstart',function(e){
  ty0=e.touches[0].clientY;
},{passive:true});

window.addEventListener('touchend',function(e){
  var dy=ty0-e.changedTouches[0].clientY;
  if(Math.abs(dy)>50) {
    if(dy>0) goTo(Math.min(cur+1, TOTAL_CARDS-1));
    else goTo(Math.max(cur-1,0));
  }
},{passive:true});
```

> `TOTAL_CARDS` reemplaza el `4` hardcodeado de Luis (su deck tenía 5 cards, índices 0–4) — en fondeos se calcula según la cantidad real de cards definidas en el contenido.

### Lo que NO se trae de Luis

- Gating por % de video visto (`UMBRAL`, YouTube IFrame API, `done{1,2,3}`, `localStorage` de progreso de video) — no aplica, fondeos no tiene ese tipo de contenido.
- `localStorage` de progreso en general — descartado para esta pieza (capacitación sincrónica en vivo, no consumo individual asincrónico; ver discusión en el historial de esta conversación si se reconsidera a futuro para un reuso como material de consulta post-capacitación).
- Slideshow de imágenes del hero (`.slideshow`, `pool`, `allSlides`) — específico del hero de Luis, no se reutiliza salvo que una card puntual de fondeos lo pida.
- Botón de WhatsApp con número prellenado (`btn-wa`, `wa.me/...`) — **explícitamente descartado**. El teléfono de Johnny no va público en el HTML. Las respuestas de la audiencia se envían por WhatsApp fuera de la página, a un canal que Johnny define aparte (no es parte de este documento).

---

## Paleta y tipografía — extraído de la guía de inicio rápido

Fuente: `~/jifu-knowledge/guia-inicio-rapido.html` (repo `jifu-knowledge`, GitHub Pages propio servido en `johnnyfxec.com/jifu-knowledge/` vía Cloudflare).

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;1,400&display=swap');

:root {
  /* Paleta */
  --c-bg:        #0A0A0A;
  --c-card:      #141414;
  --c-border:    #252525;
  --c-gold:      #C9A84C;
  --c-gold-lt:   #E8C97A;
  --c-gold-dim:  rgba(201,168,76,0.10);
  --c-gold-ring: rgba(201,168,76,0.35);
  --c-text:      #F0EDE8;
  --c-muted:     #7A7672;
  --c-success:   #3FB950;

  /* Tipografía — una sola familia */
  --font: 'Inter', system-ui, -apple-system, sans-serif;

  /* Escala tipográfica */
  --text-xs:   0.70rem;
  --text-sm:   0.825rem;
  --text-base: 1rem;
  --text-lg:   1.125rem;
  --text-xl:   1.25rem;
  --text-2xl:  1.5rem;
  --text-3xl:  2rem;
  --text-hero: clamp(2rem, 5vw, 3.4rem);

  /* Espaciado — múltiplos de 8 */
  --s1: 8px; --s2: 16px; --s3: 24px; --s4: 32px; --s5: 40px; --s6: 48px; --s8: 64px;

  /* Radios */
  --r-sm: 6px; --r-md: 12px; --r-lg: 16px; --r-pill: 999px;
}

*, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }

body {
  font-family: var(--font);
  font-size: var(--text-base);
  font-weight: 400;
  line-height: 1.6;
  background: var(--c-bg);
  color: var(--c-text);
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
}
```

---

## Tipos de card definidos

1. **Portada / Hero** — título principal, subtítulo breve, branding (equivalente al `#card-0` de Luis, sin slideshow salvo que se pida).
2. **Contenido explicativo** — título + subtítulo + bullets o puntos clave, estilo visual tipo tarjeta de tarea de la guía (ícono, hook, texto breve) pero sin checkbox de progreso.
3. **Pregunta interactiva** — enunciado de la pregunta. La audiencia responde por WhatsApp fuera de la página, en vivo, durante el tiempo que Johnny da en la capacitación. La card incluye un control para **revelar la respuesta correcta** después de ese tiempo (mecanismo de reveal exacto: pendiente de definir — ver sección siguiente).
4. **Cierre / CTA** — mensaje de cierre, sin botón de WhatsApp con número embebido (a diferencia del CTA final de Luis).

---

## Pendiente de definir

- **Card tipo "pregunta + reveal" — DESCARTADA.** La única interactividad real de la página son los Ejercicios aleatorios y la Calculadora de consistencia (ambos con inputs y cálculo en vivo). Las preguntas por WhatsApp en vivo siguen siendo parte de la dinámica de Johnny al dar la capacitación, pero no requieren ninguna card ni mecanismo dedicado dentro del HTML.
- **Contenido real**: definido en detalle en `fondeos/ESTRUCTURA.md` (estructura completa de ~20 cards en 6 fases).
- **Cantidad total de cards** (`TOTAL_CARDS` en el JS): a confirmar contando las cards finales de `fondeos/ESTRUCTURA.md` una vez cerrados los pendientes de esa estructura.

## Links de FAQ por empresa (para la Card 3)

- Atmos: https://help.atmosfunded.com/en/
- FTMO: https://ftmo.com/es/faq/
- 5ERS: https://the5ers.com/faqs/
- FundingPips (Trading Objectives): https://fundingpips.com/trading-objectives
- FundingPips (FAQs): https://help.fundingpips.com/hc/en-us
- Alpha Capital: https://help.alphacapitalgroup.uk/en/
- Breakout: https://intercom.help/breakoutprop/en/

## Fuente de calendario de noticias fundamentales (para Card 15)

- ForexFactory: https://www.forexfactory.com
- Investing.com (Economic Calendar): https://www.investing.com/economic-calendar
