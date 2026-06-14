# Figma Prompts — Redirecting to HSBC (Bank Authorize Handoff)

**Feature:** bank-authorize-handoff
**Archetype:** loading (transitional full-screen takeover, no chrome)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: preparing

Design a full-screen Android mobile screen (390×844dp) for the "Redirecting to HSBC" transitional takeover in the HSBC Open Banking app. There is no top app bar and no bottom navigation bar.

**Background:** `#F9FAEF` (light sage green).

**Content column**, centred both horizontally and vertically (24dp padding all sides):

1. `account_balance` (bank building) Material icon, 80dp, tinted `#4C662B` (forest green), centred.
2. Headline text "Getting ready to connect securely" — Outfit 24sp, weight 400, `#1A1C16`, centre-aligned, 24dp top margin.
3. Body paragraph: "You'll sign in directly with HSBC to approve access. Your username, password and security codes are never entered in this app — and you'll come straight back here once you've approved." — Outfit 14sp, weight 400, `#44483D`, centre-aligned, 8dp top margin.
4. Circular indeterminate progress indicator, 32dp, `#4C662B`, centred, 24dp top margin.
5. Caption text "Encrypted connection · You can return here anytime" — Outfit 12sp, weight 400, `#74796D` (muted grey-green), centre-aligned, 16dp top margin.

**No buttons, no error states, no input fields.** This is a fully automated preparation phase — the app stages the consent and builds the signed HSBC authorise URL while the spinner runs.

---

## Screen: redirecting

Same base layout as `preparing` with these changes:

1. Headline text changes to: "Taking you to HSBC to sign in and approve"
2. Remove the circular indeterminate spinner entirely.
3. Add a full-width filled button in its place:
   - Label: "Continue to HSBC"
   - Fill: `#4C662B`, label colour `#FFFFFF`, Outfit 14sp weight 500, 8dp corner radius, 16dp vertical padding, 24dp top margin.
   - This is a manual-launch fallback — the app auto-launches the Custom Tab; this button re-opens the URL if needed.
4. Security note and body paragraph remain in the same positions.

Add a design note: "This button launches an external browser — the screen appears to 'leave' the app while the Custom Tab is open."

---

## Screen: error

Same base layout (icon + headline + `#F9FAEF` background) with these changes:

1. Headline: "We couldn't start your secure sign-in"
2. Remove the spinner, body paragraph, and security note.
3. Below the headline, add an error card:
   - Background `#FFDAD6` (M3 error-container), 8dp corner radius, 12dp padding, 24dp top margin.
   - Row: `error` icon 20dp `#BA1A1A` + 8dp gap + text "We couldn't start your secure sign-in with HSBC. Please check your connection and try again." — Outfit 12sp, `#410002`.
4. Below the error card, a full-width filled button "Try again":
   - `#4C662B` fill, `#FFFFFF` label (Outfit 14sp weight 500), 8dp radius, 16dp vertical padding, 24dp top margin.
5. Below that, a text-link button "Cancel":
   - No background, `#386663` label (Outfit 14sp weight 500), centred, minimum height 44dp.

**DO NOT** show a back arrow or navigation chrome. The cancel button is the only exit from the error state — it routes to the "consent-declined" screen.

---
