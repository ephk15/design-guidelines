# Text fields — rule card

A **text field** is a control for a single line of text entry (or a text area for multiple lines). It's the user's writing instrument, so clarity and forgiveness matter most.

**Triggers**: `TextField`, `TextFormField`, `TextEditingController`, `input`, `<input`, `type="text"`, `type="email"`, `type="password"`, `type="search"`, `type="number"`, `textarea`, `TextArea`, `multiline`, `FormField`, `search field`, `SearchBar`, `password field`, `OTP`, `code input`.

## Rules

1. **Visible boundaries.** A field's affordance (border/fill/underline) must make it obvious it's editable. Fields that look like plain text but accept input break the mental model.
2. **The keyboard matches the input.** Numbers → numeric keypad, email → email keyboard, text → text. Wrong keyboard = pure friction.
3. **Auto-advance and autofill** are applied for sequential forms: email, phone, address, one-time codes. Debounce/space for one-time codes; allow paste.
4. **Placeholder vs label.** Placeholder text is a hint that disappears; it is not a substitute for a persistent label when the field may be empty. Long forms benefit from persistent labels.
5. **Validated input explains *itself***: errors appear at the field (inline), state what's wrong in human terms, and help fix it — not a generic toast. Error text must persist and be reachable by screen readers.
6. **Secure fields (password) let the user peek when the concern is typos** — show/hide toggle is user-friendly; don't force blind entry.
7. **Character limits show politely**: counter near the field when limits are meaningful; truncation at limit (silently) only when absolutely required.
8. **States are clear** — normal, focused, filled, error, disabled each look distinct, and the transition is obvious.
9. **Tap target + spacing** per foundations; fields must be comfortably tappable, adjacent fields well spaced.
10. **Single-line for single values, text area for prose.** Never crop real content into a single-line field.

## The why

Text entry is where users are most vulnerable to feeling stupid. Fields that confuse (no boundary, wrong keyboard, unexplained errors) make people mistrust the whole interface; fields that forgive (explain, peek, autofill) earn loyalty.

## Implementation hints

- Detect triggers above. Check:
  - Editable affordance present (border/fill) → else flag.
  - Keyboard type matches (`keyboardType`, `inputType`, `type=`), especially numeric/email/codes → flag mismatches.
  - Errors: inline + human + persistent + announced → else flag.
  - Password toggle present → else flag (when it's security-low-risk).
  - Labels persistent for empty-at-rest forms.
  - Autofill/smart suggestions on repeated data → flag missing when form has email/phone/address.

## Checklist

- [ ] visible editable affordance
- [ ] correct keyboard
- [ ] autofill + code auto-advance where relevant
- [ ] persistent labels or obvious context
- [ ] inline, human, announced errors
- [ ] password peek toggle
- [ ] distinct normal/focus/error states
- [ ] comfortable targets + spacing