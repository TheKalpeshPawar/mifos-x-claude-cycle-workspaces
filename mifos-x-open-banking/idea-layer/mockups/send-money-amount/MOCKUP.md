# Send Money — Visual Specification

| Field     | Value             |
|-----------|-------------------|
| Feature   | send-money-amount |
| Flavor    | consumer          |
| Archetype | form              |

---

## Screen Layout

Top-to-bottom hierarchy on a vertically scrolling form screen under a "Send Money" top app bar:

```
[ ← Send Money ]                            ← top app bar, back arrow
──────────────────────────────────────────
[ 🏦 Primary Checking — €4,820.00      ⌄ ]  ← from_account_selector, outlined
[ €  0.00                                 ]  ← amount_input, outlined, € prefix
  To                                         ← to_label, label_large #44483D
[ 🔍 Search beneficiary...                ]  ← beneficiary_search, outlined
┌────────────────────────────────────────┐
│ James Whitfield                        │  ← beneficiary_row, white card, border
└────────────────────────────────────────┘
[ Payment for invoice #1234               ]  ← reference_input (Max 35 characters)
  Payment Type                               ← payment_type_label
[ (SEPA) ( Domestic ) ( International✕ )  ]  ← payment_type_chips, filter
  International unavailable — no BIC…         ← rail_ineligible_reason, body_small
┌────────────────────────────────────────┐
│ ℹ Estimated fee: Free (SEPA)           │  ← fee_banner, #CDEDA3 fill, r=8dp
└────────────────────────────────────────┘
[ Continue            (filled, #4C662B)   ]  ← continue_button, full-width, 52dp
```

---

## Components

### from_account_selector
- Outlined list item, leading `account_balance` icon, trailing `expand_more`, 12dp radius
- Content "Primary Checking — €4,820.00"; tap opens the account picker

### amount_input
- Outlined text field, "€" prefix, "0.00" placeholder, decimal keyboard, 12dp radius
- Required, rule `amount > 0`; error "Please enter a valid amount greater than 0"

### to_label
- "To" — `label_large`, `#44483D`

### beneficiary_search
- Outlined, leading `search`, "Search beneficiary..." placeholder; required

### beneficiary_row
- White (`#FFFFFF`) card, 12dp radius, `#E1E4D5` 1dp border, 12dp padding
- Selectable recipient (e.g. "James Whitfield")

### reference_input
- Outlined, "Payment for invoice #1234" placeholder, supporting "Max 35 characters", max_length 35

### payment_type_label
- "Payment Type" — `label_large`, `#44483D`

### payment_type_chips
- Filter chip group: SEPA · Domestic · International
- Ineligible rails are disabled with a reason; selected chip uses the primary tint

### rail_ineligible_reason
- "International unavailable — no BIC on file for this beneficiary" — `body_small`, `#44483D`

### fee_banner
- `#CDEDA3` fill, 8dp radius, 16dp horizontal + 12dp vertical padding, leading `info` icon
- "Estimated fee: Free (SEPA)", text `#102000`

### internal_transfer_note (sandbox path)
- Replaces the chips + fee banner + ineligible reason when `useSandboxTan` is set
- "Internal bank transfer — sent instantly within the bank." — `body_medium`, `#1A1C16`

### sandbox_block_reason (conditional)
- "On the sandbox, amounts this large can only be sent to accounts within the bank." — `body_small`, `#BA1A1A`

### continue_button
- Filled, `#4C662B` background, `#FFFFFF` label; full-width, 12dp radius, 52dp height
- Shows "Checking..." while the Confirmation-of-Funds check runs; navigates to send-money-confirm on success

---

## States

| State           | Visual                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------|
| loading         | Centered progress indicator; form components hidden                                             |
| content         | Full editable form as drawn above; sandbox path swaps rail UI for internal_transfer_note        |
| empty           | Empty illustration + "No accounts available to send from."                                       |
| error           | `cloud_off` icon, "Could not load payment form", "Check your connection and try again", Retry    |
| no_network      | Same as error (`cloud_off`, retry)                                                               |
| unauthenticated | Same as error (`cloud_off`, retry)                                                               |

---

## Interaction Patterns

| Interaction              | Component             | Result                                            |
|--------------------------|-----------------------|---------------------------------------------------|
| Tap from-account         | from_account_selector | Account picker opens; switching reloads beneficiaries|
| Type amount              | amount_input          | Live validation against `amount > 0`              |
| Search/select recipient  | beneficiary_search/row| Filters beneficiaries; selecting locks the row    |
| Tap a rail chip          | payment_type_chips    | Selects rail; ineligible chips disabled with reason|
| Tap "Continue"           | continue_button       | CoF check runs ("Checking..."), then navigate to confirm |

---

## Content Data

| Element          | Value                       |
|------------------|-----------------------------|
| Source account   | Everyday Current — £2,483.57 (InterimAvailable) |
| Beneficiary      | James Whitfield             |
| Amount (demo CoF)| £150.00                     |
| Fee              | Free (SEPA)                 |

> Real OBIE content from demo-data.yaml (accounts, balances, beneficiaries, funds-confirmation collections).

---

## Design Notes

**Form rhythm:** 12dp top margin between field groups gives the dense form breathing room; section labels ("To", "Payment Type") in `label_large` `#44483D` chunk the form into scannable groups.

**Rail eligibility as guidance, not error:** Ineligible rail chips are disabled with an inline reason in neutral `#44483D` — not the error red — because the user has done nothing wrong; the rail simply lacks a BIC.

**Fee banner reassurance:** The `#CDEDA3` primary-container fill on the fee banner reads as a calm, positive affordance for the zero-cost SEPA path.

**Confirmation-of-Funds gate:** The Continue button doubles as the CoF pre-flight surface — its "Checking..." label communicates the live `POST /cbpii/funds-confirmations` round-trip before the user leaves the form.

*Generated by /idea export | 2026-06-15*
