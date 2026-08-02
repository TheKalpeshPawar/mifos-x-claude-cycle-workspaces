# Account holder — Figma Design Prompt

> Generated from `screens/account-holder/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Identity card, contact group |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Display name, row values |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Role label, row labels, leading icons, empty glyph |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Avatar** fill |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Avatar initials |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

**No money tokens and no Roboto Mono binding** — this screen shows an identity, not a figure.
Radius: card `radius/md`, avatar `radius/full`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading — with a caption

```
Frame: account-holder_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Account holder" (titleLarge, color/onSurface, Fill)
  ├─ LoadingContent (Hug, Auto Layout Vertical, center, gap 16dp)
  │   ├─ loading_indicator (48dp circular, color/primary)
  │   └─ loading_caption: "Loading account holder…"
  │         (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav (Fill × 80dp)
```

**Keep the caption.** One of the few loading states in the app that has one — the party endpoint
sits behind a revocable consent and can be slower than a balance read, so the caption stops a slow
fetch reading as a hang. Same reasoning as `payment-consent`'s stage detail.

### Content

```
Frame: account-holder_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   ├─ identity_card (Fill × Hug, padding 24dp, radius/md, gap 8dp,
  │   │                 Auto Layout Vertical, align CENTER)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ avatar (72dp × 72dp, radius/full, Fill: color/secondaryContainer)
  │   │   │   └─ Initials: "MN" (headlineSmall, color/onSecondaryContainer)
  │   │   ├─ display_name: "Mr Nico" (headlineSmall, center, color/onSurface)
  │   │   └─ role_label: "Account holder" (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   ├─ identity_section_header (Fill, Hug, padding 16/4/8/4)
  │   │   └─ "CONTACT" (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   └─ identity_section (Fill, Auto Layout Vertical, gap 0dp, radius/md,
  │                        clip content, Fill: color/surfaceContainer)
  │       ├─ email_row   (Fill × 64dp, padding 12/16, Horizontal, gap 16dp)
  │       │   ├─ Leading: mail (24dp, color/onSurfaceVariant)
  │       │   └─ TextColumn (Fill, gap 2dp)
  │       │       ├─ Label: "Email" (bodySmall, color/onSurfaceVariant)
  │       │       └─ Value: "nico.m@example.co.uk" (bodyLarge, color/onSurface)
  │       ├─ mobile_row  (same shape — leading `call`, "+44 7700 900312")
  │       └─ address_row (Hug height — leading `home`, two-line address)
  └─ BottomNav
```

The avatar is **initials, not a photo** — OBIE carries no party imagery. Do not design an image
slot or a placeholder-person glyph implying one is missing.

Contact rows are clipped inside one `radius/md` container so they read as a single group, matching
the tier table in `product`.

**Rows are not tappable — build them with no interactive states.** No mailto, no tel, no map. This
is an AISP read of `OBReadParty2`: the app displays what the bank holds, it does not act on it.
A ripple or chevron would promise an action that does not exist.

### Empty

```
Frame: account-holder_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: person_off (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No account holder details" (headlineMedium, center)
  │   └─ Body: "The bank didn't return party information for this account."
  │            (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

No CTA — nothing the customer can do about an absent party record.

### Error

```
Frame: account-holder_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load account holder details" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

---

## 4. Component Variants

### avatar

72dp × 72dp · Radius `radius/full` · Fill `color/secondaryContainer` · Initials `headlineSmall`
`color/onSecondaryContainer`, centred. Larger than the 40dp `beneficiaries` avatar — this is the
screen's subject, not a list row. No image variant.

### card: `identity_card`

- Fill × Hug · Padding 24dp · Radius `radius/md` · Gap 8dp · **Align centre**
- Fill `color/surfaceContainer` · Elevation `level1` tonal
- **No interactive states**

Centre alignment is specific to this card; every other card in the app is left-aligned. It is a
portrait, not a data row.

### list_item: contact rows

| Property | Values |
|---|---|
| Leading icon | mail, call, home |
| Value lines | **1** (default), 2 — address |

- Fill × 64dp (1 line) / Hug (2 lines) · Padding 12/16 · Gap 16dp
- **No Pressed / Focused states** — not interactive

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
| `mail` | 24dp | Email row leading |
| `call` | 24dp | Mobile row leading |
| `home` | 24dp | Address row leading |
| `person_off` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None. Avatars are generated initials.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width card. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped 600dp, centred. The identity card stays centre-aligned; do not left-align it at width |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The identity card is the closest thing in the app to a hero surface, but a gradient behind a named individual's contact details reads as branding applied to a person. Flat `surfaceContainer` keeps it factual. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** The avatar uses the flat `secondaryContainer` role. `tertiary` unused project-wide (reserved for PFM, since removed). |

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
| `onSurfaceVariant` `#41474D` (leading icons) | `surfaceContainer` `#EBEEF3` | 8.2:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. Each contact row's meaning is carried by its text label, never the glyph alone.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). **No entrance animation on the avatar** — no
scale-in or fade-up. It is a person's identity record, not a reveal.
