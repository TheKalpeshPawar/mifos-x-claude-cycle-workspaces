# Product — Figma Design Prompt

> Generated from `screens/product/ui.yaml` by `/idea-feature-mockup`
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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Header card, rate rows |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Product name, row labels |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Section headers, product id, **rates + charges (neutral)** |
| `color/secondary` | `#50606E` | `#B7C9D9` | Product type label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

`bodyLarge`/`bodySmall` → **Roboto Mono** for rates, charges and the product id. Radius: card
`radius/md`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: product_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Product" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

### Content

```
Frame: product_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   ├─ product_header_card (Fill × Hug, padding 16dp, radius/md, gap 4dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ product_type_label: "PERSONAL CURRENT ACCOUNT"
  │   │   │     (labelSmall, UPPERCASE, color/secondary)
  │   │   ├─ product_name: "HSBC Advance Account" (titleLarge, color/onSurface)
  │   │   └─ product_id: "PCA-ADV-001" (bodySmall, Roboto Mono,
  │   │         color/onSurfaceVariant)
  │   ├─ fees_header (Fill, Hug, padding 16/0/8/0)
  │   │   └─ "FEES & CHARGES" (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   ├─ monthly_max_charge_row (Fill × 56dp, padding 12/16, radius/md,
  │   │                          Auto Layout Horizontal, space-between, align center)
  │   │   Fill: color/surfaceContainer
  │   │   ├─ Label: "Monthly maximum charge" (bodyLarge, color/onSurface, Fill)
  │   │   └─ Value: "£80.00" (bodyLarge, Roboto Mono, color/onSurfaceVariant)
  │   ├─ credit_interest_header → "CREDIT INTEREST"
  │   └─ credit_interest_list (Fill, Auto Layout Vertical, gap 0dp, radius/md,
  │                            clip content, Fill: color/surfaceContainer)
  │       └─ tier_band_row (Fill × 48dp, padding 12/16,
  │                         Auto Layout Horizontal, align center, gap 8dp)
  │           ├─ Tier: "Tier 1" (bodyMedium, color/onSurfaceVariant)
  │           ├─ Range: "£0 – £1,000" (bodyMedium, Roboto Mono, Fill)
  │           └─ Rate: "0.15%" (bodyLarge, Roboto Mono, color/onSurfaceVariant,
  │                 align end)
  └─ BottomNav
```

> **Write a single `%`, never `%%`.** Compose Multiplatform's resource formatter does **not**
> collapse Android's `%%` escape — `"%1$s%% AER"` renders as `0.15%% AER` on device. No test
> catches it (tags and counts pass), so verify against a screenshot golden. This screen is the
> app's densest user of the percent sign; it is the most likely place for the bug to appear.

Tier bands arrive **pre-flattened** — `ProductTerms` in `core/model` converts the nested OBIE
`PCA`/`BCA` band groups into plain lists. Design a flat repeating row; do not build a nested
group-within-group structure.

Rates and charges are `color/onSurfaceVariant` (`semantic.money.neutral`) and **unsigned** — an
interest rate is not a credit or a debit.

### Empty

```
Frame: product_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: description (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No product details" (headlineMedium, center)
  │   └─ Body: "The bank doesn't publish terms for this account."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

**Two distinct outcomes render this frame, and neither is an error:**

| Outcome | Why |
|---|---|
| `Success(null)` | no `PCA` or `BCA` block — the **normal** answer for GlobalMoney, Savings, CreditCard |
| **HTTP 404** | the bank publishes no product resource for this account |

Neither gets the error glyph or a Retry. Do **not** route 404 to the Error frame — a stale test
row (`tests.yaml` TC-PROD-006) still asserts that it should; the contradiction was resolved to
empty on 2026-07-30 and the test was not updated.

### Error

```
Frame: product_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load product details" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

Reserved for **401, 403 and transport failures only**.

---

## 4. Component Variants

### card: `product_header_card`

- Fill × Hug · Padding 16dp · Radius `radius/md` · Gap 4dp
- Fill `color/surfaceContainer` · Elevation `level1` tonal
- **No interactive states** — informational

### list_item: `monthly_max_charge_row` / `tier_band_row`

| Property | Values |
|---|---|
| Shape | **Charge row** (label + value), Tier row (tier + range + rate) |

- Fill × 56dp (charge) / 48dp (tier) · Padding 12/16 · Fill `color/surfaceContainer`
- **No interactive states** — nothing on this screen is tappable

Tier rows are clipped inside a single `radius/md` container so consecutive bands read as one table
rather than separate cards.

### section_header

Fill × Hug · Padding 16/0/8/0 · `labelMedium` **uppercase** `color/onSurfaceVariant`.
Non-interactive; the padding is what separates groups — there are no dividers.

### button: `retry_button`

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
States: Default / Pressed (+ripple) / Focused (2dp outline offset) / Disabled (38%).

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `description` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width cards. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped 600dp, centred. Do **not** widen the tier table — a rate 900dp from its band range stops reading as a pair |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Product terms are a charges disclosure; a decorative wash behind fee information is exactly the wrong emphasis in a regulated context. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `secondary` `#50606E` | `surfaceContainer` `#EBEEF3` | 6.0:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. Rates and charges are `bodyLarge` (16sp) — below the 18sp large-text threshold —
so measured against 4.5:1. Ratios from `state/DESIGN_SYSTEM_STATE.yaml`.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). Because this screen is **uncached** by design
(`cache_strategy: none`), the spinner appears on every visit — do not add a stagger or reveal
animation to the tier rows, which would make a routine re-fetch feel like a slow load.
