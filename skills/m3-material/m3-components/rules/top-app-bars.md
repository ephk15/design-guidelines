# Top app bars — rule card

A **top app bar** provides a screen with its identity (title/logo), navigation affordances, and primary actions at the top. Material: center-aligned, small, medium, and large variants.

**Triggers** (stack-agnostic detection signals): `AppBar`, `AppBarTheme`, `LargeAppBar`, `MediumAppBar`, `app-bar`, `<header`, `Toolbar`, `navigationBar` at top, `topbar`.

## Rules

1. **Variant per hierarchy**: small bar = default for most screens (title + actions); large/medium = hero title for top-level/landing surfaces. Don't stack a large on every screen or the hierarchy dies.
2. **Title is hierarchically meaningful**: the title states the screen's identity; large variants collapse to small on scroll (animations respect motion rules).
3. **Actions live Pо the bar**: primary actions (share, add) sit at the trailing edge; overflow (more menu) holds secondary actions. Never stuff every action into the bar — that's what the more-menu abstracts.
4. **Navigation affordance**: on a nested screen show back/up navigation; on the root, show the drawer/menu affordance or brand.
5. **State & theming**: bar uses surface tokens at its elevation level (scroll shows scrim/surface tint transition); status bar color harmonizes.
6. **Accessibility**: title labels the screen; action buttons carry names; touch targets ≥ 48dp.

## The why

The top app bar orients the user (where am I, what can I do). Variant consistency + restrained actions keep it a frame, not a feature.

## Implementation hints

- Detect via triggers. Then check:
- Large/medium bars on non-top-level screens → flag.
- Too many visible actions (no overflow) → flag.
- Missing back/up on nested screen → flag.
- No scroll elevation/scrim transition → flag.

## Checklist

- [ ] variant matches hierarchy
- [ ] large/medium collapse on scroll with motion
- [ ] actions: primary in bar, secondary in menu
- [ ] back/up or brand affordance present
- [ ] elevation/scrim transition on scroll
- [ ] named actions, ≥ 48dp