# Buttons — rule card

A **button** is a control that triggers an action when activated. Distinguished from a *link* (navigation) and from *toggles* (state switching). If it navigates, it is a link, not a button.

**Triggers** (stack-agnostic detection signals): `Button`, `button`, `<button`, `ElevatedButton`, `TextButton`, `OutlinedButton`, `FilledButton`, `IconButton`, `onPressed`, `onClick`, `onTap`, `btn`, `action`, `FAB`, `FloatingActionButton`, `raised`, `pushbutton`, `.secondary`, `.bordered`.

## Rules

1. **One primary action per surface.** The default/filled button is reserved for the surface's single most important action. More than one filled primary button dilutes the emphasis into noise. Everything else is secondary (plain/outlined) or tertiary (link-style).
2. **Styles communicate hierarchy, not decoration.** Filled = primary, plain/outline = secondary, link-style = tertiary/destructive-in-context. A secondary surface must not dress up as a primary.
3. **Label the action with a verb, specifically.** "Save", "Send", "Add", "Delete". Never "OK" on a consequential action. Two words max is typical. Title case for the platform language; sentence context-aware (follow platform text conventions).
4. **Destructive actions appear last** in a set and may be visually destructive (red) **only when the action destroys data irrevocably**. Red is a warning, not a theme.
5. **A disabled button is visually dimmed and non-interactive** — and the reason it's disabled must be recoverable by the user (don't leave them guessing; prefer keeping the button enabled and explaining on the next step, or offer guidance near it).
6. **Touch target minimum ~44pt** on touch platforms (see foundations layout). Pointer platforms may use tighter but not smaller than comfortable (~30pt).
7. **Feedback is immediate.** Press produces a visible state change (not just at the handler's response time).
8. **Full-bleed buttons.** In a modal/form context, a primary bar at the bottom spanning content width is preferred over a floating center primary.
9. **Icon buttons** used alone must be unambiguous (see foundations icons) and carry an accessible name. Group icon buttons with consistent spacing; keep fill/weight consistent across the group.

## The why

Buttons are the most frequent control in a UI. Hierarchy within buttons is how people know *where to act*. Consequence visibility (destructive, disabled, primary) is how you keep people safe and in control.

## Implementation hints

- Detect via triggers above. Then check:
- Count primary-styled buttons on the surface → >1 → flag (suggest reclassing to secondary).
- Inspect label text: any "OK"/"Save & Continue"/generic → flag, suggest verb-specific.
- Look for red used as brand/decoration vs used on a destructive action → flag if decorative.
- Check disabled styling exists and is recoverable.
- Compare interaction target size (hit area / min-width / min-height) vs 44pt-ish → flag undersized.
- Ensure icon-only buttons have an accessible name (tooltip, `aria-label`, semantics).

## Checklist

- [ ] exactly one primary emphasis per surface
- [ ] label is an action verb, specific
- [ ] destructive action acknowledged + red only when truly destructive
- [ ] disabled state dimmed and recoverable
- [ ] tap target ≥ ~44pt (touch)
- [ ] immediate pressed feedback
- [ ] icon-only buttons named for screen readers