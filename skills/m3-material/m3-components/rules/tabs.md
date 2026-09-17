# Tabs — rule card

**Tabs** switch between same-level views within a page (content negotiation). Distinct from navigation (destinations) and from steppers (sequential tasks).

**Triggers** (stack-agnostic detection signals): `TabBar`, `TabController`, `TabView`, `tab`, `<tab-list`, `role="tablist"`, `TabPageView`, top tabs, bottom tabs.

## Rules

1. **Tabs organize views of the same content**, not unrelated destinations (that's navigation). If tabs switch "modules" of the app, reconsider — nav components are for destinations.
2. **Every tab has a clear label** (optionally icon-wide); selected tab has an indicator (under-line/pill) + active color, unselected is secondary tone. Selection by color+indicator.
3. **Tab labels are short and distinct**: no truncated/overflowing labels; fixed tabs fit on one line; scrollable for many.
4. **Content is switchable without surprises**: switching tabs preserves scroll/state where sensible; don't re-load the whole screen on every switch (render lazily).
5. **State layers**: pressed/hover/focus on tabs; the effect is visible.
6. **Swipe between tabs** is allowed where platform conventions support it, with accessibility (announced, keyboard-switchable).
7. **Accessibility**: `role=tab`, `aria-selected`, keyboard arrows move focus between tabs, labels announced.

## The why

Tabs answer "show me the other view of this thing." Clear selection + consistent labels are what make a tab bar navigable without thinking.

## Implementation hints

- Detect via triggers. Then check:
- Tabs used as app destinations → flag, prefer nav components.
- Selected tab not distinguishable by indicator/color → flag.
- Labels truncated or duplicate → flag.
- Full re-load/re-render on switch → flag.
- Not keyboard/ARIA accessible → flag.

## Checklist

- [ ] tabs switch same-level content
- [ ] selected/unselected states via indicator + color
- [ ] short, distinct, non-truncated labels
- [ ] state preserved, lazy rendering
- [ ] swipe + keyboard/ARIA support
- [ ] labels announced