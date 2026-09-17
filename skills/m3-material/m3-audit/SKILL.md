---
name: m3-audit
description: 'Audit a surface or an entire project against the Material Design 3 (M3) rules (m3-material skillset), stack-agnostic. Produces a sorted list of deviations with severity, the rule violated, and a proposed fix — never a bare score. Supports delta audits to track regressions between runs and a correction plan the user accepts/rejects/assumes. Use when asked to review, audit, or check M3/Material 3 compliance of an interface or codebase.'
---

# M3 Audit

The guardrail against drift on large projects. The audit reads the relevant rule cards (`m3-components/rules/*.md`, `m3-patterns/patterns/*.md`, `m3-platforms/platforms/*.md`, `m3-foundations/SKILL.md`), examines the surface/code, and produces a **prioritized list of deviations** — the thing to act on.

Core principle: the audit is a **partner, not a judge**. It flags, proposes, and remembers the choices you accept.

## When to run

- On a new screen before it ships.
- On a project at meaningful milestones (the fix for *"the AI drifts as the project grows"* is running the audit regularly).
- On a single component you just built (lightweight: load only that component's card).
- Before/after a big refactor.

## How to run

1. **Identify the target.** A whole project? A single screen? Specific components? Either the caller tells you, or you infer by scanning the codebase for UI code.
2. **Identify the targets' sizes/platforms** (config files, breakpoint usage, platform folders) — loads the right `m3-platforms/platforms/<name>.md` (adaptive/etc.). If unknown, audit compact/mobile defaults and say so.
3. **Load the relevant rule sources** (foundations always; components and patterns matching what is actually present — you load only the cards you need, from their index).
4. **Examine the target** (read screens, scan code, grep triggers from each card). Check each rule. Some rules need *judgment*, not grep — e.g., is that button genuinely primary? Say so per deviation.
5. **Produce the deviation list** (below).
6. **Load the previous audit state** if a state file exists for this project (see Delta).
7. **Present the correction plan** (below). Nothing is changed in the codebase by the audit itself — fixes are proposed, not applied.

## Deviation list format

Output as markdown, each deviation:

```
### [P1][buttons] More than one primary action on the login surface
- Surface: `lib/views/LoginScreen.dart` (btn-proceed, btn-continue)
- Rule: m3-components/rules/buttons.md → #2 (one primary effective button)
- Problem: two filled buttons compete; user can't tell the primary path
- Fix: make `btn-continue` text/outlined; keep `btn-proceed` filled
- Status: open   ← (accepted / assumed / fixed set on review)
```

**Severity:**
- **P0 Critical** — blocks the task, or violates accessibility/safety (contrast fail, un-dismissible dialog, no screen-reader name).
- **P1 High** — visibly breaks an M3 pattern or central rule (two primary actions, no error state on text fields, blank loading).
- **P2 Medium** — foundation/style-token discipline (off-8dp spacing, out-of-scale radius, state layers missing).
- **P3 Low** — polish nit (inconsistent icon family, mixed density without reason).

**Order:** severity, then by risk-surface impact. List counts at the top (TOTAL, by severity). Never output a single global score as the headline.

## Delta (regression tracking)

State lives in a per-project folder the audit maintains:

```
{audit_state_root}/<project>/
  <project>-latest.yaml       ← last audit state (full deviation list + statuses)
  <project>-YYMM.yaml         ← historical snapshots
```

State root default: `_bmad-output/m3-audits/` (see config `audit_state_root` for the m3 module). If a previous state exists, the audit adds a **Delta section** at the top of the output:

```
## Delta since <last-date>
▶ New: 3      ▶ Fixed: 1      ▶ Regressions: 2 (deviation returned after being marked fixed)
- REGRESSION: login screen lost its error state (P1)
- NEW: text field missing state layer (P2)
```

Deviations previously marked `assumed` (deliberate brand deviations) are **not** re-flagged, but are listed once under "Assumed deviations" so they stay visible. Statuses flow: `open` → `fixed` (user confirms) / `assumed` (user opts in deliberately) / `accepted` (user says fine as-is) / `regression` (auto-detected).

## Correction plan

After the list, offer to work through fixes **one at a time**, each as a proposal:

```
Proposal 1/5 (P1, buttons): make btn-continue text/outlined on LoginScreen.
  Apply · Reject · Assume (deliberate brand choice) · Skip for now · Different approach?
```

- **Apply** → make the change.
- **Reject** → drop it, stays open or mark won't-fix (user's call).
- **Assume** → record as assumed deviation (no longer re-flagged, but listed).
- Different approach → do what they say instead.

Never auto-apply all deviations. Re-run of audit picks up the new state.

## Running on a codebase vs on a screenshot/render

- **Codebase**: use card triggers to grep for components; verify rules by reading the implementation (styles, layout, a11y props).
- **Screenshot/design** (no code): audit visually against the same cards — where a rule needs code-level proof (a11y name, contrast value), state that it is *unverifiable from the image* and needs a code check.

## Scope guardrails

- The audit checks **fidelity to Material Design 3**. It is not a general UI critic — respect the caller's brand deviations (that's what `assumed` is for).
- Audit runs *review* only. No code is changed unless the user accepts the correction plan's proposals.

## Working with other skills

- Sources: `m3-foundations`, `m3-components` (rule cards), `m3-patterns`, `m3-platforms`.
- Trigger entry point: `m3-orchestrator` invokes the audit; the audit also runs standalone.
- After a full audit, a delta-friendly cadence (per milestone/per feature) is the recommended rhythm for big projects.