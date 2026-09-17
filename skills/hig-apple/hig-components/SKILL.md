---
name: hig-components
description: 'Apple HIG components catalog — a host skill that routes to per-component rule cards. Use when designing, implementing, or reviewing any UI component (buttons, alerts, sheets, navigation, inputs, lists, menus, status, and more) in any technology. Load only the rule card for the component you are working on, not the whole catalog.'
---

# HIG Components

Host skill for Apple's component guidance, made technology-agnostic. **You do not load all rules at once** — you look up the component you are working on and load only that card.

## How to use

1. Identify the component(s) present in the surface or code you're working on.
2. Find the matching rule card in the index below.
3. Read `rules/<card>.md` — that card contains the full rules for the component.
4. Apply or audit against the card's rules, checklist, and implementation hints.

The cards are written in language-agnostic terms: every rule is expressed against *what the component does*, not against any framework. Implementation hints give stack-agnostic detection signals.

## Index of rule cards

### Content
| Component | Card | When you see |
|---|---|---|
| Charts | `rules/charts.md` (todo) | chart, plot, axis, legend |
| Image views | `rules/image-views.md` (todo) | image display, grid of images |
| Text views | `rules/text-views.md` (todo) | paragraphs, read-only text blocks |
| Web views | `rules/web-views.md` (todo) | embedded browser content |

### Layout & organization
| Component | Card | When you see |
|---|---|---|
| Collections | `rules/collections.md` (todo) | grid of items, gallery, card grids |
| Disclosure controls | `rules/disclosure-controls.md` (todo) | expand/collapse, disclosure triangle |
| Labels | `rules/labels.md` (todo) | static caption/descriptor text |
| Lists and tables | `rules/lists.md` | rows, list items, table rows |
| Tab views | `rules/tab-views.md` | top tab switchers, paged content |
| Boxes / Split views / Column views / Outline views / Lockups | segmented panels, divider layout, tree lists, icon+text lockups (todo) |

### Menus & actions
| Component | Card | When you see |
|---|---|---|
| Buttons | `rules/buttons.md` | any clickable action trigger |
| Context menus | `rules/context-menus.md` (todo) | long-press / right-click menu |
| Edit menus | `rules/edit-menus.md` (todo) | cut/copy/paste select menu |
| Toolbars | `rules/toolbars.md` (todo) | action cluster at top/bottom edge |
| Activity views | `rules/activity-views.md` (todo) | share sheet |
| Home Screen quick actions | system experience | shortcut actions (see system) |

### Navigation & search
| Component | Card | When you see |
|---|---|---|
| Navigation bars | `rules/navigation-bars.md` | top title + actions bar |
| Tab bars | `rules/tab-bars.md` | bottom persistent navigation |
| Sidebars | `rules/sidebars.md` (todo) | persistent left/right column nav |
| Search fields | `rules/search-fields.md` | search input |
| Path controls | `rules/path-controls.md` (todo) | breadcrumb navigation |
| Token fields | `rules/token-fields.md` (todo) | chip/tag input field |

### Presentation
| Component | Card | When you see |
|---|---|---|
| Alerts | `rules/alerts.md` | modal warning/confirmation |
| Action sheets | `rules/action-sheets.md` (todo) | choice list from a button |
| Sheets | `rules/sheets.md` | modal card sliding up |
| Popovers | `rules/popovers.md` (todo) | anchored small panel |
| Page controls | `rules/page-controls.md` (todo) | paging dots |
| Panels | `rules/panels.md` (todo) | inspector / utility panel |
| Scroll views | `rules/scroll-views.md` (todo) | scrollable container |
| Windows | platform-specific (todo), see hig-platforms | desktop window |

### Selection & input
| Component | Card | When you see |
|---|---|---|
| Text fields | `rules/text-fields.md` | text entry box |
| Pickers | `rules/pickers.md` (todo) | date/time/value picker |
| Segmented controls | `rules/segmented-controls.md` (todo) | mutually exclusive segment switch |
| Sliders | `rules/sliders.md` (todo) | value slider with thumb |
| Steppers | `rules/steppers.md` (todo) | increment/decrement control |
| Toggles | `rules/toggles.md` | boolean switch |
| Color wells | `rules/color-wells.md` (todo) | color pick button |
| Combo boxes / Clickable text fields / Dropdown | typed input with selectable list (todo) |
| Digit entry / Virtual keyboards | numeric keypad input (todo, see hig-platforms) |

### Status
| Component | Card | When you see |
|---|---|---|
| Progress indicators | `rules/progress-indicators.md` | loading spinner or bar |
| Gauges | `rules/gauges.md` (todo) | radial meter |
| Activity rings | `rules/activity-rings.md` (todo) | fitness rings |
| Rating indicators | `rules/rating-indicators.md` (todo) | star rating display |

### System experiences (see hig-system-experiences)
Widgets, Live Activities, Notifications, Complications, Top Shelf, App Shortcuts, Status bars, Watch faces — cross-platform guidance lives with `hig-platforms`.

## Cross-cutting rule: the same component everywhere

The rule cards assume the foundations skill was applied first (color, spacing, typography, motion, accessibility). If a card contradicts foundations, foundations wins.

## Working with other skills

- **Lookup path**: `hig-orchestrator` → detects component → reads the right `rules/<card>.md`.
- **Auditing**: `hig-audit` reads the relevant cards and reports deviations.
- Cards tagged `(todo)` are not yet written — when you encounter one, treat the HIG page itself as the reference and apply the general principles from `hig-foundations`.