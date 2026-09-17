# Confirming and saving — pattern card

The **confirming and saving** pattern governs how a user commits values: when to confirm explicitly, when to save silently, and how confirmations read.

## Structure

1. **Two regimes — know which you are in**:
   - **Explicit commit** (submit/save button): the user reviews then commits; the action word tells what happens next.
   - **Auto-commit** (settings switches, forms that save on exit): changes are by definition intentional; use switches that take effect immediately.
2. **Confirm when destructive or hard to undo.** Irreversible or wide-impact actions get an explicit confirmation — but confirming every little thing is modal abuse (`see components/dialogs`).
3. **The save button says *what* it saves**: "Save", "Publish", "Create account" — not "OK" / "Submit". A disabled primary button until valid is Material-sanctioned; explain why only when the user would be stuck.
4. **Feedback matches weight**:
   - Light action → ephemeral feedback (snackbar "Saved" is often too chatty; keep context).
   - Medium commit → acknowledge in place (button becomes "Saved ✓", or sheet text updates).
   - Big commit → navigate to the result surface (don't leave the user staring at the form).
5. **Auto-save / save on exit**: if edits save implicitly, the UI must say so ("Saved just now", "All changes saved"). Silent loss = broken trust.
6. **Undo beats confirm**: where undo is cheap (deleting a draft, toggling), prefer an undo snackbar over a confirm dialog.

## Cross-layer rules

- Confirmation surfaces → `see components/dialogs`.
- Ephemeral feedback → `see components/snackbars`.
- Switch/auto-commit semantics → `see components/selection-controls`.

## Implementation hints

- Detect: `save`, `submit`, `onWillPop`, `Form`, `PopScope`, `confirm`, `showDialog`, `SnackBar` undo.
- Common catches: confirm dialog on every little action; save button changes to "Saved" with no visible state; auto-save silent with no indicator; "OK" label on consequential commit.

## Checklist

- [ ] explicit vs auto-commit regime chosen and consistent
- [ ] confirm only when destructive/hard-to-undo
- [ ] primary button says exactly what saves
- [ ] commit button states (disabled/enabled/saved) honest
- [ ] feedback weight matches action weight
- [ ] undo preferred over confirm where cheap
- [ ] auto-save is never silent