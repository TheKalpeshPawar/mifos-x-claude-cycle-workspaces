# Figma Prompts — Reconnect Your Account (Consent Expired)

**Feature:** consent-expired
**Archetype:** error (full-screen interstitial, no chrome)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: loading

Design a full-screen Android mobile screen (390×844dp) for the "Reconnect Your Account" interstitial in the HSBC Open Banking app. There is no top app bar and no bottom navigation bar.

**Background:** `#F9FAEF` (light sage green).

**Content column**, centred horizontally and vertically with 24dp padding all sides:

1. `schedule` (clock/time) Material icon, 72dp, tinted `#386663` (teal), 16dp bottom margin.
2. Headline text "Time to reconnect" — Outfit 28sp, weight 700, `#1A1C16`, centre-aligned, 8dp bottom margin.
3. Body paragraph: "Your permission to access your HSBC account data has expired. Banks ask you to renew this regularly to keep your data secure. Reconnect to pick up where you left off." — Outfit 14sp, weight 400, `#44483D`, centre-aligned, 24dp bottom margin.
4. White card (`#FFFFFF`, 16dp corner radius, 24dp padding, full-width, no elevation shadow):
   - Subheading "When you reconnect:" — Outfit 14sp, weight 500, `#1A1C16`, bold, 8dp bottom margin.
   - Body point 1: "You'll approve access again at HSBC — your saved preferences stay put" — Outfit 14sp, `#44483D`, 4dp bottom margin.
   - Body point 2: "Your accounts and transaction history reload automatically once it's done" — Outfit 14sp, `#44483D`.
5. Status-check inline banner below the card: `#CDEDA3` fill (primary-container green), 8dp radius, 12dp padding, 16dp bottom margin. Row layout: 20dp circular indeterminate progress indicator `#4C662B` + 8dp gap + caption "Checking your connection status…" Outfit 12sp `#1A1C16`.
6. Filled button "Reconnect" — full-width, `#4C662B` fill, `#FFFFFF` label (Outfit 14sp weight 500), 8dp radius, 16dp vertical padding. Shows a small circular spinner on the label (loading state).
7. Text button "Not now" — full-width, `#386663` label (Outfit 14sp weight 500), centred, 16dp vertical padding, no background.

**DO NOT add:** elevation shadows, gradient overlays, decorative patterns, or any credential-entry fields. This screen is purely informational.

---

## Screen: content

Same layout as `loading` with two changes:

1. Remove the `#CDEDA3` status-check banner entirely.
2. Add a muted reference line between the white card and the "Reconnect" button:
   - Text: "consent expired (EXPD) · 12 Mar 2026"
   - Outfit 12sp, weight 400, `#44483D`, centre-aligned.
   - 16dp bottom margin before the Reconnect button.
3. "Reconnect" button has no spinner — fully active, solid `#4C662B` fill.

Everything else (icon, headline, body, white card, "Not now" button) is identical to the loading state.

---

## Screen: error

Same layout as `content` with one change:

1. The reference line ("consent expired (EXPD) · 12 Mar 2026") is absent — the space collapses.
2. The status-check banner is absent.
3. "Reconnect" button is fully active with no spinner.

The screen shows the generic renewal copy (identical headline + body + white card) without any technical status detail. This is intentional — the error state is invisible to the PSU; they see the same reassuring content and can still tap Reconnect.

---
