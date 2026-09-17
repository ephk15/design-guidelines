# Search fields — rule card

Search lets people find content or an action among many. The **search field** is the entry point; great search is forgiving and fast.

**Triggers**: `SearchBar`, `SearchField`, `SearchAnchor`, `searchable`, `searchController`, `TextField` with type search, `type="search"`, `placeholder` "Search…", `lookup`, `filter field`, `SearchDelegate`, `showSearch`, mobile search with icon.

## Rules

1. **A real entry point and a real result path.** The field exists where users expect it (top of the screen/section, or a dedicated search view) and its activation leads to a results experience, not a dead end.
2. **Search bar at top, results update live.** Filter as you type with a tiny debounce; never require a submit button for live search. For search-as-command (file actions), results show actions inline.
3. **Clear affordance.** A one-tap clear (X) inside the field; a cancel/close that returns to context. Empty-after-clear restores the pre-search state.
4. **The placeholder tells the scope** ("Search images", "Search people"), not a tautology ("Type here").
5. **No results ≠ dead end.** Show "No results for “query”" with a sensible next step (check spelling, reveal broader scope), not a blank.
6. **Recent & suggested terms** help when the space is mature: recents are clearly marked as such and removable.
7. **Keyboard matches input** (text; numeric only for numeric-identifiers search).
8. **Accessible**: label/placeholder announced; results announced for screen readers; focus jumps to field on activation.

## The why

Search is an escape hatch for people who got lost in navigation. Its job is to make finding *effortless* — which means forgiving input, live results, and a graceful empty case. Any friction there multiplies frustration because going back to navigation costs time.

## Implementation hints

- Detect triggers above. Check:
  - Submit-required live search → flag (debounced-live is expected).
  - Clear affordance present + restores prior state → else flag.
  - No-results view with actionable copy → else flag (blank is a trap).
  - Placeholder says scope, not "type here" → else flag.
  - Recents removable when present.
  - Keyboard type; SR announcement of results/empty.

## Checklist

- [ ] lives where users expect it
- [ ] live update (debounced), no submit required
- [ ] clear + cancel back to context
- [ ] scoped placeholder
- [ ] instructive no-results state
- [ ] recents removable (when present)
- [ ] accessible announcements