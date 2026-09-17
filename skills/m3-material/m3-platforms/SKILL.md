---
name: m3-platforms
description: 'Material Design 3 (M3) adaptation layer, made stack-agnostic. The core rules in m3-foundations, m3-components and m3-patterns are platform-independent; THIS skill adds the deltas for adaptive layout (compact/medium/expanded breakpoints), density, and platform nuances (Android, web, Flutter, etc.). Use to review or implement when breakpoints/adaptive behavior, density options, or a specific target platform matter.'
---

# M3 Platforms

Material 3 is explicitly *adaptive*: the same design system expresses itself differently at different screen sizes and input types. This skill is an **extension layer** — it never restates core rules; it adds only what differs across the M3 responsive breakpoints and platforms.

## How to use

1. Confirm the target dimensions/platform(s) of the surface you're working on.
2. Load the extension file: `platforms/<name>.md`.
3. Apply core rules from `m3-foundations`, `m3-components`, `m3-patterns`, then layer the adaptation deltas on top.
4. If the design must run on **multiple breakpoints**, design compact-first, then ensure medium/expanded deltas don't conflict (flag conflicts explicitly).

## Platform index

| Context | Source | Extension file |
|---|---|---|
| Adaptive layout / breakpoints | `platforms/adaptive.md` | compact (<600dp), medium (600–840dp), expanded (>840dp); navigation morphing; density |
| Android (Compose/Views) | `platforms/android.md` (todo) | dynamic color, back handling, touch |
| Web / desktop | `platforms/web-desktop.md` (todo) | pointer-first, keyboard, windowing |
| Flutter (cross-platform) | `platforms/flutter.md` (todo) | platform-adaptive components, Material 3 opt-in |

## Cross-cutting platform rules

1. **Platform conventions are defaults, not chains.** A custom brand identity can deliberately deviate, but the deviation must be a *design decision*, not an accident.
2. **Never copy a platform's control literally across platforms** — gestures and affordances differ (a desktop menu ≠ a mobile sheet). Translate the *intent*, not the widget.
3. **Responsive is the baseline, not an option.** The same logical app must adapt layout/input from the smallest to the largest screen, not merely reflow a phone screenshot.
4. **A platform's system affordances are part of its UX** — system back (Android), scrollbar + pointer (desktop), touch targets (mobile). Respect them or flag the deviation.
5. **Density is opt-in, not survival.** Compact density is a token choice users opt into (not a desperate fit-to-screen).

## Working with other skills

- Core rules always come first: foundations → components → patterns → platform deltas.
- `m3-audit` asks which target sizes/platforms a project targets so it can include the deltas in its deviation report.
- `m3-orchestrator` detects responsive/platform work and loads the relevant `platforms/<name>.md`.