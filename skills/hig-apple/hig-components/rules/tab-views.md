# Tab views — rule card

A **tab view** is a top-edge control that switches between mutually exclusive content panes within the *same* screen or section — distinct from the tab *bar* (app-level navigation).

**Triggers**: `TabBar` (top), `TabView`, `TabController`, `tabController`, `TabBarView`, `DefaultTabController`, `SegmentedButton`-style tabs, `tabs`, `TabPanel`, `role="tab"`, top-anchored tabs.

## Rules

1. **Tabs are for related content, not app structure.** A tab view splits one section into sub-views that share context. If contents belong to different top-level areas, that's a navigation problem — not tabs.
2. **Few, constant tabs.** 2–5 tabs. Don't let tab sets grow dynamically per item — the structure should feel stable.
3. **Clear selection:** the active tab is visibly emphasized (accent underline/fill), inactive are readable but secondary. State must not depend on color alone.
4. **Tab labels are short and concrete** — the noun of the content ("Overview", "Stats", "Settings"). Avoid verbs that read as actions.
5. **Switching preserves recognition.** When you switch, the user should not be surprised by *where* and *what* re-render. If tab content is heavy, indicate load, don't blank.
6. **Swipe navigation optional, expected when scrollable.** When the panes swipe horizontally, the gesture must not conflict with inner horizontal scrolling.
7. **Accessibility:** each tab is focusable/announced with selected state; arrow keys switch tabs where keyboard is primary.

## The why

Tab views organize *within* a space. Their promise is "same place, different facet" — consistency across panes and a stable, small set is what keeps that promise coherent.

## Implementation hints

- Detect triggers above. Check:
  - Do the tabs represent distinct top-level areas? → flag as misplaced (should be tab bar / navigation).
  - Count >5 → flag.
  - Selection emphasized beyond color → else flag.
  - Labels: verb-like or generic ("Info", "More" vague) → flag.
  - Pane switch: blank screen or full reload → flag; suggest skeleton/fade or preserve scroll.
  - Keyboard/focus handles selected tab → else flag.

## Checklist

- [ ] tab set is constant and small (2–5)
- [ ] contents share the same section context
- [ ] selection obvious, not color-only
- [ ] short concrete labels
- [ ] no jarring re-render on switch
- [ ] accessible (focus + selected announced)