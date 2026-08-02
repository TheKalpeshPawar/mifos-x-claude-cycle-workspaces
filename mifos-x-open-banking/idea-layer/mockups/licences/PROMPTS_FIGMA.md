# Open-source licences — Figma Design Prompt

> Generated from `screens/licences/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow**
- **Bottom nav**: **ABSENT** — terminal reference document reached from Settings

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. This screen binds the smallest subset in the project:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surface` | `#F7F9FF` | `#101417` | Background — flat, no card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Licence body text |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Intro paragraph |
| `color/primary` | `#266489` | `#95CDF7` | Back icon |

No containers, no chips, no money tokens, no error roles. Theme **auto**.

**Typography — the one thing that matters here:**

| Style | Font | Size | Usage |
|---|---|:---:|---|
| bodyMedium | Roboto | 14sp | Intro paragraph |
| bodySmall | **Roboto Mono** | 12sp | **Licence body** |

---

## 3. Auto Layout Structure

### Content — the only frame

```
Frame: licences_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Open-source licences" (titleLarge, color/onSurface, Fill)
  └─ ScrollContent (Fill, Auto Layout Vertical, padding 16dp, gap 16dp)
      ├─ licences_intro (Fill, Hug)
      │   "This app is built with open-source software. The full licence text is
      │    reproduced below." (bodyMedium, color/onSurfaceVariant)
      └─ licences_body (Fill, Hug)
          Mozilla Public License 2.0, full text
          (bodySmall, ROBOTO MONO, color/onSurface, line-height 16sp)
          — NO wrapping override; preserve the source file's hard line breaks
  (no BottomNav)
```

Build **one frame**. There are no loading, empty or error variants: the text is a bundled resource
(`composeResources/files/mpl_licence.txt`) read via `produceState`. A bundled file cannot 404, be
empty, or fail the network. Do not add a skeleton — the read completes in microseconds.

Three constraints that are functional, not aesthetic:

1. **Roboto Mono on the body.** The MPL-2.0 is a legal document with hard-wrapped lines and ASCII
   rules (`====`). A proportional font reflows them into ragged nonsense. Same principle that binds
   mono to money and account numbers: fidelity of the original form.
2. **Flat — no card, no `surfaceContainer`.** The text *is* the screen. A container around several
   thousand words draws a border around content with no natural end.
3. **No bottom nav.** A tab tap out of a legal text is not a journey the app supports.

---

## 4. Component Variants

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`. States: Default / Pressed (12%
state-layer) / Focused (2dp outline).

### text: `licences_body`

No variants. Fill width, Hug height, `bodySmall` Roboto Mono `color/onSurface`, line-height 16sp.
Text-align **left** — never justified, which would stretch spaces inside a monospaced block and
destroy the column alignment mono exists to preserve.

There are **no other components on this screen.** No buttons, no links, no rows, no chips.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |

No bottom-nav icons — no bottom nav. No illustration — no empty or error state.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, 16dp margins. Primary target. |
| Medium (600–840dp) | Text column capped **560dp**, centred |
| Expanded (> 840dp) | Text column capped **560dp**, centred |

Tighter cap than the 600dp used elsewhere: monospaced text at 12sp exceeds a comfortable
measure well before a proportional font would, and the source file's hard line breaks assume a
roughly 80-column width. Do not let the column grow to the viewport.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** A gradient behind a licence is decoration on a legal notice — the one place in the app where brand expression is actively inappropriate. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface exists on this screen. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `onSurface` `#E0E3E8` (dark) | `surface` `#101417` (dark) | 14.9:1 | 4.5 | ✅ |

All pass WCAG AA. The body is 12sp — below the 18sp large-text threshold — so it is measured
against the **4.5:1** normal-text requirement, which `onSurface` clears with wide margin.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

**No animation on this screen** beyond the standard push/pop transition from Settings and native
scroll. There is one state, so there is nothing to transition between.
