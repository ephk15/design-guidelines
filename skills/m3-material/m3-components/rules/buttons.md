# Buttons — rule card

A **button** is a control that triggers an action when activated. Distinguished from a *link* (navigation) and from *toggles* (state switching). Material offers five button types — each signals a distinct hierarchy level.

**Triggers** (stack-agnostic detection signals): `Button`, `button`, `<button`, `FilledButton`, `OutlinedButton`, `TextButton`, `ElevatedButton`, `TonalButton`, `FilledTonalButton`, `onPressed`, `onClick`, `btn`, `action`.

## Rules

1. **Five strengths, one hierarchy.** Material button types form a ladder: `filled` (highest emphasis) > `filled tonal` > `elevated` > `outlined` > `text` (lowest emphasis). Pick the minimum emphasis that carries the action — over-filling every button flattens the hierarchy.
2. **One primary action per surface.** The filled button is reserved for the surface's single most important action. Everything that competes drops a rung.
3. **Styles communicate hierarchy, not decoration.** Always use the same type for the same tier of action across the app — don't dress a secondary surface as primary.
4. **Label the action with a verb, specifically.** "Save", "Send", "Add", "Delete". Never "OK" on a consequential action. Two words max is typical.
5. **Destructive actions appear last** in a set and may be visually destructive (error color) **only when the action destroys data irrevocably**.
6. **A disabled button is visually dimmed and non-interactive** — and the reason it's disabled must be recoverable by the user.
7. **Touch target ≥ 48dp** on touch platforms (foundations layout). Extend the hit area to 48dp even if the visual is smaller.
8. **Feedback is immediate and layered.** Press shows the state layer (hover/focus/pressed) instantly — Ink ripples/state layers, not a laggy handler response.
9. **Full container width** for a primary bar in forms/modals when Material recommends it; otherwise don't stretch buttons beyond comfortable width.
10. **Icon buttons** used alone must be unambiguous and carry an accessible name; keep fill/weight consistent across the group.

## The why

Material's type ladder exists so users always know *where to act*. Hierarchy in buttons is the difference between a calm interface and a wall of competing actions.

## Implementation hints

- Detect via triggers above. Then check:
- Count the highest-emphasis (filled) buttons per surface → >1 → flag (suggest dropping rungs).
- Verify button type tier is consistent with other surfaces for the same hierarchy.
- Inspect label text: any "OK"/generic → flag.
- Check state layers exist on every button (hover/pressed/focus/disabled) → flag missing.
- Compare interaction target size vs 48dp → flag undersized.
- Ensure icon-only buttons have an accessible name.

## Checklist

- [ ] exactly one primary (filled) emphasis per surface
- [ ] button type consistently maps action tier across the app
- [ ] label is an action verb, specific, ≤ 2 words
- [ ] destructive action acknowledged + error color only when truly destructive
- [ ] disabled state dimmed and recoverable
- [ ] tap target ≥ 48dp with state layers
- [ ] icon-only buttons named for screen readers