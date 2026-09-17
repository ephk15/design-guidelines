# Progress indicators — rule card

A **progress indicator** keeps the user informed that content is loading. Material: linear (determinate/indeterminate) and circular.

**Triggers** (stack-agnostic detection signals): `ProgressIndicator`, `CircularProgressIndicator`, `LinearProgressIndicator`, `<progress`, `spinner`, `skeleton`, `shimmer`, `loading`, `isLoading`.

## Rules

1. **Right indicator for the shape**: full-screen/page loads → linear or centered circular; inline/section → contained/small; determinate when a known value/progress exists, indeterminate when the wait length is unknown. Skeletons fit content-shaped loads (lists, cards).
2. **Never blank**: while awaiting, the interface shows something honest — a progress indicator, skeleton with real shape, or prior content dimmed. A blank or stuck-freeze is a bug, not a loading state.
3. **Stable layout**: indicators that appear/disappear without reserving space cause layout jumps — placeholder space or inline rows keep the page still.
4. **Perceive speed & fail**: optimistic UI where near-certain; every loading path ends in success or an in-place error with recovery (no endless spinner).
5. **Constrained animation**: progress motion is fast, muted, non-interrupting; respects reduced motion (indeterminate cycles may be slowed/static).
6. **Determinate must mean it**: a determinate indicator that freezes at 100% forever (or never moves) is a lie — fix by binding to real progress or switching to indeterminate.
7. **Accessibility**: loading announced (aria-busy, role=progressbar with value where determinate).

## The why

Progress is the interface's honesty under load. It exists to make *waiting* legible and keep users in control — the moment it lies (blank, endless, jumping), trust breaks.

## Implementation hints

- Detect via triggers. Then check:
- Whole-view spinner instead of skeleton for content → flag.
- Layout jump when loading rows arrive → flag.
- No error branch → infinite spinner on failure → flag.
- Spinner on micro-actions → flag (see feedback).
- Determinate stuck near-complete → flag.
- Not announced / reduced-motion ignored → flag.

## Checklist

- [ ] correct indicator kind + determinism
- [ ] something visible during load (never blank)
- [ ] layout stable (reserved space, no jump)
- [ ] ends in success or in-place error + retry
- [ ] respects reduced motion
- [ ] busy state announced