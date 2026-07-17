# Scheduled Payments — Figma Design Prompts

> Auto-generated from `screens/scheduled-payments/ui.yaml`
> Canvas: 393×852dp (Pixel 5), Roboto / Roboto Mono, Material Design 3 light theme
> Design system: Open Banking — Trust Blue (seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Canvas and Project Setup

Create a new Figma page titled "Scheduled Payments — Screen States". Set the file to use a 4dp base grid with nudge set to 4dp increments. Import the Open Banking colour styles from your shared design system library or manually define the variables described in the token mapping table below before placing any components.

Create four top-level frames named exactly:

- `SP / Loading`
- `SP / Content`
- `SP / Empty`
- `SP / Error`

Each frame is **393dp wide × 852dp tall**, clip content enabled, fill colour `color/background` (#F7F9FF). Arrange all four horizontally in an Auto Layout parent container titled `Scheduled Payments — All States`, with 48dp horizontal gap and 32dp padding on all sides.

---

## Design System Summary

### Resolved Colour Palette (M3 Light)

| Role | Hex | Usage in this screen |
|---|---|---|
| primary | #266489 | back_button icon tint, Accounts nav tab active, retry_button fill |
| onPrimary | #FFFFFF | retry_button label text |
| primaryContainer | #C9E6FF | — |
| onPrimaryContainer | #004B6F | — |
| secondary | #50606E | — |
| secondaryContainer | #D3E5F5 | sp_type_chip background |
| onSecondaryContainer | #384956 | sp_type_chip label and icon tint |
| error | #BA1A1A | sp_amount text, error state icon tint |
| onError | #FFFFFF | — |
| background | #F7F9FF | screen background fill |
| surface | #F7F9FF | screen surface |
| onSurface | #181C20 | sp_payee_name, top app bar title, headings |
| surfaceVariant | #DDE3EA | — |
| onSurfaceVariant | #41474D | sp_scheduled_date, sp_account_id, sp_reference, nav default tab |
| surfaceContainer | #EBEEF3 | top app bar background |
| surfaceContainerLow | #F1F4F9 | scheduled_payment_card fill (elevated card) |
| outline | #72787E | — |
| outlineVariant | #C1C7CE | card border (subtle, M3 elevated) |

### Typography Scale (Roboto, M3 defaults)

| Token | Size / Leading / Weight | Usage |
|---|---|---|
| titleLarge | 22sp / 28sp / 400 | Top app bar title |
| headlineSmall | 24sp / 32sp / 400 | sp_amount payment amount (Roboto Mono) |
| titleMedium | 16sp / 24sp / 500 | sp_payee_name payee display name |
| bodyMedium | 14sp / 20sp / 400 | error body text, empty body text |
| bodySmall | 12sp / 16sp / 400 | sp_scheduled_date formatted date |
| labelLarge | 14sp / 20sp / 500 | sp_type_chip label, retry_button label |
| labelSmall | 11sp / 16sp / 500 | sp_account_id, sp_reference captions (Roboto Mono for account) |

Use **Roboto Mono** for sp_amount and sp_account_id to ensure numeric alignment and legibility of sort code / account numbers.

### Semantic Token → Figma Variable Mapping

| Semantic token | Figma variable name | Resolved value |
|---|---|---|
| `color/primary` | `color/primary` | #266489 |
| `color/onPrimary` | `color/onPrimary` | #FFFFFF |
| `color/secondaryContainer` | `color/secondaryContainer` | #D3E5F5 |
| `color/onSecondaryContainer` | `color/onSecondaryContainer` | #384956 |
| `color/error` | `color/error` | #BA1A1A |
| `color/background` | `color/background` | #F7F9FF |
| `color/onSurface` | `color/onSurface` | #181C20 |
| `color/onSurfaceVariant` | `color/onSurfaceVariant` | #41474D |
| `color/surfaceContainer` | `color/surfaceContainer` | #EBEEF3 |
| `color/surfaceContainerLow` | `color/surfaceContainerLow` | #F1F4F9 |
| `typography/titleLarge` | `typography/titleLarge` | Roboto 22/28 Regular |
| `typography/headlineSmall` | `typography/headlineSmall` | Roboto Mono 24/32 Regular |
| `typography/titleMedium` | `typography/titleMedium` | Roboto 16/24 Medium |
| `typography/bodySmall` | `typography/bodySmall` | Roboto 12/16 Regular |
| `typography/labelSmall` | `typography/labelSmall` | Roboto Mono 11/16 Medium |
| `spacing/screen_padding` | `spacing/screen_padding` | 16dp |
| `shape/medium` | `shape/medium` | 12dp corner radius |
| `shape/full` | `shape/full` | 9999dp (pill) |

---

## Frame 1: SP / Loading

### Frame Structure

The Loading frame represents the screen while `ScheduledPaymentsViewModel` emits `ScheduledPaymentsUiState.Loading`, which occurs immediately on mount before the GET request to the HSBC AISP endpoint completes.

Begin with the **Top App Bar**. Create a rectangle spanning the full 393dp width, 64dp tall, fill `color/surfaceContainer` (#EBEEF3), zero corner radius. Inside it, place an arrow-back icon button on the left side with 16dp from the left edge, vertically centred, 48dp × 48dp touch target, 24dp icon size, icon colour `color/primary` (#266489). To the right of the icon, add the screen title "Scheduled Payments" in Roboto 22sp / 28sp / Regular, colour `color/onSurface` (#181C20). The title should start at 72dp from the left edge, vertically centred within the bar.

In the **content area** (393dp wide × 708dp tall, positioned below the top app bar), place a single circular indeterminate progress indicator centred both horizontally and vertically. The indicator is 48dp in diameter with a 4dp stroke, coloured `color/primary` (#266489). For design purposes, represent the spinning arc at roughly the 180° position to suggest motion. Annotate that in Compose this is `CircularProgressIndicator(color = MaterialTheme.colorScheme.primary)`.

Finish the frame with the **Bottom Navigation Bar**. The bar is 393dp wide × 80dp tall at the bottom of the frame, fill `color/background` (#F7F9FF). It contains four evenly spaced tabs:

- **Home** — icon: home, label: "Home", state: default, tint `color/onSurfaceVariant` (#41474D)
- **Accounts** — icon: account_balance, label: "Accounts", state: **selected**, tint `color/primary` (#266489), with the M3 active indicator pill (64dp wide × 32dp tall, fill #C9E6FF with 16dp radius) behind the icon
- **Transactions** — icon: receipt_long, label: "Transactions", state: default, tint #41474D
- **More** — icon: more_horiz, label: "More", state: default, tint #41474D

Each tab occupies exactly 98.25dp of horizontal space. Icons are 24dp. Tab labels use Roboto 12sp / 16sp / Medium.

### Auto Layout — Loading Frame

The entire frame uses a **Vertical Auto Layout** with these regions stacked from top to bottom:

- Top App Bar: fixed height 64dp, fill container width
- Content Area: fill remaining height (708dp), fill container width, child centred using alignment Horizontal Center + Vertical Center for the progress indicator
- Bottom Nav: fixed height 80dp, fill container width

---

## Frame 2: SP / Content

### Frame Overview

The Content frame represents `ScheduledPaymentsUiState.Content` with four `ScheduledPaymentUiModel` items loaded from account 40051512345678. The list scrolls vertically — the total card height (4 × 192dp + 3 × 8dp gap = 792dp) exceeds the 708dp content area by 84dp. Show a subtle scroll indicator on the right edge to communicate scrollability.

### Top App Bar

Identical to the Loading frame — 393dp × 64dp, fill #EBEEF3. Back button on left (48dp × 48dp, arrow_back, #266489), title "Scheduled Payments" (Roboto 22sp Regular #181C20).

### Scheduled Payments List

Create a **Vertical Auto Layout** frame for the list, spanning 393dp wide × 708dp tall, fill transparent, padding: 16dp left, 16dp right, 8dp top, 16dp bottom. Set to clip content. Inside the list, place four payment card components with an 8dp gap between each card.

#### Payment Card Component

Design a reusable component titled `ScheduledPaymentCard`. The card is a **Vertical Auto Layout** frame:

- Width: fill container (resolves to 361dp inside the list with 16dp horizontal padding on each side)
- Height: hug contents (~192dp depending on content)
- Fill: `color/surfaceContainerLow` (#F1F4F9)
- Corner radius: 12dp (M3 `shape/medium`)
- Elevation: 1dp — express this as a drop shadow: offset X 0, offset Y 1, blur 1, spread 0, colour rgba(0,0,0,0.15)
- Padding: 16dp all sides
- Gap between children: 4dp (vertical)

Inside the card, place six child layers in order from top to bottom:

**Layer 1 — sp_payee_name**: Text element, Roboto 16sp / 24sp / Medium (titleMedium), colour `color/onSurface` (#181C20). Single line, truncate with ellipsis at card boundary. Resize: fill container width, hug height.

**Layer 2 — sp_amount**: Text element, Roboto Mono 24sp / 32sp / Regular (headlineSmall), colour `color/error` (#BA1A1A). This colour is intentional — all outgoing payment amounts use the error colour for immediate visual differentiation. Resize: fill container width, hug height. This is the most visually prominent field, creating a clear visual hierarchy where the amount commands attention immediately after the payee name.

**Layer 3 — sp_scheduled_date**: Text element, Roboto 12sp / 16sp / Regular (bodySmall), colour `color/onSurfaceVariant` (#41474D). Prefix "Due:" is localised from strings.sp_due_prefix. Resize: fill container width, hug height.

**Layer 4 — sp_type_chip**: This is an Assist Chip component. Structure it as a Horizontal Auto Layout frame:

- Height: 32dp fixed
- Width: hug contents
- Fill: `color/secondaryContainer` (#D3E5F5)
- Corner radius: 9999dp (full pill, M3 chip shape)
- Padding: 0dp vertical, 8dp leading, 16dp trailing
- Gap: 8dp
- Vertical alignment: center

Inside the chip, place:
- Icon: 18dp × 18dp, tint `color/onSecondaryContainer` (#384956). Use `calendar_today` for Execution type payments, `arrow_downward` for Arrival type payments.
- Label text: Roboto 14sp / 20sp / Medium (labelLarge), colour #384956. Content: "Execution date" (Execution type) or "Arrival date" (Arrival type).

Add 8dp top spacing above the chip (increase the gap between sp_scheduled_date and sp_type_chip to 8dp to give the chip room to breathe).

**Layer 5 — sp_account_id**: Text element, Roboto Mono 11sp / 16sp / Medium (labelSmall), colour `color/onSurfaceVariant` (#41474D). Prefix "To:" is localised from strings.sp_account_prefix. Using Roboto Mono here ensures sort code characters (hyphens, digits) render at consistent width for quick scanning. Resize: fill container width, hug height.

**Layer 6 — sp_reference**: Text element, Roboto 11sp / 16sp / Medium (labelSmall), colour #41474D. Prefix "Ref:" is localised from strings.sp_ref_prefix. Resize: fill container width, hug height.

#### Four Card Instances with Real Content

Detach four instances of ScheduledPaymentCard and populate each with the following real data from demo-data.yaml:

**Card 1 — SP-001 (HMRC Self Assessment):**
- sp_payee_name: "HMRC Self Assessment"
- sp_amount: "GBP 842.00"
- sp_scheduled_date: "Due: Fri 31 Jul 2026"
- sp_type_chip: icon calendar_today, label "Execution date"
- sp_account_id: "To: 08-32-00 12001039"
- sp_reference: "Ref: HMRC-SA-2526"

**Card 2 — SP-002 (Westminster Council Tax):**
- sp_payee_name: "Westminster Council Tax"
- sp_amount: "GBP 198.00"
- sp_scheduled_date: "Due: Sun 5 Jul 2026"
- sp_type_chip: icon calendar_today, label "Execution date"
- sp_account_id: "To: 60-23-05 20490017"
- sp_reference: "Ref: CTAX-JUL"

**Card 3 — SP-003 (Direct Line Insurance):**
- sp_payee_name: "Direct Line Insurance"
- sp_amount: "GBP 412.50"
- sp_scheduled_date: "Due: Sat 15 Aug 2026"
- sp_type_chip: icon arrow_downward, label "Arrival date" — note the chip icon is different for Arrival type
- sp_account_id: "To: 20-00-00 73428901"
- sp_reference: "Ref: DL-HOME-INS-26"

**Card 4 — SP-004 (Amazon Payments UK):**
- sp_payee_name: "Amazon Payments UK"
- sp_amount: "GBP 95.00"
- sp_scheduled_date: "Due: Tue 14 Jul 2026"
- sp_type_chip: icon calendar_today, label "Execution date"
- sp_account_id: "To: 23-69-72 10001289"
- sp_reference: "Ref: PRIME-ANN-26"

### Bottom Navigation — Content Frame

Same structure as described in Frame 1. Accounts tab remains selected (#266489).

---

## Frame 3: SP / Empty

### Frame Overview

This frame represents `ScheduledPaymentsUiState.Empty`, shown when the OBIE response returns an empty `Data.ScheduledPayment[]` array. No retry button is needed — the empty state communicates that there are simply no scheduled payments on this account, which is a valid non-error condition.

### Top App Bar

Same as Loading and Content frames — 64dp × 393dp, fill #EBEEF3, back button left (#266489), title "Scheduled Payments" (#181C20).

### Empty State Content

In the content area (393dp × 708dp), centre a **Vertical Auto Layout** group both horizontally and vertically. The group should have 16dp gap between children and 32dp horizontal padding on either side (effectively 329dp wide for the text elements).

Place the following children top to bottom:

First, a Material Design icon `schedule` at 48dp × 48dp, tint `color/onSurfaceVariant` (#41474D). Set contentDescription to "No scheduled payments" for accessibility. The schedule icon — a clock with a circular refresh indicator — visually reinforces the concept of planned future payments without implying an error.

Below the icon, place the title text: "No scheduled payments" in Roboto 24sp / 32sp / Regular (headlineSmall), colour `color/onSurface` (#181C20), text alignment centred.

Below the title, place the body text: "No payments are scheduled for this account." in Roboto 14sp / 20sp / Regular (bodyMedium), colour `color/onSurfaceVariant` (#41474D), text alignment centred, max width 329dp, allow line wrapping.

Do not add a CTA button or action here. The empty state for scheduled payments is read-only — the AISP consent gives no ability to create payments. Deliberately omitting a button communicates this constraint naturally.

### Bottom Navigation — Empty Frame

Same structure, Accounts tab selected.

---

## Frame 4: SP / Error

### Frame Overview

This frame represents `ScheduledPaymentsUiState.Error`, surfaced when the HSBC AIS endpoint responds with 401, 403, 429, or when a network exception occurs. The design must communicate the error clearly and offer a recovery action via the retry button. The primary demo render uses the NetworkError variant (EC-SP-004).

### Top App Bar

Same structure as all other frames — 64dp × 393dp, fill #EBEEF3, back button, title.

### Error State Content

In the content area, centre a **Vertical Auto Layout** group both horizontally and vertically. Gap between children: 16dp. Horizontal padding: 32dp on each side.

Place the following children in order:

First, a Material Design icon `error_outline` at 48dp × 48dp, tint `color/error` (#BA1A1A). Using the outline variant (error_outline rather than error) keeps the icon visually lighter, preventing the screen from feeling overly alarming for a transient network failure. Set contentDescription to "Error loading scheduled payments".

Below the icon, the title "Unable to load scheduled payments" in Roboto 24sp / 32sp / Regular (headlineSmall), colour `color/onSurface` (#181C20), centred. This phrasing is specific to the operation that failed, not generic.

Below the title, place the dynamic body text. Design four text overrides (as Figma variants or documentation layers) showing each error message:
- EC-SP-001 (401): "Session expired. Please log in again."
- EC-SP-002 (403): "Account access consent has been revoked."
- EC-SP-003 (429): "Too many requests. Please wait a moment and try again."
- EC-SP-004 (network): "No network connection. Check your connection and retry."

Use EC-SP-004 as the default visible text in the primary frame. Style as Roboto 14sp / 20sp / Regular (bodyMedium), colour `color/onSurfaceVariant` (#41474D), centred, allow wrapping.

Below the body text, add **16dp additional spacing** before the retry button to give the button visual separation from the error explanation.

Create the **retry_button** as a Figma component using a **Horizontal Auto Layout** frame:
- Width: fill container within the 32dp horizontal padding on each side (effective width 329dp)
- Height: 56dp fixed
- Fill: `color/primary` (#266489)
- Corner radius: 9999dp (M3 FilledButton, full pill)
- Horizontal padding: 24dp, vertical alignment: center
- Child: text "Try again" in Roboto 14sp / 20sp / Medium (labelLarge), colour `color/onPrimary` (#FFFFFF), centred

The retry_button minimum touch target is 56dp (height already 56dp, so compliant). For pressed state, show fill as `color/primary` with a 12% white overlay (#FFFFFF1F) per M3 ripple. For disabled state (not applicable in this flow — retry is always enabled when error is visible), fill would be onSurface at 12% opacity.

### Bottom Navigation — Error Frame

Same structure, Accounts tab selected.

---

## Auto Layout Specifications Summary

The following table captures the Figma Auto Layout configuration for each key container in this screen:

**Top App Bar** (all states): Direction Horizontal, padding 16dp left 16dp right, 0 top 0 bottom, gap 16dp between back button and title, align items Center Vertically, height 64dp fixed, width Fill Container.

**Content Area** (loading): Direction Vertical, align Center Horizontally, align Center Vertically for child progress indicator placement. Height Fill, width Fill.

**Scheduled Payments List** (content): Direction Vertical, padding 16dp left 16dp right 8dp top 16dp bottom, gap 8dp between items, height Fill Container with clip enabled, width Fill Container.

**ScheduledPaymentCard**: Direction Vertical, padding 16dp all sides, gap 4dp (increase to 8dp above sp_type_chip for breathing room), height Hug Contents (~192dp), width Fill Container. Background #F1F4F9, corner radius 12dp, drop shadow 0/1/1 rgba(0,0,0,0.15).

**sp_type_chip**: Direction Horizontal, padding 0 vertical 8dp leading 16dp trailing, gap 8dp, height 32dp fixed, width Hug Contents, background #D3E5F5, corner radius 9999dp, align items Center Vertically.

**Empty / Error State Container**: Direction Vertical, gap 16dp, padding 32dp horizontal, align Center Horizontally, vertically centred within the 393×708dp content area using Align Center in parent.

**retry_button**: Direction Horizontal, padding 24dp horizontal, height 56dp fixed, width Fill Container, background #266489, corner radius 9999dp, align Center.

**Bottom Navigation Bar**: Direction Horizontal, height 80dp fixed, width Fill Container, background #F7F9FF, padding 0dp horizontal, gap 0 (tabs are evenly distributed, each tab 98.25dp wide).

---

## Component Variants

Design the ScheduledPaymentCard component with a `chipType` property to switch between chip variants:

| Property | Value A | Value B |
|---|---|---|
| chipType | Execution | Arrival |
| chip icon | calendar_today | arrow_downward |
| chip label | "Execution date" | "Arrival date" |
| chip a11y | "Money leaves your account on {date}" | "Funds arrive at {payee} on {date}" |

Design the sp_type_chip as a nested component with an `icon` property and a `label` string property.

For the retry_button, define the following interaction states as Figma variants:

| State | Fill | Label colour | Overlay |
|---|---|---|---|
| Default | #266489 | #FFFFFF | none |
| Hovered | #266489 | #FFFFFF | 8% white (#FFFFFF14) |
| Pressed | #266489 | #FFFFFF | 12% white (#FFFFFF1F) |
| Focused | #266489 | #FFFFFF | 12% white + 3dp focus ring #266489 |

For the back_button icon button, define:

| State | Background | Icon tint |
|---|---|---|
| Default | transparent | #266489 |
| Hovered | transparent + 8% #266489 (primary) state-layer overlay | #266489 |
| Pressed | #266489 at 12% | #266489 |
| Focused | transparent + 3dp focus ring | #266489 |

---

## Prototype Interaction Flow

Wire the following interactions in Figma Prototype mode:

On the **SP / Loading** frame, there are no tappable elements visible to the user (the progress indicator is not interactive). The transition to SP / Content or SP / Error occurs automatically when the ViewModel emits a new state. In Figma, connect SP / Loading → SP / Content using a Smart Animate transition, duration 300ms, ease-out easing, triggered by After Delay 1500ms (for demo purposes).

On the **SP / Content** frame, the back_button (arrow_back) navigates back to the account-detail screen. Connect back_button → account-detail frame (or a representative screen) using Navigate To with Smart Animate, duration 300ms, ease-out. The payment cards themselves are display-only under AISP read-only consent — do not wire tap interactions on the cards.

On the **SP / Empty** frame, the back_button navigates back to account-detail identical to the content frame.

On the **SP / Error** frame:
- back_button → navigate back to account-detail frame, Smart Animate 300ms ease-out
- retry_button → SP / Loading frame, Smart Animate 300ms ease-in, represents the re-trigger of `LoadScheduledPayments(accountId)`. After delay 1500ms → SP / Content (happy path demo).

---

## Accessibility Specifications

Every interactive element in this screen must meet WCAG AA contrast ratios and a minimum 48dp touch target.

The **back_button** has a minimum 48dp × 48dp touch area. contentDescription resolves to "Navigate back" (strings.sp_back_a11y). In Figma, annotate the touch zone with a 48dp × 48dp transparent overlay labelled "Touch target 48dp".

Each **ScheduledPaymentCard** has a merged accessibility node with label "Payment of {amount} {currency} to {payee name}" (pattern: `strings.sp_card_a11y_prefix + item.InstructedAmount.Amount + item.InstructedAmount.Currency + strings.sp_card_a11y_to + item.CreditorAccount.Name`). Example for SP-001: "Payment of 842.00 GBP to HMRC Self Assessment". The individual child text nodes (sp_payee_name, sp_amount, sp_scheduled_date, sp_type_chip, sp_account_id, sp_reference) are individually focusable for TalkBack sequential traversal.

The **sp_amount** field uses colour #BA1A1A on #F1F4F9 (card background). Contrast ratio = 5.23:1, passes WCAG AA (4.5:1 required for 24sp normal text). Passes. Annotate this in the accessibility notes layer.

The **sp_type_chip** label #384956 on #D3E5F5 background: contrast ratio = 4.67:1, passes WCAG AA for normal text at 14sp. Passes. The chip's `accessibility_label` is the expanded a11y string: "Money leaves your account on 31 Jul 2026" (Execution) or "Funds arrive at Direct Line Insurance on 15 Aug 2026" (Arrival).

The **sp_account_id** Roboto Mono text #41474D on #F1F4F9: contrast ratio = 6.15:1 — well above WCAG AA threshold. The Roboto Mono typeface at 11sp/16sp improves readability of the sort-code format (08-32-00 12001039) compared to proportional Roboto.

The **empty state icon** (schedule 48dp at #41474D on #F7F9FF): icon is decorative in visual terms but carries semantic meaning — contentDescription "No scheduled payments" should be set, making it non-decorative for accessibility APIs.

The **retry_button** text "Try again" (#FFFFFF) on #266489 fill: contrast ratio = 4.89:1, passes WCAG AA for normal text at 14sp. The button height 56dp inherently provides the 48dp minimum touch target.

All bottom navigation tabs maintain 48dp minimum touch targets. The selected Accounts tab uses indicator colour `color/primaryContainer` (#C9E6FF) with icon and label in `color/primary` (#266489). Ensure the active indicator provides sufficient contrast against the #F7F9FF background.

Reduce-motion considerations: the circular progress indicator in the loading state should fall back to a static spinner arc (no rotation animation) when the device has "Reduce Motion" enabled. This is handled in Compose via `LocalAccessibilityManager.current.isAnimationEnabled`. In Figma, document this with an annotation layer on the loading frame.

---

## Notes for Design Handoff

The scheduled_payment_card height (~192dp) assumes single-line payee names. For longer payee names (over 24dp width in titleMedium), the card will grow vertically due to the Column `height = wrapContentHeight` layout. Design should accommodate up to two-line payee names — set maxLines 2 with ellipsis in the Compose implementation. In Figma, set the sp_payee_name text element to auto-height with a maximum of 2 lines.

The list contains up to N payment cards determined by the OBIE API response. The demo shows 4 items. When more than 3 cards are present, the list becomes scrollable. In Figma Prototype, add a vertical scroll behaviour on the SP / Content frame's list area.

The sp_type_chip chip variant (Execution vs Arrival) is the primary semantic differentiator for payment type. The icon choice (calendar_today vs arrow_downward) reinforces the directional semantics: calendar_today for a scheduled outgoing execution on a date, arrow_downward for a scheduled inward arrival. Ensure these icons are visible at 18dp at the M3 chip scale and annotate minimum icon size in the component documentation.

The Roboto Mono typeface requirement for sp_amount and sp_account_id is specified in design-tokens.yaml (`typography.font_family.mono = "Roboto Mono"`). Ensure "Roboto Mono" is installed in the Figma file team library — it is a Google Font available at fonts.google.com/specimen/Roboto+Mono. The monospaced rendering ensures "08-32-00 12001039" aligns predictably regardless of sort code character variation.
