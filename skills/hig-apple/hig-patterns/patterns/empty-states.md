# Empty states — pattern card

The **empty state** is the screen a user hits before there's content: no items yet, no search results, no messages, an empty inbox or cart. It is the first impression for new users and the recovery point after filtering.

> Note: "Empty" here covers both *no data at all* (onboarding-ish) and *no matches for a search/filter* — they share the same DNA.

## Structure

1. **Say what would be here.** One clear, short message naming the missing thing ("No trips yet", "No results for “Kinshasa”").
2. **Explain why it's empty** when useful (only not obvious on first-run vs after filtering).
3. **Offer the natural next step.** A primary action that resolves the emptiness ("Find a ride", "Create your first project", "Clear filters"). If no sensible action, at least give the user a way back (clear search, back).
4. **Illustration/icon is optional and meaningful** — it supports the message, it's not decoration or a brand dump. Keep it small and quiet.

## Rules

1. Never a bare blank area with a lone "No items" text in a corner — emptiness states are designed, not defaulted.
2. Never a generic error ("Something went wrong") where an understandable empty reason exists.
3. On list screens, the empty state replaces the list (or is shown inline where the list would be) — it must not look like a bug.
4. If the empty state can resolve itself (data yet to arrive), right-structure it as loading instead (`see patterns/loading`).
5. Accessibility: the message is announced; the action is reachable; icon is decorative (hidden from SR).

## Implementation hints

- Detect: filter with zero results, `isEmpty`, no-data branches, `Else`/ternary returning placeholder, `<template>` for empty, `ListView` with no items, `display: none` fallbacks.
- Catches: empty screen with no action; error copy used for empty; whitespace-only empty state; empty state indistinguishable from a loading bug.

## Checklist

- [ ] names the missing content
- [ ] explains why (when relevant)
- [ ] one clear next-step action
- [ ] illustration optional + quiet
- [ ] never bare/blank
- [ ] not confused with loading or error
- [ ] accessible (announced, reachable action)