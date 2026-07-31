# User onboarding — Figma Design Prompt

> Generated from `screens/user-onboarding/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, **24dp margin** (wider than the app's 16dp — see §3)
- **Status bar**: 54dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: **ABSENT**
- **Bottom nav**: **ABSENT**

The only frame in the project with neither chrome. Content is edge-to-edge between the safe areas.
There is nothing to navigate back to (this is the launch destination) and no tabs (tabs live behind
authentication).

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surface` | `#F7F9FF` | `#101417` | Background — flat |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Headline |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Body copy |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Trust chip fill |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Trust chip label |
| `color/primary` | `#266489` | `#95CDF7` | CTA fill |
| `color/onPrimary` | `#FFFFFF` | `#00344E` | CTA label |

No error roles, no money tokens, no containers beyond the chips. Theme **auto**.

| Style | Font | Size | Usage |
|---|---|:---:|---|
| headlineMedium | Roboto | 28sp | Headline |
| bodyMedium | Roboto | 14sp | Body copy |
| labelLarge | Roboto | 14sp | CTA, chip labels |

**No Roboto Mono binding** — there are no figures, amounts or identifiers on this screen.

---

## 3. Auto Layout Structure

### Intro — the only frame

```
Frame: user-onboarding_intro (Fill, Auto Layout Vertical, padding 24dp,
                              space-between, gap 24dp)
  ├─ Spacer (Fill weight 1)              — pushes content off the top edge
  ├─ ContentBlock (Fill, Hug, Auto Layout Vertical, center, gap 24dp)
  │   ├─ hero_illustration (240dp × 240dp, centered)
  │   │   Source: OnboardingHeroIllustration — a COMPOSABLE, not a raster asset
  │   │   Alt: "{strings.user_onboarding.hero_alt}"  — decorative: FALSE
  │   ├─ intro_headline (Fill, Hug)
  │   │   "See all your accounts in one place"
  │   │   (headlineMedium, center, color/onSurface, role: HEADING)
  │   ├─ intro_body (Fill, Hug)
  │   │   "Connect your HSBC accounts securely with Open Banking. No passwords
  │   │    are ever shared with this app, and you stay in control of your data."
  │   │   (bodyMedium, center, color/onSurfaceVariant)
  │   └─ trust_chips (Hug, Auto Layout Horizontal, center, gap 8dp)
  │       ├─ fapi_chip: "FAPI 1.0 Advanced"  (assist chip, NON-interactive)
  │       └─ fca_chip:  "FCA regulated"      (assist chip, NON-interactive)
  ├─ Spacer (Fill weight 1)
  └─ continue_button (Fill × 48dp, radius/full, Fill: color/primary)
      └─ Label: "Continue" (labelLarge, color/onPrimary)
```

Three structural decisions worth preserving:

1. **24dp margins, not the app's 16dp.** Every other screen is a dense data surface where 16dp
   maximises content width. This one is a single centred proposition; tighter margins make it read
   as cramped rather than composed.
2. **Space-between with two flexible spacers.** The CTA sits at the bottom edge and the content
   block floats optically centred, so the layout holds on a 852dp phone and a 640dp small screen
   without the CTA drifting mid-screen.
3. **Flat background — no gradient.** See Mood Palette below.

### There are no other frames

One state (`intro`), `state_model: {}`, a stateless composable. Do **not** build loading, empty or
error variants — nothing is fetched. Do **not** build a pager: the idea-layer described a
three-step pager until 2026-07-28; source ships one screen and the pager was removed.

---

## 4. Component Variants

### image: `hero_illustration`

240dp × 240dp, centred. **`decorative: false`** — this is the only non-decorative image in the
app, and it carries alt text. Every other glyph is a Material Symbol marked decorative and hidden
from the accessibility tree. Do not mark it decorative; it conveys the product proposition to a
screen-reader user.

It is a **composable** (`OnboardingHeroIllustration.kt`), not a raster export. Design it as vector
shapes on the trust-blue ramp; do not hand off a PNG.

### chip: `fapi_chip` / `fca_chip` — assist chips, **non-interactive**

| Property | Values |
|---|---|
| State | **Default only** |

- Hug × 32dp · Padding 6/12 · Radius `radius/full`
- Fill `color/secondaryContainer` · Label labelLarge `color/onSecondaryContainer`

**Build with no Pressed, Focused or Selected states.** `selection_mode: none` — these cannot be
tapped, selected or filtered by. They state the regulatory posture before the PSU is asked to
connect a bank account. Giving them interactive states would be a lie about their affordance, and
a customer who taps expecting an explanation gets nothing.

### button: `continue_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |

| State | Background | Border | Opacity |
|---|---|---|:---:|
| Default | `color/primary` | none | 100% |
| Pressed | `color/primary` + ripple | none | 100% |
| Focused | `color/primary` | 2dp outline offset | 100% |

Fill × 48dp · Radius `radius/full` · labelLarge `color/onPrimary`.

**No Disabled state** — there is no precondition to satisfy. The screen's only interactive element
and its only outward edge. Do not add "Skip" or "Maybe later": the app has no unauthenticated
content to skip to.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

**None.** No app bar, no bottom nav, no state illustrations, no chip icons.

### Images

| Asset | Dimensions | Format | Usage |
|---|---|---|---|
| `OnboardingHeroIllustration` | 240 × 240dp | **Compose vector composable**, not a raster | Hero |

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single centred column, 24dp margins. Primary target. |
| Medium (600–840dp) | Content column capped **480dp**, centred; hero 280dp |
| Expanded (> 840dp) | Content column capped **480dp**, centred; hero 280dp |

Narrower cap (480dp) than the data screens' 600dp: this is a single proposition, and a headline
stretched across a wide viewport loses the centred composition the layout depends on.

Small-height phones (< 700dp): reduce the hero to 180dp before shrinking type. The CTA must stay
above the bottom safe area and never require a scroll.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused, and this is the screen where that is most surprising.** The token is literally named `hero`, and this is the app's only hero surface. It stays unused because DESIGN.md's low-variance dial forbids decorative gradients, and because a wash behind a regulatory trust claim reads as marketing exactly where the customer is being asked to trust the app with bank data. The illustration carries the visual weight; the background stays flat `color/surface`. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 3.0 (large) | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `onSurface` `#E0E3E8` (dark) | `surface` `#101417` (dark) | 14.9:1 | 3.0 (large) | ✅ |
| `onPrimary` `#00344E` (dark) | `primary` `#95CDF7` (dark) | 8.4:1 | 4.5 | ✅ |

All pass WCAG AA. The headline at 28sp clears the **large-text** 3:1 threshold; body and chip
labels are measured against the 4.5:1 normal-text requirement.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

One state, so no state transitions. The only motion is the push to `login` on Continue, at
`medium` (300ms). **No entrance animation on the hero** — no fade-up, no scale-in, no stagger. It
is the app's first frame; animating it delays the proposition and conflicts with the low-motion
dial. Under OS reduce-motion the push becomes a cross-fade.
