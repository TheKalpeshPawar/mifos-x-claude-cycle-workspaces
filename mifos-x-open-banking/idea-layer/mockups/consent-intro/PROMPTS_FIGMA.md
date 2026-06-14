# Figma Prompts — Connect Your HSBC Account (Consent Intro)

**Feature:** consent-intro
**Archetype:** onboarding
**States:** content

---

## State: content

Design a full-screen onboarding screen for an HSBC Open Banking connection flow on Android (390dp baseline width). No Top App Bar. No bottom navigation bar. Background `#F9FAEF`.

**Hero section:** At the top centre, place a Material `account_balance` icon at 72dp, filled `#4C662B`. Below it, a headline (Outfit 28sp, weight 700, `#1A1C16`, center): "Connect your HSBC account". Below that, body text (Outfit 14sp, `#44483D`, center, `spacing.lg` bottom padding): "Link your HSBC account securely through Open Banking to see your balances, transactions and payees — and to make payments when you choose to. Your HSBC password is never entered in this app."

**Trust card:** Outlined card (`#FFFFFF` fill, 1dp `#C5C8BA` border, 12dp corner radius, `spacing.md` padding, `spacing.md` bottom margin, full width). Heading (Outfit 16sp, weight 700, `#1A1C16`): "You stay in control". Four body-medium (Outfit 14sp, `#386663`) bullet items:
1. "You approve access at HSBC — not here. Sign-in and approval happen on HSBC's own secure pages."
2. "You choose exactly what to share. Pick which accounts and details to connect on the next screen."
3. "Read-only unless you authorise a payment. We can view your data; money only moves when you approve a payment at HSBC."
4. "Revoke access any time in Settings — disconnecting takes effect immediately."

**Access card:** Outlined card (`#FFFFFF` fill, 1dp `#C5C8BA` border, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin, full width). Heading (Outfit 16sp, weight 700, `#1A1C16`): "What we'll read". Bulleted list (Outfit 14sp, `#44483D`):
- "Your account names, numbers and balances"
- "Your transaction history and statements"
- "Standing orders, direct debits and payees"

**Redirect card:** Filled card (`#CDEDA3` fill, no border, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin, full width). Horizontal row: Material `open_in_browser` icon 24dp `#4C662B` on the left, then body-small text (Outfit 12sp, `#1A1C16`, `spacing.sm` start padding): "Next, you'll be taken to HSBC's own secure sign-in to approve this connection. We never see your HSBC username or password."

**Security note:** Body-small text (Outfit 12sp, `#44483D`, center, `spacing.md` bottom padding): "You can review exactly what you're sharing on the next screen before anything is connected."

**Primary CTA:** M3 FilledButton full-width, `#4C662B` background, `#FFFFFF` label (Outfit 14sp, weight 500): "Connect your HSBC account". 8dp corner radius. `spacing.md` padding. `spacing.sm` top margin.

**Legal links row:** Horizontal stack, center-justified, `spacing.md` gap between links, `spacing.md` top padding. Two inline text links (Outfit 14sp, `#386663`, 44dp min touch target): "Terms of Service" | "Privacy Policy".

**Footer:** Body-small (Outfit 12sp, `#44483D`, center, `spacing.xl` bottom padding): "Powered by Open Banking".

**DON'Ts:**
- No password or input fields anywhere on this screen.
- No loading spinner or skeleton — content is static and renders instantly.
- Do not use #E8A317 or any amber — Earth-green palette only.
- Do not add a Top App Bar or bottom navigation bar to this onboarding frame.

---
