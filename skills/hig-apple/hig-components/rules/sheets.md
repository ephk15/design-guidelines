# Sheets — rule card

A **sheet** is a modal panel that slides up from the bottom edge, presenting a self-contained secondary task without leaving the current context. It is the modern Apple pattern for views that were historically modal screens.

**Triggers**: `BottomSheet`, `showModalBottomSheet`, `sheet`, `Sheet`, `modalBottomSheet`, `draggableScrollableSheet`, `actionSheet`, `presentSheet`, `.sheet(` (SwiftUI, informational), `bottom-sheet`, `<dialog` with slide-up.

## Rules

1. **One task per sheet.** A sheet presents a focused, completable task (adjust settings, compose a short message, pick options over a form, view details). If it contains full navigation with multiple levels, it is a screen, not a sheet.
2. **Dismissible by drag + explicit close.** Standard sheets are dismissed by swiping down and have a visual grabber/close affordance appropriate to the platform. A sheet the user cannot escape is a trap.
3. **Atomic outcome or no outcome.** The user can cancel with no side effects; if the sheet changes data, changes apply clearly (save on action, or explicit Done vs Cancel).
4. **Title for orientation** when the content alone doesn't make the task obvious.
5. **Height discipline.** Sheet height should communicate scope: a small task gets a small sheet; a large task may become nearly full-screen but the user must know it (a full-screen sheet needs an explicit close/back and handles deep content).
6. **Avoid stacks of sheets.** Layering sheet-on-sheet reads as awkward; consolidate or push a screen.
7. **Content above the sheet remains visible as context** — the dimming/overlay should be light enough that the user retains where they are.
8. **Implement scroll correctly:** the sheet body scrolls independently; drag-to-dismiss only begins at the top of the scroll (no accidental dismissal mid-scroll).

## The why

Sheets keep the user in place — they answer a *side question* without abandoning the main task. Their central value is the ability to come and go freely; everything that blocks dismissal or loses context defeats the pattern.

## Implementation hints

- Detect via triggers above. Then check:
  - Single task scope: multiple distinct sub-navigations inside → suggest a screen instead.
  - Dismissibility: drag handler present? explicit close present? → flag if neither.
  - State on dismiss: unrecovered changes possible without warning for non-trivial edits → flag.
  - Nested sheets → flag.
  - Scroll + drag interplay: accidental dismiss while scrolling a list → flag.
  - Dimming light enough to keep context visible.

## Checklist

- [ ] one focused task
- [ ] drag + explicit dismiss, no trap
- [ ] cancel = no side effects (or explicit save)
- [ ] titled when scope isn't obvious
- [ ] height maps to scope
- [ ] no sheet stacking
- [ ] context preserved under overlay
- [ ] scroll/dismiss interplay correct