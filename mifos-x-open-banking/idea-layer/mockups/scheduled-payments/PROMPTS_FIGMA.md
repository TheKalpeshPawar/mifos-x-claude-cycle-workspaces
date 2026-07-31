# Scheduled payments — Figma Design Prompt

> Generated from `screens/scheduled-payments/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow** (account-scoped pushed screen)

---

## 2. Design Token Variables

One shared Figma variable collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Payment card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Payee name, date |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Identifier, reference, **amount (neutral)**, unsupported glyph |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Scheduled-type chip |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Chip label + icon |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration **only** |

`headlineSmall`/`bodySmall` → **Roboto Mono** for amounts and sort-code/account identifiers.
Radius: card `radius/md`, chip and button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: scheduled-payments_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Scheduled payments" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

Centred spinner, **not** a shimmer skeleton — list length is unknown, so a skeleton would guess a
shape it cannot know. (Contrast `accounts`, where three cards are always plausible.)

### Content

```
Frame: scheduled-payments_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ scheduled_payments_list (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   └─ scheduled_payment_card (Fill × Hug, padding 12dp, radius/md, gap 4dp)
  │       Fill: color/surfaceContainer · Elevation: level1 (tonal)
  │       ├─ payeeName: "HMRC Self Assessment" (titleMedium, color/onSurface)
  │       ├─ creditorIdentification: "08-32-00 12001039"
  │       │     (bodySmall, Roboto Mono, color/onSurfaceVariant)
  │       ├─ Row (Fill, Auto Layout Horizontal, space-between, align center)
  │       │   ├─ typeChip (Hug, padding 4/8, gap 4dp, radius/full,
  │       │   │            Fill: color/secondaryContainer)
  │       │   │   ├─ Icon (16dp) — calendar_today | arrow_downward
  │       │   │   └─ Label (labelSmall) — "Execution date" | "Arrival date"
  │       │   └─ amountLabel: "GBP 842.00" (headlineSmall, Roboto Mono,
  │       │                                 color/onSurfaceVariant, align end)
  │       ├─ reference: "HMRC-SA-2526" (bodySmall, color/onSurfaceVariant)
  │       └─ scheduledDateLabel: "Thu 31 Jul 2026" (bodySmall, color/onSurface)
  └─ BottomNav
```

Cards are **not tappable** — no detail screen exists. Do not add Pressed/ripple states or a
chevron; both would promise navigation that does not exist.

Amount is `color/onSurfaceVariant` and **unsigned**: a scheduled instruction is not a movement.

### Empty

```
Frame: scheduled-payments_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: schedule (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No scheduled payments" (headlineMedium, center)
  │   └─ Body: "This account has no future-dated payments set up."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

### Unsupported — a separate frame, not an error variant

```
Frame: scheduled-payments_unsupported (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ UnsupportedContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: info_outline (64dp, color/onSurfaceVariant)   ← NOT color/error
  │   ├─ Title: "Scheduled payments aren't available for this account"
  │   │          (headlineMedium, center, color/onSurface)
  │   └─ Body: "{uiState.message}" (bodyMedium, center, color/onSurfaceVariant)
  │            — the ASPSP's own words, verbatim
  └─ BottomNav
```

**No retry button.** Build this as its own frame, not an Error variant with the CTA hidden — the
two states mean different things and must not converge. Three rules:

1. Glyph is `info_outline` in `color/onSurfaceVariant`, **never** `error_outline` in `color/error`.
   A product that does not offer a feature is not a fault.
2. No retry, no CTA at all. There is nothing to retry — the servicer refused the resource.
3. The body is the bank's own message rendered verbatim, not a paraphrase.

Mirrors `direct-debits_unsupported` and `standing-orders_unsupported` exactly; the three gated
features share one visual contract.

### Error

```
Frame: scheduled-payments_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load scheduled payments" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ Label: "Try again" (labelLarge, color/onPrimary)
  └─ BottomNav
```

Retry is **unconditional** — all four error kinds (`TokenExpired`, `ConsentRevoked`,
`RateLimited`, `NetworkError`) are retryable.

---

## 4. Component Variants

### card: `scheduled_payment_card`

| Property | Values |
|---|---|
| Scheduled type | **Execution date** (default), Arrival date |

- Fill × Hug · Padding 12dp · Radius `radius/md` · Gap 4dp
- Fill `color/surfaceContainer` · Elevation `level1` tonal
- **No interactive states** — not tappable

### chip: `typeChip`

| Property | Values |
|---|---|
| Type | **Execution date** (default), Arrival date |

| Type | Icon | Label | Meaning |
|---|---|---|---|
| Execution date | `calendar_today` | "Execution date" | money **leaves** the account that day |
| Arrival date | `arrow_downward` | "Arrival date" | funds **arrive at the beneficiary** that day |

Hug × 24dp · Padding 4/8 · Gap 4dp · Radius `radius/full` · Fill `color/secondaryContainer` ·
Icon 16dp · Label labelSmall `color/onSecondaryContainer`.

These are different promises about the customer's money, not a cosmetic pair. Keep both the icon
and the label — dropping the label to save width would leave two near-identical glyphs carrying a
distinction the PSU needs.

### button: `retry_button`

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
States: Default / Pressed (+ripple) / Focused (2dp outline offset) / Disabled (38%).

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`. Meets the 48dp minimum — do not
shrink the frame to the glyph.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `calendar_today` | 16dp | Execution-date chip |
| `arrow_downward` | 16dp | Arrival-date chip |
| `schedule` | 64dp | Empty illustration |
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
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** grid — the chip/amount row relies on space-between across the full card width |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash belongs to home's balance card; a list of equal-weight future payments must not privilege a row. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
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

Loading → content cross-fades at `medium` (300ms). The unsupported and empty frames arrive without
transition: they are answers, not loading outcomes, and animating them in suggests something is
still resolving.
