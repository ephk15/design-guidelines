# Navigation bars — rule card

A **navigation bar** is the top-edge bar that orients the user: it carries the screen title, and may carry primary actions for that screen. It's the anchor of "where am I?".

**Triggers**: `AppBar`, `appBar`, `NavigationBar` (top), `navigationBar`, `TopAppBar`, `Toolbar`, `NavBar`, `<header`, `topbar`, `title bar`, `SliverAppBar`, scroll-aware top bars, iOS-style large-title headers.

## Rules

1. **The title says where you are.** The bar's title is the screen's name — concrete and short. Branding text in place of a title is a missed orientation (brand belongs in a dedicated space).
2. **Context informs title style.** A Level-1 screen (top destination) may use a larger/scrollable title; a pushed detail screen uses a compact title + an explicit back affordance. Title scale should map to hierarchy, not decoration.
3. **Back affordance present when pushed.** Any screen that isn't a top destination must have a clear back control; it should read "previous context", not "app home" (label or chevron appropriate to platform).
4. **Actions count stays low and purposeful.** 1–3 actions max in a nav bar; more belongs in a menu or a toolbar. Primary screen action can sit here (compose, add) — but never in the tab bar.
5. **Actions must be recognizable** (icons systems-aware) and `see hig-components/buttons`. Never overload the right edge beyond thumb reach.
6. **Scroll behavior is tasteful.** Larger titles collapse gracefully as you scroll; bar's background may become translucent/material when content scrolls beneath — never clip content, never cause jumps.
7. **Accessibility:** title announced as screen name; actions announced; back labeled for screen readers.

## The why

The navigation bar is the constant proof of orientation in a paged app. It answers the two questions everyone asks silently: *where am I* (title/back) and *what can I do here* (actions). Both must stay crisp, or the whole app feels lost.

## Implementation hints

- Detect triggers above. Check:
  - Title present and equals the screen's name → else flag (brand-as-title, generic "Home", missing).
  - Back affordance on every non-top screen → else flag.
  - Action count >3 → flag (suggest overflow menu).
  - Action inside tab-bar AND duplicated in nav bar → flag duplication.
  - Large-title/scroll behavior exists on level-1 → else usage note; collapsing doesn't jump layout.

## Checklist

- [ ] concrete screen-name title
- [ ] title scale maps to hierarchy
- [ ] back affordance on pushed screens
- [ ] ≤3 purposeful actions
- [ ] primary action not duplicated in tab bar
- [ ] graceful scroll behavior