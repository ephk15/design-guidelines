# Adaptive layout — platform extension

The **adaptive** extension covers Material 3's breakpoint system: how the same content rearranges at compact, medium, and expanded widths, and how density participates.

## Breakpoints (window width classes)

| Class | Width | Typical changes |
|---|---|---|
| Compact | < 600dp | Navigation bar (bottom); single column; full-screen dialogs; sheets edge-to-edge |
| Medium | 600–840dp | Navigation rail; 2-column layouts; dialogs sized; side sheets may appear |
| Expanded | > 840dp | Navigation drawer; multi-column; side sheets standard; larger dialogs/sheets |

## Rules

1. **Design per class, don't stretch one** — compact is not "phone artboard scaled." Each class gets its own arrangement of the *same* content (rearrange, re-scale, re-rank — never just re-size).
2. **Navigation morphs**: bottom navigation bar → navigation rail → navigation drawer as width grows. Keep the same top-level destinations; only the surface changes.
3. **Content columns** follow the class: 1 column compact, 2 medium, 3+ expanded; content containers size to columns, not telephone widths.
4. **Modal surfaces behave per class**: sheets sit edge-to-edge on compact; become narrower/centered with scrim at medium/expanded. Dialogs cap their width on larger screens.
5. **Density**: comfortable is default; compact/comfortable density tokens exist for power surfaces. Density is a token switch, not squish-to-fit.
6. **Targets stay ≥ 48dp** at every class (expanded ≠ smaller targets).
7. **Safety**: content avoids clipping/overflow at every class; test at the boundary widths, not just three pixels-wide spots.
8. **Accessibility at every class**: order, focus order, and semantics reflow with the layout — don't reorder visually but leave keyboard order stale.

## Implementation hints

- Detect: `MediaQuery`, `LayoutBuilder`, `Breakpoint`, `breakpoint`, window width, `maxWidth`, `size.width`, `WindowSizeClass`, responsive adapters.
- Check: one-fixed-layout codebase for multiple targets → flag.
- Check: nav component not swapping across classes (bar on tablet width) → flag.
- Check: sheet/dialog stretching full width at expanded → flag.
- Check: keyboard/Tab order mismatched with visual reorder → flag.

## Checklist

- [ ] layout authored per size class (not stretched)
- [ ] navigation morphs per class
- [ ] columns per class; no full-width modals on large screens
- [ ] density via tokens (comfortable default)
- [ ] ≥ 48dp targets at all classes
- [ ] no overflow at boundary widths
- [ ] focus/semantics order matches visual reorder