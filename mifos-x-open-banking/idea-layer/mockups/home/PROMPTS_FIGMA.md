# Home — Figma Design Prompt

> Generated from `screens/home/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, **Home tab active** · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp, **no leading icon** (tab root)

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Hero card, transaction group |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Row pressed |
| `color/surfaceContainerLowest` | `#FFFFFF` | `#0B0F12` | **Bottom sheet** surface |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Merchant names, hero balance |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Dates, labels, **hero balance (neutral)** |
| `color/primary` | `#266489` | `#95CDF7` | **Credit amounts**, active tab, links |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Debit amounts** |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Selected row in sheet |

`displaySmall`/`bodyLarge` → **Roboto Mono** for all money. Radius: cards `radius/md`, sheet
**`radius/xl` (28dp) top corners only**. Theme **auto**.

---

## 3. Auto Layout Structure

### Content

```
Frame: home_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, padding 4/16)
  │   └─ Title: "Home" (titleLarge, color/onSurface)   — NO leading icon
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 16dp)
  │   ├─ AccountSwitcherRow (Fill × 48dp, padding 8/4, Horizontal, gap 4dp)
  │   │   ├─ "Current account ·· 3349" (bodyLarge, color/onSurface, Fill)
  │   │   └─ Icon: arrow_drop_down (24dp, color/onSurfaceVariant)
  │   ├─ HeroBalanceCard (Fill × Hug, padding 20dp, radius/md, gap 4dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ Label: "Available" (bodyMedium, color/onSurfaceVariant)
  │   │   ├─ Balance: "£21,530.92" (displaySmall, ROBOTO MONO,
  │   │   │     color/onSurfaceVariant)      ← NEUTRAL, UNSIGNED
  │   │   └─ Sub: "Current £21,530.92" (bodyMedium, Roboto Mono,
  │   │         color/onSurfaceVariant)
  │   │   TAP TARGET: the whole card → opens AccountSelectorSheet
  │   ├─ SectionRow (Fill, Horizontal, space-between, align center)
  │   │   ├─ "RECENT" (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   │   └─ view_all_transactions_link (Hug, padding 8/4)
  │   │       └─ "View all" (labelLarge, color/primary)
  │   └─ RecentTransactionsSection (Fill, Vertical, gap 0dp, radius/md, clip,
  │                                 Fill: color/surfaceContainer)
  │       └─ transaction_row (Fill × 64dp, padding 12/16, Horizontal,
  │                           space-between, align center)
  │           ├─ TextColumn (Fill, gap 2dp)
  │           │   ├─ Merchant: "Tesco Stores" (bodyLarge, color/onSurface)
  │           │   └─ Date: "29 Jul 2026" (bodySmall, color/onSurfaceVariant)
  │           └─ Amount: "−£42.19" (bodyLarge, ROBOTO MONO, align end)
  │                 Variant: Credit → color/primary | Debit → color/error
  └─ BottomNav (Fill × 80dp) — Home active
```

**The money rule on this screen, and it differs by component:**

| Figure | Colour | Signed? |
|---|---|:---:|
| Hero balance | `color/onSurfaceVariant` (neutral) | **No** |
| Transaction amount | `color/primary` credit / `color/error` debit | **Yes** |

A balance is a *position*; a transaction is a *movement*. Signing a running balance off a
per-transaction `CreditDebitIndicator` renders a healthy account as negative — a real trap in this
codebase. Never green/red: these two hues stay distinguishable under deuteranopia and protanopia.

> **The hero card's tap opens the account-selector sheet — it does NOT navigate.** `ui.yaml`
> declared `navigate_account_detail → account-detail` until 2026-07-30; source has no such
> navigation (`HomeContent.kt:63` → `onClick = onOpenAccountSelector`, and
> `onNavigateToAccountDetail` appears nowhere in `feature/home`). Account detail is reached from
> the **Accounts tab**. Do not add a chevron or any navigational affordance to this card.

### Overlay: `AccountSelectorSheet` — the app's only bottom sheet

```
Overlay: home_account_selector_sheet
  Fill: color/surfaceContainerLowest · Radius: radius/xl TOP CORNERS ONLY (28dp)
  Elevation: level3 · Scrim: color/scrim @ 32%
  ├─ DragHandle (32dp × 4dp, radius/full, color/onSurfaceVariant @ 40%, centered)
  ├─ Title: "Choose an account" (titleMedium, padding 16dp)
  └─ AccountRow ×N (Fill × 64dp, padding 12/16, Horizontal, gap 16dp)
      Variant: Selected | Unselected
      ├─ Icon: check (24dp, color/primary)        [Selected only]
      ├─ TextColumn (Fill) — name (bodyLarge) + balance (bodyMedium, Roboto Mono)
      └─ Selected row Fill: color/secondaryContainer
```

Build the **content as its own component**, separate from the sheet wrapper. Source splits them
deliberately: a sheet renders in its own window where `onNodeWithTag` is unreliable, so tests drive
the content composable directly. A single monolithic sheet component cannot be tested that way.

Radius applies to the **top corners only** — bottom corners are square against the screen edge.

### Loading

```
Frame: home_loading (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ SkeletonColumn (Fill, Vertical, padding 12dp, gap 16dp)
  │   ├─ Shimmer (160dp × 24dp, radius/sm)          — switcher
  │   ├─ Shimmer (Fill × 132dp, radius/md)          — hero card, REAL height
  │   └─ Shimmer ×3 (Fill × 64dp, radius/sm)        — transaction rows
  └─ BottomNav (same)
```

Shimmer heights match real content exactly (hero 132dp, rows 64dp) so content arrival causes no
layout jump.

### Empty

```
Frame: home_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: account_balance_wallet (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No accounts connected" (headlineMedium, center)
  │   └─ Body: "Your Open Banking consent has no active accounts. Connect a bank
  │             from Settings → Consents to get started."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav (same)
```

> **No CTA button.** A `connect_bank_button → login` was declared in `ui.yaml` until 2026-07-30 and
> **removed**: `HomeEmpty.kt:37` says *"Points the PSU to Settings rather than offering its own
> connect button"*, the source file has no `Button` and no `onClick`, and `homeGraph` has no login
> lambda. The connect/renew affordance lives **only** on the consent screens — same convention
> `beneficiaries` and `accounts` follow. Do not design a button here.

### Error

```
Frame: home_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load your account" (headlineMedium, center)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav (same)
```

---

## 4. Component Variants

### card: `HeroBalanceCard`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |

- Fill × Hug (≈132dp) · Padding 20dp · Radius `radius/md` · Fill `color/surfaceContainer` ·
  Elevation `level1`
- Pressed: `color/surfaceContainerHigh` + ripple · Focused: 2dp `color/primary`

**Interactive** (unlike most cards in the app) — the whole card is the tap target for the selector
sheet. But **no chevron, no arrow, no navigational glyph**: it opens a sheet, it does not navigate.

### list_item: `transaction_row`

| Property | Values |
|---|---|
| Direction | **Debit** (default), Credit |
| State | Default, Pressed, Focused |

- Fill × 64dp · Padding 12/16 · space-between
- Amount: `bodyLarge` **Roboto Mono**, align end

| Direction | Amount colour | Prefix |
|---|---|---|
| Debit | `color/error` | `−` |
| Credit | `color/primary` | `+` |

Rows are tappable → `transaction-detail`. Pressed `color/surfaceContainerHigh` + ripple.

### AccountRow (sheet)

| Property | Values |
|---|---|
| Selected | **false** (default), true |

Fill × 64dp · Padding 12/16 · Selected: Fill `color/secondaryContainer` + leading `check` 24dp
`color/primary`. Selecting persists **and** closes the sheet in one action.

### button: `view_all_transactions_link` / `retry_button`

Link: Hug, padding 8/4, labelLarge `color/primary`, text emphasis.
Retry: Fill × 48dp, `radius/full`, `color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_drop_down` | 24dp | Account switcher |
| `check` | 24dp | Selected row in sheet |
| `account_balance_wallet` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped 600dp, centred. Sheet becomes a centred dialog at 400dp max-width |

Do not place the hero card and transaction list side by side at width — the hero is the screen's
single focal point, and pairing it with a list demotes it.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused, and this is the closest call in the project.** The token is named `hero` and this is the app's hero card. It stays flat because the card is now also a **tap target** for the selector sheet: a gradient would read as decorative emphasis on a surface whose affordance is already under-signalled (no chevron by design). DESIGN.md's low-variance dial settles it. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Transaction amounts carry the only colour semantics here, and they must be flat `primary`/`error` to stay readable as credit/debit. `tertiary` unused project-wide. |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `primary` `#266489` (credit) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (debit) | `surfaceContainer` `#EBEEF3` | 5.7:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainerLowest` `#FFFFFF` | 16.8:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `primary` `#266489` (link) | `surface` `#F7F9FF` | 6.11:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |

All pass WCAG AA. Credit/debit amounts clear 4.5:1 **and** carry a `+`/`−` sign, so direction never
depends on colour alone (WCAG 1.4.1).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Sheet enters at `medium` (300ms) with the standard M3 slide-up + scrim fade; dismiss at `short`
(150ms). Switching account re-emits the hero and list at `short` cross-fade — **no** counting or
odometer animation on the balance. Under OS reduce-motion the sheet cross-fades in place.
