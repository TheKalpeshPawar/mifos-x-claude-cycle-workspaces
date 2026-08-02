# Payment consent — Figma Design Prompt

> Generated from `screens/payment-consent/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp, **no leading icon**
- **Bottom nav**: **ABSENT on every frame** — the only PISP screen that hides it

Both omissions are deliberate and structural. The PSU is mid-authorisation on an irreversible
action; a tab tap or a back arrow would strand a staged consent. The only exits are
`abandon_button` and completion. Do not add a back arrow "for consistency."

---

## 2. Design Token Variables

Token values are identical across every feature — one Figma variable collection resolved from
`design-tokens.yaml` 2.1.0. Full tables in `mockups/send-money/PROMPTS_FIGMA.md §2`.

The subset this screen binds:

| Variable | Light | Dark | Usage here |
|---|---|---|---|
| `color/primary` | `#266489` | `#95CDF7` | Indicator, `verified_user`, restart CTA, abandon label |
| `color/onPrimary` | `#FFFFFF` | `#00344E` | Restart CTA label |
| `color/surface` | `#F7F9FF` | `#101417` | Background |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Titles |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Progress detail, body copy |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

No chips, no cards, no money figures — this screen shows **no monetary values at all**. It is a
progress surface. Roboto throughout; **no Roboto Mono binding needed**.

Theme is **auto**. Do not pin a mode.

---

## 3. Auto Layout Structure

### Validating / Exchanging / Checking — ONE frame, three variants

These three states are structurally identical. Build **one** frame with a Stage variant property;
only the detail string changes, plus one conditional child.

```
Frame: payment-consent_progress (Fill, Auto Layout Vertical, center)
  Variant property: Stage = Validating | Exchanging | Checking
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16)
  │   └─ Title: "Authorising payment" (titleLarge, color/onSurface, Fill)
  │       — NO leading icon
  ├─ ProgressContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ authorising_indicator (48dp circular, color/primary)
  │   ├─ progress_detail (bodyMedium, center, color/onSurfaceVariant)
  │   │   Validating → "Verifying the response from your bank…"
  │   │   Exchanging → "Completing authorisation…"
  │   │   Checking   → "Checking with your bank…"
  │   └─ check_again_button (Hug, padding 12/16)        [Checking ONLY]
  │       Label: "Check again" (labelLarge, color/primary) — text variant
  └─ (NO bottom nav)
```

`check_again_button` is **text** emphasis, not filled or tonal: the automatic backing-off poll is
the primary mechanism, and a prominent button would imply the PSU must act. They usually need not.

`progress_detail` is not decoration — it is what stops a slow consent poll from reading as a hang.
Never build a bare-spinner variant.

### Authorised

```
Frame: payment-consent_authorised (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ AuthorisedContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: verified_user (64dp, color/primary)
  │   ├─ Title: "Payment authorised" (headlineMedium, center, color/onSurface)
  │   └─ Body: "Sending your payment now…" (bodyMedium, center, color/onSurfaceVariant)
  └─ (NO bottom nav)
```

Two details that carry meaning:

- The glyph is **`verified_user`, not `check_circle`.** This confirms *authorisation*, not
  settlement. `check_circle` is reserved for a settled payment on `payment-status`.
- The copy is "Sending your payment now…", **not** "Payment sent". Nothing has been submitted at
  this point — send-money performs the submit after this screen hands back.

This frame is **transient**. It appears briefly, emits its event, and is torn down. Do not design a
dwell-time CTA into it.

### Error

```
Frame: payment-consent_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Authorisation didn't complete" (headlineMedium, center)
  │   ├─ Message: "{error.message}" (bodyMedium, center, color/onSurfaceVariant)
  │   ├─ restart_authorisation_button (Fill × 48dp, radius/full, filled)  [CONDITIONAL]
  │   │   Fill: color/primary · Label: "Try again" (labelLarge, color/onPrimary)
  │   └─ abandon_button (Hug, padding 12/16)                              [ALWAYS]
  │       Label: "Abandon payment" (labelLarge, color/primary) — text variant
  └─ (NO bottom nav)
```

Give `restart_authorisation_button` a **Visible** boolean variant, defaulted **off**. Half the
error types must not offer restart:

| Error type | Restart | Why |
|---|:---:|---|
| `CodeExpired` · `AuthorisationTimedOut` · `NetworkError` | **shown** | nothing submitted; a fresh consent is safe |
| `StateMismatch` | **hidden** | a security failure — possible replay/injection. Never silently retried |
| `NoPendingAuthorisation` | **hidden** | the single-use pending auth is gone; nothing to resume |
| `ConsentRejected` | **hidden** | the PSU declined. Re-prompting would override their decision |

`abandon_button` renders in **every** error variant, including the three with no restart. There is
always an exit.

---

## 4. Component Variants

### progress_indicator: `authorising_indicator`

- 48dp circular, `color/primary`, indeterminate
- Bound to three states; no size or colour change between them

### button: `restart_authorisation_button` (filled)

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, Disabled |
| Visible | **false** (default), true |

| State | Background | Border | Opacity |
|---|---|---|:---:|
| Default | `color/primary` | none | 100% |
| Pressed | `color/primary` + ripple | none | 100% |
| Focused | `color/primary` | 2dp outline offset | 100% |
| Disabled | `color/primary` | none | 38% |

Fill width × 48dp · Radius `radius/full` · Label labelLarge `color/onPrimary`.

### button: `abandon_button` / `check_again_button` (text)

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |

- Hug × 48dp min touch target · Padding 12/16 · Label labelLarge `color/primary`
- Pressed: `color/primary` @ 12% state-layer · Focused: 2dp `color/primary` outline

Text emphasis on both is deliberate. `abandon_button` is destructive but must not be styled
`color/error` — abandoning a *staged, unauthorised* consent is a safe exit, not a hazard, and the
consent expires on its own. Red would misrepresent the risk.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `verified_user` | 64dp | Authorised state |
| `error_outline` | 64dp | Error state |

No bottom-nav icons — this screen has no bottom nav. No `arrow_back` — no leading icon.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single centred column. Primary target. |
| Medium (600–840dp) | Content column capped 400dp, centred both axes |
| Expanded (> 840dp) | Content column capped 400dp, centred both axes |

Narrower cap (400dp) than the data screens' 600dp: this is a single centred message, and stretching
a one-line progress label across a wide viewport looks broken.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** A hero wash on a security-sensitive authorisation screen would add brand flourish exactly where the PSU should be reading plain factual status. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (text buttons) | `surface` `#F7F9FF` | 6.11:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (icon) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |
| `primary` `#95CDF7` (dark, indicator) | `surface` `#101417` | 10.89:1 | 3.0 | ✅ |

All pass WCAG AA. Text buttons are measured against the 4.5:1 **text** threshold, not the 3:1
non-text one — their label is the affordance.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Stage-to-stage transitions (`validating → exchanging → checking`) cross-fade the detail label at
`short` (150ms) while the indicator runs continuously — the spinner must not restart between
stages, or a three-stage flow reads as three failed attempts.
