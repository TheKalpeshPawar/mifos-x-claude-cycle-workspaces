# Figma Prompts — Send Money (Amount Entry)

**Feature:** send-money-amount
**Archetype:** form (top app bar, no bottom nav)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: content

Design a full-screen Android mobile screen (390×844dp) for the "Send Money" payment form in the HSBC Open Banking app.

**Top app bar:** small M3 app bar, `#F9FAEF` surface, title "Send Money" (Outfit 22sp `#1A1C16`) with a leading `arrow_back` icon `#1A1C16`. No actions. No bottom navigation bar.

**Background:** `#F9FAEF`. Content is a vertically scrolling column, 16dp horizontal padding, 16dp top padding, 12dp gap between groups.

1. **From-account selector** — outlined list item, full-width, 12dp corner radius, 1dp `#75796C` border, leading `account_balance` icon `#386663`, label "Primary Checking — €4,820.00" (Outfit 16sp `#1A1C16`), trailing `expand_more` icon.
2. **Amount field** — outlined text field, full-width, 12dp radius, leading "€" prefix (Outfit 16sp `#44483D`), placeholder "0.00".
3. **Section label "To"** — Outfit 14sp weight 500, `#44483D`, 12dp top margin.
4. **Beneficiary search** — outlined text field, leading `search` icon, placeholder "Search beneficiary…", 12dp radius.
5. **Beneficiary row** — white `#FFFFFF` card, 12dp radius, 1dp `#E1E4D5` border, 12dp padding, text "James Whitfield" (Outfit 16sp `#1A1C16`).
6. **Reference field** — outlined text field, placeholder "Payment for invoice #1234", supporting text "Max 35 characters" (Outfit 12sp `#44483D`).
7. **Section label "Payment Type"** — Outfit 14sp weight 500, `#44483D`.
8. **Filter chip row** — three M3 filter chips: "SEPA" (selected: `#CDEDA3` fill, `#102000` label), "Domestic" (unselected outline), "International" (disabled, greyed). Horizontal, 8dp gap, scrollable.
9. **Ineligible reason** — "International unavailable — no BIC on file for this beneficiary" — Outfit 12sp `#44483D`.
10. **Fee banner** — `#CDEDA3` fill, 8dp radius, 16dp horizontal + 12dp vertical padding, leading `info` icon `#102000`, text "Estimated fee: Free (SEPA)" (Outfit 14sp `#102000`).
11. **Continue button** — filled, full-width, `#4C662B` fill, `#FFFFFF` label "Continue" (Outfit 16sp weight 500), 12dp radius, 52dp height, 20dp top margin.

**DO NOT add:** a bottom navigation bar, elevation shadows on the form fields, or a confirm/summary card (that lives on the next screen).

---

## Screen: loading

Same top app bar and `#F9FAEF` background. The form area is replaced by a single centred 40dp circular indeterminate progress indicator `#4C662B`, vertically centred in the content area. No form fields, no buttons.

---

## Screen: empty

Same top app bar and background. Centred column: an `account_balance_wallet` outline icon 64dp `#75796C`, then body text "No accounts available to send from." (Outfit 14sp `#44483D`, centred). No form fields, no Continue button.

---

## Screen: error

Same top app bar and background. Centred column with 24dp padding:
1. `cloud_off` Material icon, 64dp, `#75796C`, 16dp bottom margin.
2. Title "Could not load payment form" — Outfit 18sp weight 600 `#1A1C16`, centred, 8dp bottom margin.
3. Body "Check your connection and try again" — Outfit 14sp `#44483D`, centred, 24dp bottom margin.
4. Outlined button "Retry" — `#4C662B` border + label, 12dp radius, centred.

> The `no_network` and `unauthenticated` states render identically to `error` (same `cloud_off` illustration, title, body, and Retry button).

---
