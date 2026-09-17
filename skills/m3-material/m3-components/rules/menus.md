# Menus — rule card

A **menu** is a collection of options displayed in a floating surface anchored to a trigger. Material: contextual menus (right-click/long-press) and dropdown/menu-button menus.

**Triggers** (stack-agnostic detection signals): `PopupMenuButton`, `showMenu`, `DropdownMenu`, `MenuAnchor`, `menu`, `<select`, `dropdown`, `DropdownButton`, `context menu`.

## Rules

1. **Menu for options, not for client content**: menus present *choices* (actions, settings, nav); if the surface must show rich/complex content it's a dialog or sheet, not a menu.
2. **Anchor + one item per action**: the menu opens anchored to its trigger; each item is a single action (label ± icon). No sub-menus beyond one reasonably deep level; long item lists → rethink (dialog/select).
3. **Keyboard/focus first-class**: open with keyboard, arrow navigate, Esc closes, focus returns to trigger — menus are a keyboard pattern, not pointer-only.
4. **State layers on items** (hover/press/focus); disabled items visibly disabled (no hidden mystery options).
5. **Flanker interactions**: add/insert items at correct position (not end); destructive items stylized (error tone) respecting destructive rules.
6. **Close semantics**: selecting closes (unless multi-part), clicking outside/back closes; no sticky-open menus.
7. **Accessibility**: `role=menu/menuitem`, aria-expanded on trigger, announced label.
8. **Contrast with select**: a `<select>`-like control is fine for *picking among many known values*; a menu button is for *actions on an entity*. Use accordingly.

## The why

Menus conserve space until the user engages. They fail when they eat keyboard support, nest forever, or hide actions without affordance.

## Implementation hints

- Detect via triggers. Then check:
- Menu opened only by pointer (no keyboard) → flag.
- Sub-menu depth > 1-2 levels → flag.
- No state-layer feedback on items → flag.
- No focus return / no Esc → flag.
- Dropdown select misused for actions → flag.

## Checklist

- [ ] menu for choices, not content
- [ ] anchored, one action per item
- [ ] keyboard nav + focus return + Esc
- [ ] state layers, disabled visible
- [ ] destructive styled correctly
- [ ] closes on select/outside/back
- [ ] ARIA menu semantics