---
name: hig-foundations
description: 'Apple HIG design foundations distilled into stack-agnostic rules. Use when designing or reviewing color, typography, layout, spacing, dark mode, icons, materials, motion, privacy, writing, or accessibility in any UI — independent of programming language or framework. Enforces Apple''s craft standards without referencing any specific technology.'
---

# HIG Foundations

Apple's design foundations, made technology-agnostic. These are the rules that govern the *feel* of an Apple-quality interface regardless of the stack you build with.

## When to use

Load this skill when you are:
- Choosing or reviewing colors, gradients, or emphasis
- Setting type, type scale, or text legibility
- Laying out content, spacing, or page structure
- Implementing dark mode or dynamic appearance
- Using icons, symbols, or imagery
- Designing surfaces, blur, transparency, or elevation
- Adding motion, transitions, or feedback animation
- Writing copy or interface text
- Handling privacy-relevant UI
- Designing for accessibility (Dynamic Type, contrast, screen readers, reduced motion)

## The guiding principles

Every rule below traces back to these three Apple design principles:

1. **Clarity** — Every element on screen has a purpose. Text is legible, icons are precise, decorations are removed when they stop adding meaning.
2. **Deference** — The content is the hero. Chrome — chrome bars, heavy borders, decorative chrome — recedes so people focus on the task, not the UI furniture.
3. **Depth** — Meaning is communicated through layering, motion, and light, not only through color. Dismissing and revealing are a performance, not a state change.

Any decision you make that contradicts these must be a *conscious brand choice*, not an accident.

---

## Color

### Rules
- Use a small, disciplined accent color set. One primary accent for interactive emphasis, a neutral set for everything else. More than 3–4 accent hues reads as noise.
- Accent color is reserved for meaningful states: active selection, primary action, focused element. Appling accent to everything is anti-deference.
- Ensure contrast meets accessibility: body text at 4.5:1, large text at 3:1, UI components and icons at 3:1 against adjacent colors.
- Never convey meaning by color alone. Pair color with text labels, icons, or position.
- Respect appearance adaptation: colors must work in light and dark contexts (see Dark Mode).

### The why
Apple keeps color purposeful so the eye knows where to look. Color as decoration reduces clarity; color as signal focuses attention.

### Implementation hints
- Detect: references to palette files, theme/color token definitions, hardcoded hex values in style objects, `Color(`, `Color.fromARGB`, `--color-`, `accentColor`, `primary`.
- Check: count distinct accent hues in the palette. Flag anything beyond a disciplined set.
- Check: look for accent applied to non-interactive decorative elements.

---

## Typography

### Rules
- Use a **hierarchical, limited type scale**: a large display/large-title size, a title size, body size, and a small caption size are enough for most interfaces. Resist a size for every occasion.
- Maintain a consistent type ramp between steps (commonly ~1.2× between levels).
- Body text must be comfortably legible at its natural reading distance: never default body below ~15–16px equivalent.
- Use weight and size for hierarchy; prefer fewer steps of weight over more sizes.
- Text must reflow and scale: it must remain legible when the user enlarges it (Dynamic Type) and when the container changes width.
- Avoid all-caps body text; it sacrifices legibility. Sentence case is Apple's default.
- Numerals in tables and data align better with tabular figures.
- Line height should not clip ascenders/descenders, especially with custom fonts or scale increases.

### The why
People read interfaces more than they look at them. A disciplined ramp communicates hierarchy instantly; a chaotic set of sizes communicates chaos.

### Implementation hints
- Detect: font-size literals, `fontSize`, `textStyle`, `Typographie`, `fontSize:`, `className="text-`, `TextStyle(fontSize`, `TextStyle`.
- Check: count distinct font sizes used across the surface. More than ~7 on one screen = broken hierarchy. Every size should map to a named ramp level.
- Check: body text below 15px (or non-scale-capped) → flag.

---

## Layout & Spacing

### Rules
- Build on an **8-point grid**: use increments of 8 for margins, padding, and spacing (4 for dense/tight spacing within a component is acceptable where the base is 8).
- Maintain consistent **screen edge margins** (~16pt equivalent on the sides of phone content).
- Group related content closer; separate unrelated groups with more space. Spacing *is* hierarchy.
- Alignment: align to a single grid; dangling half-point offsets signal sloppiness.
- Keep interactive targets a minimum comfortable size — never below ~44pt on touch platforms, ~30pt on pointer-driven ones.
- Content should adapt, not overflow: flexible widths, fluid layouts, safe areas respected.

### The why
An invisible grid is what makes dense interfaces feel calm instead of chaotic. Consistent spacing lets the eye flow; inconsistent spacing makes every screen feel slightly wrong.

### Implementation hints
- Detect: spacing literals in style objects, `padding`, `margin`, `gap`, `SizedBox`, `EdgeInsets`, `space-`, `p-`, `m-`.
- Check: any padding/margin value not on the 8-point rhythm (except 4) → flag with suggested nearest 8 multiple.
- Check: touch target smaller than 44px with no pointer alternative → flag.

---

## Dark Mode

### Rules
- Dark appearance is not colors inverted; it is a *re-authored* surface. Design both appearances deliberately.
- Use surfaces with depth ordering: base surfaces darker, raised surfaces slightly lighter or elevated by shadow, so hierarchy survives darkness.
- Reduce reliance on pure black backgrounds; Apple uses near-black with tinted surfaces.
- Semantic colors (background, secondary background, separator) adapt; accent often stays similar between modes.
- Text and icon contrast must be re-verified in dark mode — mid-grays that pass in light fail in dark.
- Never hardcode light appearance only.

### The why
People run in dark mode at night, in low light, OLED duty cycles, and by preference. An interface that breaks in dark mode breaks for a large share of users.

### Implementation hints
- Detect: theme definitions, `darkTheme`, `ThemeData.dark`, `prefers-color-scheme`, `darkMode`, `.dark`, `onBackground`.
- Check: is there a dark token set at all? If every color is a single light-mode literal → flag.
- Check: dark surfaces use near-black (not `#000`) with at least two depth levels.

---

## Icons & Symbols

### Rules
- Icons must be **instantly recognizable** in silhouette at small sizes. Prefer familiar, well-tested glyphs over novel metaphors.
- Keep icons optically consistent within the same family: same stroke weight, same corner treatment, same visual weight.
- Administrative/destructive actions should carry recognizable meaning — never a clever metaphor that reads ambiguous.
- Icons are rarely the only label: pair with text when meaning could be ambiguous (tabs, toolbars, buttons that must be clear).
- Provide filled/selected vs. unfilled/deselected states where selection semantics matter.

### The why
Icons are read by shape before meaning. Inconsistent families and ambiguous metaphors force users to stop and decode — the opposite of clarity.

### Implementation hints
- Detect: icon usages, `Icon(`, `<svg`, `IconData`, `Icons.`, `IconButton`, `Image.asset` with icon names.
- Check: mixed icon families (some filled, some stroked, different weights) in the same row → flag.
- Check: an icon used alone where its meaning is ambiguous → flag, suggest adding label.

---

## Materials & Surfaces

### Rules
- Use **layered surfaces** to communicate depth: base, raised, and overlay levels. Distinguish by background tone and subtle shadows/elevation, not hard borders.
- Transparency and blur (materials) should be subtle — frosted glass lends texture, heavy blur asserts chrome.
- Split-view / sidebar / toolbar surfaces are distinguishable by surface level, not by thick visible borders.
- Avoid drop shadows as the primary depth signal on small elements; use tone + slight elevation.

### The why
Depth in Apple interfaces is physical: layered glass and light-gathering surfaces. The eye reads levels instantly without needing borders.

### Implementation hints
- Detect: surface colors, elevation, `BoxDecoration`, `shadow`, `elevation`, `blur`, `backdrop-filter`, `frosted`, `glass`.
- Check: does the UI define ≥2 surface levels? Flat one-tone interfaces with hard borders read as non-Apple → check.
- Check: heavy border use (`border-width` > 1 or visible box borders everywhere) → flag as anti-deference.

---

## Motion

### Rules
- Motion must be **purposeful** — it explains spatial relationships (what came from where, what goes where) and state changes. Decoration-only motion is noise.
- Transitions between screens/panels should be smooth and quick; slow or sluggish transitions feel broken.
- Respect **reduced motion**: meaningful content can appear instantly, never rely on motion to communicate essential information.
- Interruption: if the user interrupts an animation (tap, scroll), the animation should respond — cancel or settle quickly, not finish a long script.
- Consistent timing language across the app: don't mix one snappy and one glacial animation for the same event class.

### The why
Apple's motion is storytelling: it keeps the user's mental model of where things are. Motion that fights the user's intent (long mandatory animations) violates the "user in control" principle.

### Implementation hints
- Detect: animation durations, `Duration(milliseconds:`, `animationDuration`, `transition`, `ease-`, `transition-`, `AnimatedContainer`, `animate`, CSS `transition`.
- Check: any essential UI state conveyed *only* through a transient animation → flag.
- Check: durations longer than ~500ms for simple state transitions without reason → flag.

---

## Privacy

### Rules
- Ask for the **minimum** permissions and data the feature needs; explain *why* in plain language at request time.
- Data collection that isn't essential must be optional and reversible.
- Privacy-sensitive surfaces (location, camera, health, contacts) must show clear, constant indicators of active collection where the platform requires.
- Don't hide what the app knows about the user behind dense text; make data practices scrutable.

### The why
Trust is a design material. An interface that feels surveilled fails at deference — the user must hold at least as much power as the app.

### Implementation hints
- Detect: permission prompts, location/camera/mic usage, `requestPermission`, `Permission.`, `navigator.permissions`, `Ask`, `onboarding` for permissions.
- Check: is permission requested in context (before the feature that needs it) rather than at launch → otherwise flag.

---

## Writing

### Rules
- Write in **plain, direct language**. Short sentences, active voice.
- User-facing labels use sentence case and match platform conventions; avoid jargon and marketing-speak inside the interface.
- Error messages state what happened and what to do next, in human terms — not technical codes.
- Keep button and control labels action-oriented and specific: "Save", "Share", "Cancel" — never "OK" for a consequential action.
- Be concise: Apple's copy allows one clear message, not an explanation essay.

### The why
Interface copy is the user's main guide. The best UI fails with bad words — clarity applies to language as fiercely as to layout.

### Implementation hints
- Detect: string literals rendered to user, `label:`, `Text('`, `title:`, `<title`, button text.
- Check: error strings containing enum names, stack traces, or "Error 0x…" → flag.
- Check: labels longer than a short phrase for a button/action → flag.

---

## Accessibility

### Rules
- **Text scaling** is non-negotiable: all text must remain legible (and non-clipped) up to extra-large accessibility sizes.
- **Contrast** per Color rules.
- **Screen-reader support**: every meaningful element has a readable name; decorative elements are marked hidden; interaction elements announce state (button, checked, expanded, etc.).
- **Reduced motion** respected (see Motion).
- **Touch target** minimums respected (see Layout).
- Never rely on a single sensory channel (vision, gesture only, color only).
- Keyboard/focus navigation must reach every interactive element and give visible focus.

### The why
Accessibility is not a feature branch; it is the definition of quality. Interfaces that only work for one kind of human are broken interfaces.

### Implementation hints
- Detect: `semanticLabel`, `Semantics`, `aria-`, `accessibilityLabel`, `role=`, `alt=`, `tooltip`, `focus`.
- Check: images/webviews with no label or alt → flag.
- Check: icon-only buttons with no accessible name → flag.

---

## Aggregated review checklist

When auditing a surface, run these in order:
1. Color: palette discipline + contrast + color-not-alone
2. Typography: scale hierarchy + body legibility + scale safety
3. Layout: 8-pt grid + consistent margins + target sizes + spacing groupings
4. Dark mode: both appearances authored + near-black + depth levels
5. Icons: family consistency + pair-with-label + recognizability
6. Materials: ≥2 surface levels + subtle depth
7. Motion: purpose + reduced-motion + interruptibility
8. Privacy: minimum data + in-context permission
9. Writing: plain + action labels + human errors
10. Accessibility: text scale + SR names + focus + no single-channel

## Working with other skills

- **Highest-value order**: run foundations first on any screen — foundations violations poison components.
- `hig-components` assumes foundations are respected; shop rule cards by component when implementing or reviewing specific elements.
- `hig-audit` aggregates foundations checks with component and pattern checks into one deviation list.
- `hig-orchestrator` triggers foundations automatically when it detects layout, styling, or theme code.