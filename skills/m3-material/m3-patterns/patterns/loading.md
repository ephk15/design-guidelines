# Loading — pattern card

The **loading** pattern governs how the UI behaves while content or an operation is pending. It's the bridge between "empty" and "ready".

## Structure

1. **Stage the wait correctly:** determine *what* loads (new view, refresh, background sync, submit) and *how long* it can take. Short < 1s: immediate result or minimal progress. Medium: skeleton or spinner with stable layout. Long (> 4–5s): real progress + cancel + keep context.
2. **Never blank.** While async work runs, the interface is populated with something honest: skeleton with real shape, prior content dimmed with a spinner, or an inline progress row. Indeterminate surfaces, not empty/slab.
3. **Stable layout.** Content that arrives must not shift the page: reserve space (skeleton matches dimensions), pre-size rows/avatars, fix the scroll position.
4. **Perceive speed:** immediate feedback on action (pressed state), optimistic UI where the outcome is nearly certain, skeleton before network resolves.
5. **Fail visibly** — the loading pattern ends in success *or* an in-place failure with a recovery path (retry button, message). An endless spinner is a lie.

## Cross-layer rules

- Skeleton vs spinner vs determinate progress → `see components/progress-indicators`.
- Failure copy → `see patterns/errors` and foundations writing.
- Refresh (pull-to-refresh, refresh affordance) → `see patterns/refreshing` (todo).

## Implementation hints

- Detect: async loads, fetch/await blocks, `loading` boolean, `isLoading`, `FutureBuilder`, `StreamBuilder`, `useEffect`+fetch, Spinner/ProgressIndicator usages, skeletons/shimmer, pull-to-refresh.
- Common catches: whole-view spinner instead of skeleton; layout jump when rows load; no error branch (infinite spinner on network fail); spinner on micro-actions; full-page skeleton for partial load.

## Checklist

- [ ] something visible during load (never blank)
- [ ] skeleton/shape matches final layout (no jump)
- [ ] correct progress kind for the wait stage
- [ ] optimistic where safe
- [ ] in-place error + retry, no endless spinner
- [ ] screen-reader announcement of busy/finished