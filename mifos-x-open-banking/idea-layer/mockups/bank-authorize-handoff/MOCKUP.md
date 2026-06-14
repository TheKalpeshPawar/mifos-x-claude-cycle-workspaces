# MOCKUP — Redirecting to HSBC (Bank Authorize Handoff)

**Archetype:** loading (transitional full-screen takeover, no chrome)
**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background.
**Accent:** #4C662B (Earth-green). Error: #BA1A1A / #FFDAD6. Typography: Outfit. Design system: M3.

---

## Screen: preparing

```
┌─────────────────────────────────────┐
│                                     │  ← no TopAppBar, no bottom nav
│                                     │
│                                     │
│                                     │
│            [  🏦  ]                  │  ← account_balance icon, 80dp, #4C662B, centred
│                                     │
│  Getting ready to connect           │  ← headline_small, Outfit 24sp, #1A1C16, centre
│  securely                           │     spacing.lg top padding
│                                     │
│  You'll sign in directly with       │  ← body_medium, Outfit 14sp, #44483D, centre
│  HSBC to approve access. Your       │     spacing.sm top
│  username, password and security    │
│  codes are never entered in this    │
│  app — and you'll come straight     │
│  back here once you've approved.    │
│                                     │
│                ◌                    │  ← circular indeterminate spinner, 32dp, #4C662B
│                                     │     spacing.lg top
│  Encrypted connection · You can     │  ← body_small, Outfit 12sp, #74796D, centre
│  return here anytime                │     spacing.md top
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen `#F9FAEF`. Column centred both axes, spacing.lg padding. No buttons — automatic progression. The PKCE + consent staging + request-object signing happens here; no user action required. Spinner runs indeterminate throughout. Security explainer body copy `#44483D` builds PSU trust that credentials never touch this app.

---

## Screen: redirecting

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│                                     │
│            [  🏦  ]                  │  ← account_balance icon, 80dp, #4C662B
│                                     │
│  Taking you to HSBC to sign         │  ← headline_small, Outfit 24sp, #1A1C16, centre
│  in and approve                     │     spacing.lg top
│                                     │
│  You'll sign in directly with       │  ← body_medium, Outfit 14sp, #44483D, centre
│  HSBC to approve access. Your       │     (same security explainer copy)
│  username, password and security    │
│  codes are never entered in this    │
│  app — and you'll come straight     │
│  back here once you've approved.    │
│                                     │
│  ┌──────────────────────────────┐   │  ← Continue to HSBC filled button
│  │      Continue to HSBC        │   │     #4C662B fill, #FFFFFF label
│  └──────────────────────────────┘   │     Outfit/label_large, 8dp radius
│                                     │     spacing.lg top, match_parent
│  Encrypted connection · You can     │  ← body_small, #74796D, centre
│  return here anytime                │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Spinner replaced by "Continue to HSBC" filled button — this is the manual-launch fallback only. The app auto-launches the Custom Tab first; this button re-opens the URL if the auto-launch was blocked. The screen "leaves" the app when the Custom Tab opens; the return is a deep-link to `auth-callback`. Heading copy updates from "Getting ready" to "Taking you to HSBC…". Security note and explainer body remain.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│            [  🏦  ]                  │  ← account_balance icon, 80dp, #4C662B
│                                     │
│  We couldn't start your             │  ← headline_small, Outfit 24sp, #1A1C16, centre
│  secure sign-in                     │     spacing.lg top
│                                     │
│  ┌────────────────────────────────┐ │  ← error card: #FFDAD6, 8dp radius, spacing.md pad
│  │  ⚠  We couldn't start your    │ │  ← error icon #BA1A1A 20dp + body_small #410002
│  │     secure sign-in with HSBC. │ │
│  │     Please check your         │ │
│  │     connection and try again. │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌──────────────────────────────┐   │  ← Try again filled button
│  │          Try again           │   │     #4C662B fill, #FFFFFF label
│  └──────────────────────────────┘   │     Outfit/label_large, 8dp radius, match_parent
│                                     │     spacing.lg top
│            Cancel                   │  ← text button, #386663, label_large, centre
│                                     │     min_height 44dp → consent-declined
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Spinner and security explainer hidden. Error card `#FFDAD6` (M3 error-container) with `error` icon `#BA1A1A` 20dp and message `#410002`. "Try again" is match_parent filled button that returns the screen to the `preparing` state (re-stages consent + rebuilds request). "Cancel" is a text-variant link (`#386663`, min_height 44dp) routing to `consent-declined`. The body copy paragraph is also hidden in this state — replaced by the error card.

---

## Design Checklist (Figma / Stitch)

- [ ] No Top App Bar, no bottom navigation — full-screen `#F9FAEF` takeover
- [ ] `account_balance` (bank) icon: 80dp, `#4C662B`, centred
- [ ] Headline: Outfit/headline_small (24sp), `#1A1C16`, centre — phase-driven text (preparing / redirecting / error variants)
- [ ] Security explainer body: Outfit/body_medium (14sp), `#44483D`, centre — visible in preparing + redirecting states; hidden in error state
- [ ] Spinner: circular indeterminate 32dp `#4C662B`, spacing.lg top — visible in preparing state only; replaced by button in redirecting
- [ ] "Continue to HSBC" button: filled `#4C662B`, `#FFFFFF` label (Outfit 14sp/500), 8dp radius, match_parent, spacing.lg top — visible in redirecting state only (manual-launch fallback)
- [ ] Security note: Outfit/body_small (12sp), `#74796D`, centre, spacing.md top — visible in preparing + redirecting states; hidden in error state
- [ ] Error card: `#FFDAD6` fill, 8dp radius, spacing.md padding, spacing.lg top margin — visible in error state only
- [ ] Error card icon: `error` glyph 20dp `#BA1A1A`
- [ ] Error card message: Outfit/body_small (12sp), `#410002`, spacing.sm start padding
- [ ] "Try again" button: filled `#4C662B`, `#FFFFFF` (Outfit 14sp/500), 8dp radius, match_parent — error state only
- [ ] "Cancel" link: text variant `#386663`, Outfit 14sp/500, centre, min_height 44dp — error state only
- [ ] No credential-entry fields anywhere; no username/password inputs
- [ ] Outfit typeface throughout; all touch targets ≥ 48dp

---

_Generated by /idea export | 2026-06-14_
