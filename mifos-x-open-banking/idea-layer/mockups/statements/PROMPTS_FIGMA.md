# Statements — Figma Design Prompt

> Generated from `screens/statements/ui.yaml` by `/idea-feature-mockup`
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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Statement card |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Card pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Period label |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Statement id, format, empty glyph |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, **download icon**, retry CTA |
| `color/inverseSurface` | `#2D3135` | `#E0E3E8` | **Snackbar** surface |
| `color/inverseOnSurface` | `#EEF1F6` | `#2D3135` | Snackbar label |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

**No money tokens** — statement metadata carries no amounts on this screen. Radius: card
`radius/md`, snackbar `radius/xs`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: statements_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Statements" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

### Content — two tap targets per row

```
Frame: statements_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ statements_list (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   └─ statement_card (Fill × Hug, padding 12dp, radius/md,
  │                      Auto Layout Horizontal, align center, gap 12dp)
  │       Fill: color/surfaceContainer · Elevation: level1 · TAPPABLE
  │       ├─ TextColumn (Fill weight 1, Auto Layout Vertical, gap 2dp)
  │       │   ├─ periodLabel: "1 Jun – 30 Jun 2026" (titleMedium,
  │       │   │     color/onSurface)
  │       │   └─ meta: "Statement 0042 · PDF" (bodySmall,
  │       │         color/onSurfaceVariant)
  │       └─ download_button: IconButton (48dp × 48dp touch target,
  │             download 24dp, color/primary)
  └─ BottomNav
```

**Two distinct tap targets in one row, and they must stay visually separate.** The card body opens
`statement-detail`; the download icon fetches the PDF **without navigating**. A single target that
sometimes downloads and sometimes navigates is unpredictable — give the icon its own 48dp frame
with its own ripple, and do not extend the card's ripple beneath it.

### Empty

```
Frame: statements_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: description (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No statements yet" (headlineMedium, center)
  │   └─ Body: "Statements appear here once your first billing period closes."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

No CTA — nothing the customer can do but wait.

### Error — list failures only

```
Frame: statements_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load statements" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

**There is no Unsupported frame.** This feature's store does not call `recordIfUnsupported` — the
chip is simply hidden on non-credit products. Do not copy the gated-list pattern here.

### Download failure — a snackbar over intact content

```
Overlay: statements_download_error (on the CONTENT frame, not replacing it)
  └─ Snackbar (Fill − 32dp margin, Hug, padding 14/16, radius/xs,
               anchored above BottomNav + 16dp)
      Fill: color/inverseSurface
      └─ Label: "Couldn't download that statement" (bodyMedium,
            color/inverseOnSurface)
```

**A failed download must never replace the screen with the Error frame.** The list is still valid
and the PSU may want a different statement. Two events exist, both download-failure snackbars.

**A successful download raises no event and shows no snackbar** — the platform's own save/share
sheet is the feedback. A "Downloaded" toast would double-report an outcome the OS already
confirmed.

---

## 4. Component Variants

### card: `statement_card`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |

- Fill × Hug (≈64dp) · Padding 12dp · Radius `radius/md` · Gap 12dp
- Fill `color/surfaceContainer` · Elevation `level1`

| State | Background |
|---|---|
| Default | `color/surfaceContainer` |
| Pressed | `color/surfaceContainerHigh` + ripple |
| Focused | `color/surfaceContainer` + 2dp `color/primary` |

### icon_button: `download_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, **Downloading** |

48dp × 48dp touch target · 24dp `download` glyph · `color/primary`.

**Downloading**: swap the glyph for a 20dp indeterminate indicator and disable the tap. The row
stays interactive — the customer can still open the detail screen while a PDF is fetching.

### icon_button: `back_button` / button: `retry_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. Retry: Fill × 48dp, `radius/full`,
`color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `download` | 24dp | Per-row download |
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
| Medium (600–840dp) | List column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** grid — the period/download row relies on the download icon sitting at the far trailing edge |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** A list of billing periods is reference material; equal-weight rows must not be privileged, and a wash would fight the download affordance for attention. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `inverseOnSurface` `#EEF1F6` | `inverseSurface` `#2D3135` | 12.1:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (download icon) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 3.0 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. The download icon is measured against the 3:1 non-text threshold and carries an
`accessibility_label`, so it is never an unlabelled glyph-only control.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). Snackbar enters at `short` (150ms) slide-up,
auto-dismisses after 4s. The download glyph → indicator swap is a `short` cross-fade — **no
progress bar**, since HSBC returns the PDF as a single `ByteArray` with no streamed progress to
report.

---

## Note: this screen has pixel goldens

`feature/statements` is the first *feature* to apply Roborazzi. Every state above has a committed
golden under `src/androidUnitTest/screenshots/`, so a visual change fails `verifyRoborazziDebug`
rather than passing silently. Re-record with `recordRoborazziDebug` when a change here is intended.
