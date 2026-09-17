---
name: m3-foundations
description: 'Material Design 3 (M3) design foundations distilled into stack-agnostic rules. Use when designing or reviewing color/tonal palettes, typography, shape, elevation, dark mode, iconography, motion, state layers, layout/density, writing, accessibility, or design tokens in any UI — independent of programming language or framework. Enforces Material 3 craft standards without referencing any specific technology.'
---

# M3 Foundations

Material Design 3 design foundations, made technology-agnostic. These are the rules that govern the *feel* of a Material-quality interface regardless of the stack you build with.

## When to use

Load this skill when you are:
- Building or reviewing **color**: the 5-role tonal system, containers, dynamic color / Material You
- Setting **typography**: type scale, hierarchy, legibility, text scaling
- Defining **shape**: corner scale, shape tokens
- Working with **elevation** and **surfaces**: elevation levels, tonal elevation, scrim
- Implementing or reviewing **dark mode** / dynamic appearance
- Using **icons / symbols**
- Adding **motion** and state change feedback
- Styling **state layers** (hover, focus, pressed, dragged, disabled)
- Doing **layout** and **density**: 8dp grid, breakpoints, touch targets
- Writing interface **copy**
- **Accessibility**: contrast, text scale, state announcements, focus
- Working with **design tokens**: roles → values → themes

## The guiding principles

Every rule below traces back to Material 3's core design themes:

1. **Seed-centric color.** A single seed color generates the whole tonal system (dynamic color). The palette is *computed*, not hand-picked per screen.
2. **Roles over colors.** The eye understands hierarchy because color *roles* (primary, secondary, tertiary, error, surface) are consistently applied — never because hues are pretty.
3. **Adaptive every where.** Material runs on every screen size and input type; layout and density are authored per breakpoint, not stretched.
4. **Fulfill, don't decorate.** Motion, shape, and elevation exist to explain spatial relationships and state — decoration that adds no meaning is noise.
5. **Accessibility is baseline.** Contrast, touch targets, text scale, and state announcements are part of the system, not an add-on.

Any decision you make that contradicts these must be a *conscious brand choice*, not an accident.

---

## Color (tonal palette system)

### Rules
- **Five core roles minimum**: `primary` (brand, most prominent — interactive components, selected states, FAB, primary button fill), `secondary` (medium emphasis), `tertiary` (contrasting, expressive accents), `error` (error states), `surface`/`background` (the page). Every color in the UI should come from a role, not ad-hoc hex.
- **Each role has a tonal palette**: a set of tones from 0–100 (e.g. primary ranges from dark to light. The vowel naming is per-tone: tone N = a specific luminance step). `on-<role>` colors (text/icons placed on a role) come from the same palette's opposite end so contrast is guaranteed.
- **Container variant**: most roles also have a `<role>-container` / `on-<role>-container` used for emphasis swaths (primary-container for selected-list backgrounds, tertiary-container for featured/delight surfaces).
- **Dynamic color (Material You)**: when the target platform supports it (Android 12+), the tonal system is generated from the user's wallpaper via a seed. When not, generate from your brand seed — but keep the *mechanics*: seed → 5 roles → tonal palettes → on/container variants.
- **The baseline Material scheme** is defined by the Material color role diagram; switch between light/dark by swapping tonal palette mappings, not by inventing new roles.
- **Contrast is non-negotiable**: body text ≥ 4.5:1, large text ≥ 3:1, UI components and icons ≥ 3:1 against adjacent colors.
- Never convey meaning by color alone — pair with text label, icon, or shape (e.g. error = color + icon + text).
- Respect appearance adaptation: light and dark variants come from the same role system, both authored.

### The why
Color in M3 is not decoration; it is a calibrated signal system. When every hue maps to a role and a contrast-verified tone, screens stay harmonious, adaptive, and accessible *without art direction per screen*.

### Implementation hints
- Detect: theme definitions, `ColorScheme`, `colorScheme`, `seedColor`, `dynamicColor`, `MaterialTheme`, `--md-sys`, color role tokens, `fromSeed`.
- Check: any color literal not mapped to a role (hardcoded hex in a widget) → flag.
- Check: dynamic color supported? Ideally the scheme derives from a seed; a fully hand-picked palette may be a deliberate brand choice — note it.
- Check: `on-<role>` pairs meet contrast; container colors exist for roles used as emphasis.

---

## Typography

### Rules
- Use the **M3 type scale**: five type groups — `display` (40/44), `headline` (32–24), `title` (22–16), `body` (16–14), `label` (14–11) — each in large/medium/small. You don't need all 15, but sizes must map to the scale, not be invented.
- **Body is the workhorse**: default body ~14–16sp, comfortably legible; never default body below ~12sp equivalent.
- Hierarchy via size + weight from the scale; resist a size for every occasion.
- Text must scale: it must remain legible (and uncropped) when the user enlarges it (up to 200% on Android) and when containers change width.
- Sentence case is Material's default; avoid all-caps body text.
- Numerals in tables and data: align with tabular figures.
- Line height should not clip ascenders/descenders, especially with custom fonts or scale increases.

### The why
Material's type scale is the contract between designers and engineers. A disciplined ramp communicates hierarchy instantly; a chaotic set of sizes communicates chaos — and breaks the scalability promise.

### Implementation hints
- Detect: font-size literals, `fontSize`, `TextStyle`, `textTheme`, `--md-sys-typescale`, `className="text-`.
- Check: count distinct font sizes on the surface. Every size should map to a named scale step; > ~8 unmapped sizes → flag.
- Check: body below 12sp or non-scale-capped body text → flag.

---

## Shape

### Rules
- Use the **M3 shape scale**: `none` (0), `extra-small` (4), `small` (8), `medium` (12), `large` (16), `extra-large` (28), `full`. Each shape *role* maps to a component level (e.g. card = medium, FAB = extra-large, toolbar = 0/small).
- Shapes communicate *information about the component*, not arbitrary styling: larger radius = more elevated/expressive; sharp corners = denser, more utilitarian.
- Components in the same category share the same corner treatment. Don't round draggable/fixed components inconsistently.
- A **fractional radius** breaks the grid — corners belong to the scale.

### The why
In M3, shape is a semantic dimension (with color and elevation): familiar corner treatments make the eye read the hierarchy room- by room.

### Implementation hints
- Detect: border radius values, `borderRadius`, `RoundedRectangleBorder`, `shape`, `--md-sys-shape`, `.rounded-`.
- Check: radius values not on the M3 scale → flag with nearest scale step.
- Check: same category of components using mixed radii → flag.

---

## Elevation & Surfaces

### Rules
- **Elevation in M3 is two-dimensional**: a *showcasing* elevation via shadow/surface tint, and a tonal elevation via tinted surface layers. Use elevation **levels** (e.g. 0–5) consistently: cards, FABs, dialogs, side sheets get sensible default levels.
- **A surface's elevation is communicative** — the FAB floats above the page, dialogs above the scrim, nav drawers above content. Two surfaces that should feel equal must not float at different heights.
- **Scrim**: when a modal (dialog, bottom sheet, nav drawer) is on screen, dim the background with a scrim (typically a semi-transparent ink/surface tone) so the modal's elevation reads.
- **Nested elevation** must not cascade: a dialog on a card on a page is rare; layers above a scrim should have a controlled, consistent elevation, not escalation by stacking.
- Avoid drop shadows as the *primary* depth signal on small elements — in M3, surface tint + elevation level do the work; heavy shadows read as stale Android v1.

### The why
Elevation is how Material makes physical depth legible: what floats, what is fixed, what takes the stage. Done consistently, users never wonder what's tappable or dismissible.

### Implementation hints
- Detect: elevation values, `elevation`, `BoxShadow`, `shadow`, `Scrim`, `scrimColor`, `MaterialStateProperty`.
- Check: elevation values outside a small set of levels → flag.
- Check: modal surfaces without a scrim → flag.

---

## Dark Mode

### Rules
- Dark is **not** colors inverted: it is the same role system mapped to darker tonal palettes, with surfaces that read as layered in depth rather than flat black.
- Use moderate-dark surfaces (not pure `#000`); raised surfaces get lighter/tinted so depth survives darkness.
- With dynamic color, dark mode is generated from the *same seed* with a dark tonal palette mapping.
- Text/icon contrast must be re-verified in dark — mid-grays that pass on light often fail on dark.
- Never hardcode light appearance only; every theme must have a dark counterpart.

### The why
Dark mode is a top Material and OS expectation. An interface that breaks in darkness breaks for a large share of users — and the role system makes the dark theme nearly free if built right.

### Implementation hints
- Detect: dark theme definitions, `darkColorScheme`, `darkTheme`, `ThemeData.dark`, `prefers-color-scheme`, `.dark`, `onPrimary`.
- Check: is there a dark token set at all? Light-only hexes → flag.
- Check: dark surfaces near-black `#000` with no depth layering → flag.

---

## Icons & Symbols

### Rules
- Use an **icon system, consistently**: Material Symbols / Material Icons family preferred. One family, one stroke weight per surface.
- **Stateful icons** express state (filled vs outlined selected/unselected, e.g. navigation bar, checkbox-like controls).
- Icons must be **instantly recognizable** at small sizes; prefer familiar glyphs over novel metaphors.
- Administrative/destructive actions carry unambiguous meaning.
- Pair icons with text labels where meaning could be ambiguous (nav destinations, buttons).
- Never mix icon families (Material + FontAwesome + custom) on the same surface — inconsistent stroke weight and silhouette breaks coherence.

### The why
Icons are read by silhouette before meaning. A single, consistent system keeps the eye fluent; mixing families forces users to re-decode every glyph.

### Implementation hints
- Detect: `Icons.`, `IconData`, `Icon(`, `<Icon`, material-symbols, `Image.asset` icon names, FontAwesome keys.
- Check: multiple icon families co-located → flag.
- Check: an icon used alone where meaning is ambiguous → flag, suggest label.

---

## Motion

### Rules
- M3 has a motion **theme**: easing curves (`standard`, `emphasized`, `accelerated`, `decelerated`) + volumetric durations (~150ms short, ~250–300ms medium, ~400ms large). Use the system, not ad-hoc values.
- Motion must be **purposive**: it explains where things come from and go (contained, overlapping, and shared-axis transitions). Decoration-only motion is noise.
- Respect **reduced motion**: content can appear without animation; never rely on motion to convey essential state.
- **Interruption**: if the user interrupts an animation (scroll, tap), respond — cancel or settle quickly.
- Consistent timing language across the app.

### The why
Material's motion is a spatial story: it preserves the user's mental model of relationships between screens and elements. Fought or ignored, it breaks orientation.

### Implementation hints
- Detect: animation durations, `Duration(milliseconds:`, `Curves.`, `easeOut`, `AnimatedContainer`, `transition`, `TweenAnimationBuilder`, CSS `transition`.
- Check: durations off the M3 system (>500ms for simple state changes) → flag.
- Check: essential state *only* through a transient animation → flag.

---

## State Layers

### Rules
- **Every interactive element has state layers** — hover, focus, pressed, dragged, disabled — applied as a *tonal overlay* on the element's base color, not as separate recolored fills.
- A **state layer** is a semi-transparent surface/primary-role overlay: hover ~8%, focus ~12%, pressed ~16% (darker target) over the control's color.
- State layers must not change layout or move pixels — the element *fills*, it doesn't jump.
- Disabled state: reduce opacity/use disabled colors; ensure the call-to-action still reads but clearly inactive.
- The layer's visibility transitions smoothly (100–150ms) for a responsive feel.

### The why
State layers are how Material keeps interaction feedback free of layout jitter. Instant, subtle, non-disruptive feedback is the difference between "feels like software" and "feels alive".

### Implementation hints
- Detect: `stateLayer`, `overlayColor`, `hoverColor`, `InkWell`, `MaterialStateProperty`, `pressed`, `ripple`, CSS `:hover`/`:focus`/`:active`.
- Check: interactive elements with no visible pressed state → flag.
- Check: states implemented by swapping colors between event handlers → flag, prefer overlay.

---

## Layout, Breakpoints & Density

### Rules
- Build on a **8pt (8dp) grid**: increments of 8 for margins, padding, spacing (4 acceptable for dense/tight, base must be 8).
- Material defines **breakpoints**: an app responds to screen width — typical M3 breakpoints: compact (<600dp), medium (600–840dp), expanded (>840dp). Layout, navigation, and density change *at* these breakpoints, not fluidly pixel-by-pixel.
- **Navigation adapts**: bottom navigation bar ↔ navigation rail ↔ navigation drawer based on width.
- Content should reflow, not overflow: flexible widths, safe areas respected.
- Consistent edge margins per breakpoint (e.g. 16dp compact, larger on tablet).
- Keep interactive targets a minimum comfortable size — M3 targets are ≥ 48dp (touch), despite density options.

### The why
Material's promise is *adaptive*: the same experience on a watch, phone, tablet, and desktop. Breakpoints + spacing system is the machinery that delivers it without duplicated designs.

### Implementation hints
- Detect: spacing literals, `MediaQuery`, `Breakpoint`, `breakpoint`, `maxWidth`, `size.width`, `SizedBox`, `EdgeInsets`, `gap`, Tailwind `-p-`/`-m-`.
- Check: padding/margin not on the 8dp rhythm (except 4) → flag with nearest 8 multiple.
- Check: no breakpoint handling for a responsive target → flag.
- Check: touch targets < 48dp without platform excuse → flag.

---

## Accessibility

### Rules
- **Text scaling** is non-negotiable: all text legible and non-clipped up to large accessibility sizes (Android: user font scale up to 200%).
- **Contrast** per Color rules.
- **Screen-reader support**: every meaningful element has a readable name; decorative elements hidden; interactive elements announce state (button, checked, expanded, etc.).
- **Reduced motion** respected (see Motion).
- **Touch target** minimums respected (see Layout): ≥ 48dp.
- Never rely on a single sensory channel (vision, gesture only, color only).
- Keyboard/focus navigation reaches every interactive element with visible focus.

### The why
Accessibility is the definition of quality in M3 — the system is designed *around* scaling, contrast, and state semantics, not as a bolt-on.

### Implementation hints
- Detect: `semantics`, `Semantics`, `aria-`, `accessibilityLabel`, `role=`, `alt=`, `focusNode`, `tooltip`.
- Check: image/icon-only controls with no name → flag.
- Check: color-only error/selection indication → flag.

---

## Writing

### Rules
- Write in **plain, direct language**. Short sentences, active voice.
- Use **sentence case** for labels (Material default); avoid marketing-speak inside the interface.
- Error messages state what happened and how to fix it, not a technical code.
- Control labels are action-oriented and specific: "Save", "Add", "Cancel" — never a bare "OK" for a consequential action.
- Keep copy concise: one clear message.

### The why
Copy is the interface's guide. Material's clarity principles apply to words as fiercely as to pixels.

### Implementation hints
- Detect: string literals rendered to user, `Text('`, `label:`, `<title`, button text.
- Check: error strings with enum names, stack traces, "Error 0x…" → flag.
- Check: long label essays on buttons → flag.

---

## Design tokens

### Rules
- **Color, type, shape, elevation, and motion are tokens** (roles → values per theme). No component owns a literal color/radius/duration.
- Define **light and dark token sets** from the same roles; themes reference tokens, never hexes.
- Tokens are how dynamic color, dark mode, and per-brand theming all stay consistent — a single source of truth.

### The why
Tokens are the operating system of Material theming: change the seed, every screen follows. Hardcoded literals are the classic drift the audit exists to catch.

### Implementation hints
- Detect: theme object, `ThemeData`, `colorScheme`, `--token`, `Theme.of(context)`, CSS variables.
- Check: color/radius/font-size literals living outside the theme → flag.

---

## Aggregated review checklist

When auditing a surface, run these in order:
1. Color: roles + containers + on-roles, dynamic-color or seed, contrast, no color-only meaning
2. Typography: scale-mapped sizes, legible body, scale-safe
3. Shape: radius on the M3 scale, consistent by category
4. Elevation: level system + scrim on modals
5. Dark mode: dark palette exists, layered not flat black, dynamic-color aware
6. Icons: one family, stateful where needed, labels where ambiguous
7. Motion: tokenized curves/durations, pur-positive, reduced-motion, interruptible
8. State layers: overlay feedback, no layout jump
9. Layout: 8dp grid, breakpoints, density options, ≥48dp targets
10. Accessibility: text scale + SR names + focus + no single channel
11. Writing: plain + action labels + human errors
12. Tokens: no literal styling outside the theme

## Working with other skills

- **Highest-value order**: run foundations first on any screen — foundations violations poison components.
- `m3-components` assumes foundations are respected; shop rule cards by component when implementing or reviewing specific elements.
- `m3-audit` aggregates foundations checks with component and pattern checks into one deviation list.
- `m3-orchestrator` triggers foundations automatically when it detects layout, styling, or theme code.