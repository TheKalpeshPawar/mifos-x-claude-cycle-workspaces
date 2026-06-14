# MOCKUP — Reconnect Your Account (Consent Expired)

**Archetype:** error
**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background.
**Accent:** #4C662B (Earth-green). Secondary teal: #386663. Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │  ← no TopAppBar, no bottom nav
│                                     │
│               ( ⏱ )                 │  ← schedule icon, 72dp, #386663, centred
│                                     │
│         Time to reconnect           │  ← headline_medium, Outfit, #1A1C16, bold, centre
│                                     │
│  Your permission to access your     │  ← body_medium, #44483D, centre
│  HSBC account data has expired.     │
│  Banks ask you to renew this        │
│  regularly to keep your data        │
│  secure. Reconnect to pick up       │
│  where you left off.                │
│                                     │
│  ┌──────────────────────────────┐   │  ← #FFFFFF card, 16dp radius, spacing.lg padding
│  │ When you reconnect:          │   │  ← title_small, #1A1C16, bold
│  │ · You'll approve access      │   │  ← body_medium, #44483D
│  │   again at HSBC — your saved │   │
│  │   preferences stay put       │   │
│  │ · Your accounts and          │   │
│  │   transaction history reload │   │
│  │   automatically once done    │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌── ◌ Checking your connection ──┐ │  ← #CDEDA3 banner, 8dp radius; a11y role=status
│  │   status…                      │ │     spinner #4C662B 20dp + body_small #1A1C16
│  └────────────────────────────────┘ │
│                                     │
│  ┌──────────────────────────────┐   │  ← Reconnect filled button, #4C662B, 8dp radius
│  │    ◌  Reconnect              │   │     spinner overlay (loading_when), label_large
│  └──────────────────────────────┘   │
│                                     │
│            Not now                  │  ← text button, #386663, label_large, centre
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen `#F9FAEF`. No app chrome. Content column centred (align + justify center, spacing.lg padding all sides). Check banner `#CDEDA3` appears below the info card while `isChecking == true`; the Reconnect button shows a spinner overlay during this phase. Icon, title, subtitle, info card all visible in every state.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│               ( ⏱ )                 │  ← schedule icon, 72dp, #386663
│                                     │
│         Time to reconnect           │  ← headline_medium, #1A1C16, bold, centre
│                                     │
│  Your permission to access your     │  ← body_medium, #44483D, centre
│  HSBC account data has expired.     │
│  Banks ask you to renew this        │
│  regularly to keep your data        │
│  secure. Reconnect to pick up       │
│  where you left off.                │
│                                     │
│  ┌──────────────────────────────┐   │  ← #FFFFFF card, 16dp radius
│  │ When you reconnect:          │   │
│  │ · You'll approve access      │   │
│  │   again at HSBC — your saved │   │
│  │   preferences stay put       │   │
│  │ · Your accounts and          │   │
│  │   transaction history reload │   │
│  │   automatically once done    │   │
│  └──────────────────────────────┘   │
│                                     │
│  consent expired (EXPD) · 12 Mar    │  ← body_small, #44483D, centre; API-driven
│  2026                               │     visible_when: uiState == Content
│                                     │
│  ┌──────────────────────────────┐   │  ← Reconnect filled button, #4C662B, 8dp radius
│  │          Reconnect           │   │     full-width, label_large, #FFFFFF text
│  └──────────────────────────────┘   │
│                                     │
│            Not now                  │  ← text button, #386663, label_large
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Check banner hidden. Reference line `"consent expired (EXPD) · 12 Mar 2026"` visible — bound to `Status` + `ExpirationDateTime` from the GET consent response. Both CTAs fully active. RJCT/CANC variant reads "consent revoked (RJCT) · {date}". Min touch target 48dp on both buttons; Reconnect is match_parent width.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│               ( ⏱ )                 │  ← schedule icon, 72dp, #386663
│                                     │
│         Time to reconnect           │  ← headline_medium, #1A1C16, bold, centre
│                                     │
│  Your permission to access your     │  ← body_medium, #44483D, centre
│  HSBC account data has expired.     │  (generic copy — status unknown)
│  Banks ask you to renew this        │
│  regularly to keep your data        │
│  secure. Reconnect to pick up       │
│  where you left off.                │
│                                     │
│  ┌──────────────────────────────┐   │  ← #FFFFFF card, 16dp radius
│  │ When you reconnect:          │   │
│  │ · You'll approve access      │   │
│  │   again at HSBC — your saved │   │
│  │   preferences stay put       │   │
│  │ · Your accounts and          │   │
│  │   transaction history reload │   │
│  │   automatically once done    │   │
│  └──────────────────────────────┘   │
│                                     │  ← reference line hidden (checkFailed == true)
│  ┌──────────────────────────────┐   │  ← Reconnect filled button, #4C662B
│  │          Reconnect           │   │
│  └──────────────────────────────┘   │
│                                     │
│            Not now                  │  ← text button, #386663
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Status-check failed (network / 400 / 401 / 404) — banner hidden, reference line hidden, generic copy remains. The PSU can still tap Reconnect to start a fresh consent; the failing status check is invisible to them. Both buttons remain fully active with the same nav targets (consent-request / consent-intro).

---

## Design Checklist (Figma / Stitch)

- [ ] No Top App Bar, no bottom navigation bar — full-screen `#F9FAEF` interstitial
- [ ] `schedule` icon: 72dp, tint `#386663`, centred, spacing.md bottom padding
- [ ] "Time to reconnect" headline: Outfit/headline_medium (28sp), `#1A1C16`, bold, centre-aligned
- [ ] Subtitle body: Outfit/body_medium (14sp), `#44483D`, centre-aligned, spacing.lg bottom
- [ ] Info card: `#FFFFFF` fill, 16dp radius, spacing.lg padding, match_parent width
- [ ] Info card heading "When you reconnect:": Outfit/title_small (14sp), `#1A1C16`, bold, spacing.sm bottom
- [ ] Info card body points: Outfit/body_medium (14sp), `#44483D`
- [ ] Check banner (loading state): `#CDEDA3` fill, 8dp radius, spacing.md padding; spinner `#4C662B` 20dp + body_small `#1A1C16`
- [ ] Reference line (content state): Outfit/body_small (12sp), `#44483D`, centre; 1-line shimmer in loading
- [ ] "Reconnect" button: filled, `#4C662B` fill, `#FFFFFF` text (Outfit/label_large 14sp), 8dp radius, match_parent, spinner overlay while checking
- [ ] "Not now" button: text variant, `#386663`, Outfit/label_large (14sp), match_parent, centre
- [ ] Min touch target 48dp for both CTAs
- [ ] All text: Outfit typeface throughout

---

_Generated by /idea export | 2026-06-14_
