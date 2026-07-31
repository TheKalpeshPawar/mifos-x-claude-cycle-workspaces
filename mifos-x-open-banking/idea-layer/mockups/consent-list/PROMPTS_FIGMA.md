# Consent list — Figma Design Prompt

> Generated from `screens/consent-list/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp, **More tab active** · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow** (pushed from Settings)

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Consent card |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Card pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Brand name, permission bullets |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Dates, labels, empty glyph |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Active** status chip |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Chip label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, Connect / Reconnect CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration **only** |

**No money tokens, no Roboto Mono** — this screen shows permissions and dates, not figures.
Radius: card `radius/md`, chip and buttons `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: consent-list_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Manage consents" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp) — More active
```

### Content — a list of exactly one

```
Frame: consent-list_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp)
  │   └─ consent_card (Fill × Hug, padding 16dp, radius/md, gap 16dp)
  │       Fill: color/surfaceContainer · Elevation: level1 · TAPPABLE
  │       ├─ HeaderRow (Fill, Horizontal, align center, gap 8dp)
  │       │   ├─ Icon: verified_user (24dp, color/onSurfaceVariant)
  │       │   ├─ Brand: "HSBC UK Personal" (titleMedium, color/onSurface, Fill)
  │       │   └─ status_chip (Hug, padding 2/8, radius/full,
  │       │         Fill: color/secondaryContainer)
  │       │       └─ "Active" (labelSmall, color/onSecondaryContainer)
  │       ├─ DatesGroup (Fill, Vertical, gap 4dp)
  │       │   ├─ Row: "Connected" / "29 Jun 2026"
  │       │   └─ Row: "Expires"   / "27 Sep 2026"
  │       │       Label bodySmall color/onSurfaceVariant ·
  │       │       Value bodyMedium color/onSurface
  │       ├─ PermissionsGroup (Fill, Vertical, gap 4dp)
  │       │   ├─ "Sharing" (bodySmall, color/onSurfaceVariant)
  │       │   └─ Bullet ×5 (bodyMedium, color/onSurface)
  │       │       "Accounts and balances" · "Transactions" ·
  │       │       "Standing orders, direct debits" ·
  │       │       "Beneficiaries and statements" · "Account holder details"
  │       └─ Trailing: chevron_right (24dp, color/onSurfaceVariant, align end)
  └─ BottomNav (same)
```

**Render every permission. No truncation, no "and 3 more", no collapsed accordion.** DESIGN.md
names the consent card the trust-critical surface: *"always explicit, never truncated."* This is
what the customer agreed to share — hiding part of it behind a tap is the one thing this screen
must not do. Let the card grow and the page scroll.

**One card only.** This screen reads `session.consentId()` — the *current* connection. There is no
device-side consent history. Do not design a multi-row list or an empty-slot placeholder.

The expiry row is a **regulatory fact** (90-day reconfirmation, SCA-RTS Art 36(6) / Art 10A), not a
convenience — do not demote it to a subtitle or hide it behind the chevron.

### Empty — the one empty state that *does* get a CTA

```
Frame: consent-list_empty (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ EmptyContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: link_off (64dp, color/onSurfaceVariant)
  │   ├─ Title: "No bank connected" (headlineMedium, center)
  │   ├─ Body: "Connect your HSBC accounts to get started."
  │   │        (bodyMedium, center, color/onSurfaceVariant)
  │   └─ connect_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Connect HSBC" (labelLarge, color/onPrimary)
  └─ BottomNav (same)
```

`home`, `accounts` and `beneficiaries` all deliberately omit a connect CTA — the affordance lives
**only** on the consent screens. This *is* a consent screen, so the button belongs here. Target is
`LoginRenewRoute` (login inside the authenticated host, no onboarding intro).

### Error auth — a separate frame, not an Error variant

```
Frame: consent-list_error_auth (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ AuthContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: warning_amber (64dp, color/onSurfaceVariant)   ← NOT color/error
  │   ├─ Title: "Your connection has expired" (headlineMedium, center)
  │   ├─ Body: "Reconnect to keep seeing your account information."
  │   │        (bodyMedium, center, color/onSurfaceVariant)
  │   └─ reconnect_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ "Reconnect" (labelLarge, color/onPrimary)
  └─ BottomNav (same)
```

**Build this as its own frame.** An expired or revoked consent is not a transient failure —
retrying the same call fails identically. Three consequences for the design:

1. The CTA is **Reconnect**, not Try again, and it routes to `LoginRenewRoute`.
2. The glyph is `warning_amber` in `color/onSurfaceVariant`, **not** `error_outline` in
   `color/error`. A 90-day expiry is the system working as designed, not a fault.
3. Do not collapse it into the Error frame with a swapped label — the two states mean different
   things and lead to different destinations.

### Error

```
Frame: consent-list_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load your consent" (headlineMedium, center)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav (same)
```

Transport and unexpected server failures only.

---

## 4. Component Variants

### card: `consent_card`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused |
| Status | **Active** (default), Expiring, Expired |

- Fill × Hug · Padding 16dp · Radius `radius/md` · Gap 16dp · Fill `color/surfaceContainer` ·
  Elevation `level1`
- Pressed `color/surfaceContainerHigh` + ripple · Focused 2dp `color/primary`

Height is **content-driven** — it must grow to fit every permission bullet. Do not set a max height
or add internal scrolling.

### chip: `status_chip`

| Status | Fill | Label colour |
|---|---|---|
| Active | `color/secondaryContainer` | `color/onSecondaryContainer` |
| Expiring | `color/secondaryContainer` | `color/onSecondaryContainer` |
| Expired | transparent + 1dp `color/outline` | `color/onSurfaceVariant` |

Hug × 20dp · Padding 2/8 · Radius `radius/full` · labelSmall. **Never `color/error`** — an expired
consent is a lifecycle state, not a failure.

### button: `connect_button` / `reconnect_button` / `retry_button`

Fill × 48dp · Radius `radius/full` · Fill `color/primary` · labelLarge `color/onPrimary`.
States: Default / Pressed (+ripple) / Focused (2dp outline offset) / Disabled (38%).

Three different labels and two different destinations — do not merge into one component whose
label is a free-text override; the destination differs.

### icon_button: `back_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `verified_user` | 24dp | Consent card header |
| `chevron_right` | 24dp | Consent card trailing |
| `link_off` | 64dp | Empty illustration |
| `warning_amber` | 64dp | **Expired-consent** illustration |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width card. Primary target. |
| Medium (600–840dp) | Card capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Card capped 600dp, centred. Do **not** put permissions in two columns — a scanned list of what is being shared must read top-to-bottom in one pass |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The consent card is the app's trust-critical surface; a decorative wash behind a data-sharing disclosure is exactly the wrong register. Flat `surfaceContainer` keeps it factual. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface. `tertiary` unused project-wide (reserved for PFM, since removed). |

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
| `outline` `#72787E` (expired chip) | `surfaceContainer` `#EBEEF3` | 3.9:1 | 3.0 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. The status chip carries a **text label** in every variant, so consent state never
depends on chip colour alone.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). **Permission bullets do not stagger in** — a
customer must be able to see the complete list at first paint, not watch it assemble.
