# Figma Prompts — Access Not Granted (Consent Declined)

**Feature:** consent-declined
**Archetype:** error
**States:** content, error

---

## State: content

Design a full-screen terminal feedback screen for an HSBC Open Banking consent decline on Android (390dp baseline width). No Top App Bar. No bottom navigation bar. Background `#F9FAEF`. Column layout, center-aligned, `spacing.lg` padding.

**Hero:** Centre a Material `block` icon at 72dp, `#BA1A1A`. `spacing.md` bottom padding.

**Title:** headline_medium (Outfit 28sp, weight 700, `#1A1C16`, center, `spacing.xs` bottom padding): "Access wasn't granted"

**Subtitle:** body_medium (Outfit 14sp, `#44483D`, center, `spacing.lg` bottom padding): "You didn't finish granting access at HSBC, so we couldn't connect your account. No data was shared and nothing was changed."

**Reasons card:** `#FFFFFF` fill, 16dp corner radius, `spacing.lg` padding, `spacing.md` bottom margin, full width. Heading (Outfit 14sp, weight 700, `#1A1C16`, `spacing.sm` bottom padding): "This can happen if:". Three body-medium (Outfit 14sp, `#44483D`) items with `spacing.xs` bottom padding each:
1. "You chose 'Cancel' or 'Deny' on the HSBC approval screen"
2. "The approval timed out before it was confirmed"
3. "HSBC couldn't verify your identity during sign-in"

**No technical reference line in this state** — the `declined_status_note` is hidden when there is no explicit OAuth error code.

**Buttons:** M3 FilledButton full-width, `#4C662B` fill, `#FFFFFF` label (Outfit 14sp, weight 500, `spacing.md` padding): "Try again". 8dp corner radius. Then a Text button full-width, `#386663` text (Outfit 14sp, weight 500): "Maybe later".

**DON'Ts:**
- Do not show the technical reference line in this state — it only appears in the error state.
- Do not use alarming red for the card or the headline — the copy is reassuring and non-blaming.
- Do not show a TopAppBar or bottom navigation bar.
- Do not use the word "Error" or "Failed" anywhere on screen — the headline is "Access wasn't granted".

---

## State: error

Same layout as `content`. After the reasons card, add one additional element before the "Try again" button:

**Technical reference line:** body_small (Outfit 12sp, `#44483D`, center, `spacing.lg` bottom padding): "Reference: access_denied · consent RJCT"

This line is muted and diagnostic — NOT a large error message. Use body_small `#44483D` (same muted grey as the subtitle, not `#BA1A1A`). It sits between the reasons card and the "Try again" button. For the `login_required` variant the line reads: "Reference: login_required · consent RJCT".

**DON'Ts:**
- Do not make the reference line visually prominent — it is a secondary technical aide for support, not the primary message.
- Do not change the hero icon colour or title text in the error state — the layout is structurally identical to content.

---
