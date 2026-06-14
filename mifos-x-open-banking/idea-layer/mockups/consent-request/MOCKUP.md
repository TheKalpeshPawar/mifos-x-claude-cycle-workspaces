# MOCKUP — Review & Grant Access (Consent Request)

**Archetype:** form
**Shell:** No explicit Top App Bar. No bottom navigation. Onboarding continuation shell.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar (onboarding shell continuation)
│  Review what you'll share           │  ← headline_medium (Outfit 28sp), #1A1C16
│                                     │     spacing.xs bottom padding
│  This app is asking to read the     │  ← body_medium (Outfit 14sp), #44483D
│  following information from your    │     spacing.lg bottom padding
│  HSBC account. Tap Grant access     │
│  to continue to HSBC's secure       │
│  sign-in.                           │
│                                     │
│  ┌───────────────────────────────┐  │  ← Scope card: #F0F1E6 fill, 12dp radius
│  │  ⚏  Shared with: all your    │  │  ← account_balance 20dp #386663 + body_medium #1A1C16
│  │     HSBC accounts            │  │     weight 600
│  │                              │  │
│  │  ⏱  Access until:            │  │  ← schedule 20dp #386663 + body_medium #1A1C16
│  │     11 September 2026 (90d)  │  │     weight 600
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Clusters card: #FFFFFF, #C5C8BA border, 12dp radius
│  │  Read-only data clusters      │  │  ← title_medium, #1A1C16, bold
│  │  ─────────────────────────── │  │
│  │  ◼ Account details           [Req]│ ← account_balance_wallet 20dp #4C662B + body_med #1A1C16
│  │    names, numbers, sort codes│  │     Required badge: outlined #44483D, #C5C8BA border
│  │  ─────────────────────────── │  │  ← #E1E4D5 divider
│  │  ◼ Balances                  [Req]│ ← savings 20dp #4C662B
│  │    current & available bal.  │  │     Required badge: outlined
│  │  ─────────────────────────── │  │
│  │  ◼ Transactions              [Req]│ ← receipt_long 20dp #4C662B
│  │    payments, dates, amounts  │  │     Required badge: outlined
│  │  ─────────────────────────── │  │
│  │  ◼ Payees                    [Opt]│ ← group 20dp #4C662B
│  │    saved payees              │  │     Optional badge: #CDEDA3 fill, #102000 text
│  │  ─────────────────────────── │  │
│  │  ◼ Standing orders           [Opt]│ ← event_repeat 20dp #4C662B
│  │    recurring payments        │  │     Optional badge
│  │  ─────────────────────────── │  │
│  │  ◼ Direct debits             [Opt]│ ← sync_alt 20dp #4C662B
│  │    mandates & recent payments│  │     Optional badge
│  │  ─────────────────────────── │  │
│  │  ◼ Scheduled payments        [Opt]│ ← event_upcoming 20dp #4C662B
│  │    future-dated payments     │  │     Optional badge
│  │  ─────────────────────────── │  │
│  │  ◼ Account-holder info       [Opt]│ ← contact_page 20dp #4C662B
│  │    holder's name & contact   │  │     Optional badge
│  │  ─────────────────────────── │  │
│  │  ◼ Product details           [Opt]│ ← inventory_2 20dp #4C662B
│  │    account type, rates       │  │     Optional badge
│  │  ─────────────────────────── │  │
│  │  ◼ Statements                [Opt]│ ← description 20dp #4C662B
│  │    statements & periods      │  │     Optional badge
│  └───────────────────────────────┘  │
│                                     │
│  This access expires automatically  │  ← body_small, #44483D, spacing.md bottom padding
│  after 90 days. You can disconnect  │
│  sooner at any time from Settings.  │
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Grant access        │    │  ← FilledButton, #4C662B fill, #FFFFFF label_large
│  └─────────────────────────────┘    │     8dp radius, full width
│                                     │
│  ┌─────────────────────────────┐    │
│  │           Cancel            │    │  ← OutlinedButton, #4C662B border+text, 8dp radius
│  └─────────────────────────────┘    │     full width
│                                     │
│  You'll approve this at HSBC.       │  ← body_small, #44483D, center, spacing.xl bottom
│  We never see your password.        │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background `#F9FAEF`. Full-width column, `spacing.lg` padding.
- No TopAppBar — onboarding shell continuation, no back arrow.
- Scope card: `#F0F1E6` fill, 12dp radius — two rows each with a 20dp `#386663` icon + semibold body_medium `#1A1C16` text. `spacing.md` bottom margin.
- Clusters card: `#FFFFFF` fill, 1dp `#C5C8BA` border, 12dp radius — 10 rows separated by `#E1E4D5` dividers. Each row: 20dp `#4C662B` icon left, body_medium `#1A1C16` description (flex:1), then badge trailing.
- "Required" badge: outlined variant — `#44483D` text, `#C5C8BA` 1dp border, 8dp radius, Outfit/label_small (11sp). Three rows.
- "Optional" badge: tonal variant — `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small (11sp). Seven rows.
- All 10 cluster rows are always visible in content state. Screen scrolls vertically.
- Expiry note: body_small `#44483D`, `spacing.md` bottom padding.
- "Grant access": filled, full width, `#4C662B`, `spacing.sm` top margin.
- "Cancel": outlined, full width, `#4C662B` border + text, `spacing.sm` top margin.
- Footer: body_small `#44483D`, center-aligned, `spacing.md` top / `spacing.xl` bottom.

---

## Screen: submitting

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar
│                                     │
│                                     │
│                                     │
│                ◌                    │  ← circular_indeterminate spinner, 32dp, #4C662B, centered
│                                     │
│         Creating your consent…      │  ← body_medium (Outfit 14sp), #44483D, center
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Column centered vertically and horizontally. Spinner 32dp `#4C662B`. Message body_medium `#44483D` below.
- All other content (scope card, clusters, buttons) hidden — full-screen loading.
- The "Grant access" button also shows its inline `loading_when: Submitting` spinner while transitioning.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar
│  Review what you'll share           │  ← headline_medium
│  [subtitle]                         │
│  [scope card]                       │
│  [10-row clusters card]             │
│                                     │
│  ┌── ⚠ ─────────────────────────┐  │  ← Error banner: #FFDAD6 fill, 8dp radius
│  │   We couldn't start your     │  │  ← error icon 20dp #BA1A1A + body_small #410002
│  │   connection. Please check   │  │     spacing.sm start padding on text
│  │   your network and try again.│  │
│  └──────────────────────────────┘  │
│                                     │
│  [expiry note]                      │
│  [Grant access button]              │  ← same filled button — PSU can retry
│  [Cancel button]                    │
│  [footer]                           │
└─────────────────────────────────────┘
```

**Layout notes:**
- Error banner (`#FFDAD6`, 8dp radius, `spacing.md` padding) inserted between expiry note and Grant button — but positioned above Grant button per visible_components ordering in `error` state.
- `error` icon 20dp `#BA1A1A` on the left of the banner; body_small `#410002` message with `spacing.sm` start padding.
- All other content remains visible — PSU can review and retry.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar
│                                     │
│               [⚏]                   │  ← account_balance 48dp, #75796C, centered
│                                     │
│         No accounts to share        │  ← title_medium, #1A1C16, bold, center
│                                     │
│  We couldn't find any HSBC          │  ← body_medium, #44483D, center, spacing.md top
│  accounts to connect. Check that    │
│  your accounts are open and         │
│  eligible for Open Banking,         │
│  then try again.                    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │           Cancel            │    │  ← OutlinedButton, #4C662B, 8dp radius, full width
│  └─────────────────────────────┘    │     only CTA — no Grant button in empty state
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Column centred vertically and horizontally. `account_balance` icon 48dp tinted `#75796C`. Title title_medium `#1A1C16` bold. Body body_medium `#44483D` center, `spacing.sm` top padding, `spacing.md` bottom padding. Only "Cancel" button — there is nothing to consent to without eligible accounts.

---

## Design Checklist (Figma / Stitch)

- [ ] No TopAppBar, no bottom nav — onboarding shell continuation
- [ ] Screen background `#F9FAEF`; full-width column `spacing.lg` padding
- [ ] Title: headline_medium (Outfit 28sp), `#1A1C16`, no bold
- [ ] Subtitle: body_medium (Outfit 14sp), `#44483D`, `spacing.lg` bottom padding
- [ ] Scope card: `#F0F1E6` fill, 12dp radius — `account_balance` + `schedule` icons 20dp `#386663`; semibold body_medium text `#1A1C16`
- [ ] Clusters card: `#FFFFFF` fill, 1dp `#C5C8BA` border, 12dp radius, full-width
- [ ] All 10 cluster rows visible — `#4C662B` 20dp icon left, body_medium `#1A1C16` description, badge trailing
- [ ] Dividers between rows: `#E1E4D5` 1dp horizontal rule
- [ ] "Required" badge (3 rows): outlined, `#44483D` text, `#C5C8BA` border, 8dp radius, Outfit/label_small
- [ ] "Optional" badge (7 rows): tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small
- [ ] Expiry note: body_small (Outfit 12sp), `#44483D`, `spacing.md` bottom padding
- [ ] "Grant access": filled `#4C662B`, `#FFFFFF` label_large, 8dp radius, full width; inline loading spinner in submitting state
- [ ] "Cancel": outlined `#4C662B`, label_large, 8dp radius, full width
- [ ] Footer: body_small `#44483D`, center, `spacing.xl` bottom padding
- [ ] Submitting state: 32dp circular spinner `#4C662B` + "Creating your consent…" body_medium `#44483D`, all other content hidden
- [ ] Error banner: `#FFDAD6` fill, 8dp radius — `error` icon 20dp `#BA1A1A` + body_small `#410002` message
- [ ] Empty state: `account_balance` 48dp `#75796C` + title_medium + body_medium — Cancel button only
- [ ] All text: Outfit typeface. Min touch targets 48dp for buttons.

---

_Generated by /idea export | 2026-06-15_
