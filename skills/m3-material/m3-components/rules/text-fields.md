# Text fields — rule card

A **text field** is an input for a short line of text, a number, or another single-line value. Material offers filled and outlined variants. Distinct from: multiline text areas, search fields, pickers.

**Triggers** (stack-agnostic detection signals): `TextField`, `TextFormField`, `OutlinedTextField`, `FilledTextField`, `TextInputAction`, `<input`, `textarea`, `input`, `field`, `TextEditingController`, `decoration`.

## Rules

1. **Choose the variant once, per hierarchy**: outlined for high-emphasis/standalone forms, filled for dense in-context entry. Don't mix variants arbitrarily on the same screen.
2. **Label every field** — a persistent label (top or floating) names the field. Never the placeholder as the only label; a placeholder is a hint, not a name.
3. **Container communicates state**: the container (fill color, outline) must visibly express enabled vs *focused*, and the field carries supporting/helper text, not just color. Focus state uses the primary color state layer.
4. **Error handling**: error state shows an error **icon + supporting text** (never color alone), states what went wrong and how to fix it, and appears on the field that failed. Readable at a glance.
5. **Validation timing**: validate on blur/submit for full fields; validate on change only to clear a shown error — never annoy with live errors before the user is done.
6. **Input affordances**: use the right keyboard type, autocapitalization, and text-input action (next/done) per field content (foundations writing + platform conventions).
7. **Touch target ≥ 48dp**; a field that sits below 40dp (dense) must still offer a 48dp compliant variant and be an explicit density choice.
8. **Accessibility**: every field has a label read by screen readers; error and state are announced, not only shown.
9. **Character/format limits** are surfaced honestly: don't silently truncate; show remaining counts or enforce with an error message.

## The why

Text fields are the most error-prone part of forms. Consistent variants, real labels, and honest errors are what keep a form from becoming a blame-game.

## Implementation hints

- Detect via triggers. Then check:
- Any field where the only label is a `hintText`/placeholder → flag.
- Error conveyed by color/outline only, or by generic message not tied to a field → flag.
- Mixed variants without reason on one screen → flag.
- Keyboard type mismatch (letters keyboard for numeric/email, no next action) → flag.

## Checklist

- [ ] persistent label, never placeholder-only
- [ ] one variant per hierarchy, mixed only deliberately
- [ ] error = icon + supporting text + recovery hint
- [ ] validation timed sanely (blur/submit, not live-spam)
- [ ] correct keyboard/autocapitalize/text-action per content
- [ ] ≥ 48dp target, dense only as deliberate choice
- [ ] label/error announced to screen readers