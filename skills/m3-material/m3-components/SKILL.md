---
name: m3-components
description: 'Material Design 3 (M3) components catalog — a host skill that routes to per-component rule cards. Use when designing, implementing, or reviewing any UI component (buttons, FABs, cards, chips, dialogs, bottom sheets, snackbars, text fields, selection controls, sliders, tabs, navigation, menus, progress, and more) in any technology. Load only the rule card for the component you are working on, not the whole catalog.'
---

# M3 Components

Host skill for Material 3's component guidance, made technology-agnostic. **You do not load all rules at once** — you look up the component you are working on and load only that card.

## How to use

1. Identify the component(s) present in the surface or code you're working on.
2. Find the matching rule card in the index below.
3. Read `rules/<card>.md` — that card contains the full rules for the component.
4. Apply or audit against the card's rules, checklist, and implementation hints.

The cards are written in language-agnostic terms: every rule is expressed against *what the component does*, not against any framework. Implementation hints give stack-agnostic detection signals.

## Index of rule cards

### Actions
| Component | Card | When you see |
|---|---|---|
| Buttons | `rules/buttons.md` | any clickable action trigger (filled, tonal, outlined, elevated, text) |
| FAB (floating action buttons) | `rules/fabs.md` | floating round/extended action button |
| Icon buttons | `rules/icon-buttons.md` (todo) | square icon-only control, ToggleButton |
| Segmented buttons | `rules/segmented-buttons.md` (todo) | mutually exclusive action group |

### Containers
| Component | Card | When you see |
|---|---|---|
| Cards | `rules/cards.md` | elevated/filled/outlined container for grouped content |
| Chips | `rules/chips.md` | assist/filter/input/suggestion token |
| Lists | `rules/lists.md` | rows of items, list tiles, supporting text |
| Data tables | `rules/data-tables.md` (todo) | tabular data with header row |

### Selection & input
| Component | Card | When you see |
|---|---|---|
| Text fields | `rules/text-fields.md` | text entry box (filled/outlined) |
| Selection controls | `rules/selection-controls.md` | checkbox, radio, switch |
| Sliders | `rules/sliders.md` | value slider with thumb |
| Date & time pickers | `rules/date-time-pickers.md` (todo) | date/time selection |

### Feedback & presentation
| Component | Card | When you see |
|---|---|---|
| Dialogs | `rules/dialogs.md` | alert dialog, full-screen dialog, confirmation |
| Bottom sheets | `rules/bottom-sheets.md` | modal/standard sheet sliding up |
| Snackbars | `rules/snackbars.md` | transient action/confirmation message |
| Tooltips | `rules/tooltips.md` (todo) | hover/short-press hint |
| Progress indicators | `rules/progress-indicators.md` | loading spinner or bar |

### Navigation
| Component | Card | When you see |
|---|---|---|
| Navigation bar | `rules/navigation-bar.md` | bottom persistent navigation (compact) |
| Navigation rail | `rules/navigation-rail.md` (todo) | side navigation (medium/expanded) |
| Navigation drawer | `rules/navigation-drawer.md` (todo) | modal/standard side navigation |
| Top app bar | `rules/top-app-bars.md` | top title + actions bar |
| Tabs | `rules/tabs.md` | top/bottom tab switchers |
| Search | `rules/search.md` (todo) | search bar, search view |

### Status & layout
| Component | Card | When you see |
|---|---|---|
| Badges | `rules/badges.md` (todo) | notification dots/counts |
| Dividers | `rules/dividers.md` (todo) | thin separating lines |
| Menus | `rules/menus.md` | dropdown/popup menu |

## Cross-cutting rule: the same component everywhere

The rule cards assume the foundations skill was applied first (color roles, state layers, shape, motion, accessibility). If a card contradicts foundations, foundations wins.

## Working with other skills

- **Lookup path**: `m3-orchestrator` → detects component → reads the right `rules/<card>.md`.
- **Auditing**: `m3-audit` reads the relevant cards and reports deviations.
- Cards tagged `(todo)` are not yet written — when you encounter one, treat the M3 component page itself as the reference and apply the general principles from `m3-foundations`.