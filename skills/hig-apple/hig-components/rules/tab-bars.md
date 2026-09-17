# Tab bars — rule card

A **tab bar** is the bottom-edge, persistent navigation that lets the user switch between the app's top-level destinations. It stays fixed while content changes above it.

**Triggers**: `BottomNavigationBar`, `bottomNavigationBar`, `NavigationBar`, `TabBar`, `tabBar`, `BottomNavigationBarItem`, `TabBarItem`, `tab bar`, `bottom-nav`, `navigation bar` with `destination`s, `Material`-bottom-nav, `Tabs`, `<nav>` fixed-bottom.

## Rules

1. **Tabs are navigation, not actions.** A tab switches top-level destinations. Primary app actions (compose, add, create) **do not belong in the tab bar** — they are toolbar/primary buttons elsewhere. This is the most common Apple anti-pattern violation.
2. **3–5 tabs.** More than 5 top-level destinations means the information architecture needs work, not more tabs. Keep it scannable.
3. **Every tab earns its place.** Each represents a genuinely distinct, frequently used top-level section. If a tab is rarely used or is a detail of another section, it should not be a tab.
4. **Order by importance/frequency.** The most-used destination first (reading order / left-first); the first tab is usually the app's home.
5. **Selected state is visually obvious** — emphasis (filled icon, accent) marks the current tab. Unselected tabs remain visible so the user knows what else exists.
6. **Consistent label + icon.** Each tab has a label and an icon; label text is short (typically 1 word, ≤ 2). Icons must be recognizable (see foundations).
7. **No badges out of context.** Badges (counts/dots) are permitted but meaningful only on tabs where they make sense (activity/inbox).
8. **Tab positions are fixed** — dragging to reorder or referencing "current" elsewhere breaks the mental model.

## The why

The tab bar is the app's map. It answers "where can I go?" at every moment. Preserving its structure (fixed, few, readable) is how navigation stays calm; repurposing it for actions breaks the map.

## Implementation hints

- Detect via triggers above. Count destinations:
  - >5 → flag, suggest hierarchy simplification.
  - Contains an action-style item (add/compose/new with a distinctive float) → flag as action-not-navigation (this is the #1 catch).
  - Labels >2 words or sentence case oddities → flag.
  - Selected-state emphasis exists and is not color-only → else flag.
  - Order: home/destination-first check.
- Cross-check with navigation bars: primary actions should live in the top bar, not the tab bar.

## Checklist

- [ ] 3–5 tabs
- [ ] tabs are destinations, not actions
- [ ] order = importance
- [ ] clear selected state (not color-only)
- [ ] short labels + recognizable icons
- [ ] no reordering/dynamic tabs
- [ ] badges only where meaningful