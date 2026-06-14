# MOCKUP — Access Not Granted (Consent Declined)

**Archetype:** error
**Shell:** No Top App Bar. No bottom navigation. Full-screen terminal feedback layout.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar (terminal feedback shell)
│                                     │
│              [⊘]                    │  ← block icon, 72dp, #BA1A1A, centered
│                                     │     spacing.md bottom padding
│      Access wasn't granted          │  ← headline_medium (Outfit 28sp), #1A1C16, bold, center
│                                     │     spacing.xs bottom padding
│  You didn't finish granting access  │  ← body_medium (Outfit 14sp), #44483D, center
│  at HSBC, so we couldn't connect    │     spacing.lg bottom padding
│  your account. No data was shared   │
│  and nothing was changed.           │
│                                     │
│  ┌───────────────────────────────┐  │  ← Reasons card: #FFFFFF, 16dp radius
│  │  This can happen if:          │  │  ← title_small (Outfit 14sp), #1A1C16, bold
│  │                               │  │     spacing.sm bottom padding
│  │  You chose 'Cancel' or 'Deny' │  │  ← body_medium, #44483D
│  │  on the HSBC approval screen  │  │     spacing.xs bottom padding
│  │                               │  │
│  │  The approval timed out       │  │  ← body_medium, #44483D
│  │  before it was confirmed      │  │     spacing.xs bottom padding
│  │                               │  │
│  │  HSBC couldn't verify your    │  │  ← body_medium, #44483D
│  │  identity during sign-in      │  │
│  └───────────────────────────────┘  │
│                                     │
│                                     │  ← declined_status_note HIDDEN in content state
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Try again           │    │  ← FilledButton, #4C662B fill, #FFFFFF label_large
│  └─────────────────────────────┘    │     8dp radius, full width
│                                     │
│         Maybe later                 │  ← Text button, #386663, label_large, full width
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background `#F9FAEF`. Full-screen column, `spacing.lg` padding, center-aligned.
- No TopAppBar — terminal shell; no back arrow, no bottom nav.
- Hero `block` icon: 72dp, `#BA1A1A`, horizontally centered, `spacing.md` bottom padding.
- Title: headline_medium (Outfit 28sp), `#1A1C16`, bold (700), center, `spacing.xs` bottom padding.
- Subtitle: body_medium (Outfit 14sp), `#44483D`, center, `spacing.lg` bottom padding.
- Reasons card: `#FFFFFF` fill, 16dp radius, `spacing.lg` padding, `spacing.md` bottom margin, full width. Heading title_small (Outfit 14sp, `#1A1C16`, bold, `spacing.sm` bottom padding), then three body_medium `#44483D` items each with `spacing.xs` bottom padding (last item no bottom padding).
- `declined_status_note` is **hidden** in content state — not rendered when `callbackError = null`.
- "Try again": filled, full width, `#4C662B`, 8dp radius, `spacing.md` padding.
- "Maybe later": text button, full width, `#386663`, label_large.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar
│              [⊘]                    │  ← block icon, 72dp, #BA1A1A, centered
│      Access wasn't granted          │  ← headline_medium, #1A1C16, bold, center
│  [reassurance subtitle]             │
│                                     │
│  ┌───────────────────────────────┐  │  ← Reasons card: #FFFFFF, 16dp radius (same as content)
│  │  This can happen if:          │  │
│  │  You chose 'Cancel' or 'Deny' │  │
│  │  on the HSBC approval screen  │  │
│  │  The approval timed out       │  │
│  │  HSBC couldn't verify your    │  │
│  │  identity during sign-in      │  │
│  └───────────────────────────────┘  │
│                                     │
│  Reference: access_denied ·         │  ← body_small, #44483D, centered — VISIBLE in error state
│  consent RJCT                       │     spacing.lg bottom padding
│                                     │     (data-driven: {callbackError} · consent {consentStatus})
│  ┌─────────────────────────────┐    │
│  │         Try again           │    │  ← FilledButton, #4C662B, same as content
│  └─────────────────────────────┘    │
│                                     │
│         Maybe later                 │  ← Text button, #386663
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Identical structure to `content`, with one addition: `declined_status_note` is **visible** between the reasons card and the "Try again" button.
- Reference line: body_small (Outfit 12sp), `#44483D`, centered, `spacing.lg` bottom padding. Format: "Reference: {callbackError} · consent {consentStatus}".
- Demo values: `access_denied` state → "Reference: access_denied · consent RJCT"; `login_required` state → "Reference: login_required · consent RJCT".
- The reference line is muted and unobtrusive — it is diagnostic information, not an alarming error headline.

---

## Design Checklist (Figma / Stitch)

- [ ] No TopAppBar, no bottom nav — terminal full-screen feedback shell
- [ ] Screen background `#F9FAEF`; full-screen column `spacing.lg` padding, center-aligned
- [ ] Hero `block` icon: 72dp, `#BA1A1A`, centered, `spacing.md` bottom padding
- [ ] Title: headline_medium (Outfit 28sp), `#1A1C16`, bold (700), center
- [ ] Subtitle: body_medium (Outfit 14sp), `#44483D`, center, `spacing.lg` bottom padding — reassurance, non-blaming copy
- [ ] Reasons card: `#FFFFFF` fill, 16dp corner radius, `spacing.lg` padding, full width
- [ ] Reasons heading: title_small (Outfit 14sp, weight 500), `#1A1C16`, bold
- [ ] Three reason items: body_medium (Outfit 14sp), `#44483D`, `spacing.xs` bottom padding each
- [ ] Technical reference note (`declined_status_note`): body_small (Outfit 12sp), `#44483D`, centered — HIDDEN in content state, VISIBLE in error state
- [ ] Reference line format: "Reference: {callbackError} · consent {consentStatus}" e.g. "Reference: access_denied · consent RJCT"
- [ ] "Try again": filled, `#4C662B`, `#FFFFFF` label_large, 8dp radius, full width
- [ ] "Maybe later": text button, `#386663`, label_large, full width
- [ ] All text: Outfit typeface. Minimum touch target 48dp for buttons.
- [ ] No input fields, no loading state — terminal informational screen only.

---

_Generated by /idea export | 2026-06-15_
