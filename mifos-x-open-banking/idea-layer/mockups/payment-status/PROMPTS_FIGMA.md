# Payment status — Figma Design Prompt

> Generated from `screens/payment-status/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, Pay tab active · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow** (pushed screen, unlike its send-money parent)

---

## 2. Design Token Variables

Token values are **identical across every feature in this project** — one Figma variable
collection, resolved once from `design-tokens.yaml` 2.1.0. Do not re-derive per file. The full
light/dark colour tables, the M3 type scale, spacing and radius are enumerated in
`mockups/send-money/PROMPTS_FIGMA.md §2`.

The subset this screen actually binds:

| Variable | Light | Dark | Usage here |
|---|---|---|---|
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **In-progress chip** |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | In-progress chip text + icon |
| `color/primaryContainer` | `#C9E6FF` | `#004B6F` | **Settled chip** |
| `color/onPrimaryContainer` | `#004B6F` | `#C9E6FF` | Settled chip text + icon |
| `color/errorContainer` | `#FFDAD6` | `#93000A` | **Rejected chip** |
| `color/onErrorContainer` | `#93000A` | `#FFDAD6` | Rejected chip text + icon |
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Summary card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Values, title |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Labels, note text, **amount (neutral)** |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, refresh CTA, active tab |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

Typography: `headlineSmall` bound to **Roboto Mono** for the amount; everything else Roboto.
Radius: card `radius/md` (12dp), buttons and chips `radius/full`.

Theme is **auto**. Do not pin a mode.

---

## 3. Auto Layout Structure

### Loading

```
Frame: payment-status_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp × 48dp, icon arrow_back 24dp, color/primary)
  │   └─ Title: "Payment status" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp) — Pay active
```

### Content — the one frame, three chip variants

Build **one** content frame. The disposition differences are a chip variant plus two conditional
children — not three separate frames.

```
Frame: payment-status_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same as loading)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 16dp, gap 16dp)
  │   ├─ status_chip (Hug, Auto Layout Horizontal, padding 8/16, gap 8dp, radius/full)
  │   │   Variant property: Disposition = In progress | Settled | Rejected
  │   │   ├─ Icon (18dp)      — schedule | check_circle | error
  │   │   └─ Label (labelLarge) — "In progress" | "Settled" | "Rejected"
  │   ├─ payment_summary (Fill × Hug, padding 16dp, radius/md, gap 16dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ Pair: "Amount"    / "£850.00"            (headlineSmall, Roboto Mono, onSurfaceVariant)
  │   │   ├─ Pair: "To"        / "Jameson Lettings"   (bodyLarge, onSurface)
  │   │   ├─ Pair: "Reference" / "RENT-FLAT12"        (bodyLarge)
  │   │   ├─ Pair: "From"      / "Current account ·· 3349" (bodyLarge)
  │   │   └─ Pair: "Submitted" / "30 Jul 2026, 10:44" (bodyLarge)
  │   │       Labels: bodySmall color/onSurfaceVariant
  │   ├─ in_progress_note (Fill, bodyMedium, color/onSurfaceVariant)   [In progress ONLY]
  │   │   "Accepted by the bank. The money has not moved yet — this can take a few
  │   │    moments to settle."
  │   ├─ refresh_button (Fill × 48dp, radius/full, tonal)              [In progress ONLY]
  │   │   Fill: color/secondaryContainer · Label: "Refresh" (labelLarge, onSecondaryContainer)
  │   └─ new_payment_button (Fill × 48dp, radius/full, filled)         [Rejected ONLY]
  │       Fill: color/primary · Label: "Start a new payment" (labelLarge, onPrimary)
  └─ BottomNav (Fill × 80dp) — Pay active
```

The **Settled** variant shows neither conditional child: nothing to refresh, nothing to restart.

The amount is `color/onSurfaceVariant` (`semantic.money.neutral`) and **unsigned** — a payment
amount is not a signed ledger movement. Do not tint it credit-blue or debit-red.

### Error

```
Frame: payment-status_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load this payment" (headlineMedium, center, color/onSurface)
  │   ├─ Message: "Payment not found" (bodyMedium, center, color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, filled)   [CONDITIONAL — see below]
  └─ BottomNav (same)
```

`retry_button` has a **Visible** boolean variant property. Default it to **off**: two of the four
error types (`PaymentNotFound`, `ConsentRevoked`) are terminal and must not offer it.

---

## 4. Component Variants

### chip: `status_chip` — the load-bearing component

| Property | Values |
|---|---|
| Disposition | **In progress** (default), Settled, Rejected |

| Disposition | Container | On-container | Icon | Contrast |
|---|---|---|---|:---:|
| In progress | `color/secondaryContainer` | `color/onSecondaryContainer` | `schedule` | 7.22:1 |
| Settled | `color/primaryContainer` | `color/onPrimaryContainer` | `check_circle` | 7.27:1 |
| Rejected | `color/errorContainer` | `color/onErrorContainer` | `error` | 7.24:1 |

- Height: Hug, min 32dp · Padding: 8/16 · Radius: `radius/full` · Gap: 8dp
- Icon 18dp · Label labelLarge

Three rules that are **not** stylistic preferences:

1. **Every variant carries icon *and* text label.** Colour is never the sole signal (WCAG 1.4.1).
   Do not build an icon-only or colour-only variant.
2. **In progress is `secondaryContainer`, not `primaryContainer`.** Primary is the credit colour in
   this system; a primary chip reads as *money arrived*. `AcceptedSettlementInProcess` means
   accepted, not settled.
3. **Settled is trust-blue, not green.** No green tick, no celebration — this is calm regulated
   finance.

Default the variant to **In progress**: an unmapped OBIE status renders as in-progress, never as
success or failure.

### card: `payment_summary`

- Width: Fill · Height: Hug · Padding: 16dp · Radius: `radius/md` · Gap: 16dp
- Fill: `color/surfaceContainer` · Elevation: `level1` (tonal, no drop shadow)
- Row: label bodySmall `color/onSurfaceVariant` above value bodyLarge `color/onSurface`
- Non-interactive — no Pressed/Focused states

Shown in **all three** dispositions, including Rejected. A rejected payment is not a blank screen.

### button: `refresh_button` (tonal) / `new_payment_button` (filled)

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, Disabled |
| Emphasis | Tonal (refresh), Filled (new payment) |

| State | Tonal background | Filled background | Opacity |
|---|---|---|:---:|
| Default | `color/secondaryContainer` | `color/primary` | 100% |
| Pressed | `color/secondaryContainer` + ripple | `color/primary` + ripple | 100% |
| Focused | + 2dp `color/primary` outline | + 2dp outline offset | 100% |
| Disabled | `color/secondaryContainer` | `color/primary` | 38% |

Height 48dp · Radius `radius/full` · Label labelLarge.

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back` glyph, `color/primary`. Meets
`accessibility.min_touch_target_dp` (48dp) — do not shrink the frame to the glyph.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `schedule` | 18dp | In-progress chip |
| `check_circle` | 18dp | Settled chip |
| `error` | 18dp | Rejected chip |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None. Material Symbols at 64dp, consistent with every other screen.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width card and CTAs. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped 600dp, centred. Do **not** widen the summary card — label/value pairs separated across 1000dp stop scanning as pairs |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash is a dashboard device. A status screen must read as factual; a gradient behind a disposition chip would add emphasis the disposition itself is supposed to carry. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface here. `tertiary` is unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onPrimaryContainer` `#004B6F` | `primaryContainer` `#C9E6FF` | 7.27:1 | 4.5 | ✅ |
| `onErrorContainer` `#93000A` | `errorContainer` `#FFDAD6` | 7.24:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |

All pass WCAG AA. Ratios are the measured values in `state/DESIGN_SYSTEM_STATE.yaml` (15 pairs
validated 2026-07-30), not re-derived.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

The chip's disposition change (in-progress → settled) uses `medium` (300ms) as a cross-fade. It
must **not** bounce, pulse or animate triumphantly — a settlement is reported, not celebrated.
