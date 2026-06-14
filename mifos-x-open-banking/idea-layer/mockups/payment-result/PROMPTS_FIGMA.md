# Figma Prompts — Payment Sent (Payment Result)

**Feature:** payment-result
**Archetype:** confirmation (terminal result, no chrome)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: content

Design a full-screen Android mobile screen (390×844dp) for the "Payment Sent" terminal result in the HSBC Open Banking app. There is no top app bar and no bottom navigation bar.

**Background:** `#F9FAEF` (light sage green).

**1 — Hero gradient card** (full-width, anchored to the top, 28dp bottom-corner radius only):
- Background: a vertical earth-green gradient (top `#5C7A33` → bottom `#4C662B`).
- Padding: 72dp top, 36dp bottom, 24dp horizontal. Content centre-aligned.
- a. A 92dp white (`#FFFFFF`) circle containing a `check` Material icon tinted `#4C662B`, centred. 16dp bottom margin.
- b. Headline "Payment sent" — Outfit 36sp, weight 700, `#FFFFFF`, centred, 8dp bottom margin.
- c. Summary "£150.00 to James Whitfield" — Outfit 16sp, weight 400, `#F5FFE6`, centred, 16dp bottom margin.
- d. Status pill "● COMPLETED" — pill shape, white fill at 18% opacity, `#FFFFFF` label (Outfit 12sp), the leading "●" dot tinted `#B6F2C0`, 8dp horizontal + 6dp vertical inner padding.

**2 — Details card** (white `#FFFFFF`, 16dp corner radius, elevation 2 soft shadow, 16dp margin from the hero and screen edges, 20dp horizontal + 8dp vertical inner padding):
- Row "Transaction ID" / "dp-7a21c9f4-…" — label Outfit 14sp `#44483D` left, value Outfit 14sp `#1A1C16` right, 14dp vertical padding, space-between.
- Divider `#E1E4D5`, 1dp, full-width.
- Row "From" / "Everyday Current" — same row style.
- Row "Charge" / "£0.00" — same row style.
- Row "Posted" / "Just now" — same row style.

**3 — Filled button "View transaction"** — full-width, `#4C662B` fill, `#FFFFFF` label (Outfit 16sp weight 500), 12dp corner radius, 52dp height, 16dp top margin.

**4 — Text button "Done"** — full-width, `#4C662B` label (Outfit 14sp weight 500), centred, no background, 8dp top margin.

**DO NOT add:** a top app bar, a bottom navigation bar, elevation shadows on the hero card, or any input fields. This is a read-only terminal result.

---
