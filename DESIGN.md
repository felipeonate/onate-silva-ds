# DESIGN.md — Oñate Silva Design System

*Marca personal de Felipe Oñate Silva, consultor estratégico en UX y diseño de productos digitales (15+ años). Este archivo es la fuente de verdad del lenguaje visual — para agentes de IA (Claude Code, Cursor, Lovable, Stitch) que generan o editan interfaces on-brand.*

---

## Estado de implementación (leer antes que cualquier token)

Este sistema define el **objetivo de marca**, no el estado actual del sitio en producción.

- **Producción hoy** (`felipeonate.com`, tema WordPress `felipeonate-1`): PHP + CSS con convención BEM (`.c-desafio-row`, `.c-pricing-card`, `.c-outcomes__inner`) y tokens con prefijo `--color-*` (`--color-turquesa-500`, etc.). No usa componentes React ni las variables semánticas de este archivo (`--surface-*`, `--accent`, `--text-body`).
- **Este DS**: recreación on-brand construida en Claude Design, con componentes React (`Button`, `Card`, `Badge`, `Tag`, etc.) y capa semántica de tokens. Es el objetivo de migración, no lo que corre hoy.
- **Regla para Claude Code**: si estás editando templates PHP del tema WordPress, sigue las convenciones de `CLAUDE.md` (BEM, prefijo `pf_`, `--color-*`) hasta que exista una migración explícita. Si estás construyendo un prototipo nuevo, un mockup, o trabajando en Claude Design/Lovable/Stitch, usa este archivo como fuente.
- Los valores base de color (turquesa/menta/gris 50→900) **son idénticos** entre ambos sistemas — solo cambia el prefijo del nombre de variable y la capa semántica. La migración de tokens de color es de bajo riesgo; la migración de componentes (BEM → React) no lo es.

---

## Brief de producto

Sitio de marca personal y vehículo principal de captación de clientes para Felipe Oñate Silva. Audiencias: dueños de startups, directivos C-Level, líderes de producto/diseño, y profesionales en transición. La interfaz debe transmitir criterio estratégico y autoridad técnica sin caer en ornamento — cada elemento visual debe poder justificarse con la misma lógica que la marca aplica al diseño: evidencia antes que estética.

## Principios de diseño

- **Contraste calmado, no decorativo.** El turquesa y la menta se usan en dosis pequeñas y deliberadas — nunca como relleno.
- **Los radios son modestos.** La marca gráfica es angulosa; nada de esquinas sobre-redondeadas ni "blobs".
- **La elevación se sugiere, no se dramatiza.** Sombras suaves, tintadas en frío, bajo contraste.
- **Un CTA primario por vista.** La autoridad viene del argumento, no del volumen de botones ni de signos de exclamación.
- **El espacio en blanco es un activo de marca**, no espacio desperdiciado — ritmo vertical generoso.

---

## Tokens de color

Escala base (idéntica en ambos sistemas, solo cambia el prefijo):

```yaml
turquesa-500: "#168196"
# Primario de marca. Acciones principales, links, la marca gráfica, acentos clave.
# Nunca como fondo de página completo. Escala 50→900 disponible para tintes/textos.

menta-500: "#68B6A4"
# Secundario — más suave, de soporte. Acentos secundarios, rellenos suaves, estados de éxito.
# Único gradiente permitido: turquesa → menta (horizontal o diagonal). Sin otros gradientes decorativos.

gris-500: "#676B6C"
# Columna neutral. gris-700 (#353A3B) es la tinta del wordmark — úsalo para texto de máxima fuerza en contexto de marca.

negro: "#02090A"
# Tinta pura. Solo para el texto más fuerte y superficies inversas. No usar como texto de cuerpo por defecto.

blanco: "#FAFAFA"
# Superficie de página por defecto. Las tarjetas suben a blanco puro (#FFFFFF).
```

Capa semántica (esta es la que Claude Code debería preferir sobre los valores crudos al escribir componentes nuevos):

```yaml
--text-strong: var(--negro)      # Titulares, texto de máximo peso.
--text-body: var(--gris-700)     # Cuerpo de texto por defecto.
--text-muted: var(--gris-500)    # Texto secundario, leads.
--text-brand: var(--turquesa-600) # Eyebrows, texto que necesita asociarse a marca.

--surface-page: var(--blanco)
--surface-card: var(--pure-white) # #FFFFFF — las tarjetas siempre suben a blanco puro sobre fondo --blanco.
--surface-brand-soft: var(--turquesa-50) # Tintes de fondo suaves (chips seleccionados, alerts info/brand).

--accent: var(--turquesa-500)
--accent-hover: var(--turquesa-600)   # Los botones primarios oscurecen en hover, nunca cambian de familia de color.
--accent-active: var(--turquesa-700)

--border-subtle: var(--gris-100)  # Hairlines de tarjetas.
--border-focus: var(--turquesa-400)

--ring: 0 0 0 3px color-mix(in srgb, var(--turquesa-500) 28%, transparent)
# Anillo de foco — siempre turquesa, nunca azul de sistema operativo por defecto.
```

Estados (desaturados a propósito — nunca rojo/verde web puro):

```yaml
success: "#2E8E6A"
warning: "#C98A2B"
danger:  "#C0473C"
info:    "#1A38B2"
# Cada uno tiene versión -soft para fondos de Alert/Badge. Reservados exclusivamente para
# significado semántico real (estado de un proceso, validación de formulario). Nunca decorativos.
```

---

## Tipografía

```yaml
display:
  font: "Comfortaa SemiBold (600)"
  usage: Titulares hero y declaraciones de alto impacto. Tracking negativo (-0.02em). Nunca dentro de componentes o tarjetas — solo a nivel de sección/página.

header:
  font: "Montserrat Bold (700)"
  usage: Encabezados de sección, eyebrows, etiquetas de UI. Los eyebrows van en mayúsculas con tracking amplio (0.28em) — nunca el cuerpo de texto en mayúsculas sostenidas.

body:
  font: "Montserrat Regular (400) / Medium (500)"
  usage: Texto corrido, párrafos, controles de formulario.
```

Escala: `11px → 88px` (`--text-2xs` a `--text-5xl`), ver `tokens/typography.css`. En superficies de marketing, usar los tamaños grandes de display; en UI/componentes, mantener `base`/`sm`.

Ambas familias cargan desde Google Fonts (`tokens/fonts.css`). Si se necesita self-hosting, pedir los pesos licenciados antes de agregar `@font-face`.

---

## Espaciado

Grilla base de 8px, paso de 4px para UI densa (`--space-1` a `--space-10`). Anchos de contenedor de 640px a 1320px; el contenido de marketing centra en `--container-lg` (1120px). Cuando haya duda entre más o menos espacio, elegir más — la densidad se lee como estrés para esta audiencia (directivos ocupados, profesionales evaluando credibilidad).

---

## Forma, elevación y movimiento

- **Radios:** controles/inputs `--radius-md` (8px); tarjetas `--radius-lg`/`--radius-xl` (12–18px); tags y badges `--radius-pill`. Nunca radios grandes tipo "blob" — la marca gráfica es angulosa.
- **Tarjetas:** blanco puro, `--radius-lg`, hairline `--border-subtle` **o** `--shadow-sm`/`--shadow-md` — nunca ambos a la vez, nunca borde lateral de color.
- **`--shadow-brand`** (resplandor turquesa) reservado para CTAs primarios y momentos hero — no usar en tarjetas normales.
- **Movimiento:** `--duration-base` 220ms, `--ease-out` en casi todo. Fades/rises de 4–8px al entrar. Sin bounce, sin spin, sin parallax.
- **Hover:** primarios oscurecen (`--accent-hover`); secundarios/ghost ganan un fill suave; links pasan a `--accent-hover`.

---

## Iconografía

**Lucide** (SVG, open-source) para toda la UI — 16–20px en interfaz, 20–24px en marketing, stroke 1.75–2px, `currentColor`. **Font Awesome se reserva exclusivamente para íconos de marca en el footer** (LinkedIn, Instagram, Medium) — coincide con lo ya establecido en producción. El isologo de hojas apiladas nunca se reemplaza por un ícono genérico de Lucide. Sin emojis como iconografía, en ningún contexto.

---

## Componentes (lógica de decisión)

**Button** — `primary` (turquesa, resplandor de marca) para la acción principal; `secondary` (blanco, hairline) y `ghost` (solo texto) para acciones de soporte; `danger` para acciones destructivas. Nunca más de un `primary` por grupo de vista — si sientes que necesitas dos, el layout necesita repensarse, no el botón.

**Card** — `elevated` (blanco + sombra suave) para contenido que compite por atención; `outline` (hairline, plano) cuando hay muchas tarjetas juntas y el contraste visual pesado cansaría; `soft` (tinte turquesa, sin borde) para destacar sin la formalidad de una sombra. `interactive` agrega lift en hover solo si la tarjeta completa es clickeable. Nunca borde lateral de color — ese patrón no existe en este sistema.

**Badge vs. Tag** — son fáciles de confundir, la diferencia es intención: **Badge** es de solo lectura (un estado, un conteo — "Activo", "Nuevo"), nunca clickeable. **Tag** es para selección controlada por el usuario (filtros, multi-select) — más alto, interactivo, puede tener `onRemove` o estado `selected`. Si el usuario puede tocarlo para cambiar algo, es Tag. Si solo informa, es Badge.

**Avatar** — foto o iniciales de respaldo sobre disco con tinte suave cuando no hay `src`. `status` agrega punto de presencia. Nunca usar para representar algo que no sea una persona.

**Input** — campo con `label` siempre visible (nunca placeholder-only como label). `error` tiñe el borde de rojo y reemplaza el hint por el mensaje — no coexisten error y hint. El foco siempre muestra el anillo turquesa (`--ring`), nunca el azul de sistema operativo por defecto.

**Switch** — controlado únicamente (requiere `checked` + `onChange`), nunca no-controlado. Track turquesa cuando está activo, gris cuando no.

**Tabs** — barra con subrayado turquesa en la pestaña activa y etiqueta en tinta fuerte. Controlado vía `value`/`onChange`; el panel de contenido se renderiza aparte, el componente no lo incluye.

**Alert** — banner de superficie tintada suave con borde hairline a juego. Mensajes cortos y tranquilizadores — este no es el lugar para explicaciones largas ni para tono de urgencia salvo que la tonalidad sea `danger`.

---

## Nunca hacer

```
- No gradientes decorativos fuera del único sancionado: turquesa → menta.
- No colores de estado (success/warning/danger/info) de forma decorativa — están reservados a significado real.
- No más de un botón `primary` por grupo de vista.
- No sombra + borde grueso a la vez en tarjetas. Uno u otro, nunca ambos con peso visual alto.
- No radios grandes tipo blob — la geometría de marca es angulosa, los radios son modestos (máx. --radius-2xl, 28px).
- No mayúsculas sostenidas en cuerpo de texto — reservadas a wordmark y eyebrows.
- No signos de exclamación salvo casos excepcionales — la autoridad viene del argumento.
- No emojis como iconografía ni en copy, en ningún contexto.
- No reemplazar el isologo por un ícono genérico de Lucide.
- No asumir que producción (WordPress) ya implementa estos componentes React o tokens semánticos — ver "Estado de implementación" arriba.
- No usar Font Awesome fuera de los íconos de marca del footer.
```

---

*Fuente: extraído directamente de `tokens/*.css`, `readme.md` y `components/**/*.prompt.md` del Design System construido en Claude Design (`On_ate_Silva_Design_System.zip`). Última actualización: 22 jul 2026.*
