# Dialogs — rule card

A **dialog** is a modal surface that interrupts the current context to present a critical piece of information, confirmation, or a focused task. Material: alert dialogs, dialogs (content+actions), full-screen dialogs.

**Triggers** (stack-agnostic detection signals): `showDialog`, `AlertDialog`, `Dialog`, `dialog`, `<dialog`, `confirm`, `showModalBottomSheet` variants, full-screen dialog, `modal`.

## Rules

1. **Pause, don't push**: a dialog interrupts — use it only when the interruption is justified (irreversible action, missing required input, a task that must complete before continuing). Regular choices embed inline.
2. **Title states the situation; actions resolve it.** Content carries the explanation; buttons present the choices. Never overload a dialog with content (M3: title + short body; complex tasks go full-screen).
3. **One clear primary action**, per button rules — don't make people choose between two filled buttons in a dialog.
4. **Dismissibility**: dialogs are dismissible (back/close/outside via scrim) for non-critical states; irreversible-action dialogs downgrade outside-dismissal so the user can't accidentally blow past the warning.
5. **Focus management**: focus lands on the dialog when it opens and must not escape to the background; focus trap inside.
6. **Reduced motion**: opens promptly; screen readers announce the dialog and its role (alertdialog).
7. **Full-screen dialogs** (complex tasks like adding an item from scratch) get a real title, its own navigation (close, save), and cover the compact viewport.

## The why

Dialog = interruption. Judging when interruption earns its keep, and making actions obvious, is what separates useful nudges from modal abuse.

## Implementation hints

- Detect via triggers. Then check:
- Dialog used where an inline/expansion choice would do → flag.
- Two competing filled buttons, or no clear primary → flag.
- Irreversible-action dialog dismissible outside → flag (should require explicit confirm).
- No focus trap / no SR announcement → flag.

## Checklist

- [ ] interruption justified
- [ ] title + short body; complex content → full-screen
- [ ] one clear primary action
- [ ] dismissal matches severity
- [ ] focus trapped inside, announced as dialog
- [ ] reduced-motion respected