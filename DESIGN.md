# DESIGN.md — Oñate Silva Design System

*Marca personal de Felipe Oñate Silva, consultor estratégico en UX y diseño de productos digitales (15+ años). Fuente de verdad del lenguaje visual — para agentes de IA (Claude Code, Cursor, Lovable, Stitch) que generan o editan interfaces on-brand.*

---

## Estado de este documento

**Este archivo es la fuente de verdad (SOT).** Se commitea a `onate-silva-ds` en GitHub y reemplaza al `DESIGN.md` anterior de ese repo. Jerarquía de fuentes, de mayor a menor autoridad:

1. **Este `DESIGN.md`** — lo que dice acá es lo correcto, punto.
2. **Producción** (`felipeonate2026`, tema `felipeonate`) — de donde se extraen los valores `PROD`, y quien gana por defecto cuando este documento todavía no tiene una decisión tomada sobre un token.
3. **Exports de Claude Design** (`Onate-Silva-Design-System.zip`, `tokens/*.css`) — insumo de diseño, no autoridad. Útil para generar prototipos y como borrador de valores nuevos, pero puede quedar desactualizado respecto a este documento (como pasó con `warning`) sin que eso sea un problema que bloquee nada — simplemente significa que el próximo export necesita corregirse para alinearse a este archivo, no al revés.

Cada token está marcado:

- **`PROD`** — implementado y verificado en `assets/css/main.css` / `templates/*.css` de producción, vía lectura directa de código.
- **`TARGET`** — objetivo de marca, no implementado en producción hoy. Viene de la capa semántica (`--surface-*`, `--accent`, componentes React) o de valores nunca extraídos a `:root` en producción.
- **`AMBOS`** — mismo valor en los dos sistemas.
- **`RESUELTO EN DESIGN.MD`** — un token donde este documento fijó un valor que corrige o reemplaza lo que dice el export de Claude Design vigente. Cuando se re-exporte el DS, ese export debe alinearse a este archivo, no producir una nueva discusión.

**Si estás editando templates PHP del tema:** usa solo los valores `PROD` o `AMBOS`, y la convención `--color-*` de `CLAUDE.md`. Nunca introduzcas `--surface-*`, `--accent` ni nombres semánticos en ese contexto — ese vocabulario es exclusivo de prototipos en Claude Design / Lovable / Stitch.

**Historial de consolidación (7 ago 2026):** cruce inicial contra `DESIGN.md` raw de GitHub → lectura de `main.css`/`templates/*.css` de producción → lectura de `tokens/*.css` del export `Onate-Silva-Design-System.zip`, que resolvió espaciado y movimiento (no eran conflictos, el DS ya los reconciliaba) → confirmación visual directa del peso del H1 (300, ver sección Tipografía) → establecimiento de este archivo como SOT por sobre Claude Design.

---

## Brief de producto

Sitio de marca personal y vehículo principal de captación de clientes para Felipe Oñate Silva. Audiencias: dueños de startups, directivos C-Level, líderes de producto/diseño, y profesionales en transición. La interfaz debe transmitir criterio estratégico y autoridad técnica sin caer en ornamento — cada elemento visual debe poder justificarse con la misma lógica que la marca aplica al diseño: evidencia antes que estética.

## Principios de diseño

- **Contraste calmado, no decorativo.** Turquesa y menta en dosis pequeñas y deliberadas — nunca como relleno.
- **Los radios son modestos.** La marca gráfica es angulosa; nada de esquinas sobre-redondeadas ni "blobs".
- **La elevación se sugiere, no se dramatiza.** Sombras suaves, tintadas en frío, bajo contraste.
- **Un CTA primario por vista.** La autoridad viene del argumento, no del volumen de botones ni de signos de exclamación.
- **El espacio en blanco es un activo de marca**, no espacio desperdiciado — ritmo vertical generoso.

---

## Color

### Escala base — `AMBOS`, verificada byte a byte contra `main.css`

```yaml
turquesa-50:  "#E8F2F4"
turquesa-100: "#D0E6EA"
turquesa-200: "#A2CDD5"
turquesa-300: "#73B3C0"
turquesa-400: "#459AAB"
turquesa-500: "#168196"  # Primario de marca — CTAs, links activos, la marca gráfica. Nunca fondo de página completo.
turquesa-600: "#126778"
turquesa-700: "#0D4D5A"
turquesa-800: "#09343C"
turquesa-900: "#041A1E"

menta-50:  "#F0F8F6"
menta-100: "#E1F0ED"
menta-200: "#C3E2DB"
menta-300: "#A4D3C8"
menta-400: "#86C5B6"
menta-500: "#68B6A4"  # Secundario — acentos, rellenos suaves. Único gradiente permitido: turquesa → menta.
menta-600: "#539283"
menta-700: "#3E6D62"
menta-800: "#2A4942"
menta-900: "#152421"

gris-50:  "#E6E6E7"
gris-100: "#CCCECE"
gris-200: "#B3B5B6"
gris-300: "#9A9D9D"
gris-400: "#808484"
gris-500: "#676B6C"  # Texto secundario, bordes, metadatos.
gris-600: "#4E5354"
gris-700: "#353A3B"  # Tinta del wordmark. Texto de máxima fuerza en contexto de marca.
gris-800: "#1A1D1D"
gris-900: "#0D0E0E"

negro:  "#02090A"  # Tinta pura. Solo texto más fuerte y superficies inversas. No usar como texto de cuerpo por defecto.
blanco: "#FAFAFA"  # Superficie de página por defecto. Las tarjetas suben a blanco puro (#FFFFFF) donde el componente lo requiera.
```

### Estados semánticos — `RESUELTO EN DESIGN.MD` para `warning`, resto `AMBOS`

```yaml
error:   "#C0473C"  # 4.78:1 sobre blanco — válido como texto de cuerpo. AMBOS, coincide.
success: "#2E8E6A"  # AMBOS, coincide.
warning: "#B47318"  # RESUELTO EN DESIGN.MD — este es el valor correcto, sin ambigüedad.
                     # Historia: el original (#C98A2B) daba 2.57:1 sobre warning-soft — no
                     # alcanzaba el umbral WCAG de 3:1 para elementos no textuales. Producción
                     # lo corrigió a #B47318 (3.41:1 sobre warning-soft, pasa 3:1 — válido para
                     # bordes/íconos), documentado en un comentario explícito dentro de main.css.
                     # LÍMITE: ninguno de los dos valores alcanza 4.5:1 sobre --blanco (B47318 da
                     # 3.72:1) — warning NUNCA como texto de cuerpo directo sobre blanco, solo
                     # bordes, íconos, o texto sobre su propio -soft (gris-700/negro encima).
                     # El export de Claude Design del 7 ago 2026 todavía trae #C98A2B — no es un
                     # bloqueo. Este documento manda; el próximo export del DS debe alinearse a
                     # este valor, no generar una nueva discusión sobre cuál es el correcto.
info:    "#1A38B2"  # AMBOS, coincide.

error-soft:   "#F7E7E5"
success-soft: "#E7F3EE"
warning-soft: "#F8EFE0"
info-soft:    "#E8ECFB"
```

Reservados exclusivamente a significado semántico real (estado de un proceso, validación de formulario). Nunca decorativos.

### Capa semántica — `TARGET`, no implementada en producción

```yaml
--text-strong: var(--negro)
--text-body:   var(--gris-700)
--text-muted:  var(--gris-500)
--text-brand:  var(--turquesa-600)

--surface-page:       var(--blanco)
--surface-card:       "#FFFFFF"
--surface-brand-soft: var(--turquesa-50)

--accent:        var(--turquesa-500)
--accent-hover:  var(--turquesa-600)  # Botones primarios oscurecen en hover, nunca cambian de familia de color.
--accent-active: var(--turquesa-700)

--border-subtle: var(--gris-100)
--border-focus:  var(--turquesa-400)

--ring: 0 0 0 3px color-mix(in srgb, var(--turquesa-500) 28%, transparent)
# Anillo de foco — siempre turquesa, nunca azul de sistema operativo por defecto.
```

**Nota de superficies oscuras — `PROD`, no documentada en el DS original:** producción define `--color-dark-surface: var(--color-turquesa-900)` y `--color-dark-card: var(--color-menta-900)`, usadas en `.contact-section` y `.site-footer`. El DS no tiene equivalente semántico para esto — es información que solo existe en producción y falta incorporar al vocabulario `--surface-*` (ej. `--surface-inverse`).

---

## Tipografía

```yaml
display:
  font: "Comfortaa"
  weight: 300  # CONFIRMADO por Felipe (7 ago 2026, comparación visual directa) como el peso de marca correcto.
               # PROD ya lo tenía así en las tres plantillas (home.css, services.css, portfolio.css).
               # TARGET (tokens/typography.css, base.css .os-display, guideline card type-display.html)
               # todavía declara 600 — ESO es lo que hay que corregir en el DS, no producción.
  # RIESGO TÉCNICO PENDIENTE: tokens/fonts.css solo importa Comfortaa en pesos 500/600/700
  # (`family=Comfortaa:wght@500;600;700`). El peso 300 no está en ese @import — verificar el
  # enqueue real de Google Fonts en functions.php de producción para confirmar que 300 carga
  # como fuente real y no como síntesis del navegador.
  usage: Titulares hero y declaraciones de alto impacto. Nunca dentro de componentes o tarjetas — solo a nivel de sección/página.
  size_prod: "3.6rem (57.6px) desktop / 2.5rem mobile ≤768px"  # PROD, valor exacto de CLAUDE.md y CSS.
  tracking: "-0.02em"  # TARGET (--tracking-tight), no verificado en el CSS de producción del H1.

header:
  font: "Montserrat Bold (700)"  # AMBOS — coincide con --fw-bold de producción.
  usage: Encabezados de sección, eyebrows, etiquetas de UI. Eyebrows en mayúsculas con tracking 0.28em (TARGET, --tracking-widest, confirmado en tokens/typography.css como "eyebrow / overline caps") — nunca el cuerpo de texto en mayúsculas sostenidas.

body:
  font: "Montserrat Regular (400) / Medium (500, solo TARGET) / Semibold (600)"
  # PROD solo tiene --fw-regular(400) y --fw-semibold(600) — no existe un --fw-medium(500) en
  # producción. El DS sí lo declara (--weight-medium: 500) pero no hay evidencia de que se use
  # en ningún componente de producción. TARGET únicamente hasta que aparezca un caso de uso real.
  usage: Texto corrido, párrafos, controles de formulario.
```

**Pesos — comparación completa:**
```yaml
# PROD (--fw-*):        TARGET (--weight-*, tokens/typography.css):
--fw-regular:  400        --weight-regular:  400   # AMBOS
                           --weight-medium:   500   # TARGET — declarado a propósito, no vestigial.
                                                     # Sin caso de uso en producción todavía. No es
                                                     # una decisión pendiente: se usa el día que un
                                                     # componente lo necesite, no antes.
--fw-semibold: 600        --weight-semibold: 600   # AMBOS
--fw-bold:     700        --weight-bold:     700   # AMBOS
# Ninguno de los dos sistemas tiene un --fw-light/--weight-light (300), a pesar de que
# producción usa ese peso en el elemento más visible del sitio (el H1 hero). Gap real en ambos —
# ver Tipografía arriba, ya resuelto que el valor correcto es 300.
```

**Escala tipográfica completa — `TARGET`, ahora verificada contra `tokens/typography.css`:**
```yaml
--text-2xs: 0.6875rem  # 11px — legal, captions
--text-xs:  0.75rem    # 12px
--text-sm:  0.875rem   # 14px
--text-base: 1rem      # 16px — body default
--text-md:  1.125rem   # 18px — lead
--text-lg:  1.375rem   # 22px
--text-xl:  1.75rem    # 28px
--text-2xl: 2.25rem    # 36px
--text-3xl: 3rem       # 48px
--text-4xl: 4rem       # 64px
--text-5xl: 5.5rem     # 88px — display hero
```
Escala tipo major-third ajustada (~1.250). Ningún paso coincide exactamente con el `3.6rem` (57.6px) que usa el H1 real de producción — el H1 de producción cae entre `--text-4xl` (64px) y `--text-3xl` (48px), no sobre un escalón limpio de esta escala. Otro dato a favor de que el H1 de producción se definió por fuera del sistema, no derivado de él.

**Line-heights y letter-spacing — `TARGET`, sin uso verificado en producción:**
```yaml
--leading-tight:   1.1
--leading-snug:    1.25
--leading-normal:  1.5
--leading-relaxed: 1.7

--tracking-tight:  -0.02em
--tracking-normal:  0
--tracking-wide:    0.04em
--tracking-wider:   0.12em   # wordmark OÑATE SILVA
--tracking-widest:  0.28em   # eyebrow/overline caps
```
El H1 real de producción usa `line-height: 4.5rem` sobre `font-size: 3.6rem` — eso da un ratio de 1.25, que coincide con `--leading-snug`, no con `--leading-tight` (1.1) que el DS asigna a `.os-display`. Otro punto de fricción entre el rol "display" del DS y cómo se implementó realmente el H1 en producción.

**H1 homologado — `PROD`, spec exacta (Home `.hero h1` + Consulting/servicios `.c-hero__title`):**
```css
font-family: 'Comfortaa', sans-serif;
font-size: 3.6rem;
font-weight: 300;
line-height: 4.5rem;
color: var(--color-blanco);
text-transform: uppercase;
```
Excepción Home: incluye un `<span>` animado con typed.js — exclusivo de Home. Consulting usa título estático con fade-in CSS (`pfHeroFadeIn`), sin typed.js.

---

## Espaciado

**RESUELTO — no era un conflicto, era información incompleta de mi parte.** `tokens/spacing.css` mantiene deliberadamente los dos sistemas en paralelo, con el segundo etiquetado en el propio archivo como *"Named aliases (matches production theme)"*:

```yaml
# TARGET — grilla numérica de 4px, para componentes nuevos:
--space-0:  0
--space-1:  0.25rem  # 4px
--space-2:  0.5rem   # 8px
--space-3:  0.75rem  # 12px
--space-4:  1rem     # 16px
--space-5:  1.5rem   # 24px
--space-6:  2rem     # 32px
--space-7:  3rem     # 48px
--space-8:  4rem     # 64px
--space-9:  6rem     # 96px
--space-10: 8rem     # 128px

# AMBOS — alias con nombre, valores IDÉNTICOS byte a byte a lo que ya usa producción:
--space-xs:  0.5rem   # 8px
--space-sm:  1rem     # 16px
--space-md:  1.5rem   # 24px
--space-lg:  2.5rem   # 40px
--space-xl:  4rem     # 64px
--space-2xl: 6rem     # 96px
```

Verificado: los 6 valores con nombre coinciden exactamente entre `tokens/spacing.css` del DS y el `:root` de `main.css` de producción. El DS ya resolvió esto antes de que yo lo marcara como pendiente — mi error fue trabajar con la versión en prosa de `DESIGN.md` (raw de GitHub) en vez de los tokens CSS reales, que evidentemente están más actualizados que el `.md` publicado.

**Contenedores — `TARGET`, sin verificar contra producción:**
```yaml
--container-sm: 640px
--container-md: 880px
--container-lg: 1120px
--container-xl: 1320px
--gutter: var(--space-5)  # 24px
```

Filosofía (`AMBOS`): ante la duda, más espacio — la densidad se lee como estrés para esta audiencia (directivos ocupados evaluando credibilidad).

---

## Forma, elevación y movimiento

### Radios — `TARGET` completo, `PROD` observado, migración de 14px resuelta

```yaml
# TARGET, tokens/radius-shadow.css:
--radius-none:   0
--radius-sm:     4px
--radius-md:     8px    # Controles, inputs.
--radius-lg:     12px   # Tarjetas (rango bajo). RESUELTO EN DESIGN.MD: destino de migración del 14px de producción.
--radius-xl:     18px   # Tarjetas (rango alto).
--radius-2xl:    28px   # Máximo permitido — nunca radios tipo "blob".
--radius-pill:   999px  # Tags y badges.
--radius-circle: 50%    # Confirmado como token real — no es un caso suelto, es parte de la escala.

# PROD (main.css + templates/*.css, sin variable — valores sueltos):
# 2px, 6px, 8px, 10px, 12px, 14px, 50%, 999px repartidos sin patrón declarado.
```

`50%` y `999px` coinciden exactamente con `--radius-circle` y `--radius-pill` — esos dos migran directo sin fricción. **`14px` (el más frecuente en tarjetas de producción: badges, steps, pricing-card, photo) migra a `--radius-lg` (12px)** — resuelto en este documento. La diferencia visual es imperceptible y evita mantener un escalón extra fuera de la escala. `2px` y `6px` tampoco existen en la escala TARGET (el escalón más chico ahí es `--radius-sm`, 4px) — sin caso de uso claro todavía para decidir su migración, quedan sin resolver pero no son bloqueantes (son radios menores, en detalles puntuales, no en componentes repetidos).

### Sombras — `TARGET` completo con valores exactos, comparado contra `PROD`

```yaml
# TARGET, tokens/radius-shadow.css:
--shadow-xs:    0 1px 2px rgba(2,9,10,0.05)
--shadow-sm:    0 1px 3px rgba(2,9,10,0.06), 0 1px 2px rgba(2,9,10,0.04)
--shadow-md:    0 4px 12px rgba(2,9,10,0.07), 0 2px 4px rgba(2,9,10,0.04)
--shadow-lg:    0 12px 28px rgba(2,9,10,0.10), 0 4px 10px rgba(2,9,10,0.05)
--shadow-xl:    0 24px 56px rgba(2,9,10,0.14), 0 8px 18px rgba(2,9,10,0.06)
--shadow-brand: 0 10px 30px rgba(22,129,150,0.22)   # CTAs primarios y momentos hero. NUNCA en tarjetas normales.
--shadow-brand-soft: 0 20px 48px rgba(22,129,150,0.15)  # RESUELTO EN DESIGN.MD — nuevo token.
                     # Hover de tarjetas interactivas (badges, steps, desafío-row, project-cards).
                     # Documenta lo que producción ya hacía en 4+ componentes antes de que existiera
                     # este token — no es una migración, es reconocer el patrón real por escrito.
--shadow-inner: inset 0 1px 2px rgba(2,9,10,0.06)

# PROD, valores reales observados en templates/*.css:
card_rest:      0 1px 3px rgba(2,9,10,0.06), 0 2px 6px rgba(2,9,10,0.03)   # casi --shadow-sm, segunda capa distinta (2px 6px 0.03 vs 1px 2px 0.04)
card_hover:     0 20px 48px rgba(22,129,150,0.15)   # = --shadow-brand-soft, exacto.
pricing_hover:  0 20px 48px rgba(2,9,10,0.18)        # variante sin tinte turquesa
brand_glow_cta: 0 8px 24px rgba(22,129,150,0.3)      # usado en el CTA hero — más cerca de --shadow-brand que de --shadow-brand-soft.
```

**Regla actualizada:** `--shadow-brand` para CTAs primarios y momentos hero. `--shadow-brand-soft` para hover de tarjetas interactivas — nunca al revés (no usar la versión intensa en tarjetas, ni la suave en un CTA).

Sigue habiendo un desajuste menor sin resolver: `brand_glow_cta` (el que usa el CTA real del hero, `0 8px 24px rgba(22,129,150,0.3)`) no coincide exactamente con el `--shadow-brand` del DS (`0 10px 30px rgba(22,129,150,0.22)`) — mismo concepto, valores distintos. Ese es el punto 3 de los pendientes, más chico que el original.

### Movimiento — `TARGET` reconciliado con `PROD`, ya no es conflicto

```yaml
# TARGET, tokens/radius-shadow.css — sistema completo:
--ease-standard: cubic-bezier(0.4, 0, 0.2, 1)
--ease-out:      cubic-bezier(0.16, 1, 0.3, 1)
--ease-in-out:   cubic-bezier(0.65, 0, 0.35, 1)
--duration-fast: 140ms
--duration-base: 220ms
--duration-slow: 360ms

# AMBOS — alias explícito en el mismo archivo, etiquetado "matches production theme":
--transition-base: 0.2s ease-in-out   # 200ms, idéntico al de main.css.
```

Igual que con el espaciado: el DS ya reconcilió esto manteniendo un alias de compatibilidad. No hay conflicto real. Lo que sí sigue siendo cierto: producción usa duraciones sueltas (0.15s, 0.25s, 0.28s, 0.3s) en `home.css`/`services.css`/`portfolio.css` que no pasan por ningún token — ni el `--transition-base` viejo ni el `--duration-*` nuevo. Ninguna de esas coincide con `--duration-fast` (140ms) ni `--duration-slow` (360ms) tampoco — son valores ad hoc por componente, no una tercera escala.

**Hover** (`AMBOS`): primarios oscurecen (`--accent-hover`), secundarios/ghost ganan un fill suave, links pasan a `--accent-hover`. Consistente con lo que hace producción, aunque sin los nombres semánticos.

---

## Breakpoints — `PROD`, nunca declarados como sistema en ningún documento

```yaml
# Observados en main.css + templates/*.css, sin variable, sin escala formal:
575px  # solo home.css
560px  # solo portfolio.css y services.css
767/768px  # main.css usa max-width:767px, CLAUDE.md documenta el quiebre como "768px" — mismo punto, dos formas de expresarlo.
991/992px  # el más usado — header, servicios, portfolio.
```

`560px` y `575px` son casi el mismo punto de quiebre pero con valores distintos entre archivos — no es intencional, es drift. El DS no define breakpoints en absoluto, así que no hay `TARGET` con qué compararlo. Gap real en ambos sistemas.

---

## Z-index — sin sistema en ningún lado

```yaml
# PROD, valores puntuales relacionados entre sí pero no como escala documentada:
1030  # .site-header (mismo valor que .sticky-top de Bootstrap, según comentario del código)
1031  # panel de dropdown de idioma — "por sobre header"
1032  # nivel superior, resuelve un caso de superposición puntual
```
Ni producción ni el DS tienen una escala real. Si se necesita más de un nivel adicional en el futuro, esto se va a romper por falta de rango — dejarlo anotado como deuda, no resolverlo inventando una escala ahora.

---

## Iconografía — `AMBOS`

Lucide para toda la UI — 16–20px en interfaz, 20–24px en marketing, stroke 1.75–2px, `currentColor`. Font Awesome reservado exclusivamente a íconos de marca del footer (LinkedIn, Instagram, Medium) — coincide con lo ya establecido en producción. El isologo de hojas apiladas nunca se reemplaza por un ícono genérico de Lucide. Sin emojis como iconografía, en ningún contexto.

**Nota — `PROD`, tamaños reales observados sin tokenizar:** 38px y 40px para íconos circulares en `.c-step__icon` / `.c-desafio-row__icon`, 56px en `.c-badge__icon`. Estos no encajan limpio en el rango "16–24px" que declara el DS porque son contenedores circulares con ícono adentro, no el ícono mismo — vale la pena aclarar esa distinción en el próximo ajuste del DS para que no se lea como contradicción cuando es, en realidad, dos cosas distintas (tamaño del ícono vs. tamaño del contenedor).

---

## Componentes (lógica de decisión) — 100% `TARGET`

No existen como componentes React en producción; producción resuelve los mismos problemas con BEM + PHP. Documentado tal cual aparece en el DS, sin verificar contra código porque no hay código equivalente que verificar.

**Button** — `primary` (turquesa, resplandor de marca) para la acción principal; `secondary` (blanco, hairline) y `ghost` (solo texto) para acciones de soporte; `danger` para acciones destructivas. Nunca más de un `primary` por grupo de vista — si sientes que necesitas dos, el layout necesita repensarse, no el botón. *Nota: producción no tiene variante Danger implementada (documentado en CLAUDE.md como "sin casos de uso" — consistente con no tener acciones destructivas en el sitio).*

**Card** — `elevated` (blanco + sombra suave) para contenido que compite por atención; `outline` (hairline, plano) cuando hay muchas tarjetas juntas y el contraste visual pesado cansaría; `soft` (tinte turquesa, sin borde) para destacar sin la formalidad de una sombra. `interactive` agrega lift en hover solo si la tarjeta completa es clickeable. Nunca borde lateral de color.

**Badge vs. Tag** — la diferencia es intención, no apariencia. **Badge** es de solo lectura (un estado, un conteo), nunca clickeable. **Tag** es para selección controlada por el usuario (filtros, multi-select), interactivo, puede tener `onRemove` o estado `selected`. Si el usuario puede tocarlo para cambiar algo, es Tag. Si solo informa, es Badge.

**Avatar** — foto o iniciales de respaldo sobre disco con tinte suave cuando no hay `src`. `status` agrega punto de presencia. Nunca usar para representar algo que no sea una persona.

**Input** — `label` siempre visible, nunca placeholder-only como label. `error` tiñe el borde de rojo y reemplaza el hint por el mensaje — no coexisten error y hint. El foco siempre muestra el anillo turquesa (`--ring`), nunca el azul de sistema operativo por defecto.

**Switch** — controlado únicamente (`checked` + `onChange`), nunca no-controlado. Track turquesa cuando está activo, gris cuando no.

**Tabs** — barra con subrayado turquesa en la pestaña activa y etiqueta en tinta fuerte. Controlado vía `value`/`onChange`; el panel de contenido se renderiza aparte, el componente no lo incluye.

**Alert** — banner de superficie tintada suave con borde hairline a juego. Mensajes cortos y tranquilizadores — no es el lugar para explicaciones largas ni tono de urgencia salvo `danger`.

---

## Nunca hacer

```
- No gradientes decorativos fuera del único sancionado: turquesa → menta.
- No colores de estado (success/warning/danger/info) de forma decorativa — reservados a significado real.
- warning nunca como texto de cuerpo directo sobre superficie blanca — falla 4.5:1 incluso con el valor corregido.
- No más de un botón `primary` por grupo de vista.
- No sombra + borde grueso a la vez en tarjetas. Uno u otro, nunca ambos con peso visual alto.
- `--shadow-brand` (intenso) solo en CTAs primarios y momentos hero. `--shadow-brand-soft` (suave) solo en hover de tarjetas interactivas. Nunca al revés.
- No radios grandes tipo blob — geometría de marca angulosa, radios modestos (máx. --radius-2xl, 28px TARGET).
- No mayúsculas sostenidas en cuerpo de texto — reservadas a wordmark y eyebrows.
- No signos de exclamación salvo casos excepcionales.
- No emojis como iconografía ni en copy, en ningún contexto.
- No reemplazar el isologo por un ícono genérico de Lucide.
- No asumir que producción (WordPress) implementa los componentes React o los tokens semánticos de este archivo.
- No usar Font Awesome fuera de los íconos de marca del footer.
- No introducir nombres --surface-*/--accent en templates PHP del tema — esa capa es exclusiva de prototipos.
- No inventar valores de radio, sombra, espaciado o tipografía intermedios que este documento marca como TARGET sin
  verificar — pedir el zip fuente del DS antes de construir algo que dependa de ellos.
```

---

## Estado del documento

Sin pendientes abiertos que requieran otra decisión de diseño. Historial de lo resuelto en esta consolidación (7 ago 2026):

1. **Espaciado y movimiento** — no eran conflictos; el DS ya reconciliaba ambos sistemas con alias de compatibilidad, solo faltaba leer `tokens/*.css` en vez de la versión en prosa del `DESIGN.md` viejo.
2. **Peso del H1 hero** — 300, confirmado por Felipe vía comparación visual directa. Corrige la declaración de 600 en el export de Claude Design.
3. **`warning`** — `#B47318`, con la razón de contraste documentada inline. Corrige `#C98A2B`, todavía presente en el export de Claude Design.
4. **`--shadow-brand` fuera de su regla** — resuelto agregando `--shadow-brand-soft` para hover de tarjetas, dejando `--shadow-brand` exclusivo para CTAs/hero.
5. **Radio 14px** — migra a `--radius-lg` (12px).
6. **`--weight-medium: 500`** — confirmado como TARGET válido, simplemente sin caso de uso todavía. No vestigial, no urgente.

Quedan dos notas menores sin decisión formal, ninguna bloqueante: los radios `2px`/`6px` de producción sin escalón TARGET equivalente (casos puntuales, no un componente repetido), y el desajuste de `brand_glow_cta` del CTA hero (`0 8px 24px rgba(22,129,150,0.3)`) contra los nuevos `--shadow-brand`/`--shadow-brand-soft` — se limpia cuando se toque ese componente, no antes.

Acción mecánica pendiente, fuera de este documento: aplicar estos seis cambios en el proyecto de Claude Design y reexportar, para que el próximo `tokens/*.css` deje de estar desalineado con este archivo. No bloquea nada — este documento manda mientras tanto.

---

*Consolidado el 7 de agosto de 2026. Fuente de verdad (SOT) de este proyecto — reemplaza al `DESIGN.md` anterior del repo `onate-silva-ds`. Jerarquía: este archivo → producción (`felipeonate2026`) → exports de Claude Design (insumo, no autoridad). Fuente de cada valor marcada inline (`PROD` / `TARGET` / `AMBOS` / `RESUELTO EN DESIGN.MD`).*
