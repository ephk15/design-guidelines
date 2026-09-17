# Snackbars — rule card

A **snackbar** is a transient message that communicates a direct action result (confirm, error recovery, undo) at the edge of the screen. It is not a persistent notification and not a toast style banner for ads/critical.

**Triggers** (stack-agnostic detection signals): `SnackBar`, `showSnackBar`, `showSnackbar`, `snackbar`, `toast`, `MaterialBanner`/banner misuse.

## Rules

1. **Use for actions, not announcements**: snackbars acknowledge a completed action and offer recovery (Undo), confirm a save, or surface an inline error with a fix. Persistent status or advertising belongs elsewhere (banners/inline).
2. **One line, short**: keep the message minimal; multi-line snackbars are for longer recovery text — still never an essay.
3. **Action button when there's recovery**: exactly one action (e.g. "Undo"); the action is a text button with strong enough contrast; tapping it fires the recovery and dismisses.
4. **Dismissible + auto-dismiss without trapping**: snackbars auto-dismiss; swipe/dismiss allowed. Never hijack focus or block interaction while visible.
5. **Position**: bottom edge (or top on large screens where the pattern specifies) — consistent placement app-wide.
6. **Stacking**: never stack two snackbars; queue replacements.
7. **Accessibility**: content is announced to screen readers; action reachable; the message is short enough to read before dismissal.

## The why

Snackbars are the "it worked / you can undo it" whisper. When they become noisy announcement banners they erode the trust the pattern exists to build.

## Implementation hints

- Detect via triggers. Then check:
- Snackbar used for persistent/advertising content → flag.
- No action button where undo/recovery exists → flag.
- Multiple snackbars stacked → flag.
- Snackbar blocking focus/interaction → flag.

## Checklist

- [ ] used for actions/results, not announcements
- [ ] short message, single line where possible
- [ ] recovery action when relevant
- [ ] auto-dismiss, no focus trap
- [ ] consistent placement
- [ ] announced to screen readers