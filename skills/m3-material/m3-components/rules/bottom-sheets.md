# Bottom sheets — rule card

A **bottom sheet** is a surface that slides up from the bottom for supplementary content or a focused task. Material: modal bottom sheets (interrupt with a scrim) and standard/expanding bottom sheets.

**Triggers** (stack-agnostic detection signals): `showModalBottomSheet`, `BottomSheet`, `DraggableScrollableSheet`, `modal-bottom-sheet`, `bottom sheet`, `bottomsheet`, `PersistentBottomSheet`.

## Rules

1. **Modal or standard — choose by interruption**: modal sheets take focus (scrim dims the page) and are dismissed by scrim tap/back; standard sheets sit alongside content (expandable) and don't block. Don't make a standard sheet act modal.
2. **A sheet is for supplementary/focused work**, not for hiding the app's main navigation — destination-heavy choice belongs in nav components.
3. **Dismissible + focus**: modal sheets dismiss by back / scrim / drag, unless severity demands otherwise; focus lands inside the sheet.
4. **Compact viewport-minded**: on phones a full-screen dialog may beat a tall sheet for complex tasks (see dialogs); sheets with long forms should scroll or promote to full-screen.
5. **Drag/hand handle** communicates the sheet is movable; scrim tap-to-dismiss is discoverable.
6. **Accessibility**: screen reader announces the sheet and its dismissal behavior; the scrim is not focusable.

## The why

Bottom sheets turn a "come back" interaction into a "deal with it here, then continue" — powerful when content is genuinely supplementary, noisy when it hides core tasks.

## Implementation hints

- Detect via triggers. Then check:
- A sheet that blocks without a scrim/@interruption → flag.
- Long-form content in a modal sheet on compact width → suggest full-screen.
- Sheet used as nav → flag, prefer nav components.
- No dismiss affordance (drag/back/scrim) → flag.

## Checklist

- [ ] modal vs standard chosen by interruption need
- [ ] not used as main navigation
- [ ] dismissible (back/scrim/drag) with severity guard
- [ ] focus inside sheet, scrim focusable
- [ ] long content scrolls or promotes to full-screen
- [ ] SR announces sheet + dismissal