# Direct Debits — Figma Design Prompt

> Generated from `screens/direct-debits/ui.yaml` by `/idea-feature-mockup`
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

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Mandate card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Payee name |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Summary, reference, **amount (neutral)**, unsupported glyph |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Active** badge fill |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Active badge label |
| `color/outline` | `#72787E` | `#8B9198` | **Inactive** badge border |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration **only** |

`bodySmall` → **Roboto Mono** for amounts. Radius: card `radius/md`, badges and button
`radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: direct-debits_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Direct Debits" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

### Content

```
Frame: direct-debits_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ summary_row (Fill, Hug, padding 12/16/4/16)
  │   └─ "3 Active · 1 Inactive" (bodyMedium, color/onSurfaceVariant)
  ├─ direct_debits_list (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   └─ mandate_card (Fill × Hug, padding 12dp, radius/md, gap 4dp)
  │       Fill: color/surfaceContainer · Elevation: level1 (tonal)
  │       ├─ Row (Fill, Auto Layout Horizontal, space-between, align center)
  │       │   ├─ name: "British Gas" (titleMedium, color/onSurface, Fill)
  │       │   └─ status_badge (Hug, padding 2/8, radius/full)
  │       │       Variant: Active | Inactive
  │       ├─ previousPayment: "Last paid £84.20 · 12 Jul 2026"
  │       │     (bodySmall, amount in Roboto Mono, color/onSurfaceVariant)
  │       └─ mandateIdentification: "Ref 4471029922"
  │             (bodySmall, Roboto Mono, color/onSurfaceVariant)
  └─ BottomNav
```

List is pre-sorted **Active-first, then Inactive** — do not add a sort control. Summary counts are
computed in the ViewModel; the UI receives a finished string.

Cards are **not tappable** — no mandate detail screen exists and this app cannot cancel a mandate.
Do not add ripple, chevron or Pressed states.

Amount is `color/onSurfaceVariant` and **unsigned**: a past direct-debit payment is a historical
record, not a signed movement.

### Empty

```
Frame: direct-debits_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: receipt_long (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No direct debits" (headlineMedium, center)
  │   └─ Body: "This account has no direct debit mandates set up."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

No CTA — this app cannot create a mandate.

### Unsupported — its own frame, not an Error variant

```
Frame: direct-debits_unsupported (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ UnsupportedContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: info_outline (64dp, color/onSurfaceVariant)   ← NOT color/error
  │   ├─ Title: "Direct debits aren't available for this account"
  │   │          (headlineMedium, center, color/onSurface)
  │   └─ Body: "{uiState.message}" (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

Same three rules as its two sibling gated screens: `info_outline` in `onSurfaceVariant` not
`error_outline` in `error`; **no CTA of any kind**; body is the bank's own message verbatim. The
three gated features share one visual contract — build this frame identically in all three files.

### Error

```
Frame: direct-debits_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load direct debits" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, filled)   [CONDITIONAL]
  └─ BottomNav
```

Give `retry_button` a **Visible** boolean variant. Unlike `scheduled-payments` — where all four
error kinds retry — this screen **suppresses retry on `ConsentRevoked` (403)**: the consent is
gone, so retrying fails identically until the PSU re-authorises. Shown for `TokenExpired`,
`RateLimited`, `NetworkError`, `ServerError`.

---

## 4. Component Variants

### badge: `status_badge` — the load-bearing variant

| Property | Values |
|---|---|
| Status | **Active** (default), Inactive |

| Status | Fill | Border | Label colour |
|---|---|---|---|
| Active | `color/secondaryContainer` | none | `color/onSecondaryContainer` |
| Inactive | transparent | 1dp `color/outline` | `color/onSurfaceVariant` |

Hug × 20dp · Padding 2/8 · Radius `radius/full` · labelSmall.

Tonal-vs-outlined, **not** green-vs-red and not colour alone. An inactive mandate is a valid
historical record, not a failure — do not dim the card, strike the text, or tint the badge `error`.

### card: `mandate_card`

- Fill × Hug · Padding 12dp · Radius `radius/md` · Gap 4dp
- Fill `color/surfaceContainer` · Elevation `level1` tonal
- **No interactive states** — not tappable

### button: `retry_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, Disabled |
| Visible | **true** (default), false — off for `ConsentRevoked` |

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `receipt_long` | 64dp | Empty illustration |
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
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash belongs to home's balance card; a list of equal-weight mandates must not privilege a row. |
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

All pass WCAG AA. The inactive badge border is measured against the 3:1 **non-text** threshold —
its label is `onSurfaceVariant` at 8.2:1, so legibility never depends on the border.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). Empty and unsupported arrive without transition:
they are answers, not loading outcomes.
