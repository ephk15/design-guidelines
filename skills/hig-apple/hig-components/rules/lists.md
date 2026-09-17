# Lists — rule card

A **list** is a vertical stack of rows, each row presenting one item (data, an option, a navigation entry). Lists are the backbone of content-heavy Apple interfaces.

**Triggers**: `ListView`, `ListTile`, `ListTile(title:`, `FlatList`, `VirtualizedList`, `<li>`, `ul`, `ol`, `TableRow`, `tableView`, `List`, `<select>`-like rows, `Repeat`/for-loop rendering rows, `.listItem`.

## Rules

1. **Rows are consistent.** Same row height pattern, same paddings, same left/right alignment across the list. Per-row improvisation reads as broken.
2. **Standard row anatomy:** leading content (icon/thumbnail), primary text (title), optional secondary text (subtitle), trailing content (chevron, value, action) — aligned in stable columns.
3. **Clear tap feedback**: rows that are interactive respond visually to press, and their affordance (chevron/action) signals tappability. A row that looks tappable but isn't (or vice versa) is a trap.
4. **Dense lists keep to ~44pt+ minimum row height** (touch) for comfort; larger for readability.
5. **Long lists need loading/perf discipline:** lazy rendering, placeholders/avatars that don't shift layout, and correct scroll/resume position.
6. **Grouped lists use section headers** to label groups; headers are substantive (not decorative), short, and uppercase-in-caption-style where the platform uses it.
7. **Empty state expresses emptiness** — never a blank area or "no items" tucked in a corner: say what's here and give a path forward (see hig-patterns: empty/onboarding).
8. **Separators** (hairlines) are subtle; dense lists may omit them within groups. Avoid loud box borders around every row.
9. **Destructive/contextual actions** are hidden by default (swipe to reveal or menu), not permanently visible — unless the list is a management UI where actions are core.
10. **Selection models are explicit:** single-select, multi-select, or none. Selected rows show clear emphasis (accent) and multi-select shows count + bulk actions contextually.

## The why

Lists get read fast and scanned persistently. Consistency in rows is what makes a list scannable at all; every broken rhythm forces the eye to slow down and decode.

## Implementation hints

- Detect triggers above. Then check:
  - Per-row structure variations → flag.
  - Tappable vs not: any row with press feedback but no handler, or chevron on non-clickable → flag.
  - Row heights mixed without reason → flag.
  - Lazy-loading for long lists; skeletons avoid layout shift.
  - Interactivity: swipe/menu present when long-press only → acceptable, ensure discoverable.
  - Group headers present for sectioned data → else flag.
  - Row min-height ≥ 44pt on touch → else flag.

## Checklist

- [ ] consistent row anatomy + alignment
- [ ] tap feedback matches interactivity
- [ ] min ~44pt rows (touch)
- [ ] long lists: lazy + stable layout + position preserved
- [ ] meaningful section headers
- [ ] honest empty state
- [ ] hairline separators, no heavy boxes
- [ ] explicit selection model with emphasis