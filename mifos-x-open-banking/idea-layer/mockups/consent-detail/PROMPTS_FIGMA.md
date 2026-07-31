# Consent detail — Figma Design Prompt

> Generated from `screens/consent-detail/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, More active · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow**

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Detail card, permissions group |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | **Dialog** surface |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Brand, permission bullets, dialog title |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Labels, consent id, dialog body |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | Active chip, **Reconfirm** CTA |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Chip + Reconfirm label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, Cancel label |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Remove access label only** |
| `color/scrim` | `#000000` | `#000000` | Dialog scrim @ 32% |

`bodyMedium` → **Roboto Mono** for the consent id. No money tokens. Radius: cards `radius/md`,
dialog `radius/lg` (16dp), chips/buttons `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Content

```
Frame: consent-detail_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Consent" (titleLarge, color/onSurface, Fill)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 16dp)
  │   ├─ detail_card (Fill × Hug, padding 16dp, radius/md, gap 12dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ HeaderRow (Fill, Horizontal, align center, gap 8dp)
  │   │   │   ├─ Icon: verified_user (24dp, color/onSurfaceVariant)
  │   │   │   ├─ Brand: "HSBC UK Personal" (titleMedium, Fill)
  │   │   │   └─ status_chip "Active" (Hug, padding 2/8, radius/full,
  │   │   │         Fill: color/secondaryContainer, labelSmall)
  │   │   └─ MetaGroup (Fill, Vertical, gap 4dp)
  │   │       ├─ "Consent ID" / "812774903" (value ROBOTO MONO)
  │   │       ├─ "Connected"  / "29 Jun 2026"
  │   │       └─ "Expires"    / "27 Sep 2026"
  │   │           Label bodySmall onSurfaceVariant · Value bodyMedium onSurface
  │   ├─ permissions_header → "WHAT YOU'RE SHARING"
  │   │     (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   ├─ permissions_group (Fill, Vertical, gap 4dp, padding 16dp, radius/md,
  │   │                     Fill: color/surfaceContainer)
  │   │   └─ Bullet ×5 (bodyMedium, color/onSurface)   — FULL LIST
  │   ├─ reconfirm_button (Fill × 48dp, radius/full, TONAL)
  │   │   Fill: color/secondaryContainer ·
  │   │   Label "Reconfirm access" (labelLarge, color/onSecondaryContainer)
  │   └─ remove_access_button (Fill × 48dp, TRANSPARENT)
  │       Label "Remove access" (labelLarge, color/error)
  └─ BottomNav (Fill × 80dp) — More active
```

**`remove_access_button` is a text button with an error-tinted *label* — never a filled red
button.** Weight comes from the confirmation gate, not alarm colour, exactly as send-money's
confirm CTA stays `primary`. A prominent red button invites a mis-tap on the one action that ends
the session. It also sits **below** Reconfirm: the recoverable action gets the higher emphasis.

Render every permission bullet — no truncation, no accordion. Same trust-critical rule as
`consent-list`.

### Revoke confirm — a dialog over dimmed content

```
Overlay: consent-detail_revoke_confirm
  Scrim: color/scrim @ 32% over the content frame
  └─ Dialog (Hug, max-width 320dp, centered, padding 24dp, radius/lg, gap 16dp)
      Fill: color/surfaceContainerHigh · Elevation: level3
      ├─ Title: "Remove access?" (headlineSmall, color/onSurface)
      ├─ Body: "This signs you out and stops this app seeing your HSBC account
      │         information. You can reconnect at any time."
      │        (bodyMedium, color/onSurfaceVariant)
      └─ ActionRow (Hug, Horizontal, align end, gap 8dp)
          ├─ cancel_button   "Cancel"        (text, labelLarge, color/primary)
          └─ confirm_button  "Remove access" (text, labelLarge, color/error)
```

**Nothing has happened yet at this point — no API call is made until Confirm.** Four requirements
this frame must satisfy:

1. A distinct surface stating exactly what will be committed.
2. The confirm **names the action** — "Remove access", not "OK" or "Confirm".
3. A **same-weight escape** beside it: Cancel is the same size, same type style, same emphasis.
   Do not shrink or grey it.
4. Confirming locks the UI — see the next frame.

The body names **both** consequences (signed out *and* data access stops) and states the
reversibility. That last clause is the honest difference from a payment: consent revocation is
destructive but **reversible**; a payment is not. Do not delete it to shorten the copy.

### Revoking — a lock

```
Frame: consent-detail_revoking (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same, back_button DISABLED)
  ├─ RevokingContent (Hug, Vertical, center, gap 16dp)
  │   ├─ progress_indicator (48dp circular, color/primary)
  │   └─ "Removing access…" (bodyMedium, center, color/onSurfaceVariant)
  └─ BottomNav (DISABLED — all four tabs non-interactive)
```

**Every control is locked, including the bottom nav and the back arrow.** That is the
double-submission guard. Do not leave tabs live "for escape" — a tab tap mid-revoke strands the
session between states.

### Empty / Error

```
Frame: consent-detail_empty  — Icon link_off (64dp, onSurfaceVariant),
       "No active consent", CTA "Connect HSBC" → LoginRenewRoute
Frame: consent-detail_error  — Icon error_outline (64dp, color/error),
       "Couldn't load this consent", CTA "Try again"
```

A **failed revoke never reaches the Error frame** — `AppLogout` swallows it by design and proceeds
to sign out locally, so a PSU can always leave even when the bank is unreachable.

---

## 4. Component Variants

### button: emphasis ladder — three levels, and the order matters

| Button | Emphasis | Fill | Label |
|---|---|---|---|
| `reconfirm_button` | **tonal** | `color/secondaryContainer` | `color/onSecondaryContainer` |
| `remove_access_button` | **text** | transparent | `color/error` |
| `cancel_button` (dialog) | text | transparent | `color/primary` |
| `confirm_button` (dialog) | text | transparent | `color/error` |

All Fill × 48dp (screen) / Hug × 40dp (dialog), `radius/full`.
States: Default / Pressed (state-layer 12%) / Focused (2dp outline) / **Disabled 38%** — disabled
matters here, since `revoking` locks everything.

**No filled destructive button anywhere in this feature.**

### card: `detail_card` / `permissions_group`

Fill × Hug · Padding 16dp · Radius `radius/md` · Fill `color/surfaceContainer` · Elevation
`level1` · **No interactive states**. Height content-driven — must grow to fit every permission.

### chip: `status_chip`

Hug × 20dp · Padding 2/8 · Radius `radius/full` · Active: `color/secondaryContainer` /
`color/onSecondaryContainer`. Expired: transparent + 1dp `color/outline`. **Never `color/error`** —
an expired consent is a lifecycle state, not a failure.

### icon_button: `back_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. **Needs a Disabled variant** for `revoking`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `verified_user` | 24dp | Detail card header |
| `link_off` | 64dp | Empty illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

No icon on the revoke dialog — a warning glyph would add alarm the copy already carries precisely.

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width cards and CTAs. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; dialog stays 320dp |
| Expanded (> 840dp) | Content column capped 600dp, centred; dialog stays 320dp |

The dialog never scales with the viewport — a confirmation for an irreversible action should stay a
compact, focused surface.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** This screen holds the app's only sign-out and its full data-sharing disclosure. Decoration behind either is the wrong register in a regulated context. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (Remove access label) | `surface` `#F7F9FF` | 6.14:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (dialog confirm) | `surfaceContainerHigh` `#E5E8ED` | 5.7:1 | 4.5 | ✅ |
| `primary` `#266489` (Cancel) | `surfaceContainerHigh` `#E5E8ED` | 5.6:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surfaceContainerHigh` `#E5E8ED` | 13.9:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |

All pass WCAG AA. Cancel and Confirm are measured against the **same** 4.5:1 text threshold — a
same-weight escape must be equally legible, not merely equally sized.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Dialog enters at `short` (150ms) fade + 95%→100% scale, exits at `short`. `revoke_confirm →
revoking` is **instant, no transition** — the lock must be visibly immediate so a second tap is
obviously impossible. Under OS reduce-motion the dialog cross-fades with no scale.
