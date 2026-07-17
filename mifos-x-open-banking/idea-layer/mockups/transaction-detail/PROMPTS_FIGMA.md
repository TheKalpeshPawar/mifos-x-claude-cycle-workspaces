# Transaction Detail — Figma Design Prompts

> Generated from `screens/transaction-detail/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5 — Android reference frame)
> Design system: Open Banking — Trust Blue (seed #266489, Material Design 3, Roboto)
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

### Resolved Colour Palette

The Open Banking — Trust Blue design system is built on Material Design 3's tonal colour roles seeded from #266489. Below are the role values for the M3 light theme that this screen uses.

Primary is the trust-blue used for interactive elements, credit amounts, and key tonal surfaces. Error red is reserved exclusively for debit amounts and error-state icons. Surface and background share the same off-white (#F7F9FF), giving the screen a clean, airy feel appropriate for regulated financial data. Tonal container colours (primaryContainer, secondaryContainer) are used for status chips. All text colour assignments meet WCAG AA (4.5:1 minimum for body text against their respective backgrounds).

- `primary` (#266489) — Trust Blue: credit amount text, interactive tints, back arrow, copy icon, chip borders, outlined button borders
- `onPrimary` (#FFFFFF) — text on primary-coloured filled button backgrounds
- `primaryContainer` (#C9E6FF) — Booked status chip background
- `onPrimaryContainer` (#004B6F) — Booked status chip label text
- `secondaryContainer` (#D3E5F5) — Pending status chip background
- `onSecondaryContainer` (#384956) — Pending status chip label text
- `error` (#BA1A1A) — debit amount text, error-state icon tint
- `onError` (#FFFFFF) — text on error-coloured surfaces (not used on this screen)
- `background` (#F7F9FF) — full-screen background
- `surface` (#F7F9FF) — same as background; top app bar surface
- `onSurface` (#181C20) — high-emphasis body text; list item secondary lines; amounts
- `onSurfaceVariant` (#41474D) — medium-emphasis text; card section header; list item primary labels; currency meta; empty/error body
- `surfaceContainerLow` (#F1F4F9) — detail card fill (elevation 1)
- `outlineVariant` (#C1C7CE) — divider colour within the detail card and header separator
- `outline` (#72787E) — inactive icon tint, outlined button border at rest (use `primary` for this screen's buttons)

### Semantic Token to Figma Variable Mapping

Create a Figma Variable collection named `Open Banking / Light` with these bindings:

| Semantic token | Figma variable path | Resolved hex |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `secondaryContainer` | `color/secondary-container` | #D3E5F5 |
| `onSecondaryContainer` | `color/on-secondary-container` | #384956 |
| `error` | `color/error` | #BA1A1A |
| `background` | `color/background` | #F7F9FF |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/on-surface` | #181C20 |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `outlineVariant` | `color/outline-variant` | #C1C7CE |
| `outline` | `color/outline` | #72787E |

### Typography Scale

All text uses Roboto. Amounts use Roboto Mono for monospaced digit alignment. Set up these text styles in Figma under a `Type /` collection:

- `Type / Display Small` — Roboto, Regular (400), 36sp, line height 44sp — used for the amount header
- `Type / Headline Medium` — Roboto, Regular (400), 28sp, line height 36sp — used for merchant name
- `Type / Title Large` — Roboto, Regular (400), 22sp, line height 28sp — top app bar title
- `Type / Title Small` — Roboto, Medium (500), 14sp, line height 20sp — card section header
- `Type / Label Large` — Roboto, Medium (500), 14sp, line height 20sp — chip labels, button labels
- `Type / Label Medium` — Roboto, Medium (500), 12sp, line height 16sp — currency sub-label
- `Type / Body Medium` — Roboto, Regular (400), 14sp, line height 20sp — list item content rows
- `Type / Body Small` — Roboto, Regular (400), 12sp, line height 16sp — supplementary captions (not primary on this screen)

### Spacing & Shape Tokens

Figma spacing tokens in the `Spacing /` collection:
- `Spacing / screen-padding` = 16dp (horizontal gutter for all content)
- `Spacing / card-internal-padding` = 16dp (inside detail_card)
- `Spacing / section-gap` = 12dp (between major sections)

Corner radius tokens in the `Radius /` collection:
- `Radius / medium` = 12dp — used for detail_card
- `Radius / full` = 9999dp — used for chips and buttons (renders as pill/stadium)
- `Radius / extra-small` = 4dp — not used on this screen

---

## Frame Specifications

### Frame: Transaction Detail — Loading

Create a frame named `Transaction Detail / Loading` at 393×852dp. Set the background fill to `color/surface` (#F7F9FF).

Place a Top App Bar component at the top of the frame. The app bar is 393dp wide and 56dp tall. Its background fill is `color/surface` (#F7F9FF). Apply a subtle bottom border of 1dp in `color/outline-variant` (#C1C7CE) to visually separate it from the body. Inside the app bar, place an icon button on the left: use the `arrow_back` Material icon at 24dp, centred in a 48dp touch target, tinted `color/primary` (#266489). The title "Transaction Detail" sits in the centre of the app bar using `Type / Title Large` (22sp Roboto Regular) coloured `color/on-surface` (#181C20).

The body area below the top app bar is 393×796dp. Set its background to `color/surface` (#F7F9FF). Place a single circular progress indicator (M3 CircularProgressIndicator) at the absolute centre of the body frame — horizontally at 196.5dp, vertically at 398dp from the top of the body. The indicator is 48×48dp and its track tint is `color/primary` (#266489). The indeterminate spinning animation runs at the standard M3 rhythm (300ms per quarter arc). In Figma, use a circle with a 4dp stroke, colour #266489, with a dashed stroke dash-gap pattern simulating the arc, or use the M3 component library's progress indicator if available.

Auto Layout for the loading frame body: set to Vertical, align items Centre, justify content Centre, no padding offset from the app bar boundary.

#### Component Variants — Loading State

The progress indicator has only one visual state in this context: indeterminate spinning. No stopped or complete variant is shown here. In Figma, create a component named `Progress Indicator / Circular / Indeterminate` with the single state.

#### Accessibility — Loading

Include a non-visible annotation layer with the text `contentDescription: "{strings.transaction_detail_loading}"`. In the Figma handoff panel, annotate the indicator with min-touch-target: not applicable (non-interactive). Ensure the body background colour meets contrast requirements for the indicator track.

---

### Frame: Transaction Detail — Content (Debit · Tesco Stores · Booked)

Create a frame named `Transaction Detail / Content – Debit` at 393×852dp with a vertical scrolling Auto Layout (overflow: scroll). Background fill: `color/surface` (#F7F9FF).

#### Top App Bar

Place the same Top App Bar component from the Loading frame at the top (393×56dp, bg #F7F9FF, leading back arrow `color/primary`, title "Transaction Detail" `Type / Title Large` #181C20). This component is fixed/sticky at the top — it does not scroll with the content.

#### Amount Header Area

Directly below the top app bar, add a vertical Auto Layout container 393dp wide with horizontal padding 16dp on each side, top padding 24dp. This container holds three elements stacked vertically, all horizontally centred.

First, place the amount text "-£42.17" using `Type / Display Small` (36sp Roboto Regular, or Roboto Mono for numeric alignment) coloured `color/error` (#BA1A1A). This large debit amount is immediately visible as a negative figure in red. The negative sign is derived at runtime from `CreditDebitIndicator = "Debit"`. Set horizontal alignment to Centre.

Directly below the amount (8dp gap), place the currency label "GBP" using `Type / Label Medium` (12sp Roboto Medium) coloured `color/on-surface-variant` (#41474D). This confirms the ISO 4217 currency code beneath the main amount. Centre-aligned. Min touch target: none required (non-interactive).

Add 16dp vertical spacing below the currency label.

For the credit variant (`Transaction Detail / Content – Credit`), change the amount to "+£2400.00" and set the text colour to `color/primary` (#266489). All other elements remain identical except the MCC row, which is hidden (see below).

#### Amount Header Auto Layout

Set this container to Vertical Auto Layout, alignment: Centre / Centre, padding: top 24dp left 16dp right 16dp bottom 0dp, gap between items 8dp (between amount and currency), then a manual 16dp spacer.

#### Merchant and Status Area

Below the amount container, add a 393dp-wide vertical Auto Layout section with 16dp horizontal padding, 0dp top padding (continuing immediately below the spacer from the amount area).

Place the merchant name "Tesco Stores" using `Type / Headline Medium` (28sp Roboto Regular) coloured `color/on-surface` (#181C20). Left-aligned. This value comes from `OBTransaction6.MerchantDetails.MerchantName`. When MerchantDetails is absent (e.g. salary credits), the ViewModel substitutes `TransactionInformation` as the display text — in that scenario the same text style applies.

Add 8dp vertical spacing, then place the status chip. Create an M3 Assist Chip component 32dp tall with auto width (min 84dp). Set the chip background fill to `color/primary-container` (#C9E6FF) for the "Booked" status. The chip label "Booked" uses `Type / Label Large` (14sp Roboto Medium) coloured `color/on-primary-container` (#004B6F). Apply a corner radius of 99dp (full pill shape). Internal horizontal padding is 12dp on each side, vertical padding 6dp. There is no leading icon on this chip.

For the Pending variant, swap the chip background to `color/secondary-container` (#D3E5F5) and the label colour to `color/on-secondary-container` (#384956), and change the label text to "Pending".

#### Header Separator

Add 12dp vertical spacing below the status chip, then place a horizontal Divider line spanning the full 393dp width. The line is 1dp tall, coloured `color/outline-variant` (#C1C7CE). Add 12dp vertical spacing below the divider.

#### Detail Card

Create a Card component named `Transaction Detail Card` at 361dp wide (full width minus 16dp each side screen_padding). The card has:
- Fill: `color/surface-container-low` (#F1F4F9)
- Corner radius: 12dp on all corners
- No explicit border (the tonal fill provides elevation separation against the #F7F9FF page background)
- Shadow: elevation 1dp, colour rgba(0,0,0,0.08) — Material 3 tonal elevation tint is already baked into the fill colour choice

Set the card's internal Auto Layout to Vertical, padding 16dp on all sides, gap 0dp (dividers provide spacing between rows).

Inside the card, begin with the section header label "TRANSACTION DETAILS" using `Type / Title Small` (14sp Roboto Medium) coloured `color/on-surface-variant` (#41474D). Left-aligned. Add 12dp vertical spacing below this header.

Now add seven list item rows separated by hairline dividers. Each row is a horizontal Auto Layout item 329dp wide (the card's inner content width). Two-line rows are 72dp tall; the single-line balance row is 56dp tall.

**Booking date row** (two-line, 72dp): The primary label "Booking date" uses `Type / Body Medium` (14sp Roboto Regular) coloured `color/on-surface-variant` (#41474D). Below it, the supporting text "2026-06-26T11:22:00Z" uses `Type / Body Medium` coloured `color/on-surface` (#181C20). Both lines are left-aligned.

Insert a Divider (329dp wide, 1dp tall, `color/outline-variant` #C1C7CE) between each row.

**Value date row** (two-line, 72dp): Primary label "Value date" (#41474D), supporting text "2026-06-26T11:22:00Z" (#181C20). Identical structure to booking date row.

**Category row** (two-line, 72dp): Primary label "Category" (#41474D), supporting text "Groceries" (#181C20). This value is client-derived from the MCC lookup (MCC 5411 → Groceries).

**Merchant code (MCC) row** (two-line, 72dp, **conditional**): Primary label "Merchant code (MCC)" (#41474D), supporting text "5411" (#181C20). This row is only visible when `MerchantDetails.MerchantCategoryCode` is non-null. In Figma, create a component property `mcc_visible: Boolean` on the detail card component. When false, collapse the row height to 0dp and hide the preceding divider. For the Tesco Stores fixture this row is visible (MCC 5411). For ACME LTD salary credit it is hidden.

**Balance after row** (single-line, 56dp): This row has a different layout — it is a horizontal spacer-between arrangement. On the left: "Balance after" in `Type / Body Medium` #41474D. On the right: "£447.63" in `Type / Body Medium` #181C20. The sign is derived from `Balance.CreditDebitIndicator = "Credit"`, so no minus sign appears. Use Auto Layout with Horizontal direction, Space Between distribution, items centred vertically.

**Reference row** (two-line, 72dp, interactive): The primary label "Reference" is #41474D. The supporting text "TESCO STORES 3476 LONDON" is #181C20. On the right, place a trailing icon button using the `content_copy` Material icon at 24dp, tinted `color/primary` (#266489), in a 48dp touch target. The entire row is tappable — set the row frame's `clip content` off and apply a ripple fill on press state. Annotate in the prototype panel: `On Tap → Copy to Clipboard (CopyTransactionReference action)`.

**Bank code row** (two-line, 72dp): Primary label "Bank code" (#41474D), supporting text "DR · HSBC" (#181C20). The `·` separator is a Unicode middle dot U+00B7.

#### Detail Card Auto Layout Summary

Vertical, fill width 361dp, padding 16dp, gap 0dp (items touch each other; dividers provide visual rhythm). Total card height approximation: 28dp (header + spacer) + 6 × 72dp (two-line rows) + 1 × 56dp (balance row) + 7 × 1dp (dividers) = 28 + 432 + 56 + 7 = **523dp**. The card is taller than the remaining body viewport (796 − 56 top bar − ~200dp header area ≈ 540dp), so the screen scrolls vertically.

#### Component Variants — Content

Create these component variants for the detail card list items:

- `List Item / Two Line / Default` — label (#41474D) + supporting text (#181C20), no trailing element
- `List Item / Two Line / With Copy` — same as above plus trailing `content_copy` icon (#266489)
- `List Item / One Line / With Trailing Text` — single label (#41474D) left, value (#181C20) right
- `List Item / Two Line / Hidden` — height 0dp, used for conditionally hidden mcc_row

For the amount_header text, create:
- `Amount / Debit` — "-£42.17" Roboto Mono Display Small #BA1A1A
- `Amount / Credit` — "+£2400.00" Roboto Mono Display Small #266489

For the status_badge chip:
- `Status Chip / Booked` — bg #C9E6FF, text #004B6F, "Booked"
- `Status Chip / Pending` — bg #D3E5F5, text #384956, "Pending"

#### Accessibility — Content

Every interactive element must meet a 48dp minimum touch target. The reference row is the key interactive element on this state — the entire 329dp-wide row within the card is tappable, not just the 24dp icon. Set `contentDescription` on the trailing icon to `"{strings.transaction_detail_copy_reference_a11y}"`. The amount_header includes an accessibility label `"{strings.transaction_detail_amount_a11y_prefix}: 42.17 GBP"` (screen readers should not read the colour-coded sign character). Verify colour contrast:

- Amount debit #BA1A1A on #F7F9FF: contrast ratio 4.65:1 — passes WCAG AA for large text (≥3:1)
- Primary #266489 on #F7F9FF: 4.6:1 — passes WCAG AA
- onSurface #181C20 on #F1F4F9 (card): exceeds 12:1 — passes AAA
- onSurfaceVariant #41474D on #F1F4F9: ~7:1 — passes AA

---

### Frame: Transaction Detail — Error (Recoverable)

Create a frame named `Transaction Detail / Error – Recoverable` at 393×852dp. Background: `color/surface` (#F7F9FF).

Place the identical Top App Bar at the top (back arrow + title "Transaction Detail"). The back arrow navigates to the transactions list even from the error state — this is the primary escape route.

The body area (796dp) uses a centred vertical column arrangement. Centre the error illustration content both horizontally and vertically within the 796dp body.

Begin with a Material icon `error_outline` at 48×48dp, tinted `color/error` (#BA1A1A). Centre this icon horizontally on the frame. The icon carries no interactive behaviour — it is purely illustrative. Set `contentDescription = null` (the title text below conveys the semantic meaning).

Below the icon (16dp gap), place the error title text using `Type / Headline Medium` (28sp Roboto Regular) coloured `color/on-surface` (#181C20). The i18n string key is `transaction_detail_error_title` — use the placeholder value "Transaction unavailable" for design purposes. Centre-align this text within 329dp (screen width minus 32dp horizontal padding).

Below the title (8dp gap), place the error body text using `Type / Body Medium` (14sp Roboto Regular) coloured `color/on-surface-variant` (#41474D). For the recoverable variant (TokenExpiredError, HTTP 401) the message reads "Session expired. Please log in again." For the network error variant (NetworkError) it reads "No network connection. Please check your connection and retry." Centre-align. Max width 329dp.

Below the body text (24dp gap), place the retry button. This is a filled M3 Button component 329dp wide, 40dp tall, with corner radius 99dp (stadium shape). Fill: `color/primary` (#266489). Label: "Try again" using `Type / Label Large` (14sp Roboto Medium) coloured `color/on-primary` (#FFFFFF). The button has a pressed state that darkens the fill with the M3 state layer (8% black overlay on primary).

The retry button is **only shown when `error.recoverable = true`**. Create a component property `recoverable: Boolean` on the error state component. When false, hide the retry button (do not replace it yet — the next frame handles the non-recoverable case).

#### Component Variants — Error Recoverable

- `Error State / Recoverable / Rest` — icon + title + body + filled Retry button at rest
- `Error State / Recoverable / Retry Pressed` — same, with filled button in pressed state (8% state layer)
- `Error State / Recoverable / Retry Loading` — same, with button showing a circular progress indicator (18dp) replacing the label during the API re-fetch

---

### Frame: Transaction Detail — Error (Non-Recoverable)

Create a frame named `Transaction Detail / Error – Non-Recoverable` at 393×852dp. Background: `color/surface` (#F7F9FF).

Use the same top app bar and the same icon, title, and body text pattern as the recoverable variant. For the non-recoverable sub-case:

- For ConsentWithdrawnError (HTTP 403), the body text reads "Access to transactions has been withdrawn."
- For TransactionNotFoundError (client filter returned zero), the ViewModel routes to the **Empty** state instead (see the Empty frame below). The error frame should not document this case.

Below the body text (24dp gap), place a single outlined M3 Button 329dp wide, 40dp tall, corner radius 99dp. The border is 1dp `color/primary` (#266489). The label "Go back" uses `Type / Label Large` (14sp Roboto Medium) coloured `color/primary` (#266489). Background fill: transparent. On press, apply an 8% `color/primary` state layer over the transparent background.

There is no retry button in this frame. The user's only available action is to return to the transactions list.

#### Component Variants — Error Non-Recoverable

- `Error State / Non-Recoverable / Rest` — icon + title + body + outlined Go Back button at rest
- `Error State / Non-Recoverable / Go Back Pressed` — same, with outlined button in pressed state
- `Error State / Non-Recoverable / Go Back Focused` — same, with a 3dp primary-coloured focus ring around the button outline

---

### Frame: Transaction Detail — Empty

Create a frame named `Transaction Detail / Empty` at 393×852dp. Background: `color/surface` (#F7F9FF).

Place the standard top app bar. The back arrow in the app bar is always operational.

The body is a centred vertical column. This state differs from the error state in two important ways: (1) the icon is `receipt_long` (not `error_outline`), signalling a neutral informational absence rather than a failure; (2) the icon colour is `color/on-surface-variant` (#41474D) rather than error red.

Place the `receipt_long` Material icon at 48×48dp, tinted #41474D, horizontally centred. Below (16dp gap), place the title text using `Type / Headline Medium` (28sp #181C20). The design placeholder reads "Transaction not found". Below the title (8dp gap), the body text in `Type / Body Medium` (14sp #41474D) reads: "This transaction is no longer available. It may have been removed or your consent scope has changed." This is a multi-line label; set it to auto-height, centre-aligned, max width 329dp.

Below the body text (24dp gap), place an outlined Go Back button identical to the one in the non-recoverable error frame: 329dp wide, 40dp tall, border 1dp #266489, label "Go back" 14sp Roboto Medium #266489, corner radius 99dp. No retry button. This is the only user action available — the transaction simply is not in the API result set.

#### Component Variants — Empty

- `Empty State / Transaction / Rest` — icon + title + body + outlined Go Back at rest
- `Empty State / Transaction / Go Back Pressed` — outlined button in pressed state
- `Empty State / Transaction / Go Back Focused` — button with 3dp focus ring

---

## Prototype Interaction Flow

Wire these interactions in the Figma prototype panel to simulate the complete Transaction Detail journey.

From the `Transaction Detail / Loading` frame, use "After delay (1500ms)" to transition to `Transaction Detail / Content – Debit`. Use a vertical slide-up transition (Ease In-Out, 300ms) consistent with M3 shared-axis navigation.

From the `Transaction Detail / Content – Debit` frame:
- Tap the **back arrow** in the top app bar → navigate to the Transactions List screen (push-pop navigate animation: slide right). Action contract: `effect: navigate, target: transactions`.
- Tap the **reference_row** (or its trailing copy icon) → trigger an overlay snackbar `Transaction reference copied` appearing at the bottom of the current frame. The snackbar uses surface inverse colours: bg `color/inverse-surface` (#2D3135), text `color/inverse-on-surface` (#EEF1F6), auto-dismiss after 4000ms. Action contract: `effect: copy_clipboard`.

From the `Transaction Detail / Error – Recoverable` frame:
- Tap **Try again** → briefly show a button loading state (progress indicator in button), then transition back to `Transaction Detail / Loading` using Instant transition (simulates the VM emitting Loading state before the API re-fetches). Action contract: `effect: call_api`.
- Tap **back arrow** → navigate to Transactions List. Action contract: `effect: navigate`.

From the `Transaction Detail / Error – Non-Recoverable` frame:
- Tap **Go back** → navigate to Transactions List. Action contract: `effect: navigate`.
- Tap **back arrow** → same.

From the `Transaction Detail / Empty` frame:
- Tap **Go back** → navigate to Transactions List. Action contract: `effect: navigate`.
- Tap **back arrow** → same.

All navigate-to-transactions transitions should use the M3 shared-axis pop animation: the current screen slides down-right and the transactions list slides in from the left, with 300ms Ease In-Out easing. This mirrors the Android NavController `popBackStack()` behaviour.

---

## Auto Layout Reference Summary

The following table captures the Auto Layout specification for each major container in this screen, suitable for direct handoff to a Figma designer or for use with Figma's AI design generation.

| Container | Direction | Padding (T R B L) | Gap | H-align | V-align | Sizing |
|---|---|---|---|---|---|---|
| `frame_root` (screen) | Vertical | 0 0 0 0 | 0 | Fill | Fill | 393 × 852 fixed |
| `top_app_bar` | Horizontal | 0 0 0 0 | auto | Space Between | Centre | Fill × 56 fixed |
| `body_scroll` (loading) | Vertical | 0 0 0 0 | 0 | Fill | Centre | Fill × Fill |
| `body_scroll` (content) | Vertical | 24 16 32 16 | 0 | Fill | Top | Fill × Fill scroll |
| `amount_section` | Vertical | 0 0 16 0 | 8 | Centre | Top | Fill × Hug |
| `merchant_section` | Vertical | 0 0 0 0 | 8 | Left | Top | Fill × Hug |
| `detail_card` | Vertical | 16 16 16 16 | 0 | Fill | Top | 361 × Hug |
| `list_item_two_line` | Vertical | 12 0 12 0 | 4 | Fill | Top | Fill × 72 fixed |
| `list_item_one_line_trailing` | Horizontal | 0 0 0 0 | auto | Space Between | Centre | Fill × 56 fixed |
| `reference_row` | Vertical | 12 0 12 0 | 4 | Fill | Top | Fill × 72 fixed |
| `body_centred` (error / empty) | Vertical | 48 24 48 24 | 16 | Centre | Centre | Fill × Fill |
| `button_area` | Vertical | 24 0 0 0 | 12 | Fill | Top | Fill × Hug |

---

## Additional Design Notes

### Credit vs Debit Amount Colour

The amount header is the single most visually important element on this screen. It must immediately communicate whether money entered or left the account. Use `color/error` (#BA1A1A) exclusively for debit amounts and `color/primary` (#266489) exclusively for credit amounts. Do not use green — the design system seed does not include a distinct green role, and using an out-of-system green would introduce an inconsistency. The Trust Blue primary tonal palette is used for credits, as inflows are the "positive" outcome in an Open Banking context.

### Roboto Mono for Amounts

The amount_header component uses Roboto Mono (the monospaced variant in the typography token `font_family.mono`) to ensure consistent digit width alignment across reload and state transitions. This prevents the layout from jumping as the number of digits changes (e.g. £6.45 vs £2400.00). All other text on this screen uses Roboto (proportional).

### MCC Row Conditional Visibility

The Merchant code (MCC) row collapses entirely when `MerchantDetails.MerchantCategoryCode` is null. This occurs for direct credits (salary transfers, bank-to-bank), ATM withdrawals, and some standing-order entries. When collapsed, the preceding divider is also hidden to avoid a double-divider gap between the Category row and the Balance after row. In Figma, manage this with a Boolean component property `showMcc` on the detail card component.

### Snackbar for Copy Confirmation

After the user taps the reference row copy icon, a one-shot snackbar appears at the bottom of the screen confirming the clipboard write. Design the snackbar as a separate overlay component positioned at the bottom of the screen with 16dp horizontal and bottom margin. Use inverse surface colours: bg #2D3135, text #EEF1F6, corner radius 4dp, elevation 6dp. The snackbar label is "Transaction reference copied". It appears with a 150ms fade-in and auto-dismisses after 4000ms. There is no action button on this snackbar.

### Scrolling Behaviour

The content state is intentionally tall (the detail card alone is approximately 523dp, and the header above it adds another 180–200dp). Total scrollable content height is approximately 720–730dp, which exceeds the 796dp body viewport only marginally. On most devices the last two rows of the card (reference and bank code) will require a small scroll. Ensure the card has sufficient bottom padding (16dp inside card + 32dp below card) so the bottom content is not clipped by the system navigation bar. Use `WindowInsets.navigationBars` padding on Android.

### Empty vs Error Distinction

The empty state (`receipt_long` icon, neutral #41474D) and error state (`error_outline` icon, error #BA1A1A) are deliberately distinguished. The error state communicates a system failure and offers either retry or navigation. The empty state communicates a data gap — the fetch worked but returned nothing matching the requested transactionId. The icon and colour choice on the empty state deliberately avoids alarm: the PSU should simply navigate back to the transactions list, which may show the transaction if the list is refreshed.

### Status Chip Sizing

M3 Assist Chips are 32dp tall with a minimum 84dp wide. Do not use the same chip size as Input or Filter chips on this screen — those are 32dp but differ in leading-icon semantics. The status chip here has no leading icon and no trailing icon. It is purely informational (non-interactive). To signal non-interactivity, do not apply a ripple to the chip on this screen — leave it as a static tonal container.

### Focus and Keyboard Navigation

For desktop/web targets (where this screen may be rendered via a Compose for Web target), ensure the interactive elements respect focus order: back arrow → reference row copy icon → (retry or go back button in error state). The detail card list items that are non-interactive should not receive keyboard focus. Only the reference_row has an interactive action (copy_to_clipboard) and therefore requires a visible 3dp focus ring in `color/primary` (#266489) when focused.

---

## Fixture-Specific Prompt Variants

These prompts cover the three primary demo-data fixtures from `demo-data.yaml`, each of which exercises a distinct visual path through the content state.

### Fixture A — Tesco Stores · Debit · Booked · MCC 5411

Create a Figma frame for the primary debit experience. The screen opens on a top app bar labelled "Transaction Detail" with a left-pointing back arrow. Below, centred in the header region, the amount "-£42.17" appears in Roboto Mono Display Small at 36sp coloured #BA1A1A (M3 error). Immediately beneath it, "GBP" appears in Roboto Medium 12sp at #41474D. Left-aligned below the amount section, the merchant name "Tesco Stores" renders in Roboto Regular 28sp at #181C20. Adjacent to the merchant name row, place an Assist Chip reading "Booked" in Roboto Medium 14sp at #004B6F over a #C9E6FF background with full pill corners.

A horizontal divider in #C1C7CE separates the header from the detail card. The card fills the remaining screen width (361dp), has a #F1F4F9 background, 12dp corner radius, and 16dp internal padding. Inside, eight rows of data are separated by #C1C7CE hairline dividers:

Booking date / 2026-06-26T11:22:00Z — Value date / 2026-06-26T11:22:00Z — Category / Groceries — Merchant code (MCC) / 5411 (visible for this fixture) — Balance after / £447.63 (right-aligned trailing) — Reference / TESCO STORES 3476 LONDON (with a `content_copy` icon at trailing right, tinted #266489) — Bank code / DR · HSBC.

All row labels use Roboto Regular 14sp #41474D. All row values use Roboto Regular 14sp #181C20. The balance trailing text and bank code use the same body medium style. Add 32dp of breathing space below the card before the bottom of the scrollable content.

### Fixture B — ACME LTD · Credit · Booked · MCC null

Create a second content-state frame for the salary credit experience. The amount "+£2400.00" is displayed in Roboto Mono Display Small at #266489 (M3 primary / trust blue), communicating an inflow. The merchant name reads "ACME LTD" at headlineMedium #181C20. The status chip retains the Booked style: #C9E6FF background, #004B6F text.

In the detail card, note that the Merchant code (MCC) row is entirely absent because `MerchantCategoryCode` is null for this salary credit. The divider that would have preceded the MCC row is also hidden. The Category row reads "Salary". The Reference row shows "SALARY JUN ACME LTD" as the supporting text, copyable via the trailing icon. The Balance after row shows "£2847.63" (no minus sign — `Balance.CreditDebitIndicator = "Credit"`). Bank code shows "CR · HSBC".

This frame demonstrates the MCC-row hidden variant. Set the detail card component property `showMcc = false` to collapse that row gracefully.

### Fixture C — Pret A Manger · Debit · Pending · MCC 5812

Create a third content-state frame for the pending pre-authorisation scenario. The amount "-£6.45" is in Roboto Mono Display Small at #BA1A1A. The merchant name is "Pret A Manger". The status chip reads "Pending" using `color/secondary-container` (#D3E5F5) as the background and `color/on-secondary-container` (#384956) for the label text. This is the only visual difference in the chip between the Booked and Pending states — the size and shape are identical.

In the detail card, note that the Booking date and Value date rows show different timestamps: "2026-06-29T09:15:00Z" (booking) versus "2026-06-30T00:00:00Z" (value date). This difference is intentional and important for pending transactions — the settlement date has not yet been reached. The Category row reads "Food & Drink". MCC is visible (5812 — Eating Places, Restaurants). Balance after shows "£441.18". Bank code shows "DR · HSBC". Reference shows "PRET A MANGER LONDON".

This frame serves as the Pending chip variant showcase. Create a shared component for the detail card, parameterised by booking_date, value_date, category, amount, amount_colour, status_chip_variant, mcc_visible, mcc_value, balance, reference, bank_code.

---

## Handoff Annotation Checklist

Use the following checklist when creating Figma handoff annotations (using Figma's Dev Mode or the Zeplin-style inspect panel) to ensure the engineering team receives complete specifications.

For every interactive element on this screen, annotate the action and its target component or system effect. The back arrow should be annotated as "NavigateBack → Transactions list (pop back stack)". The reference row copy icon should be annotated as "CopyTransactionReference(reference: String) → ClipboardService → Snackbar confirmation". The retry button in the error state should be annotated as "RetryLoad() → GET /accounts/{accountId}/transactions via ktorfit". The go back button in both non-recoverable error and empty states should be annotated identically to the back arrow.

For every text element that is i18n-driven, annotate the string key. Amount header: not i18n (dynamic numeric value). Currency meta: not i18n (ISO 4217 code). Merchant name: not i18n (API data). Status badge label: not i18n (OBIE enum value — "Booked" or "Pending"). Card section header: i18n key `transaction_detail_card_title`. Each list item label uses a corresponding `transaction_detail_*` namespace key (e.g. `transaction_detail_booking_date`, `transaction_detail_value_date`, `transaction_detail_category`, `transaction_detail_mcc`, `transaction_detail_balance_after`, `transaction_detail_reference`, `transaction_detail_bank_code`). Error state title: `transaction_detail_error_title`. Empty state title: `transaction_detail_empty_title`. Empty state body: `transaction_detail_empty_body`.

For every colour usage, annotate the semantic token name (not the raw hex) so that dark-mode variant generation is straightforward: "#BA1A1A" should be annotated as `color/error`, "#266489" as `color/primary`, "#41474D" as `color/on-surface-variant`, "#181C20" as `color/on-surface`, and so on. This enables the design system team to generate a validated dark-mode companion set by simply swapping the light token set for the dark token set (see `design-tokens.yaml` dark block for all resolved dark values).

For elevation, annotate the detail_card as `elevation: 1 (tonal)` — in Material 3, tonal elevation blends the primary colour at 5% opacity into the surface container, producing the #F1F4F9 fill at elevation 1. Do not annotate this as a drop shadow; it is a tonal fill shift, not a cast shadow.

For minimum touch targets, annotate: back_button icon_button as `min touch target: 48×48dp`, reference_row copy icon trailing area as `min touch target: 48×48dp (trailing region)`, full reference_row as `interactive: true, entire row tappable (329×72dp)`, retry_button as `min touch target: 40dp height (conforms — button is 329dp wide, exceeds 48dp criterion by width)`, go_back_button same, transaction_empty_back_button same.

For motion, annotate: content state entry → `shared-axis-Y slide-up 300ms Ease In-Out` (M3 NavHost forward navigation). Error→Loading transition (on retry) → `crossfade 150ms`. Snackbar entry → `slide-up 150ms`, exit → `fade 150ms after 4000ms hold`.
