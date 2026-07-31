# Standing Orders — Figma Design Prompt

> Generated from `screens/standing-orders/ui.yaml` by `/idea-feature-mockup`
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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Order card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Creditor name, dates |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Summary, identification, reference, **amount (neutral)** |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Active** badge fill |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Active badge label |
| `color/outline` | `#72787E` | `#8B9198` | **Inactive** badge border |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration **only** |

`bodySmall` → **Roboto Mono** for amounts and sort-code/account identifiers. Radius: card
`radius/md`, badges and button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: standing-orders_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Standing Orders" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

### Content

```
Frame: standing-orders_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ summary_row (Fill, Hug, padding 12/16/4/16)
  │   └─ "3 Active · 1 Inactive" (bodyMedium, color/onSurfaceVariant)
  ├─ standing_orders_list (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   └─ standing_order_card (Fill × Hug, padding 12dp, radius/md, gap 4dp)
  │       Fill: color/surfaceContainer · Elevation: level1 (tonal)
  │       ├─ Row (Fill, Auto Layout Horizontal, space-between, align center)
  │       │   ├─ creditorName: "Jameson Lettings" (titleMedium, Fill)
  │       │   └─ status_badge (Hug, padding 2/8, radius/full)
  │       │       Variant: Active | Inactive
  │       ├─ creditorIdentification: "40-12-09 65872310"
  │       │     (bodySmall, Roboto Mono, color/onSurfaceVariant)
  │       ├─ amountAndFrequency: "£850.00 · Monthly on the 1st"
  │       │     (bodySmall — amount in Roboto Mono, color/onSurfaceVariant)
  │       ├─ nextPayment: "Next 1 Aug 2026" (bodySmall, color/onSurface)
  │       └─ finalPayment: "Final 4 Aug 2027" (bodySmall, color/onSurfaceVariant)
  │             [CONDITIONAL — hasFinalPayment]
  └─ BottomNav
```

Two rules that are behavioural, not cosmetic:

1. **Frequency is decoded, never raw.** OBIE sends ISO 20022 codes (`IntrvlMnthDay`,
   `IntrvlWkDay`, `IntrvlDay`, `IntrvlYear`). A sealed `FrequencyDecoder` in the ViewModel turns
   them into "Monthly on the 1st" / "Every 2 weeks". Never surface the code.
2. **`Final` row is conditional, not blank.** Give it a **Visible** boolean variant, default
   **off**. An open-ended standing order has no final payment; a labelled row with an em dash reads
   as *missing* data rather than *absent* data.

Cards are **not tappable** — read-only, no detail screen, no amend/cancel. No ripple or chevron.

### Empty

```
Frame: standing-orders_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: event_repeat (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No standing orders" (headlineMedium, center)
  │   └─ Body: "This account has no standing orders set up."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

### Unsupported — its own frame

```
Frame: standing-orders_unsupported (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ UnsupportedContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: info_outline (64dp, color/onSurfaceVariant)   ← NOT color/error
  │   ├─ Title: "Standing orders aren't available for this account"
  │   │          (headlineMedium, center, color/onSurface)
  │   └─ Body: "{uiState.message}" (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

Identical contract to `direct-debits` and `scheduled-payments`: `info_outline` in
`onSurfaceVariant`, **no CTA of any kind**, bank's own message verbatim. Build the three
identically — they are one visual contract across three features.

### Error

```
Frame: standing-orders_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load standing orders" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, filled)
  └─ BottomNav
```

---

## 4. Component Variants

### badge: `status_badge`

| Property | Values |
|---|---|
| Status | **Active** (default), Inactive |

| Status | Fill | Border | Label colour |
|---|---|---|---|
| Active | `color/secondaryContainer` | none | `color/onSecondaryContainer` |
| Inactive | transparent | 1dp `color/outline` | `color/onSurfaceVariant` |

Hug × 20dp · Padding 2/8 · Radius `radius/full` · labelSmall. Tonal-vs-outlined, never
green-vs-red — an inactive standing order is a valid record, not a failure.

### card: `standing_order_card`

| Property | Values |
|---|---|
| Has final payment | **false** (default), true |

- Fill × Hug · Padding 12dp · Radius `radius/md` · Gap 4dp
- Fill `color/surfaceContainer` · Elevation `level1` tonal
- **No interactive states**

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
| `event_repeat` | 64dp | Empty illustration |
| `info_outline` | 64dp | **Unsupported** illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width cards. Primary target. |
| Medium (600–840dp) | List column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** grid — the name/badge row relies on space-between across the full card width |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash belongs to home's balance card; equal-weight list rows must not be privileged. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `outline` `#72787E` (inactive border) | `surfaceContainer` `#EBEEF3` | 3.9:1 | 3.0 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

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

Loading → content cross-fades at `medium` (300ms). Empty and unsupported arrive without transition.
