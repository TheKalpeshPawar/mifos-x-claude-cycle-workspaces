# Transactions — Figma Design Prompt

> Generated from `screens/transactions/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Transaction group |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Row pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Merchant names |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Dates, group headers |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Category tag** |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Category label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, **credit amounts**, footer indicator |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Debit amounts**, error glyph |

Amounts → **Roboto Mono**. Radius: group `radius/md`, tag `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: transactions_loading (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Transactions" (titleLarge, color/onSurface, Fill)
  ├─ SkeletonColumn (Fill, Vertical, padding 12dp, gap 8dp)
  │   └─ Shimmer ×6 (Fill × 64dp, radius/sm)   — REAL row height
  └─ BottomNav (Fill × 80dp)
```

### Content — grouped, paged

```
Frame: transactions_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ transactions_list (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   ├─ date_group_header (Fill, Hug, padding 12/4/4/4)
  │   │   └─ "JULY 2026" (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   ├─ GroupBlock (Fill, Vertical, gap 0dp, radius/md, clip,
  │   │              Fill: color/surfaceContainer)
  │   │   └─ transaction_row (Fill × 64dp, padding 12/16,
  │   │                       Horizontal, space-between, align center)
  │   │       ├─ TextColumn (Fill weight 1, Vertical, gap 2dp)
  │   │       │   ├─ merchant: "Tesco Stores" (bodyLarge, color/onSurface)
  │   │       │   └─ MetaRow (Horizontal, gap 6dp, align center)
  │   │       │       ├─ date: "29 Jul" (bodySmall, color/onSurfaceVariant)
  │   │       │       └─ tx_category_tag (Hug, padding 2/8, radius/full,
  │   │       │             Fill: color/secondaryContainer, labelSmall)
  │   │       └─ amount: "−£42.19" (bodyLarge, ROBOTO MONO, align end)
  │   │             Variant: Credit → color/primary | Debit → color/error
  │   ├─ date_group_header → "JUNE 2026"
  │   └─ GroupBlock …
  ├─ page_loading_footer (Fill × 56dp, center)   [while fetching page N+1]
  │   └─ progress_indicator (24dp circular, color/primary)
  └─ BottomNav
```

**This is a suspend cursor-pager, not a stream.** Three consequences for the design:

1. **No pull-to-refresh.** There is no stream to refresh; the gesture would restart the cursor and
   lose scroll position. Do not add the affordance.
2. **The next-page indicator is a list footer**, 24dp, not a screen-level spinner. Existing rows
   stay visible and interactive while page N+1 loads.
3. **A page-load failure does not replace the screen** — see the footer-error variant below.

Amounts are **signed and coloured**: credit `+` in `color/primary`, debit `−` in `color/error`.
Never green/red — these hues stay distinguishable under deuteranopia and protanopia, and the sign
means colour is never the sole signal.

> **`tx_category_tag` has no `accessibility_label`** — one of exactly two such components in the
> project. A screen-reader user hears merchant, date and amount but **not** the category. Recorded
> as a known gap; if you add one in Figma, mirror it into `ui.yaml`.

### Page-load failure — footer, not full screen

```
Variant: transactions_content / page_error
  page_loading_footer is replaced by:
  └─ FooterError (Fill × 56dp, Horizontal, center, gap 8dp)
      ├─ "Couldn't load more" (bodySmall, color/onSurfaceVariant)
      └─ retry_link "Retry" (labelLarge, color/primary, text button)
```

Already-loaded transactions **remain visible and tappable**. Replacing a screenful of successfully
loaded data because page 3 failed would be a worse outcome than the failure.

### Empty / Error

```
Frame: transactions_empty  — Icon receipt_long (64dp, color/onSurfaceVariant),
       "No transactions", "This account has no activity in the available period."
       NO CTA

Frame: transactions_error  — Icon error_outline (64dp, color/error),
       "Couldn't load transactions", CTA "Try again"
```

The Error frame covers **first-page failures only**.

---

## 4. Component Variants

### list_item: `transaction_row`

| Property | Values |
|---|---|
| Direction | **Debit** (default), Credit |
| State | Default, Pressed, Focused |
| Category tag | **true** (default), false |

- Fill × 64dp, **min 48dp** · Padding 12/16 · space-between
- Pressed `color/surfaceContainerHigh` + ripple · Focused 2dp `color/primary`

| Direction | Amount colour | Prefix |
|---|---|---|
| Debit | `color/error` | `−` |
| Credit | `color/primary` | `+` |

Rows are clipped inside one `radius/md` group per month so a date group reads as a block.

### chip: `tx_category_tag`

Hug × 20dp · Padding 2/8 · Radius `radius/full` · Fill `color/secondaryContainer` · labelSmall
`color/onSecondaryContainer`. **Non-interactive** — it labels, it does not filter. No Pressed or
Selected states, and no filter row exists on this screen.

### section_header: `date_group_header`

Fill × Hug · Padding 12/4/4/4 · `labelMedium` **uppercase** `color/onSurfaceVariant`.
Non-interactive, not sticky — the app's low-motion dial avoids pinned headers that animate on
scroll.

### icon_button: `back_button` / button: `retry_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. Retry: Fill × 48dp, `radius/full`,
`color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `receipt_long` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

No per-row category glyphs — the category is a text tag.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width rows. Primary target. |
| Medium (600–840dp) | List column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** grid — a ledger reads chronologically top-to-bottom, and two columns break that order |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** A ledger of equal-weight entries; privileging any row with a wash would misrepresent the data. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Amount colour carries the only semantics here and must stay flat `primary`/`error` to read as credit/debit. `tertiary` unused project-wide. |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `primary` `#266489` (credit) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (debit) | `surfaceContainer` `#EBEEF3` | 5.7:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |

All pass WCAG AA. Amounts carry a `+`/`−` sign alongside colour (WCAG 1.4.1).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). **Appended pages must not animate in** — no
fade, no slide, no stagger. New rows arriving with motion below the fold pulls the eye away from
what the customer is reading; they simply exist when scrolled to.
