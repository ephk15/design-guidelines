# Chips — rule card

A **chip** is a compact element that represents an input, attribute, filter, or action. Material offers four types: assist (an action that triggers in context), filter, input, and suggestion.

**Triggers** (stack-agnostic detection signals): `Chip`, `FilterChip`, `AssistChip`, `InputChip`, `SuggestionChip`, `ChipTheme`, `Wrap` of tag-like pills, `chips`, `<mat-chip`.

## Rules

1. **Pick the right type for the job**: filter (toggleable filter selection), input (entered value with delete affordance), suggestion (recommended option inline), assist (contextual action). Using one type for another's job muddles affordance.
2. **Chips are a set, not a menu**: they present *co-existing options* (multi-select filters, tags), never a primary action ladder — that's what buttons are for.
3. **Selection feedback**: selected chips show the checkmark/leading icon + selected container color + state layer; state silently reverts when deselected (filter) or persists (tag).
4. **Compact and scannable**: short labels (1–4 words); chips wrap naturally (`Wrap`), never truncate.
5. **Consistent sizing/typography** via chip tokens; touch target ≥ 48dp overall (chip visual may be smaller with extended hit area).
6. **Accessibility**: chips announce selected/deselected and type; deletable/dismissible chips announce the action.

## The why

Chips are the canonical M3 device for *many related choices*. Type consistency + multi-select semantics are what keep chips from being mistaken for menu buttons.

## Implementation hints

- Detect via triggers. Then check:
- Assist/suggestion/filter/input misuse (e.g. filter used as action button) → flag.
- Chips used as the only navigation/primary action → flag, prefer buttons.
- Selected chip missing checkmark/selection state → flag.
- See which type by usage: multi-select filter vs tag entry vs inline action.

## Checklist

- [ ] correct chip type per job
- [ ] chips present co-existing options, not primary actions
- [ ] selected state: checkmark + container color + layer
- [ ] labels short, chips wrap
- [ ] ≥ 48dp hit area, consistent tokens
- [ ] selections announced to screen readers