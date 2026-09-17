# Lists — rule card

A **list** is a vertical arrangement of rows (with leading/trailing content) for displaying a collection of related items.

**Triggers** (stack-agnostic detection signals): `ListView`, `ListTile`, `FlatList`, `<li>`, `ListBody`, `itemBuilder`, `data table` rows misused, `Card`-in-list misuse.

## Rules

1. **List vs table vs card**: lists organize *rows of related items* (contacts, files, settings); tables are for dense tabular data needing column semantics; cards are for richer standalone content blocks. Don't render lists as card piles or tables as lists.
2. **Rows are scannable**: leading content (avatar/icon) aligns, primary text is the row's name, supporting text is secondary; consistent row height per list.
3. **Row actions belong to the row**: swipe/tap affordances, trailing icons, chip-actions — but keep one primary interaction per row obvious.
4. **Selection in lists**: single vs multi selection semantics; selected rows show the check/selected state and state layer.
5. **Long lists**: virtualize (lazy build) — rendering thousands of rows eagerly is a perf anti-pattern; group/segmentation for huge sets.
6. **Divider discipline**: dividers separate structure but too many make rows noise; use whitespace for spacing on light lists (M3 default favors fewer dividers).
7. **Empty/loading behavior**: see `m3-patterns` (empty state, loading) — a list never renders a blank or stuck spinner.

## The why

Lists turn collections into scannable decisions. Consistent row anatomy and one clear interaction per row are what keep them fast to scan.

## Implementation hints

- Detect via triggers. Then check:
- Cards where flat list rows belong (and vice versa) → flag.
- Inconsistent row heights/alignment → flag.
- Multitple competing interactions per row → flag.
- Non-virtualized long list → flag.
- Dense divider walls → flag.
- Blank list state → see patterns.

## Checklist

- [ ] list/table/card choice matches data
- [ ] aligned, consistent rows with clear hierarchy
- [ ] one obvious primary interaction per row
- [ ] selection states named + layered
- [ ] lazy rendering for long lists
- [ ] restrained dividers; full empty/loading coverage