# MOCKUP — Completing Connection (Auth Callback)

**Archetype:** status (headless full-screen takeover, no chrome)
**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background.
**Accent:** #4C662B (Earth-green). Error: #BA1A1A / #FFDAD6. Typography: Outfit. Design system: M3.

---

## Screen: exchanging

```
┌─────────────────────────────────────┐
│                                     │  ← no TopAppBar, no bottom nav
│                                     │
│                                     │
│                                     │
│                                     │
│             [  🛡  ]                 │  ← verified_user icon, 80dp, #4C662B, centred
│                                     │
│     Finishing secure connection…    │  ← headline_small, Outfit 24sp, #1A1C16, centre
│                                     │     spacing.lg top padding
│   Securely finishing your           │  ← body_medium, Outfit 14sp, #44483D, centre
│   authorisation with HSBC. This     │     spacing.sm top
│   only takes a moment.              │
│                                     │
│                ◌                    │  ← circular indeterminate spinner, 32dp, #4C662B
│                                     │     spacing.lg top padding
│   Verifying your authorisation ·   │  ← body_small, Outfit 12sp, #74796D, centre
│   Encrypted connection              │     spacing.md top
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen `#F9FAEF`, column centred both axes, spacing.lg padding. No buttons, no error card visible. Spinner runs indeterminate — no percent or countdown. Security caption `#74796D` (muted) reinforces mTLS context without being alarming.

---

## Screen: verifying

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│                                     │
│                                     │
│             [  🛡  ]                 │  ← verified_user icon, 80dp, #4C662B
│                                     │
│      Confirming your approval…      │  ← headline_small, #1A1C16, centre
│     (or "Finalising your payment…"  │     for PAYMENT consentContext)
│                                     │
│   Checking your account-sharing     │  ← body_medium, #44483D, centre
│   approval went through.            │     (or PAYMENT variant copy)
│                                     │
│                ◌                    │  ← circular spinner, 32dp, #4C662B
│                                     │
│   Verifying your authorisation ·   │  ← body_small, #74796D, centre
│   Encrypted connection              │
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Identical visual composition to `exchanging` — same icon, spinner, security note. Only the headline and supporting copy change (data_driven via `phase + consentContext`). AIS heading: "Confirming your approval…"; PAYMENT heading: "Finalising your payment…". No user action required — auto-routes on success.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│             [  🛡  ]                 │  ← verified_user icon, 80dp, #4C662B
│                                     │
│     Finishing secure connection…    │  ← headline_small, #1A1C16
│                                     │
│   Securely finishing your           │  ← body_medium, #44483D
│   authorisation with HSBC. This     │
│   only takes a moment.              │
│                                     │
│                ◌                    │  ← spinner, 32dp, #4C662B
│                                     │
│   Verifying your authorisation ·   │  ← body_small, #74796D
│   Encrypted connection              │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Canonical loading alias — identical to `exchanging`. Satisfies the standard loading/content/error state contract. Runtime drives `exchanging → verifying` via CallbackPhase enum.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│             [  🛡  ]                 │  ← verified_user icon, 80dp, #4C662B
│                                     │
│     Finishing secure connection…    │  ← headline_small, #1A1C16 (last phase title)
│                                     │
│                                     │
│  ┌────────────────────────────────┐ │  ← error card: #FFDAD6, 8dp radius, spacing.md pad
│  │  ⚠  We couldn't complete your │ │  ← error icon #BA1A1A 20dp + body_small #410002
│  │     authorisation with HSBC.  │ │     AIS copy (PAYMENT: "Your payment authorisation
│  │     You can try again.        │ │     was declined. You can try again.")
│  └────────────────────────────────┘ │
│                                     │
│  ┌──────────────────────────────┐   │  ← Try again filled button
│  │          Try again           │   │     #4C662B fill, #FFFFFF text
│  └──────────────────────────────┘   │     Outfit/label_large, 8dp radius, match_parent
│                                     │
│            Cancel                   │  ← text button, #386663, label_large, centre
│                                     │     → consent-declined (AIS) / payment-declined (PAYMENT)
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Spinner hidden. Error card `#FFDAD6` (M3 error-container) with `error` icon `#BA1A1A` and message `#410002` (on-error-container). "Try again" is a full-width filled button (`#4C662B`). "Cancel" is a text-variant link (`#386663`, min_height 44dp). The cancel destination is context-keyed — AIS → consent-declined, PAYMENT → payment-declined — resolved by AuthCallbackViewModel (not hardcoded in the click handler). Card appears with spacing.lg top margin from the headline.

---

## Design Checklist (Figma / Stitch)

- [ ] No Top App Bar, no bottom navigation — full-screen `#F9FAEF` takeover
- [ ] `verified_user` icon: 80dp, `#4C662B`, centre-aligned at top of content column
- [ ] Headline: Outfit/headline_small (24sp), `#1A1C16`, centre — phase-driven text (3 variants)
- [ ] Supporting copy: Outfit/body_medium (14sp), `#44483D`, centre — phase-driven (3 variants)
- [ ] Spinner: circular indeterminate, 32dp, `#4C662B`, centre, spacing.lg top — hidden in error state
- [ ] Security note: Outfit/body_small (12sp), `#74796D`, centre, spacing.md top — hidden in error state
- [ ] Error card: `#FFDAD6` fill, 8dp radius, spacing.md padding, spacing.lg top margin — hidden in processing states
- [ ] Error card icon: `error` glyph, 20dp, `#BA1A1A`
- [ ] Error card message: Outfit/body_small (12sp), `#410002`, spacing.sm start padding, consentContext-keyed copy
- [ ] "Try again" button: filled `#4C662B`, `#FFFFFF` label (Outfit 14sp/500), 8dp radius, match_parent — visible only in error state
- [ ] "Cancel" link: text variant `#386663`, Outfit 14sp/500, centre, min_height 44dp — visible only in error state
- [ ] Auto-navigates on success (no tap required) — no "Continue" button in happy-path states
- [ ] Outfit typeface throughout; no credential-entry fields anywhere

---

_Generated by /idea export | 2026-06-14_
