# Settings — Figma Design Prompt

> Generated from `screens/settings/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, **More tab active** · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp, **no leading icon** (tab root)

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surface` | `#F7F9FF` | `#101417` | Screen, row background |
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Dropdown menu surface |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Row pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Row titles, theme value |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Section headers, subtitles, leading + trailing icons |
| `color/primary` | `#266489` | `#95CDF7` | Active tab, focus outline, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

**No money tokens, no Roboto Mono** — this screen shows no figures. Radius: rows square (full-bleed
list), menu `radius/sm`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Content — the only production frame

```
Frame: settings_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, padding 4/16)
  │   └─ Title: "Settings" (titleLarge, color/onSurface)   — NO leading icon
  ├─ ScrollContent (Fill, Auto Layout Vertical, gap 0dp)
  │   ├─ appearance_header (Fill, Hug, padding 24/16/8/16)
  │   │   └─ "APPEARANCE" (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   ├─ theme_row (Fill × 56dp, padding 12/16, Auto Layout Horizontal,
  │   │             align center, space-between)
  │   │   ├─ Title: "Theme" (bodyLarge, color/onSurface)
  │   │   └─ ValueGroup (Hug, Auto Layout Horizontal, gap 4dp)
  │   │       ├─ Value: "System" (bodyLarge, color/onSurfaceVariant)
  │   │       └─ Icon: arrow_drop_down (24dp, color/onSurfaceVariant)
  │   ├─ account_header → "ACCOUNT"
  │   ├─ consents_row (Fill × 64dp, padding 12/16, Auto Layout Horizontal,
  │   │                align center, gap 16dp)
  │   │   ├─ Leading: policy (24dp, color/onSurfaceVariant)
  │   │   ├─ TextColumn (Fill weight 1, gap 2dp)
  │   │   │   ├─ Title: "Manage consents" (bodyLarge, color/onSurface)
  │   │   │   └─ Subtitle: "Review and revoke access" (bodyMedium,
  │   │   │       color/onSurfaceVariant)
  │   │   └─ Trailing: chevron_right (24dp, color/onSurfaceVariant)
  │   ├─ about_header → "ABOUT & LEGAL"
  │   ├─ privacy_row (Fill × 56dp, same shape, no subtitle)
  │   │   ├─ Leading: privacy_tip · Title: "Privacy policy"
  │   │   └─ Trailing: open_in_new (24dp)      ← EXTERNAL, not chevron
  │   ├─ licences_row (Fill × 56dp)
  │   │   ├─ Leading: info · Title: "Open-source licences"
  │   │   └─ Trailing: chevron_right (24dp)
  │   └─ app_version_row (Fill × 64dp, padding 12/16)
  │       ├─ Title: "App version" (bodyLarge, color/onSurface)
  │       └─ Subtitle: "1.0.0 (142)" (bodyMedium, color/onSurfaceVariant)
  │       — NO leading icon, NO trailing, NO interactive states
  └─ BottomNav (Fill × 80dp) — More active
```

Three rules that carry meaning:

1. **The trailing glyph must tell the truth about destination.** `chevron_right` = opens in-app;
   `open_in_new` = leaves for the browser. `privacy_row` gets `open_in_new` because
   `LocalUriHandler.openUri` hands off to the platform. Do not normalise the two to chevrons — a
   customer should know before tapping that they are leaving a banking app.
2. **`app_version_row` has no affordance of any kind.** No leading icon, no trailing glyph, no
   Pressed state. It is a build-identity readout; a chevron would promise a screen that does not
   exist.
3. **Rows are full-bleed, not cards.** Square corners, `color/surface`, separated by section
   headers rather than gaps. Do not wrap groups in `surfaceContainer` cards.

### Theme dropdown — expanded

```
Overlay: settings_theme_menu (Hug, Auto Layout Vertical, radius/sm, padding 8/0)
  Fill: color/surfaceContainer · Elevation: level2
  ├─ MenuItem: "Follow system" (bodyLarge, Fill × 48dp, padding 12/16)  [selected]
  ├─ MenuItem: "Light"
  └─ MenuItem: "Dark"
  Selected item: Fill color/secondaryContainer, label color/onSecondaryContainer
```

Anchored to the row's right edge. Only picking an option persists; opening and dismissing are
local UI state.

### Empty and Error — synthetic, build them plainly

```
Frame: settings_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Auto Layout Vertical, center, gap 8dp, padding 24dp)
  │   ├─ Title: "Nothing to show yet" (headlineMedium, center, color/onSurface)
  │   └─ Body: "Your preferences aren't available." (bodyMedium, center,
  │             color/onSurfaceVariant)
  │   — NO illustration glyph
  └─ BottomNav (same)

Frame: settings_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load settings" (headlineMedium, center)
  │   ├─ Body: "Something went wrong reading your preferences." (bodyMedium, center,
  │   │         color/onSurfaceVariant)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav (same)
```

**Both states are synthetic — no production trigger.** DataStore always resolves a preference set,
falling back to defaults; neither state has been observed. They exist so the surface is exhaustive
and so `FakeUserDataRepository` can drive them in tests. Do not invest illustration work here.

`settings_empty` deliberately has **no glyph**, unlike every other empty state in the app: there is
nothing meaningful to depict, and a wallet or folder icon would imply missing data rather than an
impossible state.

**There is no Loading frame.** DataStore reads do not fail and do not take long enough to warrant a
spinner.

---

## 4. Component Variants

### list_item: settings row

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |
| Leading icon | true (default), **false** — `app_version_row` |
| Trailing | **chevron** (default), external, none |
| Subtitle | true, false |

- Fill × 56dp (no subtitle) / 64dp (with subtitle) · Padding 12/16 · Gap 16dp
- Fill `color/surface`, square corners

| State | Background |
|---|---|
| Default | `color/surface` |
| Pressed | `color/surfaceContainerHigh` + ripple |
| Focused | `color/surface` + 2dp `color/primary` |

Set `app_version_row` to leading=false, trailing=none, **and disable its interactive states** —
it is not tappable.

### select: `theme_row`

| Property | Values |
|---|---|
| Expanded | **false** (default), true |
| Selection | **Follow system** (default), Light, Dark |

Fill × 56dp · Padding 12/16 · Value `bodyLarge` `color/onSurfaceVariant` + `arrow_drop_down` 24dp.
Menu: `radius/sm`, `color/surfaceContainer`, elevation `level2`, 48dp items, selected item filled
`color/secondaryContainer`.

### section_header

Fill × Hug · Padding 24/16/8/16 · `labelMedium` **uppercase** `color/onSurfaceVariant`.
Non-interactive. The 24dp top padding is what separates groups — there are no dividers.

### button: `retry_button`

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
States: Default / Pressed (+ripple) / Focused (2dp outline offset) / Disabled (38%).

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_drop_down` | 24dp | Theme select trailing |
| `policy` | 24dp | Consents row leading |
| `privacy_tip` | 24dp | Privacy row leading |
| `info` | 24dp | Licences row leading |
| `chevron_right` | 24dp | In-app navigation trailing |
| `open_in_new` | 24dp | **External** navigation trailing |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Full-bleed rows, 16dp horizontal padding. Primary target. |
| Medium (600–840dp) | Row column capped 600dp, centred; rows stay full-bleed **within** that column |
| Expanded (> 840dp) | Row column capped 600dp, centred |

Do not turn rows into cards at wider breakpoints — the full-bleed list is the settings idiom, and
a title on the far left with a chevron 1000dp away stops reading as one row.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Settings is a utility surface; a gradient behind a preferences list is decoration on a screen the customer visits to complete a task. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainerHigh` `#E5E8ED` | 13.9:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` (icons) | `surface` `#F7F9FF` | 8.9:1 | 3.0 | ✅ |
| `primary` `#266489` (focus) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. Leading and trailing icons are measured against the 3:1 non-text threshold; each
row's meaning is carried by its text label, never by the glyph alone.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Dropdown expand/collapse at `short` (150ms). **Theme change is not animated by this screen** — the
DataStore write re-emits and the whole app retints; a local transition here would fight the global
one. Under OS reduce-motion the retint is instant.
