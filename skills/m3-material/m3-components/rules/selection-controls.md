# Selection controls — rule card

A **selection control** lets the user choose between mutually exclusive or independent options. Material: checkbox (multi-select), radio (one-of-group), switch (toggle a setting on/off).

**Triggers** (stack-agnostic detection signals): `Checkbox`, `Switch`, `Radio`, `RadioGroup`, `ToggleButton`, `<input type="checkbox">`, `<input type="radio">`, `<input type="switch">`, `role="switch"`, `Toggle`, `SwitchListTile`.

## Rules

1. **Right control per semantics**:
   - **Checkbox** — one or more independent choices from a set (accept terms, pick features). Also "select all" parents.
   - **Radio** — exactly one choice from 2+ mutually exclusive options (never for a single on/off).
   - **Switch** — a single binary setting that takes effect immediately (notifications on/off).
   Replace a checkbox with a switch when the change applies instantly; replace radio-in-dropdown with visible radios when options deserve visibility.
2. **Label every control**: an accessible, visible label describes the choice. The label is part of the tap target.
3. **State quality**: checked/unchecked, disabled, and error states are distinct; selection (fill/hue) uses the primary color; state layer gives pressed feedback.
4. **No color-only communication**: checked vs unchecked is shape + fill + icon (checkmark) — not hue alone.
5. **Group semantics for radio/checkbox groups**: a group has an accessible name; keyboard arrows navigate inside the group.
6. **Touch target ≥ 48dp** for each control (visual control may be smaller; extend hit area).
7. **Undo/rollback friendly**: selecting produces immediate visible change; where a selection triggers an action (switch = immediate effect), provide the relevant recovery pattern.

## The why

Selection controls encode *choice type*. Use the control whose semantics match the question being asked, and users never have to decode what a checkbox means here.

## Implementation hints

- Detect via triggers. Then check:
- Checkbox used for a binary immediate setting (→ switch) or single-choice (→ radio) → flag.
- Switch used where choice is part of a set (→ checkbox/radio) → flag.
- Unlabeled control → flag.
- Selection conveyed by color only (no icon/shape change) → flag.
- < 48dp hit area → flag.

## Checklist

- [ ] control type matches choice semantics
- [ ] every control labeled, label part of target
- [ ] distinct checked/unchecked/disabled/error states
- [ ] shape+icon+color mark selection, not color alone
- [ ] groups named + arrow-key navigable
- [ ] ≥ 48dp targets