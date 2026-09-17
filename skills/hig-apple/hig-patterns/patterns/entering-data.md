# Entering data — pattern card

The **entering data** pattern covers any flow where the user provides information: a form, a wizard, a settings screen, a checkout, profile setup.

## Structure

1. **Collect what's needed, nothing more.** Every field earns its place. "Nice to have" fields are future regrets; the shortest form that fulfills the task wins.
2. **Order by user's mental model, not internal model.** Group names/contact/address coherently; what-you-know first, what-you-draw-down-later after.
3. **Validate progressively:** validate on completion of a field (blur) or on submit, never scream before the user finished typing. Inline, at the field.
4. **One primary submit** visible and enabled; secondary actions (cancel) visually subordinate.

## Rules

1. Default sensible values when safe (country, language, defaults) — prefilled reduces effort, but never prefill fields that shouldn't be (e.g., passwords, terms consent).
2. Field-by-field keyboard: every text field gets its right keyboard (`see components/text-fields`).
3. Autofill + autocomplete for email/phone/address/city/zip.
4. Number formatting as you type (phone, amounts) — no raw strings.
5. Saving drafts: don't destroy user effort on accidental back/close for multi-field forms; offer resume or warn.
6. Passwords: peer toggle, no arbitrary rules without explanation, and show the rule when it's meaningful.
7. Keep motion/labels modest: no animated every-field; focus moves predictably (tab order, auto-focus logical).
8. Accessibility: labels attached to fields (not placeholders only), correct field types, errors announced.

## What good looks like

- User can complete the form without referring to prior knowledge already captured
- Errors appear at field level with instructions
- A second submission behaves identically (stable defaults, same validation) — no form amnesia

## Implementation hints

- Detect: `form`, `FormField`, `<form`, `TextFormField`, `keyboardType`, `autofillHints`, `validator`, wizard steps, `Stepper`, multi-step screens.
- Check field count/necessity; keyboard types; autofill hints; draft behavior on back; submit semantics (disabled until valid vs validate-on-submit) — flag blocking behaviors.

## Checklist

- [ ] minimal necessary fields
- [ ] logical grouping + order
- [ ] per-field inline validation, progressive
- [ ] correct keyboards + autofill
- [ ] progressive formatting
- [ ] form state preserved on back/close (or warned)
- [ ] labels + errors accessible
- [ ] stable repeat submissions