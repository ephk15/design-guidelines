# Entering data — pattern card

The **entering data** pattern covers forms and data-collection flows: gathering accurate, well-validated input with minimal friction.

## Structure

1. **One form, one job.** Each form answers one question ("create account", "book a ride"). Everything on the screen serves that single intent — no bundling (sign-up + feature tour + permissions together is noise).
2. **Fields in mental order**: put fields in the order a person would naturally answer them (not DB-column order). Group related fields with visible grouping where useful.
3. **Label every field** per text-field component rules; helper text appears where genuinely needed, not everywhere (layout noise).
4. **Validate at the right time**: validate on blur/submit for full fields; live-validate only to clear an error already shown. Commit on the primary action; feel free to enable the primary button when the form is valid.
5. **Errors are local and actionable**: inline on the failing field, specific, with the fix (see errors pattern). A single error summary at top is for long forms; never error-by-color-only.
6. **Default sensibly, but honestly**: sensible defaults reduce friction; wrong defaults cause data errors. Never silently truncate or format data (respect norms, validate).
7. **Support going back and editing** — re-entering the flow must not be a trap.
8. **Long forms get structure**: step/group/submit hierarchy; progress only when the flow genuinely benefits; full-screen dialog for adding-an-item-type flows (compact).

## Cross-layer rules

- Field anatomy, errors, keyboard affordances → `see components/text-fields`.
- Confirmation on commit → `see patterns/confirming-saving`.
- First-run entry → `see patterns/onboarding` (todo).

## Implementation hints

- Detect: `Form`, `TextFormField`, `validator`, `GlobalKey<FormState>`, `TextField`, wizard/`Stepper`, questionnaire.
- Common catches: fields in DB order; live-error spam while typing; "OK" button on consequential save; no keyboard-action chain; whole-screen form dialog when inline suffices.

## Checklist

- [ ] single intent per form
- [ ] sensible field order + grouping
- [ ] labeled fields, restrained helper text
- [ ] validation on blur/submit, clear-on-fix
- [ ] errors inline, actionable, never color-only
- [ ] editable/backable flow
- [ ] structured long forms (not one mega-scroll)