# Empty states — pattern card

The **empty state** is the designed moment when there is nothing to show: no items, no results, first-run. It is not "no UI" — it is an opportunity to guide the next step.

## Structure

1. **Every list/collection has an empty state.** `ListView` with zero rows renders something intentional, never a blank page.
2. **Categories of empty** (different copy/action each):
   - **First-use** (no data yet) → invite the first action (onboarding-ish): "No [items]. Let's add your first one." + primary action.
   - **All done / cleared** → confirm the cleared state, keep it calm ("No [items] left" + maybe undo).
   - **No search results** → say what was searched/why no results ("Nothing for 'xyz'") + suggest adjusting filters.
   - **Filtered to zero** → offer to clear filters.
3. **An empty state is actionable**: show the *next* action a user can take (primary button), not just an apology.
4. **Illustration/layout**: an intentional illustration of the empty concept + concise copy; keep it on-brand and non-sad. The illustration or icon must not look like an error (red/alert).
5. **Empty-with-context**: if the page legitimately has nothing because of a state (e.g., "recent" section), state why and what fills it.
6. **Accessibility**: the empty state reads coherently (heading + body + button), as-is focusable where primary action matters.

## Cross-layer rules

- CTA styling → `see components/buttons`.
- When the empty state implies loading → `see patterns/loading`.
- First-run flows → `see patterns/onboarding` (todo).

## Implementation hints

- Detect: `isEmpty`, no-data ternary, empty-list conditional, `!items.length`, search with zero matches, filter with zero.
- Common catches: blank/`null` render when list is empty; "No results" without a suggestion or clear-filters; funnel of empty → sad icon + no action.

## Checklist

- [ ] intentional empty state for every collection/search/filter
- [ ] category-appropriate copy (first-use vs no-results vs cleared)
- [ ] actionable: a primary next step
- [ ] on-brand, non-error-looking illustration or icon
- [ ] clear-filters affordance when filters cause zero
- [ ] accessible heading + CTA