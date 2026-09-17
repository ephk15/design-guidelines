---
name: hig-patterns
description: 'Apple HIG user-experience patterns made stack-agnostic. Use when designing flows and experiences — onboarding, feedback, loading, searching, entering data, undo/redo, notifications, managing accounts, settings, and more — in any technology. Complements hig-components (elements) and hig-foundations (visual language) with the experience layer.'
---

# HIG Patterns

Apple's experience patterns — the flows that string components together into a coherent experience. The components skill answers *"how should this element look and behave"*; patterns answer *"how should this flow be structured."*

## How to use

1. Identify the flow you are designing or reviewing (onboarding? feedback? data entry?).
2. Load the matching pattern card from `patterns/<name>.md`.
3. Apply the pattern's structure, then satisfy the specific component cards it touches.

## Pattern index

| Pattern | Card | Trigger signals |
|---|---|---|
| Onboarding | `patterns/onboarding.md` (todo) | first-run, welcome, walkthrough, set-up |
| Entering data | `patterns/entering-data.md` | form, wizard, data collection screen |
| Feedback | `patterns/feedback.md` | errors, confirmations, success messages |
| Loading | `patterns/loading.md` | async content, list loading, progress across screens |
| Searching | `patterns/searching.md` | search flow, filter, browse-and-refine |
| Managing accounts | `patterns/managing-accounts.md` (todo) | sign-in, sign-up, account settings, profile |
| Managing notifications | `patterns/managing-notifications.md` (todo) | notification settings, permission prompts |
| Undo and redo | `patterns/undo-redo.md` (todo) | undoable destructive actions, redo |
| Updating content / Refresh | `patterns/refreshing.md` (todo) | pull-to-refresh, refresh button |
| Empty states | `patterns/empty-states.md` (todo) | no data, no results, initial state |
| Modality | `patterns/modality.md` (todo) | when to be modal vs inline vs sheet |
| Advertising / Paywalls | brand constraint (note) | upsells, subscriptions |
| Widgets / Live Activities | see hig-system-experiences | home-screen widgets, live updates |

## Cross-cutting pattern rules

1. **One flow, one intent.** Each pattern serves a single user intent; stitching multiple intentions into one screen (fit sign-up, features tour, and permission asking together) reads as noise.
2. **Progressive disclosure.** Show what's needed now; reveal complexity as the user engages (see HIG foundations).
3. **Be forgiving.** Every flow supports going back, fixing, and re-entering. Trapping the user in a flow is the perennial Apple antipattern.
4. **Consistency across the app.** Once you choose a pattern for a kind of task, use it for all such tasks — mixing pattern dialects across screens is disorienting.

## Working with other skills

- `hig-components` supplies the element rules each pattern leans on (forms → text-fields; confirmations → alerts; navigation → nav bars/lists).
- `hig-foundations` sets the visual + motion + accessibility standards the patterns assume.
- `hig-audit` checks patterns as part of the deviation list; `hig-orchestrator` detects flow code and routes to the pattern cards.