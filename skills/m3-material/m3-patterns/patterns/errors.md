# Error handling — pattern card

The **error handling** pattern governs failures across a flow: validation errors, operation failures, and network issues — with actions, never blame.

## Structure

1. **Errors are a design surface, not an afterthought.** Every async path and every validation has a designed error state: what broke, why it matters, what to do next.
2. **Classify the error**:
   - **Preventable** (validation) → correct inline, at the field.
   - **Transient** (network, timeout) → retry affordance + keep context; do not lose user data.
   - **Permanent** (not found, unauthorized) → explain in human terms + the recovery path.
3. **Message anatomy**: *what happened + why it matters + how to fix* — in plain language, no error codes/stack traces (foundations writing).
4. **Placement by severity**: inline for field errors; snackbar for light operation errors; dialog/surface for blocking failures with a required action; *never* only console.
5. **Never data loss**: on transient failure, preserve the user's entered values/scroll position; a refresh must not nuke their work.
6. **Retry intelligently**: automatic retry for flaky calls is fine; show retry button for persistent; endless auto-retry spinner = lie (see loading).
7. **Nothing errors without an action** — even "dismiss" is an action. Every error block offers a path forward.

## Cross-layer rules

- Loading/failure visuals → `see components/progress-indicators`.
- Ephemeral failures → `see components/snackbars`.
- Blocking failures → `see components/dialogs`.
- Copy rules → `see m3-foundations` writing.

## Implementation hints

- Detect: try/catch → UI, `catch`, `onError`, `errorMessage`, `SnackBar` errors, `Failed to`, `Error`, toast.
- Common catches: `.catch(e) {}` silent swallow; error shows raw exception text; retry button missing after network fail; error snackbar blocks typed data with no save.

## Checklist

- [ ] every failure path designed (preventable/transient/permanent)
- [ ] message = what + why + fix, plain language
- [ ] placement matches severity
- [ ] no data loss on transient failure
- [ ] sensible retry (button, not endless loop)
- [ ] every error has an action