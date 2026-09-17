---
name: m3-patterns
description: 'Material Design 3 (M3) user-experience patterns made stack-agnostic. Use when designing flows and experiences — onboarding, data entry, confirming and saving, error handling, empty states, loading, notifications, notifications permissions, settings — in any technology. Complements m3-components (elements) and m3-foundations (visual + token language) with the experience layer.'
---

# M3 Patterns

Material 3's experience patterns — the flows that string components together into a coherent experience. The components skill answers *"how should this element look and behave"*; patterns answer *"how should this flow be structured."*

## How to use

1. Identify the flow you are designing or reviewing (onboarding? data entry? error? empty?).
2. Load the matching pattern card from `patterns/<name>.md`.
3. Apply the pattern's structure, then satisfy the specific component cards it touches.

## Pattern index

| Pattern | Card | Trigger signals |
|---|---|---|
| Entering data | `patterns/entering-data.md` | form, wizard, data collection screen |
| Confirming and saving | `patterns/confirming-saving.md` | save, confirm dialog, committed choices |
| Error handling | `patterns/errors.md` | failures, retries, validation errors |
| Empty states | `patterns/empty-states.md` | no data, no results, initial state |
| Loading | `patterns/loading.md` | async content, list loading, progress across screens |
| Notifications & permissions | `patterns/notifications.md` (todo) | permission prompts, notification settings |
| Settings | `patterns/settings.md` (todo) | preferences screens, dense list of switches |
| Onboarding | `patterns/onboarding.md` (todo) | first-run, welcome, walkthrough |
| Searching | `patterns/searching.md` (todo) | search flow, filter, browse-and-refine |
| Undo and redo | `patterns/undo-redo.md` (todo) | undoable actions, snackbar undo |

## Cross-cutting pattern rules

1. **One flow, one intent.** Each pattern serves a single user intent; stitching multiple intentions into one screen (fit sign-up, features tour, and permission asking together) reads as noise.
2. **Progressive disclosure.** Show what's needed now; reveal complexity as the user engages (see m3-foundations).
3. **Be forgiving.** Every flow supports going back, fixing, and re-entering. Trapping the user in a flow is the perennial antipattern.
4. **Consistency across the app.** Once you choose a pattern for a kind of task, use it for all such tasks — mixing pattern dialects across screens is disorienting.
5. **Toast/snackbar discipline.** Confirmations are snackbars, not dialogs; errors that block progress are inline + somewhere the user can act.

## Working with other skills

- `m3-components` supplies the element rules each pattern leans on (forms → text-fields; confirmations → dialogs; navigation → nav components).
- `m3-foundations` sets the visual + token + accessibility standards the patterns assume.
- `m3-audit` checks patterns as part of the deviation list; `m3-orchestrator` detects flow code and routes to the pattern cards.