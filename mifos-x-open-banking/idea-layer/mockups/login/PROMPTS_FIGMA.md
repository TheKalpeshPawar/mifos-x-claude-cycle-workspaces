# Login — Figma Design Prompt

> Generated from `screens/login/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 24dp margin
- **Status bar**: 54dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp — leading arrow is **route-dependent** (see §3)
- **Bottom nav**: **ABSENT on every frame**

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Bank card |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Bank name, permission bullets |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Explainer, section labels |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Trust chips |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Chip labels |
| `color/primary` | `#266489` | `#95CDF7` | Indicator, CTA fill, back icon |
| `color/onPrimary` | `#FFFFFF` | `#00344E` | CTA label |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

**No text-field tokens** — there is no input on this screen. No money tokens, no mono binding.
Radius: card `radius/md`, chips and CTA `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Content — the primary frame

```
Frame: login_content (Fill, Auto Layout Vertical)
  Variant property: Entry = Onboarding | Renew
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back)   [Renew ONLY]
  │   └─ Title: "Connect your bank" (titleLarge, color/onSurface, Fill)
  ├─ ScrollContent (Fill, Vertical, padding 24dp, gap 24dp)
  │   ├─ bank_card (Fill × Hug, padding 24dp, radius/md, align center)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   └─ "HSBC UK Personal" (titleLarge, center, color/onSurface)
  │   ├─ explainer (Fill, Hug)
  │   │   "You'll be taken to HSBC to sign in and choose what to share.
  │   │    This app never sees your password."
  │   │   (bodyMedium, color/onSurfaceVariant)
  │   ├─ PermissionsGroup (Fill, Vertical, gap 4dp)
  │   │   ├─ "What you'll share" (bodySmall, color/onSurfaceVariant)
  │   │   └─ Bullet ×5 (bodyMedium, color/onSurface)   — FULL LIST
  │   ├─ trust_chips (Hug, Horizontal, gap 8dp)
  │   │   ├─ "FAPI 1.0 Advanced"  (assist chip, NON-interactive)
  │   │   └─ "90-day consent"     (assist chip, NON-interactive)
  │   └─ connect_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Connect with HSBC" (labelLarge, color/onPrimary)
  └─ (NO bottom nav)
```

**Two things this frame must not grow:**

1. **No password, PIN or username field.** The PSU authenticates app-to-app at HSBC under FAPI 1.0
   Advanced (`private_key_jwt`, PKCE S256). This app never sees a credential, and the layout
   saying so plainly is the screen's main job. A field here would be a security lie.
2. **No bank picker.** Single brand (`uk-personal`). The card *states* which bank; it does not
   offer a choice. No dropdown, no search, no logo grid.

**Render every permission bullet.** DESIGN.md's "always explicit, never truncated" applies at the
point of *asking*, not only at review — a PSU should know what they are authorising before they
leave the app.

The **Entry** variant controls only the back arrow: `LoginRoute` (from onboarding, in `authGraph`)
shows **none** — there is nowhere to return to. `LoginRenewRoute` (from the consent screens, inside
the authenticated host) shows **back**.

### Loading / Authorising — one frame, two variants

```
Frame: login_progress (Fill, Auto Layout Vertical, center)
  Variant property: Stage = Loading | Authorising
  ├─ TopAppBar (same)
  ├─ ProgressContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ progress_indicator (48dp circular, color/primary)
  │   ├─ stage_title (bodyMedium, center, color/onSurfaceVariant)
  │   │   Loading     → "Preparing your connection…"
  │   │   Authorising → "Opening HSBC…"
  │   └─ hand_off_note (bodyMedium, center, color/onSurfaceVariant)
  │       [Authorising ONLY]
  │       "Continue in your browser. You'll come back here automatically."
  └─ (NO bottom nav)
```

`Authorising` renders while **the app is backgrounded** — the PSU is at HSBC completing SCA. Its
note exists so returning to a backgrounded app shows something coherent rather than a stale form,
and so the automatic return is expected. **No "I've finished" button, no manual code entry**:
return happens via `ConsentRedirectBus`.

### Error

```
Frame: login_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't start the connection" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ (NO bottom nav)
```

Retry re-runs the whole `StartOAuth` sequence, minting a **fresh** `state`/`nonce` — a stale
pending authorisation is never reused.

### Empty — synthetic

No configured bank brand. `default_brand: uk-personal` is set in `PROJECT_CONFIG.yaml`, so there is
no production path here. Build it plainly, like `settings`' synthetic states; do not invest
illustration work.

---

## 4. Component Variants

### button: `connect_button` / `retry_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
Pressed +ripple · Focused 2dp outline offset. **No Disabled state** — there is no form to complete
and therefore no precondition to satisfy.

### chip: trust chips — **non-interactive**

| Property | Values |
|---|---|
| State | **Default only** |

Hug × 32dp · Padding 6/12 · Radius `radius/full` · Fill `color/secondaryContainer` ·
labelLarge `color/onSecondaryContainer`.

Build with **no Pressed, Focused or Selected states**, matching `user-onboarding`'s trust chips.
They state the regulatory posture; giving them interactive states promises an explanation that does
not exist.

### card: `bank_card`

Fill × Hug · Padding 24dp · Radius `radius/md` · Fill `color/surfaceContainer` · Elevation
`level1` · centre-aligned · **No interactive states**. It identifies the bank; it is not a picker.

### icon_button: `back_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. **Visible only on the Renew variant.**

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading (Renew only) |
| `error_outline` | 64dp | Error illustration |

No bottom-nav icons. No bank logo asset — the card is a text treatment; shipping a bank mark would
add a trademark dependency for no functional gain.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, 24dp margins. Primary target. |
| Medium (600–840dp) | Content column capped 480dp, centred |
| Expanded (> 840dp) | Content column capped 480dp, centred |

480dp cap, matching `user-onboarding` — this is a single proposition with one action, not a data
surface.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** This is the consent-granting screen: the PSU is deciding whether to hand over access to their bank data. Brand flourish behind that decision is the wrong register, and the flat surface matches `user-onboarding` immediately before it. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |
| `onPrimary` `#00344E` (dark) | `primary` `#95CDF7` (dark) | 8.4:1 | 4.5 | ✅ |

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

`content → loading → authorising` cross-fades at `short` (150ms), with the indicator running
continuously across both stages — it must **not** restart, or a two-stage hand-off reads as a
failed first attempt. The browser hand-off itself is a platform transition this app does not
animate.
