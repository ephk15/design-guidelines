# Navigation bar — rule card

A **navigation bar** provides persistent access to 3–5 primary destinations at the bottom of the screen (compact width). Distinct from: tabs (same-level content switching), navigation rail/drawer (wider layouts), top app bars.

**Triggers** (stack-agnostic detection signals): `NavigationBar`, `BottomNavigationBar`, `bottom nav`, `NavigationBarTheme`, `persistent` bottom destinations, `label = always`.

## Rules

1. **3–5 destinations, top-level only**: navigation bar holds the app's primary top-level destinations — never secondary pages (settings buried? fine; settings as a bar item? reconsider hierarchy).
2. **One selected destination at a time**, visibly: active = filled primary icon + indicator/pill + label; inactive = outlined glyph + secondary tone. Selection is color+shape, not just tint.
3. **Labels always visible** (M3 default): labels under icons; don't hide them at compact width.
4. **Avoid badging everything**: badges/reserved for genuinely new/unread items (see badges rule card), not decoration.
5. **State feedback**: each item has state layers (hover/focus/pressed); selected state persists.
6. **Chart consistency**: bar placement + icons + labels stay consistent app-wide; switching styles of bar items between screens is disorienting.
7. **Accessibility**: each item announces selected/unselected (role=tab, aria-selected); labels are readable; ≥ 48dp targets.

## The why

The navigation bar is the map of the app at phone scale. Consistency and clear selected-state are what let users know where they are at a glance.

## Implementation hints

- Detect via triggers. Then check:
- >5 destinations → flag (fold into drawer/secondary).
- Secondary/none top-level destinations in bar → flag.
- Selected state by color only, no filled/indicator/icon change → flag.
- No labels → flag.
- Items not announced → flag.

## Checklist

- [ ] 3–5 top-level destinations
- [ ] clear selected/unselected (color + shape + label)
- [ ] labels always visible
- [ ] badges only for real unread/new
- [ ] state layers on items
- [ ] SR announces selection