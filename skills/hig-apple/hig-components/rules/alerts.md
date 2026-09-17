# Alerts — rule card

An **alert** is a modal interruption that surfaces time-sensitive, important information and typically asks the user to confirm a decision. It blocks the current context until dismissed or answered.

**Triggers**: `Alert`, `alert`, `AlertDialog`, `showDialog`, `showDialog<bool>`, `alert()`, `modal`, `confirm`, `SweetAlert`, `useAlert`, `<dialog`, `messagebox`.

## Rules

1. **Guard the trigger.** Alerts must be rare and important. Appearing on every screen, on startup, or for trivial information is alert spam — prefer inline feedback, a toast, or a banner instead.
2. **Understand the decision being asked.** An alert either (a) reports a critical error, (b) confirms a consequential/destructive action, or (c) asks a specific question. If it does none, it is not an alert.
3. **Structure: title + message + buttons.** Title states the situation in a short imperative/phrase; message clarifies context in ≤ 2 sentences; buttons are the choices.
4. **Buttons match the decision.** Use the vocabulary of the question: for a destructive action, the destructive confirmation ("Delete") is explicit, and "Cancel" is present. For a question, the action buttons answer it.
5. **Return the user where they were.** Dismissing any alert never destroys the user's in-progress work or context.
6. **Escapable:** the user can dismiss without extra friction — Escape/back dismisses where semantics allow, and non-consequential alerts offer an explicit dismiss.
7. **No alert in response to a page-load only.** Alerts that appear without user action and without urgency are universally hated; defer.
8. **Accessibility:** alert contents announced by screen readers; the alert receives focus; buttons reachable by keyboard.

## The why

An alert is an interruption — real control of the system. Its power must be reserved: choose it when the user *must* stop and decide, not when the interface wants attention. Frequent alerts teach people to mash "OK".

## Implementation hints

- Detect via triggers above. Check:
  - Usages count and contexts: any alert on first launch / no-user-action? → flag.
  - Is there a genuine decision? No buttons but a "Got it"? → flag as spam, suggest banner/toast.
  - Destructive confirm: confirm button label == the action verb ("Delete") and a cancel exists → else flag.
  - Red used on non-destructive confirm → flag.
  - Dismiss/back behavior preserves context.
  - Focus moves to the alert on appearance.

## Checklist

- [ ] rare + important only
- [ ] a real decision or critical error
- [ ] title, short message, explicit buttons
- [ ] destructive confirm verbatim, cancel present
- [ ] user context preserved on dismiss
- [ ] escaped + announced + focusable