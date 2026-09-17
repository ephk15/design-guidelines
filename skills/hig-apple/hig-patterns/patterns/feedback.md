# Feedback — pattern card

The **feedback** pattern covers how the app communicates outcomes: success, error, confirmation, and the absence of error (silent success).

## Structure

1. **Match the feedback to the stakes.** Silent success for low-stakes, recoverable actions (a toggle, a like). Inline message for field errors. Alert/banner for consequential or blocking problems. Full-screen only for true dead-ends (rare).
2. **Error copy tells the person three things:** what happened (human terms), why it matters (brief), what to do next ("Try again", "Check your connection", "Open Settings"). No codes, no stack traces, no blame.
3. **Errors are discoverable, not decorative.** Error states live with their subject (at the field, at the block), persist until fixed, and are announced to screen readers.
4. **Undo beats sorry.** When an action is destructive or consequential, offer undo/revert (`see patterns/undo-redo`) — never force a recovery procedure.
5. **Toast/transient messages are for ephemeral confirmations only** ("Copied", "Saved"), not for actionable errors — a vanishing error the user must act on is a trap.
6. **Tone is calm and factual.** Avoid panic phrasing ("ERROR!", "CRITICAL"); avoid chirpy downgrades of real problems.
7. **Confirmations avoid "Are you sure?" theater** — confirm only genuinely destructive/irreversible actions (`see components/alerts`).

## Implementation hints

- Detect: `SnackBar`, `Toast`, `toast()`, `<div role="alert">`, error state branches, `showError`, `setError`, `errorMessage`, banner components, `Alert`, `InlineMessage`, `validationMessage`, `exceptions` shown to user.
- Catches: actionable error in a transient toast; error without recovery action; full-screen modals for trivial states; color-only error states; success messages for self-evident results.

## Checklist

- [ ] stakes match channel (silent/inline/banner/modal)
- [ ] error = what + why + next step, human terms
- [ ] error persists at its subject until fixed
- [ ] destructive → undo offered
- [ ] no actionable info in transient toasts
- [ ] calm, factual tone
- [ ] SR-announced
- [ ] no "are you sure" without real stakes