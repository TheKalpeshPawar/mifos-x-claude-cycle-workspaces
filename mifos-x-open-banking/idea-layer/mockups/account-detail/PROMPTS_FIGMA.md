# Account detail — Figma Design Prompt

> Generated from `screens/account-detail/ui.yaml` by `/idea-feature-mockup`
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
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Header card, description card, balances group |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Chip pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Account name, balance labels |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Identifier, section headers, **balances (neutral)** |
| `color/secondary` | `#50606E` | `#B7C9D9` | Account-type label |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Explore chips**, Open Banking badge |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Chip labels + icons |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, retry CTA |
| `color/error` | `#BA1A1A` | `#FFB4AB` | Error illustration |

`headlineSmall`/`bodySmall` → **Roboto Mono** for balances and account identifiers. Radius: cards
`radius/md`, chips `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: account-detail_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title (titleLarge, color/onSurface, Fill)
  ├─ loading_spinner (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

**One spinner covers both streams** — `combineScreenStates` holds Loading until account metadata
*and* balances resolve. Do not design two independent loading regions.

### Content

```
Frame: account-detail_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 8dp)
  │   ├─ account_header_card (Fill × Hug, padding 16dp, radius/md, gap 4dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ typeLabel: "CURRENT ACCOUNT" (labelSmall, UPPERCASE, color/secondary)
  │   │   ├─ name: "Current account ·· 3349" (titleLarge, color/onSurface)
  │   │   └─ identifier: "80-20-01 10203349" (bodySmall, Roboto Mono,
  │   │         color/onSurfaceVariant)
  │   ├─ description_card (Fill × Hug, padding 12/16, radius/md)   [CONDITIONAL]
  │   │   Fill: color/surfaceContainer
  │   │   └─ "GLOBAL MONEY ACCOUNT" (bodyMedium, color/onSurface)
  │   ├─ open_banking_badge (Fill × Hug, padding 8/12, radius/md,
  │   │                      Horizontal, gap 8dp, Fill: color/secondaryContainer)
  │   │   ├─ Icon: verified_user (18dp, color/onSecondaryContainer)
  │   │   └─ "Shared via Open Banking" (labelLarge, color/onSecondaryContainer)
  │   ├─ balances_header → "BALANCES" (labelMedium, UPPERCASE)
  │   ├─ balances_list (Fill, Vertical, gap 0dp, radius/md, clip,
  │   │                 Fill: color/surfaceContainer)
  │   │   └─ balance_row (Fill × 48dp, padding 12/16, space-between)
  │   │       ├─ Label: "Available" (bodyLarge, color/onSurface, Fill)
  │   │       └─ Value: "£21,530.92" (headlineSmall, Roboto Mono,
  │   │             color/onSurfaceVariant, align end)
  │   ├─ actions_header → "EXPLORE"
  │   └─ action_chips (Fill, Auto Layout Horizontal, WRAP, gap 8dp,
  │                    scroll: horizontal)
  │       └─ Chip ×9 (Hug × 32dp, padding 6/12, gap 6dp, radius/full,
  │                   Fill: color/secondaryContainer)
  │           ├─ Icon (18dp, color/onSecondaryContainer)
  │           └─ Label (labelLarge, color/onSecondaryContainer)
  └─ BottomNav
```

**`description_card` needs a Visible boolean variant, default off.** It is **omitted, never
blanked**, when OBIE `Description` is empty — guarded with `isNotBlank()`, because the field is
free text and a whitespace-only value would leave a heading above an empty line. Do not design an
em-dash fallback.

It earns its slot because `AccountTypeCode` reports `CACC` for a Global Money wallet exactly as for
a current account — the description is often the only thing naming the product.

Balances are `color/onSurfaceVariant` (`semantic.money.neutral`) and **unsigned**. A balance is a
position, not a transaction; do not tint credit-blue or debit-red.

### The nine Explore chips

Build **one** chip component with an **Explore target** variant property (9 values) plus a
**Visible** boolean. Do not build nine separate components — the suites assert all nine in
declaration order, and visibility is data-driven.

| # | Chip | Icon | Target | Gating |
|---|---|---|---|---|
| 1 | Transactions | `receipt_long` | `transactions` | always |
| 2 | Statements | `description` | `statements` | **credit card ONLY** |
| 3 | Standing orders | `autorenew` | `standing-orders` | gated |
| 4 | Direct debits | `subscriptions` | `direct-debits` | gated |
| 5 | Scheduled payments | `schedule` | `scheduled-payments` | **all EXCEPT credit card** |
| 6 | Beneficiaries | `people` | `beneficiaries` | **all EXCEPT credit card** |
| 7 | ATM locator | `atm` | `_placeholder:atm-locator` | always (placeholder) |
| 8 | Product | `description` | `product` | always |
| 9 | Account holder | `person` | `account-holder` | always |

Statements is the **mirror** of chips 5 and 6: it appears only on a credit card; they appear on
everything but. Gating is **opt-in** — a chip absent from the `gated` map is always visible.

Chips 2 and 8 share the `description` glyph. That is correct as shipped; the labels disambiguate.

### Empty — balances only, inside content

```
balances_empty_state replaces balances_list INSIDE the content frame.
Header card, description card, badge and all nine chips REMAIN.
  └─ EmptyRow (Fill × Hug, padding 16dp, center)
      └─ "No balances available" (bodyMedium, center, color/onSurfaceVariant)
```

**There is no whole-screen empty frame.** An account in consent always has metadata to show. Do not
build one.

### Error

```
Frame: account-detail_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load this account" (headlineMedium, center)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

Retry refreshes **both** streams.

---

## 4. Component Variants

### chip: Explore chip

| Property | Values |
|---|---|
| Target | Transactions, Statements, Standing orders, Direct debits, Scheduled payments, Beneficiaries, ATM locator, Product, Account holder |
| State | Default, Pressed, Focused |
| Visible | **true** (default), false |

- Hug × 32dp · Padding 6/12 · Gap 6dp · Radius `radius/full`
- Fill `color/secondaryContainer` · Icon 18dp · Label labelLarge `color/onSecondaryContainer`

| State | Background |
|---|---|
| Default | `color/secondaryContainer` |
| Pressed | `color/surfaceContainerHigh` + ripple |
| Focused | `color/secondaryContainer` + 2dp `color/primary` |

**No Disabled variant.** A chip for an unsupported product is **hidden**, never greyed — a disabled
chip invites a tap that can only fail.

### card: `account_header_card` / `description_card`

Fill × Hug · Padding 16dp (header) / 12–16dp (description) · Radius `radius/md` ·
Fill `color/surfaceContainer` · Elevation `level1` tonal · **No interactive states**.

`description_card`: **Visible** boolean, default **off**.

### card: `open_banking_badge`

Fill × Hug · Padding 8/12 · Radius `radius/md` · Fill `color/secondaryContainer` · Icon 18dp +
labelLarge. Non-interactive — a trust statement, not a control. No Pressed state.

### list_item: `balance_row`

Fill × 48dp · Padding 12/16 · space-between · **No interactive states**. Rows clipped inside one
`radius/md` container so consecutive balances read as a table.

### icon_button: `back_button` / button: `retry_button`

48dp × 48dp touch target, 24dp `arrow_back`, `color/primary`. Retry: Fill × 48dp, `radius/full`,
`color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `verified_user` | 18dp | Open Banking badge |
| `receipt_long` · `description` · `autorenew` · `subscriptions` · `schedule` · `people` · `atm` · `person` | 18dp | Explore chips (`description` used twice — chips 2 and 8) |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column; chips scroll horizontally. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; chips **wrap** to two rows instead of scrolling |
| Expanded (> 840dp) | Content column capped 600dp, centred; chips wrap |

Wrapping beats scrolling once width allows: a horizontally scrolled row hides chips 7–9 behind a
gesture, and on this screen those are the entry points to Product and Account holder.

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The header card is a candidate hero surface, but this screen's job is dense factual disclosure — balances, product description, consent badge. A wash behind a balance figure adds emphasis the number already carries. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Chips use the flat `secondaryContainer` role; a gradient across nine chips would fight the gating signal (present vs absent). `tertiary` unused project-wide. |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `secondary` `#50606E` | `surfaceContainer` `#EBEEF3` | 6.0:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `onSecondaryContainer` (chip icons) | `secondaryContainer` | 7.22:1 | 3.0 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |
| `error` `#BA1A1A` (error glyph) | `surface` `#F7F9FF` | 6.14:1 | 3.0 | ✅ |

All pass WCAG AA. Every chip carries an icon **and** a text label, so meaning never rests on the
glyph — which matters here because chips 2 and 8 share `description`.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms). **Chips do not animate in.** Their visibility is
resolved before first paint by `availableChipsFor`; a stagger or fade would imply they are still
arriving, and a customer who sees six chips settle might reasonably wait for a seventh.
