# Cards — rule card

A **card** is a container that groups related content and actions about a single subject. Material offers elevated, filled, and outlined cards.

**Triggers** (stack-agnostic detection signals): `Card`, `CardTheme`, `card-`, `<mat-card`, `<ion-card`, `Container`+`borderRadius` used as content grouping, `ExpansionTile`.

## Rules

1. **One subject per card.** Each card presents a single idea/entity; stitching multiple subjects into one card hides structure.
2. **Choose the variant deliberately**: elevated (floats, for expandable/rich content), filled (neutral grouping, low emphasis), outlined (subdued grouping in dense layouts). A variant is a *hierarchy signal* — use consistently.
3. **Content over chrome**: padding per the M3 spacing system, restrained elevation/shadow; the card's job is to organize, not decorate.
4. **Clickable cards**: the whole card (or an explicit affordance) is tappable with a state layer (hover/focus/pressed); no layout jump on press. Don't make a whole card clickable when an inner action is the primary one — prefer an explicit button.
5. **Internal actions** follow component rules (buttons, chips) — a card never invents its own action styling.
6. **Responsive behavior**: card grids reflow across breakpoints; don't hard-code row counts.
7. **Accessibility**: grouped content has an accessible grouping name where screen readers need context; clickable cards announce clickable.

## The why

Cards provide scannable grouping. Consistent variants + restrained chrome keep cards organizing rather than competing with their content.

## Implementation hints

- Detect via triggers. Then check:
- Cards with multiple unrelated subjects → flag.
- Mixed variants with no hierarchy reason → flag.
- Whole-card tap without state layer, or card-as-button vs inner buttons ambiguity → flag.
- Hard-coded columns ignoring breakpoints → flag.

## Checklist

- [ ] one subject per card
- [ ] variant chosen per hierarchy consistently
- [ ] content-chrome restraint (spacing system, low elevation)
- [ ] clickable cards have state layers and no jump
- [ ] inner actions use component rules
- [ ] card grids reflow at breakpoints