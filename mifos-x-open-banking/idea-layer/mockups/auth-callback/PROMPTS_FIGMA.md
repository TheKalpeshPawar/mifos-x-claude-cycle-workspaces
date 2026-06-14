# Figma Prompts — Completing Connection (Auth Callback)

**Feature:** auth-callback
**Archetype:** status (headless full-screen takeover, no chrome)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: exchanging

Design a full-screen Android mobile screen (390×844dp) for the "Completing Connection" takeover in the HSBC Open Banking app. There is no top app bar and no bottom navigation bar. This screen appears automatically when the PSU returns from HSBC's login page via a deep-link redirect.

**Background:** `#F9FAEF` (light sage green).

**Content column**, centred both horizontally and vertically (24dp padding all sides):

1. `verified_user` (shield) Material icon, 80dp, tinted `#4C662B` (forest green), centred.
2. Headline text "Finishing secure connection…" — Outfit 24sp, weight 400, `#1A1C16`, centre-aligned, 24dp top margin.
3. Supporting copy: "Securely finishing your authorisation with HSBC. This only takes a moment." — Outfit 14sp, weight 400, `#44483D`, centre-aligned, 8dp top margin.
4. Circular indeterminate progress indicator, 32dp, `#4C662B`, centred, 24dp top margin.
5. Caption text "Verifying your authorisation · Encrypted connection" — Outfit 12sp, weight 400, `#74796D` (muted grey-green), centre-aligned, 16dp top margin.

**No buttons, no error states, no input fields.** This is purely a processing indicator. The screen auto-advances when the token exchange completes.

---

## Screen: verifying

Identical to `exchanging` with these copy changes only:

- AIS context — Headline: "Confirming your approval…" / Copy: "Checking your account-sharing approval went through."
- PAYMENT context — Headline: "Finalising your payment…" / Copy: "Submitting your payment to HSBC and confirming it was accepted."

All dimensions, colours, and component layout are identical to `exchanging`. Create as two sub-variants (verifying/AIS and verifying/PAYMENT).

---

## Screen: loading

Identical frame to `exchanging`. Use as the canonical loading alias frame in Figma — same headline "Finishing secure connection…", spinner, and caption.

---

## Screen: error

Same base layout as `exchanging` (icon + headline + `#F9FAEF` background) with these additions replacing the spinner and caption:

1. Remove the spinner and caption entirely.
2. Below the headline, add an error card:
   - Background `#FFDAD6` (M3 error-container), 8dp corner radius, 12dp padding, 24dp top margin.
   - Row: `error` icon 20dp `#BA1A1A` + 8dp gap + text "We couldn't complete your authorisation with HSBC. You can try again." — Outfit 12sp, `#410002`.
3. Below the error card, a full-width filled button "Try again":
   - `#4C662B` fill, `#FFFFFF` label (Outfit 14sp weight 500), 8dp radius, 16dp vertical padding, 24dp top margin.
4. Below that, a text-link button "Cancel":
   - No background, `#386663` label (Outfit 14sp weight 500), centred, minimum height 44dp.

Add a PAYMENT variant of the error card with text "Your payment authorisation was declined. You can try again."

**DO NOT** show a back arrow or any navigation chrome. The cancel button is the only exit from the error state.

---
