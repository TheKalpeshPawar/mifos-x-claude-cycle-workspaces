# Consent callback — Figma Design Prompt

> Generated from `screens/consent-callback/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 24dp margin
- **Status bar**: 54dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp, **no leading icon**
- **Bottom nav**: **ABSENT on every frame**

No back arrow and no tabs. The PSU is mid-authorisation and there is nothing to go back *to* — the
previous screen was the bank's website in a browser. Do not add either "for consistency".

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surface` | `#F7F9FF` | `#101417` | Background |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Titles |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Body copy, **declined + security glyphs** |
| `color/primary` | `#266489` | `#95CDF7` | Indicator, success glyph, CTA fill |
| `color/onPrimary` | `#FFFFFF` | `#00344E` | CTA label |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Generic error glyph ONLY** |

No cards, no chips, no money tokens, no mono binding. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading / Awaiting — one frame, two variants

```
Frame: consent-callback_progress (Fill, Auto Layout Vertical, center)
  Variant property: Stage = Loading | Awaiting
  ├─ TopAppBar (Fill × 56dp, padding 4/16)
  │   └─ Title: "Connecting" (titleLarge, color/onSurface)   — NO leading icon
  ├─ ProgressContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ progress_indicator (48dp circular, color/primary)
  │   └─ stage_detail (bodyMedium, center, color/onSurfaceVariant)
  │       Loading  → "Verifying your connection…"
  │       Awaiting → "Finishing up…"
  └─ (NO bottom nav)
```

The detail line is not decoration — it stops a slow token exchange reading as a hang. Never build a
bare-spinner variant.

### Content — authorised, transient

```
Frame: consent-callback_content (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ SuccessContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: check_circle (64dp, color/primary)
  │   ├─ Title: "You're connected" (headlineMedium, center, color/onSurface)
  │   └─ Body: "Taking you to your accounts…" (bodyMedium, center,
  │             color/onSurfaceVariant)
  └─ (NO bottom nav)
```

**Transient — no CTA.** Persisting the tokens flips `ConsentSession.isActive()` and the **root
navigator** routes to Home; this screen never navigates itself and is torn down. Do not design a
"Continue" button.

### Access denied — the register matters more than the layout

```
Frame: consent-callback_access_denied (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ DeniedContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: info_outline (64dp, color/onSurfaceVariant)   ← NOT color/error
  │   ├─ Title: "You didn't share your accounts" (headlineMedium, center)
  │   ├─ Body: "You chose not to share your HSBC account data. You can start
  │   │         again at any time." (bodyMedium, center, color/onSurfaceVariant)
  │   └─ start_over_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Start over" (labelLarge, color/onPrimary)
  └─ (NO bottom nav)
```

**The PSU declined at the bank. That is a valid choice, not a failure.** Three rules:

1. `info_outline` in `color/onSurfaceVariant` — **never** `error_outline` in `color/error`.
2. Neutral copy: "You chose not to share…". No "failed", no "denied", no apology.
3. CTA reads **"Start over"**, not "Try again" — retry language implies they made a mistake.

Getting this wrong reads as the app arguing with a customer who exercised a right the regulation
exists to protect.

### Security error — its own frame

```
Frame: consent-callback_security_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ SecurityContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: warning (64dp, color/onSurfaceVariant)
  │   ├─ Title: "Security check failed" (headlineMedium, center)
  │   ├─ Body: "The authorisation response could not be verified. Please start
  │   │         the connection process again from login."
  │   │        (bodyMedium, center, color/onSurfaceVariant)
  │   └─ start_again_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Start again" (labelLarge, color/onPrimary)
  └─ (NO bottom nav)
```

The returned `state` or `nonce` did not match the pending authorisation — a possible replay or
injection. The response is **discarded**, never retried against; the PSU restarts from login so a
fresh `state`/`nonce` pair is minted. Do not offer a retry that re-submits the same response.

### Error

```
Frame: consent-callback_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't complete the connection" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Try again" (labelLarge, color/onPrimary)
  └─ (NO bottom nav)
```

Transport failures and expired codes — the genuinely transient class, and the **only** one of the
three failure frames that offers a true retry.

### Build all three failure frames separately

| Frame | Glyph | Glyph colour | Cause | CTA |
|---|---|---|---|---|
| `access_denied` | `info_outline` | `onSurfaceVariant` | PSU declined | Start over |
| `security_error` | `warning` | `onSurfaceVariant` | `state`/`nonce` mismatch | Start again |
| `error` | `error_outline` | `error` | transport / expired code | Try again |

**Only the last is red.** Do not collapse these into one error frame with a swapped label — that
would tell a customer who made a deliberate choice that something went wrong.

---

## 4. Component Variants

### progress_indicator

48dp circular, `color/primary`, indeterminate. Bound to two stages; no size or colour change
between them, and the spinner **must not restart** between stages — a two-stage flow that restarts
reads as two failed attempts.

### button: CTA

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |
| Label | Start over, Start again, Try again |

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
Pressed +ripple · Focused 2dp outline offset. **No Disabled state** — there is no precondition.

All three are `color/primary`, including the two on failure frames. Red CTAs are reserved for
genuine destructive actions; restarting a connection is neither destructive nor an error.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `check_circle` | 64dp | Authorised |
| `info_outline` | 64dp | **Access denied** |
| `warning` | 64dp | **Security error** |
| `error_outline` | 64dp | Generic error |

No `arrow_back`, no bottom-nav icons.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single centred column, 24dp margins. Primary target. |
| Medium (600–840dp) | Content column capped 400dp, centred both axes |
| Expanded (> 840dp) | Content column capped 400dp, centred both axes |

Narrow 400dp cap, matching `payment-consent`: a single centred message stretched across a wide
viewport looks broken.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** A brand wash on the screen that reports a security-check failure or a declined consent would undercut the plain factual register those states depend on. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (success glyph) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `onSurfaceVariant` `#41474D` (info/warning glyphs) | `surface` `#F7F9FF` | 8.9:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |
| `onSurface` `#E0E3E8` (dark) | `surface` `#101417` (dark) | 14.9:1 | 4.5 | ✅ |
| `onPrimary` `#00344E` (dark) | `primary` `#95CDF7` (dark) | 8.4:1 | 4.5 | ✅ |

All pass WCAG AA. Each state's meaning is carried by its **title text**, so a customer who cannot
distinguish the glyph colours still reads which of the three outcomes occurred (WCAG 1.4.1).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

`loading → awaiting` cross-fades the detail label at `short` (150ms) while the indicator runs
continuously. Progress → any terminal state cross-fades at `medium` (300ms). **No celebratory
motion on success** — no scale-in on `check_circle`, no confetti. The frame is on screen for well
under a second before the root navigator replaces it.
