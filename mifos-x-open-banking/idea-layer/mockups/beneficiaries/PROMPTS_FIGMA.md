# Beneficiaries — Figma Design Prompt

> Generated from `screens/beneficiaries/ui.yaml` by `/idea-feature-mockup`
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
| `color/surface` | `#F7F9FF` | `#101417` | Row background, screen |
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Search bar fill |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Payee name, search text |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Scheme + identification, empty glyph |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Avatar** fill |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Avatar initials |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA, focus outline |
| `color/outline` | `#72787E` | `#8B9198` | Search bar border |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

`bodyMedium` → **Roboto Mono** for sort-code/account identifiers. **No money tokens bind on this
screen** — a beneficiary is an identity, not a balance. Radius: search bar `radius/sm` (8dp),
avatar `radius/full`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: beneficiaries_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Beneficiaries" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

**No search bar in this frame** — searching nothing is meaningless.

### Content

```
Frame: beneficiaries_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ beneficiary_search (Fill × 48dp, radius/sm, padding 8/12, margin 12dp)
  │   Fill: color/surfaceContainer · Border: 1dp color/outline
  │   ├─ Icon: search (24dp, color/onSurfaceVariant)
  │   └─ Placeholder/Value: "Search beneficiaries" (bodyLarge, color/onSurfaceVariant
  │       when placeholder, color/onSurface when filled)
  ├─ beneficiaries_list (Fill, Auto Layout Vertical, padding-h 12dp, gap 0dp)
  │   └─ beneficiary_row (Fill × Hug, min 48dp, padding 12dp,
  │                       Auto Layout Horizontal, align center, gap 16dp)
  │       ├─ beneficiary_avatar (40dp × 40dp, radius/full,
  │       │     Fill: color/secondaryContainer)
  │       │   └─ Initials: "JL" (labelLarge, color/onSecondaryContainer)
  │       └─ TextColumn (Fill weight 1, Auto Layout Vertical, gap 2dp)
  │           ├─ name: "Jameson Lettings" (bodyLarge, color/onSurface)
  │           └─ supporting: "Sort Code · 40-12-09 65872310"
  │                 (bodyMedium, Roboto Mono, color/onSurfaceVariant)
  └─ BottomNav
```

Rows are **not tappable** — no detail screen, and the app cannot add/edit/delete a payee. Do not
add ripple, chevron or Pressed states.

The avatar is **initials, not a photo**. OBIE carries no payee imagery; do not design an image
slot or a placeholder-person glyph that implies one is missing.

Search filters **client-side** (`BeneficiariesAction.Search`) — instant, no spinner, no API.

### Content — search with no matches

```
Frame: beneficiaries_search_no_results (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ beneficiary_search (SAME — retains the query, stays visible)
  ├─ NoResultsContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: search_off (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No matches" (headlineMedium, center)
  │   └─ Body: "No beneficiaries match \"zzz\"." (bodyMedium, center,
  │             color/onSurfaceVariant)
  └─ BottomNav
```

**A separate frame from Empty, and the difference is load-bearing.** This is still the `content`
state — the account *has* payees, the query matched none. The search bar **stays visible and keeps
the query** so the PSU can correct it. Never reuse the Empty frame here: it would tell a customer
with three payees that they have none.

### Empty

```
Frame: beneficiaries_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: person_off (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No beneficiaries" (headlineMedium, center)
  │   └─ Body: "This account has no saved payees. Manage your consent in
  │             Settings → Consents." (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav
```

**No CTA button.** Points at Settings in prose — the connect/renew affordance lives only on the
consent screens. `home` and `accounts` follow the same convention; a button here would fork the
consent journey. Search bar is **hidden** in this frame.

### Error

```
Frame: beneficiaries_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load beneficiaries" (headlineMedium, center)
  │   ├─ Body: "Check your connection and try again." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

**There is no Unsupported frame** — unlike the three gated list screens. This feature's store
fetcher does not call `recordIfUnsupported`, so a `U000` refusal surfaces here as `ServerError`
with a Retry that cannot succeed. Do not copy this screen as the template for a gated feature;
use `direct-debits`.

---

## 4. Component Variants

### list_item: `beneficiary_row`

| Property | Values |
|---|---|
| State | Default only |

- Fill × Hug, **min 48dp** · Padding 12dp · Gap 16dp · Fill `color/surface`
- **No Pressed / Focused / Selected states** — not interactive

### avatar: `beneficiary_avatar`

40dp × 40dp · Radius `radius/full` · Fill `color/secondaryContainer` · Initials labelLarge
`color/onSecondaryContainer`, centred. Derive initials from the payee name; no image variant.

### search_bar: `beneficiary_search`

| Property | Values |
|---|---|
| State | Placeholder, Filled, Focused |

- Fill × 48dp · Radius `radius/sm` (8dp) · Padding 8/12 · Fill `color/surfaceContainer`

| State | Border | Text colour |
|---|---|---|
| Placeholder | 1dp `color/outline` | `color/onSurfaceVariant` |
| Filled | 1dp `color/outline` | `color/onSurface` |
| Focused | **2dp** `color/primary` | `color/onSurface` |

8dp radius matches the form-field token, not the 12dp card radius — inputs sit tighter than cards
project-wide.

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
| `search` | 24dp | Search bar leading |
| `search_off` | 64dp | No-search-results illustration |
| `person_off` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None. Avatars are generated initials, not assets.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width rows. Primary target. |
| Medium (600–840dp) | List column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | List column capped 600dp, centred. Do **not** grid — avatar/name/identifier is a horizontal row, and pairing them halves the identifier width where a mono account number needs room |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash belongs to home's balance card; equal-weight payee rows must not be privileged. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Avatars use the flat `secondaryContainer` role, not a gradient — a gradient behind initials reads as branding on a person who is not the customer. `tertiary` unused project-wide. |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `outline` `#72787E` (search border) | `surfaceContainer` `#EBEEF3` | 3.9:1 | 3.0 | ✅ |
| `primary` `#266489` (focus border) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 3.0 | ✅ |
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

Search filtering re-emits the list at `short` (150ms) cross-fade — **no** slide, reorder or
stagger. The filter is client-side and instant; animating it would imply a fetch.
