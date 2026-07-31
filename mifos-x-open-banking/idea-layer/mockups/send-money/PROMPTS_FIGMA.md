# Send money — Figma Design Prompt

> Generated from `screens/send-money/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-31

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp (system)
- **Bottom nav**: 80dp — **present on every variant** (Pay tab active)
- **Safe area**: top 54dp, bottom 34dp
- **Top app bar**: 56dp, **no leading icon** (tab root)

---

## 2. Design Token Variables

Create as Figma Local Variables. Values resolved from `design-tokens.yaml` — do not re-derive.

### Colors (Light Mode)

| Variable Name | Value | Usage |
|---|---|---|
| `color/primary` | `#266489` | Confirm CTA, active tab, focus outline |
| `color/onPrimary` | `#FFFFFF` | Text on primary |
| `color/primaryContainer` | `#C9E6FF` | Settled disposition only |
| `color/onPrimaryContainer` | `#004B6F` | Text on settled chip |
| `color/secondaryContainer` | `#D3E5F5` | **In-progress chip container** |
| `color/onSecondaryContainer` | `#384956` | In-progress chip text |
| `color/surface` | `#F7F9FF` | Screen background |
| `color/onSurface` | `#181C20` | Primary text, input text |
| `color/onSurfaceVariant` | `#41474D` | Supporting text, labels, currency prefix |
| `color/surfaceContainer` | `#EBEEF3` | Review card background |
| `color/outline` | `#72787E` | Field outline, default |
| `color/error` | `#BA1A1A` | Error icon, error outline, error text |
| `color/errorContainer` | `#FFDAD6` | Rejected disposition only |

### Colors (Dark Mode)

| Variable Name | Value |
|---|---|
| `color/primary` | `#95CDF7` |
| `color/onPrimary` | `#00344E` |
| `color/primaryContainer` | `#004B6F` |
| `color/onPrimaryContainer` | `#C9E6FF` |
| `color/secondaryContainer` | `#384956` |
| `color/onSecondaryContainer` | `#D3E5F5` |
| `color/surface` | `#101417` |
| `color/onSurface` | `#E0E3E8` |
| `color/onSurfaceVariant` | `#C1C7CE` |
| `color/surfaceContainer` | `#1C2024` |
| `color/outline` | `#8B9198` |
| `color/error` | `#FFB4AB` |
| `color/errorContainer` | `#93000A` |

Theme is **auto** (follows OS). Do not pin a mode.

### Typography — Roboto, plus **Roboto Mono** for money

| Style | Font | Size | Weight | Line Height |
|---|---|:---:|:---:|:---:|
| headlineMedium | Roboto | 28sp | 400 | 36sp |
| headlineSmall | **Roboto Mono** | 24sp | 400 | 32sp |
| titleLarge | Roboto | 22sp | 400 | 28sp |
| titleMedium | Roboto | 16sp | 500 | 24sp |
| bodyLarge | Roboto | 16sp | 400 | 24sp |
| bodyMedium | Roboto | 14sp | 400 | 20sp |
| bodySmall | Roboto | 12sp | 400 | 16sp |
| labelLarge | Roboto | 14sp | 500 | 20sp |

`headlineSmall` is bound to **Roboto Mono** for the amount field specifically — mono so digits do
not reflow while typing. Account numbers and sort codes also use mono.

### Spacing

| Token | Value |
|---|:---:|
| `spacing/xs` | 4dp |
| `spacing/sm` | 8dp |
| `spacing/md` | 12dp |
| `spacing/lg` | 16dp |
| `spacing/xl` | 24dp |
| `spacing/2xl` | 32dp |

### Corner Radius

| Token | Value | Applied to |
|---|:---:|---|
| `radius/xs` | 4dp | — |
| `radius/sm` | **8dp** | text fields, amount field |
| `radius/md` | **12dp** | cards, review summary |
| `radius/lg` | 16dp | — |
| `radius/xl` | 28dp | bottom sheets |
| `radius/full` | 9999dp | buttons (pill) |

Fields sit at 8dp, tighter than a card's 12dp — a deliberate distinction, not an oversight.

---

## 3. Auto Layout Structure

### Content — Step 1 (Recipient)

```
Frame: send-money_content_step1 (Fill, Auto Layout Vertical)
  ├─ TopAppBar (Fill × 56dp, Auto Layout Horizontal, padding 4/16)
  │   └─ Title: "Send money" (titleLarge, color/onSurface, Fill)
  │       — NO leading icon: tab root
  ├─ StepIndicator (Fill, Hug, padding 16/16/8/16)
  │   └─ Text: "Step 1 of 3 · Recipient" (labelLarge, color/onSurfaceVariant)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 16dp, gap 16dp)
  │   ├─ SectionLabel: "Pay from" (titleMedium, color/onSurfaceVariant)
  │   ├─ debtor_account_selector (Fill, Auto Layout Vertical, gap 8dp)
  │   │   └─ debtor_account_row (Fill × Hug, min 48dp, padding 12/16, radius/md)
  │   │       Fill: color/surfaceContainer
  │   │       ├─ Headline: "Current account ·· 3349" (bodyLarge, color/onSurface)
  │   │       └─ Supporting: "£21,530.92 available" (bodyMedium, Roboto Mono,
  │   │           color/onSurfaceVariant)   — UNSIGNED, neutral
  │   ├─ SectionLabel: "Pay to" (titleMedium, color/onSurfaceVariant)
  │   ├─ creditor_selector (Fill, Auto Layout Vertical, gap 8dp)
  │   │   └─ creditor_row (Fill × Hug, min 48dp, padding 12/16, radius/md)
  │   │       ├─ Headline: "Jameson Lettings" (bodyLarge)
  │   │       └─ Supporting: "Sort Code · 40-12-09 65872310" (bodyMedium, Roboto Mono)
  │   ├─ no_saved_payees (Fill × Hug, centered)              [variant: 0 beneficiaries]
  │   │   — REPLACES creditor_selector only; the rest of the step is unchanged
  │   │   ├─ Icon: people_outline (48dp, color/onSurfaceVariant)
  │   │   ├─ Title: "No saved payees yet" (titleMedium, color/onSurface)
  │   │   └─ Body: "You have not saved anyone to pay. Enter their account
  │   │             details below to send money." (bodyMedium, color/onSurfaceVariant)
  │   │       manual_creditor_button below STAYS VISIBLE — this variant never
  │   │       becomes a dead end, and must not be drawn as a full-screen empty
  │   ├─ manual_creditor_button (Hug, padding 12/16)
  │   │   └─ Label: "Enter details manually" (labelLarge, color/primary)
  │   ├─ manual_sort_code (Fill × 56dp, radius/sm)          [conditional]
  │   └─ manual_account_number (Fill × 56dp, radius/sm)     [conditional]
  └─ BottomNav (Fill × 80dp) — Pay tab active (color/primary)
```

### Content — Step 2 (Amount)

```
Frame: send-money_content_step2 (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ StepIndicator → "Step 2 of 3 · Amount"
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 16dp, gap 16dp)
  │   ├─ amount_field (Fill × 56dp min, radius/sm)
  │   │   Border: 1dp color/outline → 2dp color/primary on focus
  │   │   ├─ Label: "Amount" (bodySmall, color/onSurfaceVariant) — above field
  │   │   ├─ Prefix: "£" (headlineSmall, color/onSurfaceVariant) — NOT editable
  │   │   └─ Value: "850.00" (headlineSmall, Roboto Mono, color/onSurface)
  │   ├─ reference_field (Fill × 56dp min, radius/sm, max 35 chars)
  │   │   └─ Value: "RENT-FLAT12" (bodyLarge)
  │   └─ review_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ Label: "Review payment" (labelLarge, color/onPrimary)
  └─ BottomNav (same)
```

### Content — Step 3 (Review)

```
Frame: send-money_content_step3 (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ StepIndicator → "Step 3 of 3 · Review"
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 16dp, gap 24dp)
  │   ├─ review_summary → component review_card (Fill × Hug, padding 4dp 16dp, radius/md)
  │   │   Fill: color/surfaceContainer · Stroke 1dp color/outlineVariant · Elevation: level1
  │   │   — trust_critical: outlined AND raised so it reads as a commitment surface,
  │   │     not as another content card
  │   │   ├─ review_from_row      → info_row: "From"      / "Current account ·· 3349"
  │   │   ├─ review_to_row        → info_row: "To"        / "Jameson Lettings"
  │   │   │                          secondary: "40-12-09 65872310" (Roboto Mono, bodyMedium)
  │   │   ├─ review_amount_row    → info_row: "Amount"    / "£850.00" (Roboto Mono, emphasis)
  │   │   └─ review_reference_row → info_row: "Reference" / "RENT-FLAT12"
  │   │       blank reference renders the explicit string "None", never an empty row
  │   │       Row: min-height 48dp, 1dp color/outlineVariant divider between siblings,
  │   │            none after the last · Label: bodySmall color/onSurfaceVariant ·
  │   │            Value: bodyLarge color/onSurface
  │   ├─ confirm_button (Fill × 48dp, radius/full, Fill: color/primary)
  │   │   └─ Label: "Send £850.00" (labelLarge, color/onPrimary)
  │   │       — states the ACTION and the AMOUNT, never a bare "Confirm"
  │   └─ cancel_button (Fill × 48dp, transparent)
  │       └─ Label: "Cancel" (labelLarge, color/primary) — same-weight escape
  └─ BottomNav (same)
```

Nothing in the review card is summarised or truncated. `confirm_button` is `color/primary`, **not**
`color/error` — red would frame an intended payment as a danger.

### Submitting

```
Frame: send-money_submitting (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ SubmittingContent (Hug, Auto Layout Vertical, center, gap 16dp)
  │   ├─ submitting_indicator (48dp circular, color/primary)
  │   └─ StageLabel: "Staging your payment…" (bodyMedium, color/onSurfaceVariant)
  │       — three stages: StagingConsent / AwaitingAuthorisation / SubmittingPayment
  └─ BottomNav (same)
```

All interactive elements are locked in this state — that is the double-submission guard.

### Success

```
Frame: send-money_success (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ SuccessContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: check_circle (64dp, color/primary)
  │   ├─ Title: "Payment submitted" (headlineMedium, center, color/onSurface)
  │   ├─ Body: "£850.00 to Jameson Lettings is being processed. It has been
  │   │         accepted but not yet settled." (bodyMedium, center, color/onSurfaceVariant)
  │   ├─ DispositionChip (Hug, padding 8/16, radius/full)
  │   │   Fill: color/secondaryContainer          ← NOT primaryContainer
  │   │   ├─ Icon: schedule (18dp, color/onSecondaryContainer)
  │   │   └─ Label: "In progress" (labelLarge, color/onSecondaryContainer)
  │   └─ view_payment_status_button (Fill × 48dp, radius/full, Fill: color/primary)
  │       └─ Label: "View payment status" (labelLarge, color/onPrimary)
  └─ BottomNav (same)
```

**Do not restyle this chip to `primaryContainer`.** A successful submit returns
`AcceptedSettlementInProcess` — accepted, not settled. Primary is the credit colour here, so a
primary chip reads as "money arrived", which would be a false statement about the customer's money.
The icon **and** the text label are both mandatory: colour is never the sole signal.

### Error

```
Frame: send-money_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Auto Layout Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Payment not sent" (headlineMedium, center)
  │   ├─ Message: "Payment outside control parameters" (bodyMedium, center,
  │   │            color/onSurfaceVariant)   — verbatim OBIE Errors[].Message
  │   └─ RecoveryButton (Fill × 48dp, radius/full, Fill: color/primary)
  │       — EXACTLY ONE of: Retry / Re-authorise / View consents / Edit amount
  └─ BottomNav (same)
```

Build the recovery button as **one component with a variant property**, not four stacked buttons —
they are mutually exclusive by `error.type`.

---

## 4. Component Variants

### text_field: `amount_field`

| Property | Values |
|---|---|
| State | Default, Focused, Error, Disabled |

- Width: Fill · Height: 56dp min · Padding: 8/16 · Radius: `radius/sm` (8dp)
- Background: `color/surface` · Value: headlineSmall, **Roboto Mono**, `color/onSurface`
- Prefix "£": headlineSmall, `color/onSurfaceVariant`, non-editable

| State | Border | Helper/Error text | Opacity |
|---|---|---|:---:|
| Default | 1dp `color/outline` | — | 100% |
| Focused | **2dp** `color/primary` | — | 100% |
| Error | **2dp** `color/error` | "Amount exceeds available balance" (bodySmall, `color/error`) | 100% |
| Disabled | 1dp `color/outline` | — | **38%** |

Error appears **on change after first blur** — never on the first keystroke.

### button: `confirm_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, Disabled, Loading |

- Width: Fill · Height: 48dp · Radius: `radius/full` · Fill: `color/primary`
- Label: labelLarge, `color/onPrimary`, format `"Send {amountLabel}"`

| State | Background | Border | Opacity |
|---|---|---|:---:|
| Default | `color/primary` | none | 100% |
| Pressed | `color/primary` + ripple | none | 100% |
| Focused | `color/primary` | 2dp `color/primary` outline offset | 100% |
| Disabled | `color/primary` | none | 38% |
| Loading | `color/primary` | none | 100% — label swaps to 20dp spinner, tap disabled |

### list_item: `debtor_account_row` / `creditor_row`

- Width: Fill · Height: Hug, **min 48dp** · Padding: 12/16 · Radius: `radius/md`
- Headline: bodyLarge `color/onSurface` · Supporting: bodyMedium `color/onSurfaceVariant`
- Supporting uses **Roboto Mono** where it carries a balance or an account identifier

| State | Background | Opacity |
|---|---|:---:|
| Default | `color/surfaceContainer` | 100% |
| Pressed | `color/surfaceContainerHigh` + ripple | 100% |
| Focused | `color/surfaceContainer` + 2dp `color/primary` | 100% |
| Selected | `color/secondaryContainer` | 100% |

### chip: disposition chip (success state)

| Property | Values |
|---|---|
| Disposition | **In progress**, Settled, Rejected |

| Disposition | Container | On-container | Icon | Contrast |
|---|---|---|---|:---:|
| In progress | `color/secondaryContainer` | `color/onSecondaryContainer` | `schedule` | 7.22:1 |
| Settled | `color/primaryContainer` | `color/onPrimaryContainer` | `check_circle` | 7.27:1 |
| Rejected | `color/errorContainer` | `color/onErrorContainer` | `error` | 7.24:1 |

Every variant carries icon **and** text label. An OBIE status outside the mapped vocabulary
renders as **In progress**, never as Settled or Rejected.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined, 24dp base)

| Icon | Size | Usage |
|---|:---:|---|
| `check_circle` | 64dp / 18dp | Success illustration / settled chip |
| `schedule` | 18dp | In-progress chip |
| `error` | 18dp | Rejected chip |
| `error_outline` | 64dp | Error state illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None. This feature ships no illustrations — the empty/error surfaces use Material Symbols at 64dp,
consistent with every other screen in the app.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column, full-width rows and CTA. Primary target. |
| Medium (600–840dp) | Content column capped at 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped at 600dp, centred. Do **not** widen the review card — a payment summary spanning 1000dp separates label from value and harms scanability |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** Hero wash is a dashboard device (home's balance card). A form with an irreversible action stays flat; a gradient behind a payment CTA adds visual weight where the system wants calm. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** No accent surface in this feature. `tertiary` is likewise unused project-wide (DESIGN.md: reserved for PFM, since removed). |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surface` `#F7F9FF` | 15.8:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surface` `#F7F9FF` | 8.9:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `onPrimaryContainer` `#004B6F` | `primaryContainer` `#C9E6FF` | 7.27:1 | 4.5 | ✅ |
| `onErrorContainer` `#93000A` | `errorContainer` `#FFDAD6` | 7.24:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (error text) | `surface` `#F7F9FF` | 6.14:1 | 4.5 | ✅ |
| `outline` `#72787E` (field border) | `surface` `#F7F9FF` | 4.24:1 | 3.0 | ✅ |
| `primary` `#266489` (focus border) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |

All pairs pass WCAG AA. Ratios are the measured values recorded in
`state/DESIGN_SYSTEM_STATE.yaml` (15 pairs validated 2026-07-30), not re-derived here.

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — `reduce_motion_supported: true`; honour the OS reduce-motion setting |

Step transitions use `medium` (300ms). The submitting indicator is the only looping animation.
