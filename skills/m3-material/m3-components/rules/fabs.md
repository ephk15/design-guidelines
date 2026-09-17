# FABs (floating action buttons) — rule card

A **FAB** (floating action button) is the promotion of the primary action of a screen — a single, elevated, emphasized floating action.

**Triggers** (stack-agnostic detection signals): `FloatingActionButton`, `FAB`, `FloatingActionButton.extended`, `extended` FAB, `fab`.

## Rules

1. **One FAB per screen, at most**: the FAB promotes the *single primary action* of a screen. Screens without one dominant action should have none. Never a cluster of FABs.
2. **The action must be obvious and frequent**: FABs are for actions users perform often in context (compose, add, share). A one-off buried flow doesn't earn a FAB.
3. **Correct position**: FABs float above content; standard placement is bottom-right (or bottom-center for extended); respect safe areas / bottom bars (space for it). Extended FABs carry label + icon when the action needs clarity.
4. **Elevation & animation**: FAB uses extra-large shape + high elevation; its press shows state layer; it can expand/contract (transform to a sheet or menu) but transformation must be justified and follow motion rules.
5. **Don't hide the FAB's purpose**: label/icon must make the action discoverable (extended if ambiguous).
6. **Accessibility**: named action, ≥ 48dp target.
7. **FAB vs buttons**: when the same action appears as both a button in a bar and a FAB, that's a hierarchy conflict — choose one emphasis.

## The why

The FAB is the screen's "here's what you'll do most here." Its power comes from scarcity.

## Implementation hints

- Detect via triggers. Then check:
- >1 FAB, or FAB on a screen with no dominant action → flag.
- FAB action obscure (icon-only, ambiguous) → flag/suggest extended.
- FAB overlapping content/safe areas → flag.
- Same action duplicated as button + FAB → flag.

## Checklist

- [ ] ≤1 FAB per screen, justified action
- [ ] obvious, frequent primary action
- [ ] correct position + safe-area spacing
- [ ] extended when label matters
- [ ] state layer press feedback
- [ ] named, ≥ 48dp