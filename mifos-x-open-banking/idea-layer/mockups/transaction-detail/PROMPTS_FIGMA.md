# Transaction detail — Figma Design Prompt

> Generated from `screens/transaction-detail/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow**

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Amount card, details group |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Merchant, detail values |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Timestamp, labels, **balance after (neutral)** |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Category tag |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Category label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, copy icon, **credit amount** |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Debit amount**, error glyph |
| `color/inverseSurface` | `#2D3135` | `#E0E3E8` | Copy-confirmation snackbar |

All figures → **Roboto Mono**. Radius: cards `radius/md`, tag `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Content

```
Frame: transaction-detail_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Transaction" (titleLarge, color/onSurface, Fill)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 16dp)
  │   ├─ amount_card (Fill × Hug, padding 24dp, radius/md, gap 8dp,
  │   │               Auto Layout Vertical, align CENTER)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ amount: "−£42.19" (displaySmall, ROBOTO MONO, center)
  │   │   │     Variant: Credit → color/primary | Debit → color/error
  │   │   ├─ merchant: "Tesco Stores" (titleMedium, center, color/onSurface)
  │   │   ├─ timestamp: "29 Jul 2026, 14:02" (bodyMedium, center,
  │   │   │     color/onSurfaceVariant)
  │   │   └─ category_tag (Hug, padding 2/8, radius/full,
  │   │         Fill: color/secondaryContainer, labelSmall)
  │   ├─ details_header → "DETAILS" (labelMedium, UPPERCASE,
  │   │     color/onSurfaceVariant)
  │   └─ details_list (Fill, Vertical, gap 0dp, radius/md, clip,
  │                    Fill: color/surfaceContainer)
  │       ├─ status_row       "Status"         / "Booked"
  │       ├─ type_row         "Type"           / "Card payment"
  │       ├─ balance_after_row "Balance after" / "£21,530.92"
  │       │     Value: bodyLarge ROBOTO MONO color/onSurfaceVariant — UNSIGNED
  │       └─ reference_row    "Reference"      / "TESCO 4471"  + copy_button
  │             copy_button: IconButton (48dp target, content_copy 24dp,
  │                   color/primary)
  └─ BottomNav (Fill × 80dp)
```

### The two money treatments — and why they must not be unified

| Figure | Colour | Signed? |
|---|---|:---:|
| Amount (hero) | `color/primary` credit / `color/error` debit | **Yes**, with `+`/`−` |
| **Balance after** | `color/onSurfaceVariant` | **No** |

This is a **shipped bug fix**, not a style choice. HSBC sets the per-transaction
`Balance.CreditDebitIndicator` to the **transaction's** direction, not the balance's — so every
debit on an account in credit arrives marked `Debit`. The sandbox returns
`Balance {Debit, ITBD, 21530.92}` for an account whose `/balances` reports `{Credit, ITBD,
21530.92}`. Signing the running balance off that indicator rendered **£21,530.92 as −£21,530.92**.

Do not tint `Balance after` red, do not add a `−`, and do not "make it consistent" with the hero
amount above it.

### Empty — no retry

```
Frame: transaction-detail_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: search_off (64dp, color/onSurfaceVariant)
  │   ├─ Title: "Transaction not found" (headlineMedium, center)
  │   └─ Body: "This transaction isn't in the account's available history."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

**No CTA.** The account's transactions loaded successfully; none matched. Refetching the same list
yields the same absence — usually a stale deep link or a transaction aged out of the window.

### Error

```
Frame: transaction-detail_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load this transaction" (headlineMedium, center)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

### Copy confirmation

```
Overlay: transaction-detail_copied (on the CONTENT frame)
  └─ Snackbar (Fill − 32dp, Hug, padding 14/16, radius/xs,
               anchored above BottomNav + 16dp)
      Fill: color/inverseSurface ·
      Label: "Reference copied" (bodyMedium, color/inverseOnSurface)
```

### Loading

Centred 48dp `color/primary` indicator, top app bar and bottom nav retained.

---

## 4. Component Variants

### card: `amount_card`

| Property | Values |
|---|---|
| Direction | **Debit** (default), Credit |

Fill × Hug · Padding 24dp · Radius `radius/md` · Gap 8dp · **centre-aligned** · Fill
`color/surfaceContainer` · Elevation `level1` · **No interactive states**.

Centre alignment is deliberate here, as on `account-holder`'s identity card — the amount is the
screen's subject, not a data row.

### list_item: detail rows

| Property | Values |
|---|---|
| Trailing | **none** (default), copy |
| Value tone | **default** (`onSurface`), **neutral-mono** (`onSurfaceVariant`) |

Fill × 48dp · Padding 12/16 · space-between · **No interactive states on the row itself** — only
the copy icon is tappable. Rows clipped inside one `radius/md` container so details read as a
table.

Use **neutral-mono** for `Balance after`. Every other value uses the default tone.

### icon_button: `copy_button`

48dp × 48dp touch target · 24dp `content_copy` · `color/primary`. States: Default / Pressed
(+ripple) / Focused (2dp outline).

Copy is performed by the **Screen** against `LocalClipboardManager`, not the ViewModel — the
ViewModel emits a `CopyToClipboard` event. Same seam `statements` uses for file delivery.

### chip: `category_tag`

Hug × 20dp · Padding 2/8 · Radius `radius/full` · Fill `color/secondaryContainer` · labelSmall.
Non-interactive.

### icon_button: `back_button` / button: `retry_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. Retry: Fill × 48dp, `radius/full`,
`color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `content_copy` | 24dp | Copy reference |
| `search_off` | 64dp | Not-found illustration |
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
| Expanded (> 840dp) | Content column capped 600dp, centred. Amount card stays centre-aligned; do not left-align at width |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The amount card is a hero surface, but a wash behind a figure that is already the largest coloured element competes with the one thing the screen exists to show. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Amount colour carries credit/debit semantics and must stay flat. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `primary` `#266489` (credit amount) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 3.0 (large) | ✅ |
| `error` `#BA1A1A` (debit amount) | `surfaceContainer` `#EBEEF3` | 5.7:1 | 3.0 (large) | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `inverseOnSurface` `#EEF1F6` | `inverseSurface` `#2D3135` | 12.1:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (copy icon) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 3.0 | ✅ |

All pass WCAG AA. The hero amount is `displaySmall` (36sp), so it clears the **large-text** 3:1
threshold — and it carries a `+`/`−` sign, so direction never depends on colour (WCAG 1.4.1).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). Copy snackbar enters at `short` (150ms),
auto-dismisses after 4s. **No count-up or odometer animation on the amount** — a transaction figure
is a fact, not a score.
