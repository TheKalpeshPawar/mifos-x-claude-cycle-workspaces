# MOCKUP — Connect Your HSBC Account (Consent Intro)

**Archetype:** onboarding
**Shell:** No Top App Bar. No bottom navigation. Full-screen immersive onboarding entry.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar (onboarding shell)
│                                     │
│              [⚏]                    │  ← account_balance icon, 72dp, #4C662B, centered
│                                     │     spacing.md bottom padding
│    Connect your HSBC account        │  ← headline_medium (Outfit 28sp), #1A1C16, bold, center
│                                     │     spacing.xs bottom padding
│  Link your HSBC account securely    │  ← body_medium (Outfit 14sp), #44483D, center
│  through Open Banking to see your   │     spacing.lg bottom padding
│  balances, transactions and payees  │
│  — and to make payments when you    │
│  choose to. Your HSBC password      │
│  is never entered in this app.      │
│                                     │
│  ┌───────────────────────────────┐  │  ← Trust card: #FFFFFF, #C5C8BA border, 12dp radius
│  │  You stay in control          │  │  ← title_medium, #1A1C16, bold
│  │                               │  │
│  │  • You approve access at      │  │  ← body_medium, #386663
│  │    HSBC — not here. Sign-in   │  │
│  │    and approval happen on     │  │
│  │    HSBC's own secure pages.   │  │
│  │  • You choose exactly what    │  │  ← body_medium, #386663
│  │    to share. Pick which       │  │
│  │    accounts and details to    │  │
│  │    connect on the next screen.│  │
│  │  • Read-only unless you       │  │  ← body_medium, #386663
│  │    authorise a payment.       │  │
│  │  • Revoke access any time     │  │  ← body_medium, #386663
│  │    in Settings.               │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Access card: #FFFFFF, #C5C8BA border, 12dp radius
│  │  What we'll read              │  │  ← title_medium, #1A1C16, bold
│  │                               │  │
│  │  • Account names, numbers     │  │  ← body_medium, #44483D, bulleted list
│  │    and balances               │  │
│  │  • Transaction history and    │  │
│  │    statements                 │  │
│  │  • Standing orders, direct    │  │
│  │    debits and payees          │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌── ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ──┐  │  ← Redirect card: #CDEDA3 fill, 12dp radius
│  │  [↗] Next, you'll be taken    │  │  ← open_in_browser icon 24dp #4C662B + body_small #1A1C16
│  │       to HSBC's own secure    │  │     spacing.sm start padding on text
│  │       sign-in to approve this │  │
│  │       connection. We never    │  │
│  │       see your HSBC username  │  │
│  │       or password.            │  │
│  └── ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ──┘  │
│                                     │
│  You can review exactly what you're │  ← body_small, #44483D, centered, spacing.md bottom
│  sharing on the next screen before  │
│  anything is connected.             │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Connect your HSBC account  │    │  ← FilledButton, #4C662B fill, #FFFFFF text
│  └─────────────────────────────┘    │     Outfit/label_large, 8dp radius, full width
│                                     │
│    [Terms of Service]  [Privacy Policy]│ ← inline links, body_medium, #386663, 44dp touch target
│                                     │
│        Powered by Open Banking      │  ← body_small, #44483D, centered, spacing.xl bottom
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background `#F9FAEF`. Full-screen column, `spacing.lg` padding all sides.
- No TopAppBar — onboarding-shell configuration. No bottom navigation bar.
- Hero `account_balance` icon: 72dp, `#4C662B`, horizontally centered, `spacing.md` bottom padding.
- Trust card (outlined, `#FFFFFF`, `#C5C8BA` border, 12dp radius): four bullet points — each body_medium `#386663`. Full-width. `spacing.md` bottom margin.
- Access card (outlined, `#FFFFFF`, `#C5C8BA` border, 12dp radius): three bulleted items, body_medium `#44483D`. Full-width. `spacing.md` bottom margin.
- Redirect card (filled, `#CDEDA3`, 12dp radius): horizontal row with `open_in_browser` icon (24dp `#4C662B`) + body_small `#1A1C16` text with `spacing.sm` start padding. `spacing.md` bottom margin.
- Security note: body_small `#44483D`, centered, `spacing.md` bottom padding.
- "Connect your HSBC account" button: filled, `#4C662B`, full width, 8dp radius, `spacing.md` padding, `spacing.sm` top margin.
- Legal row: horizontal stack, centered, `spacing.md` gap, `spacing.md` top padding; both links 44dp min height.
- Footer: body_small `#44483D`, centered, `spacing.md` top / `spacing.xl` bottom padding.

---

## Design Checklist (Figma / Stitch)

- [ ] No TopAppBar, no bottom navigation bar — onboarding full-screen shell
- [ ] Screen background `#F9FAEF`; all column content padded `spacing.lg`
- [ ] Hero `account_balance` icon: 72dp, `#4C662B`, center-aligned, `spacing.md` bottom padding
- [ ] Title: headline_medium (Outfit 28sp), `#1A1C16`, bold (700), center-aligned
- [ ] Subtitle: body_medium (Outfit 14sp), `#44483D`, center-aligned, `spacing.lg` bottom padding
- [ ] Trust card: `#FFFFFF` fill, `#C5C8BA` 1dp border, 12dp radius — four body_medium `#386663` trust pillars
- [ ] Access card: `#FFFFFF` fill, `#C5C8BA` 1dp border, 12dp radius — three bulleted body_medium `#44483D` items
- [ ] Redirect card: `#CDEDA3` fill, 12dp radius — `open_in_browser` 24dp `#4C662B` + body_small `#1A1C16` text
- [ ] Security note: body_small `#44483D`, centered, `spacing.md` bottom padding
- [ ] "Connect your HSBC account" button: filled `#4C662B`, `#FFFFFF` label_large, 8dp radius, full width
- [ ] Legal links row: horizontal, centered, `spacing.md` gap — both links body_medium `#386663`, 44dp touch target
- [ ] Footer "Powered by Open Banking": body_small `#44483D`, centered
- [ ] All text: Outfit typeface. Min text size 12sp. Touch targets 44dp minimum.
- [ ] No password field, no input field, no loading state — static informational screen only.

---

_Generated by /idea export | 2026-06-15_
