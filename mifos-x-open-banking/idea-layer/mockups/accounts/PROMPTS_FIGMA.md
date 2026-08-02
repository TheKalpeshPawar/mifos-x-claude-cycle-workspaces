# Accounts — Figma Design Prompt

> Generated from `screens/accounts/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, **Accounts tab active** · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp, **no leading icon** (tab root)

---

## 2. Design Token Variables

One Figma variable collection, resolved from `design-tokens.yaml` 2.1.0 and identical across every
feature. Full light/dark tables, type scale, spacing and radius: `mockups/send-money/PROMPTS_FIGMA.md §2`.

Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Account card, shimmer |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Card pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Nickname, balance |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Identifier, **balance (neutral)** |
| `color/secondary` | `#50606E` | `#B7C9D9` | Account subtype label |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Selected chip, owed badge |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Selected chip / badge text |
| `color/primary` | `#266489` | `#95CDF7` | Type icon, retry CTA, active tab |
| `color/outline` | `#72787E` | `#8B9198` | Unselected chip border |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

Typography: `headlineSmall` → **Roboto Mono** for balances; account identifiers also mono.
Radius: card `radius/md` (12dp), chips and buttons `radius/full`.

Theme **auto**. Do not pin a mode.

---

## 3. Auto Layout Structure

### Loading

```
Frame: accounts_loading (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, padding 4/16)
  │   └─ Title: "Accounts" (titleLarge, color/onSurface)
  ├─ SkeletonColumn (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   └─ Shimmer ×3 (Fill × 96dp, radius/md, Fill: color/surfaceContainer)
  │       Effect: shimmer sweep, 1.5s loop
  └─ BottomNav (Fill × 80dp) — Accounts active
```

Shimmer height is **96dp**, matching a real card exactly. Do not use a generic 60dp placeholder —
the point is that content arrival causes no layout jump. Note there is **no filter row** in this
frame: filtering nothing is meaningless.

### Content

```
Frame: accounts_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ account_type_filter (Fill, Auto Layout Horizontal, padding 12/8/12/12, gap 8dp)
  │   Scroll: horizontal · Selection: SINGLE
  │   └─ FilterChip ×4 — "All" (selected by default) · "Current" · "Savings" · "Credit"
  ├─ accounts_list (Fill, Auto Layout Vertical, padding-h 12dp, gap 8dp)
  │   └─ account_card (Fill × Hug, padding 12dp, radius/md, Fill: color/surfaceContainer)
  │       Elevation: level1 (tonal — NO drop shadow)
  │       └─ Row (Fill, Auto Layout Horizontal, align center, gap 12dp)
  │           ├─ account_type_icon (24dp, color/primary)   — decorative, hide from a11y tree
  │           ├─ TextColumn (Fill weight 1, Auto Layout Vertical, gap 4dp)
  │           │   ├─ account_subtype  "CACC"                    (labelSmall, color/secondary)
  │           │   ├─ account_nickname "Current account ·· 3349" (titleMedium, color/onSurface)
  │           │   └─ account_number   "80-20-01 10203349"       (bodySmall, Roboto Mono,
  │           │                                                  color/onSurfaceVariant)
  │           └─ BalanceColumn (Hug, Auto Layout Vertical, align end, gap 2dp)
  │               ├─ balance_amount "£21,530.92" (headlineSmall, Roboto Mono,
  │               │                               color/onSurfaceVariant, align end)
  │               └─ balance_owed_badge "balance owed" (Hug, padding 2/8, radius/full,
  │                   Fill: color/secondaryContainer, labelSmall)   [CONDITIONAL]
  └─ BottomNav (Fill × 80dp) — Accounts active
```

**Four chips only.** Do not add a "Global" chip — `AccountFilter` declares `ALL / CURRENT /
SAVINGS / CREDIT`. A Global Money wallet reports `CACC` and already sits under Current; a Global
chip could never match and would render a permanently empty list.

`balance_owed_badge` needs a **Visible** boolean variant, default **off** — credit cards only.

The balance is `color/onSurfaceVariant` (`semantic.money.neutral`) and **unsigned**. Do not tint it
credit-blue or debit-red: an account balance is a position, not a transaction.

### Empty

```
Frame: accounts_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: account_balance_wallet (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No accounts to show" (headlineMedium, center, color/onSurface)
  │   └─ Body: "Your consent doesn't include any accounts yet."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav (same)
```

**No CTA.** Connect/renew lives on the consent screens via Settings → Consents — the same
convention `beneficiaries` and `home` follow. Also **no filter row**: chips above an empty list
imply filtering caused the emptiness.

Empty uses `color/onSurfaceVariant` for its glyph, not `color/error` — an empty consent is a state,
not a fault.

### Error

```
Frame: accounts_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load your accounts" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ Label: "Try again" (labelLarge, color/onPrimary)
  └─ BottomNav (same)
```

Retry is **unconditional** here — unlike `payment-status`, every error reaching this surface
(including `NoNetwork` and `Unauthenticated`) is transient or re-authorisable.

---

## 4. Component Variants

### card: `account_card`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |
| Type | Current, Savings, Credit, Global money, Other |
| Balance owed | false (default), true |

- Width: Fill · Height: Hug, **min 48dp** · Padding: 12dp · Radius: `radius/md`
- Fill: `color/surfaceContainer` · Elevation: `level1` tonal

| State | Background | Border | Opacity |
|---|---|---|:---:|
| Default | `color/surfaceContainer` | none | 100% |
| Pressed | `color/surfaceContainerHigh` + ripple | none | 100% |
| Focused | `color/surfaceContainer` | 2dp `color/primary` | 100% |

The **Type** variant swaps only the leading glyph. It is `decorative: true` — hide it from the
accessibility tree; the subtype label already names the type in text.

### chip: filter chips

| Property | Values |
|---|---|
| Selected | false (default), true |
| State | Default, Pressed, Focused |

| Selected | Background | Border | Label |
|---|---|---|---|
| false | transparent | 1dp `color/outline` | `color/onSurfaceVariant` |
| true | `color/secondaryContainer` | none | `color/onSecondaryContainer` |

Height 32dp · Padding 6/12 · Radius `radius/full` · Label labelLarge. Single-select: "All" is
selected by default and exactly one chip is ever active.

### badge: `balance_owed_badge`

Hug × 20dp · Padding 2/8 · Radius `radius/full` · Fill `color/secondaryContainer` · labelSmall
`color/onSecondaryContainer`.

Tonal slate, **not** `color/error`. Money owed on a credit card is the product working normally,
not a fault — red would misrepresent a routine balance as an alarm.

### button: `retry_button`

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
States: Default / Pressed (+ripple) / Focused (2dp outline offset) / Disabled (38%).

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `account_balance` | 24dp | Current-account card glyph, Accounts tab |
| `savings` | 24dp | Savings card glyph |
| `credit_card` | 24dp | Credit-card glyph |
| `account_balance_wallet` | 64dp / 24dp | Empty illustration / global-money glyph |
| `error_outline` | 64dp | Error illustration |
| `home`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width cards. Primary target. |
| Medium (600–840dp) | List column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** switch to a 2-column grid — the card is a wide horizontal row (icon · text · right-aligned balance) and pairing them halves the balance column's width, breaking right-alignment as a scanning aid |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The hero wash belongs to home's single balance card. A list of equal-weight accounts must not privilege one row. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `secondary` `#50606E` | `surfaceContainer` `#EBEEF3` | 6.0:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `outline` `#72787E` (chip border) | `surface` `#F7F9FF` | 4.24:1 | 3.0 | ✅ |
| `primary` `#266489` (icon) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 3.0 | ✅ |

All pass WCAG AA. Ratios from `state/DESIGN_SYSTEM_STATE.yaml` (15 pairs validated 2026-07-30).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Filter changes re-emit the list at `short` (150ms) cross-fade — **no** slide or reorder animation.
The filter is client-side and instant; animating it would imply a fetch. Shimmer runs 1.5s and must
stop the moment content arrives.
