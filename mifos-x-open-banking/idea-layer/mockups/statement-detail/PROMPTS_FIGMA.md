# Statement Detail — Figma Design Prompts

> Generated from `screens/statement-detail/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Trust Blue seed #266489 · Roboto
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

This screen is part of the Open Banking — Trust Blue design system derived from Material 3 with
seed colour #266489. All colour values below are resolved from the M3 light-mode role set produced
by Material Theme Builder.

### Resolved Colour Palette

- **primary**: #266489 — Trust Blue; used for interactive icons, outlined borders, tonal fills
- **onPrimary**: #FFFFFF — text/icon on primary fills
- **primaryContainer**: #C9E6FF — light trust-blue container (hero cards elsewhere in the app)
- **onPrimaryContainer**: #004B6F — text on primaryContainer
- **secondary**: #50606E — muted slate; statement reference overline, secondary labels
- **onSecondary**: #FFFFFF
- **tertiary**: #64597B — muted purple; credit/positive amount colour role
- **error**: #BA1A1A — debit/negative amount colour role; error icon/title colour
- **background**: #F7F9FF — screen background
- **surface**: #F7F9FF — card surface (combined with tonal elevation)
- **surfaceContainer**: #EBEEF3 — card at elevation 2 (3dp tonal overlay)
- **surfaceContainerLow**: #F1F4F9 — card at elevation 1
- **onSurface**: #181C20 — primary text colour
- **onSurfaceVariant**: #41474D — secondary/supporting text, icons, date labels
- **outlineVariant**: #C1C7CE — list dividers
- **outline**: #72787E — outlined button border at rest
- **inverseSurface**: #2D3135 — snackbar background
- **inverseOnSurface**: #EEF1F6 — snackbar text/icon

### Typography Scale (Roboto)

- **displaySmall**: 36sp / 44sp / w400
- **headlineSmall**: 24sp / 32sp / w400 — empty/error titles
- **titleLarge**: 22sp / 28sp / w400 — top app bar title
- **titleMedium**: 16sp / 24sp / w500 — statement period, balance amounts
- **titleSmall**: 14sp / 20sp / w500 — transaction amount trailing
- **bodyLarge**: 16sp / 24sp / w400
- **bodyMedium**: 14sp / 20sp / w400 — list item supporting text, fee/interest amounts
- **bodySmall**: 12sp / 16sp / w400 — statement type, created label
- **labelLarge**: 14sp / 20sp / w500
- **labelMedium**: 12sp / 16sp / w500 — section headers, statement reference overline
- **labelSmall**: 11sp / 16sp / w500 — transaction date overline, created label

### Spacing & Shape

- Screen horizontal padding: 16dp
- Base spacing unit: 4dp
- Corner radii: extra_small=4dp · small=8dp · medium=12dp · large=16dp · extra_large=28dp · full=9999dp
- Elevation shadows follow M3 tonal elevation (colour overlay, not drop shadow in light mode)
- Min touch target: 48dp × 48dp (WCAG AA compliance for a regulated-industry app)

---

## Semantic Token → Figma Variable Mapping

Create a Figma Variables collection named **Open Banking / Trust Blue** with these mappings.
Set mode to "Light" as the default.

| Semantic Token | Figma Variable Path | Resolved Hex (Light) |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `secondary` | `color/secondary` | #50606E |
| `tertiary` | `color/tertiary` | #64597B |
| `error` | `color/error` | #BA1A1A |
| `background` | `color/background` | #F7F9FF |
| `surface` | `color/surface` | #F7F9FF |
| `surfaceContainer` | `color/surface-container` | #EBEEF3 |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `onSurface` | `color/on-surface` | #181C20 |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `outlineVariant` | `color/outline-variant` | #C1C7CE |
| `outline` | `color/outline` | #72787E |
| `inverseSurface` | `color/inverse-surface` | #2D3135 |
| `inverseOnSurface` | `color/inverse-on-surface` | #EEF1F6 |

Create a second collection **Typography / Trust Blue** with text-style variables for each scale
role listed above, applying Roboto with the specified size/line-height/weight values.

---

## Frame 1 — State: loading

Create a frame named **StatementDetail / loading** sized 393×852. Set the frame fill to
`color/background` (#F7F9FF). Apply a vertical Auto Layout with no item spacing and no padding
on the frame itself; the top app bar and bottom navigation are fixed-position elements.

### Top App Bar

Place the top app bar as a fixed component at the top of the frame, 393dp wide by 56dp tall,
with a fill of `color/background` (#F7F9FF) and no elevation shadow. Inside, create a horizontal
Auto Layout. On the left, place a navigation icon button containing the `arrow_back` icon (24dp,
tint `color/on-surface-variant` #41474D) in a 48dp × 48dp hit area with 12dp internal padding.
To the right, place the title text "Statement Detail" using the titleLarge text style (22sp Roboto
Medium #181C20). This fallback title appears because no StatementReference is available while the
network request is in flight.

### Loading Indicator

In the remaining vertical space between the top app bar and the bottom navigation, create a frame
that fills all available width and height. Set its Auto Layout alignment to centred both
horizontally and vertically. Place a Figma `Progress Indicator` component (circular variant) with
a 40dp diameter and a stroke colour of `color/primary` (#266489) at the centre. Set stroke width
to 4dp. Label this layer `progress_indicator/circular`. In the prototype, set the rotation
animation to spin continuously when this frame is visible to communicate active loading.

Add an invisible accessibility label text layer "Loading statement" above the progress indicator
with a 1dp height and `color/background` fill, marked as hidden in exports.

### Bottom Navigation

Place the bottom navigation as a fixed component at the bottom of the frame, 393dp wide by 80dp
tall, with a fill of `color/background` (#F7F9FF). Use a horizontal Auto Layout with items
distributed evenly (space-between). Create four navigation destination items, each in a vertical
Auto Layout centred horizontally with 4dp gap between icon and label:

- **Home**: icon `home` 24dp, label "Home" in labelMedium, tint `color/on-surface-variant`
  (#41474D), unselected
- **Accounts**: icon `account_balance` 24dp, label "Accounts", tint #41474D, unselected
- **Transactions**: icon `receipt_long` 24dp, label "Transactions", tint `color/primary`
  (#266489), **selected** — apply a pill indicator 64dp × 32dp filled `color/secondary-container`
  (#D3E5F5) centred behind the icon to communicate the active destination
- **More**: icon `more_horiz` 24dp, label "More", tint #41474D, unselected

Each destination area is 48dp minimum touch target. Surround the icon with the pill indicator
only on the selected destination.

---

## Frame 2 — State: content

Create a frame named **StatementDetail / content** sized 393×852 with `color/background`
(#F7F9FF) fill. The screen is a scrollable single-column layout. Represent the full-page view in
Figma as a taller artboard (393×1600dp) to show all content, then link to the clipped 393×852
prototype frame for device previews.

### Top App Bar

Identical to the loading state top app bar. Change the title text to the real statement reference:
**"MAY-2026-STMT"** using titleLarge style (22sp #181C20). The leading back arrow navigates to
the `statements` screen.

### Statement Header Card

Immediately below the top app bar (8dp gap from bar bottom), place a Card component. The card
should be 361dp wide (393 − 2×16dp horizontal padding), with auto-height wrapping its content.
Set the card fill to `color/surface-container` (#EBEEF3), corner radius 12dp, and tonal elevation
equivalent to 3dp (no drop shadow in M3 light mode — colour overlay only).

Inside the card, create a vertical Auto Layout with 16dp padding on all four sides and 4dp item
spacing between child elements:

First, add an overline text layer **"MAY-2026-STMT"** using labelMedium style (12sp Roboto Medium,
`color/secondary` #50606E). This is the machine reference identifier for the statement.

Second, add a title text layer **"01 May 2026 – 31 May 2026"** using titleMedium style (16sp
Roboto Medium, `color/on-surface` #181C20). This is the human-readable statement period derived
from StartDateTime and EndDateTime formatted as "dd MMM yyyy – dd MMM yyyy".

Third, add a body text layer **"RegularPeriodic"** using bodySmall style (12sp Roboto Regular,
`color/on-surface-variant` #41474D). This reflects the OBStatement2 `Type` field.

Fourth, add a caption text layer **"Created 01 Jun 2026, 06:00"** using labelSmall style (11sp
Roboto Medium, `color/on-surface-variant` #41474D). This is the localised "Created" prefix
concatenated with the formatted `CreationDateTime`.

### Balances Section

Immediately below the header card (0dp gap — divider handles visual separation), place a section
header. Create a row 393dp wide, 48dp tall, with horizontal padding 16dp. Add the label text
**"Balances"** using labelMedium style (12sp Roboto Medium, `color/on-surface-variant` #41474D,
left-aligned).

Below the section header, create two list item rows, each 393dp wide and 56dp tall. Use a
horizontal Auto Layout with 16dp horizontal padding and content vertically centred (alignment:
center):

- **OpeningBalance row**: supporting text "OpeningBalance" in bodyMedium (14sp #181C20) on the
  left with flex weight 1. Trailing text "£2,610.40 GBP" in titleMedium (16sp Roboto Medium,
  `color/tertiary` #64597B) right-aligned. A 1dp divider line below using `color/outline-variant`
  (#C1C7CE) spans the full width.

- **ClosingBalance row**: supporting text "ClosingBalance" bodyMedium #181C20. Trailing text
  "£2,847.63 GBP" titleMedium #64597B. No divider below (fees section follows).

Both trailing amounts use `color/tertiary` (#64597B) because `CreditDebitIndicator` is "Credit"
for both balances in this demo scenario.

### Fees Section

Place a section header row identical in structure to the Balances header. Label: **"Fees"**,
labelMedium #41474D. This section is visible only when `StatementFee.length > 0`; in this demo
scenario it is visible because one fee entry exists.

Create one list item row 393dp wide, 56dp tall:

- Supporting text **"Monthly maintenance fee"** bodyMedium #181C20 flex weight 1.
- Trailing text **"£0.00 GBP"** bodyMedium #181C20. Note: because `CreditDebitIndicator` is
  "Debit" and the amount is zero, render neutral #181C20 rather than error red — the fee is
  included in the statement but has no cost to the customer.
- 1dp divider below.

Create a boolean component property `feesVisible` to toggle this entire section. When false, set
height to 0dp and clip. In prototype mode, show Fees section by default in this frame.

### Interest Section

Section header **"Interest"** labelMedium #41474D. Visible when `StatementInterest.length > 0`.

Create one list item row 393dp wide, 56dp tall:

- Supporting text **"In-credit interest"** bodyMedium #181C20.
- Trailing text **"£0.21 GBP"** bodyMedium `color/tertiary` (#64597B) — `CreditDebitIndicator`
  is "Credit" → use tertiary colour role.
- No divider below (transactions section follows).

### Transactions Section

Section header **"Transactions"** labelMedium #41474D, 48dp tall.

Below the section header, create six transaction list item rows. Each row is 393dp wide and 72dp
tall (3-line list item). Use a horizontal Auto Layout with 16dp horizontal padding, items aligned
to top. Each row is tappable; apply a hover/pressed state with a `color/on-surface` overlay at
8% opacity for the ripple surface.

**Row structure** (inner horizontal Auto Layout, gap 16dp, vertically centred):

On the left, create a vertical Auto Layout (flex weight 1, gap 4dp):
- Overline text: date formatted "dd MMM yyyy" in labelSmall (11sp Roboto Medium,
  `color/on-surface-variant` #41474D)
- Headline text: merchant/description in bodyMedium (14sp Roboto Regular, `color/on-surface`
  #181C20), maxLines 1 with ellipsis overflow

On the right (align end), place the amount in titleSmall (14sp Roboto Medium):
- Debit amounts (CreditDebitIndicator=Debit): prepend "−", colour `color/error` #BA1A1A
- Credit amounts (CreditDebitIndicator=Credit): prepend "+", colour `color/tertiary` #64597B

The six rows with real content from demo-data.yaml:

1. Date: "03 May 2026" · Description: "TESCO STORES 3225 LONDON" · Amount: "−£82.50 GBP"
   (#BA1A1A Debit) · `transactionId: TXN-2026-05-001`
2. Date: "10 May 2026" · Description: "BACS CREDIT ACME CORP PAYROLL" · Amount: "+£3,200.00 GBP"
   (#64597B Credit) · `transactionId: TXN-2026-05-002`
3. Date: "15 May 2026" · Description: "SO LANDLORD RENT MAY 2026" · Amount: "−£650.00 GBP"
   (#BA1A1A Debit) · `transactionId: TXN-2026-05-003`
4. Date: "22 May 2026" · Description: "BRITISH GAS ENERGY BILLS" · Amount: "−£230.48 GBP"
   (#BA1A1A Debit) · `transactionId: TXN-2026-05-004`
5. Date: "24 May 2026" · Description: "TFL TRAVEL LONDON" · Amount: "−£45.00 GBP"
   (#BA1A1A Debit) · `transactionId: TXN-2026-05-005`
6. Date: "28 May 2026" · Description: "NETFLIX.COM" · Amount: "−£12.99 GBP"
   (#BA1A1A Debit) · `transactionId: TXN-2026-05-006`

Place 1dp `color/outline-variant` (#C1C7CE) dividers between each row. The last row has no
bottom divider. Add 16dp spacing below the final transaction row before the download button.

### Download PDF Button

Create an Outlined Button component 361dp wide (full width minus 16dp padding each side), 48dp
tall. Use full-pill corner radius 9999dp. The border is 1dp solid `color/primary` (#266489). The
label text reads **"Download PDF"** in labelLarge (14sp Roboto Medium, `color/primary` #266489).
Prepend a `download` icon, 18dp, tint #266489, with 8dp gap between icon and label.

Create a boolean component property `downloadEnabled` (true by default). When false (while
DownloadState == Downloading), reduce the button opacity to 38% and set interactions as non-
responsive. Add a pressed state with the button background filled `color/primary` at 12% opacity.
Add a hovered state with 8% opacity overlay.

Place the download button below the last transaction row with 16dp top margin.

### Download Progress Indicator

Directly below the download button (8dp gap), place a Linear Progress Indicator 393dp wide and
4dp tall. Fill colour `color/primary` (#266489). This component is visible only when
`downloadState == Downloading`. Create a boolean component property `downloadInProgress: false`
to toggle visibility. In the default content frame, set this to false (hidden). Create a secondary
frame variant **StatementDetail / content / downloading** where this is set to true.

The indicator uses an indeterminate animation: a moving gradient segment sweeps from left to right
across the track (trackColor: `color/primary` at 38% opacity). Apply a 300ms loop animation with
the emphasis easing curve `cubic-bezier(0.2, 0.0, 0, 1.0)`.

### Download Result Snackbar

Below the download progress indicator, create a Snackbar component 361dp wide (393 − 32dp margin)
and 48dp tall. Corner radius 4dp. Background `color/inverse-surface` (#2D3135). Place text
**"PDF saved to device"** in bodyMedium (14sp Roboto Regular, `color/inverse-on-surface`
#EEF1F6). On the trailing edge, place a close icon button (`close` icon 18dp, tint #EEF1F6) in a
48dp touch target.

Create a component property `snackbarMessage` with two variants: "PDF saved to device" (success)
and "Download failed" (error). The snackbar is hidden by default in the content frame. It appears
for 4000ms after the download completes or fails, then auto-dismisses with a 150ms fade-out.

### Bottom Navigation

Identical to the loading state bottom navigation. Transactions tab remains selected (tint
`color/primary` #266489) since statement-detail is a deep-link from the statements flow which
originates in the Transactions tab path.

---

## Frame 3 — State: empty

Create a frame named **StatementDetail / empty** sized 393×852 with `color/background` fill.

### Top App Bar

Title text: **"MAY-2026-NEW"** (the statement reference for the empty-transactions scenario).
Same structure as content state.

### Statement Header Card (retained)

The statement header card is still visible in the empty state. The OBStatement2 object has been
loaded successfully; only `statementTransactions` returned an empty array. Use these values from
the empty-transactions demo scenario:

- Reference: "MAY-2026-NEW"
- Period: "01 May 2026 – 31 May 2026"
- Type: "RegularPeriodic"
- Created: "01 Jun 2026, 06:00"

Card appearance: identical to content state — `color/surface-container` (#EBEEF3), radius 12dp,
elevation 2.

### Balances Section (retained)

Show the Balances section header and two balance rows. In this empty-transactions scenario both
balances are equal (no net movement during the period):

- OpeningBalance: "£500.00 GBP" (Credit → trailing titleMedium `color/tertiary` #64597B)
- ClosingBalance: "£500.00 GBP" (Credit → trailing titleMedium `color/tertiary` #64597B)

### Fees and Interest Sections (hidden)

In the empty-transactions scenario, `StatementFee` and `StatementInterest` are both empty arrays.
Set component properties `feesVisible: false` and `interestVisible: false`. These sections do not
render. Do not leave placeholder height — the layout collapses cleanly to the Transactions header.

### Transactions Section with Empty State

Place the Transactions section header **"Transactions"** (labelMedium #41474D, 48dp tall).

Below the section header, place the empty state illustration in a centred vertical Auto Layout
with 32dp horizontal padding and 24dp top padding. The empty state has three elements:

First, the icon `receipt_long` at 48dp by 48dp, tint `color/on-surface-variant` (#41474D).
Ensure `contentDescription` is set to "No transactions this period" in the accessibility layer.
The icon should have at least 16dp of space below before the title text.

Second, the title text **"No transactions this period"** in headlineSmall style (24sp Roboto
Regular, `color/on-surface` #181C20), centred horizontally. This is a valid, expected state for
newly opened accounts that have not yet transacted within the statement period. The message should
be informative, not alarming — the visual weight should match the calm, trust-building tone of
the rest of the screen.

Third, the body text **"This statement period has no transaction records."** in bodyMedium style
(14sp Roboto Regular, `color/on-surface-variant` #41474D), centred, with 8dp of spacing above.

### Download PDF Button (retained)

The PDF download is still available in the empty state — the statement document itself exists even
if there are no transactions within it. Render the download button with identical appearance to
the content state: outlined, 361dp wide, 48dp tall, full-pill radius, border and label
`color/primary` (#266489), icon `download` 18dp.

### Bottom Navigation

Identical to content state.

---

## Frame 4 — State: error

Create a frame named **StatementDetail / error** sized 393×852 with `color/background` fill.

### Top App Bar

Title text: **"Statement Detail"** (the fallback title string). The real StatementReference is
not available because the network request failed before any data was loaded.

### Error State Illustration

Fill the remaining space between the top app bar and bottom navigation with a Box centred both
horizontally and vertically. Add 32dp horizontal padding. Create a vertical Auto Layout with
centred horizontal alignment and 8dp item spacing:

First, the icon `error_outline` at 48dp by 48dp, tint `color/error` (#BA1A1A). Ensure the
`contentDescription` is set appropriately ("Error loading statement"). Leave 16dp of space below
before the title.

Second, the title text **"Unable to load statement"** in headlineSmall (24sp Roboto Regular,
`color/on-surface` #181C20), centred. Keep the title concise and non-technical — the body text
below provides the specific reason.

Third, the body text in bodyMedium (14sp Roboto Regular, `color/on-surface-variant` #41474D),
centred. Create a Figma component property `errorMessage` with four preset variants matching the
actual error cases from docs.yaml:

- HTTP 401: "Session expired. Please re-authenticate."
- HTTP 403: "Consent does not include ReadStatements."
- HTTP 404: "Statement not found."
- Network: "Unable to connect. Check your internet connection."

Default the demo to the HTTP 401 variant: "Session expired. Please re-authenticate."

### Retry Button

Below the error body text (24dp gap), place a filled Button component. Size it to approximately
70% of the available width (275dp) and 48dp tall with full-pill corner radius (9999dp). Background
fill `color/primary` (#266489), label text `color/on-primary` (#FFFFFF). Label: **"Try again"**
in labelLarge (14sp Roboto Medium). The button has a minimum touch target of 48dp × 48dp.

For pressed state: apply a `color/on-primary` (#FFFFFF) overlay at 12% opacity. For focused
state: apply a `color/on-primary` overlay at 12% opacity and a 3dp focus ring in `color/primary`.
For disabled state: fill `color/on-surface` at 12% opacity, label `color/on-surface` at 38%
opacity; this state is not applicable here since the retry button is always enabled.

Create a prototype interaction on the retry button: on tap, navigate to the
**StatementDetail / loading** frame with a 300ms Push Left transition to represent re-entry into
the loading state.

### Bottom Navigation

Identical to other states. No tab selection changes when the error occurs.

---

## Auto Layout Specifications per Frame

The following table lists the Auto Layout configuration for each major layout container. Apply
these values precisely in Figma to ensure the implementation team can extract accurate values.

| Layer | Direction | Padding | Item Gap | Alignment | Width | Height |
|---|---|---|---|---|---|---|
| Screen root Column | Vertical | 0dp all | 0dp | Start | Fill | Fill |
| top_app_bar | Horizontal | 4dp v / 4dp h | 0dp | Center vertical | Fill | 56dp Fixed |
| statement_header_card inner | Vertical | 16dp all | 4dp | Start | Fill | Hug |
| balances_header row | Horizontal | 0dp v / 16dp h | 0dp | Center vertical | Fill | 48dp Fixed |
| balance_row inner | Horizontal | 0dp v / 16dp h | 0dp | Center vertical | Fill | 56dp Fixed |
| fee_row inner | Horizontal | 0dp v / 16dp h | 0dp | Center vertical | Fill | 56dp Fixed |
| interest_row inner | Horizontal | 0dp v / 16dp h | 0dp | Center vertical | Fill | 56dp Fixed |
| txn_row inner | Horizontal | 0dp v / 16dp h | 0dp | Top | Fill | 72dp Fixed |
| txn_row left-stack | Vertical | 0dp | 4dp | Start | Fill (weight 1) | Hug |
| download_pdf_button inner | Horizontal | 10dp v / 24dp h | 8dp | Center | Fill | 48dp Fixed |
| empty_txns_state | Vertical | 24dp v / 32dp h | 8dp | Center | Fill | Hug |
| error_state | Vertical | 32dp h / 0dp v | 8dp | Center | Fill | Fill |
| bottom_nav | Horizontal | 0dp | Space Between | Center | Fill | 80dp Fixed |
| bottom_nav destination | Vertical | 12dp v / 0dp h | 4dp | Center | Fill | Fill |

---

## Component Variants

### Transaction Row Variants

The `statement_txn_row` component should have four states in the Figma component set:

**Default**: white/transparent background, text at full opacity, no overlay.

**Hovered**: apply a `color/on-surface` (#181C20) fill at 8% opacity over the row background.
This communicates pointer interactivity on desktop or tablet viewports. Use Figma's "Hover"
interaction trigger.

**Pressed**: apply a `color/on-surface` fill at 12% opacity. The animation simulates the Android
ripple. In Figma prototype, use the "Mouse Down" trigger with a 150ms fade to this variant, then
fade back to Default on "Mouse Up".

**Focused**: add a 2dp outline using `color/primary` (#266489) on the row perimeter. This serves
accessibility — keyboard or switch-access navigation on Android highlights the focused row.

### Download PDF Button Variants

**Default**: outlined border 1dp `color/primary` (#266489), label #266489, no fill.

**Hovered**: add a `color/primary` fill at 8% opacity inside the button, keeping the border.

**Pressed**: `color/primary` fill at 12% opacity.

**Disabled**: border and label use `color/on-surface` at 38% opacity (#41474D at 38%). Apply when
`downloadState == Downloading`. In Figma, create a property `enabled: true/false`.

**Loading variant**: when `downloadState == Downloading`, show the button in disabled state AND
make the `download_progress` linear indicator visible directly below it.

### Balance Row Amount Colour Variants

Create a component property `amountPolarity: credit | debit | neutral` on each list item row
that renders a trailing amount. This drives the trailing text colour:

- `credit` → `color/tertiary` (#64597B) — positive/incoming amounts
- `debit` → `color/error` (#BA1A1A) — negative/outgoing amounts
- `neutral` → `color/on-surface` (#181C20) — zero-value or informationally neutral amounts (e.g.
  £0.00 maintenance fee)

---

## Prototype Interaction Flow

Configure these prototype connections in Figma to enable stakeholder walkthrough and developer
handoff:

**Back navigation**: from any state frame, connect the `arrow_back` icon button in the top app
bar to the `statements` screen frame (create a placeholder frame for Statements if it does not
yet exist in the Figma file). Use a Push Left (reversed) / Slide Right 300ms transition to
communicate navigating "up" in the hierarchy.

**Transaction row tap**: from the **content** state frame, connect each `statement_txn_row` to a
`transaction-detail` placeholder frame. Use a Push Left transition at 300ms. Pass the params in
the prototype layer comment: `transactionId`, `accountId`.

**Download PDF tap**: from the **content** and **empty** state frames, connect the
`download_pdf_button` to the **StatementDetail / content / downloading** variant frame. Use a
Dissolve transition at 150ms to represent the state update (DownloadState: Idle → Downloading).
After showing the downloading variant for a moment, optionally connect to a **StatementDetail /
content / downloaded** variant where the snackbar is visible and the progress indicator is hidden.

**Retry tap**: from the **error** state frame, connect the `retry_button` to the **loading**
state frame using a Push Left transition at 300ms, representing re-entry into the fetch cycle.

**Bottom navigation**: from any frame, connect each bottom nav destination to its respective
top-level screen frame. The Transactions destination connects to the transactions list screen. All
four destinations are reachable from any depth of navigation.

---

## Accessibility Specifications

All interactive components must meet WCAG AA contrast requirements with the resolved colour pairs
in this screen. Key pairs to verify:

- Primary text #181C20 on surface #F7F9FF: contrast ratio ~18:1 (exceeds AAA)
- Secondary text #41474D on surface #F7F9FF: contrast ratio ~10:1 (exceeds AA)
- Tertiary amounts #64597B on surface #F7F9FF: contrast ratio ~5.5:1 (passes AA, borderline AAA)
- Error amounts #BA1A1A on surface #F7F9FF: contrast ratio ~5.9:1 (passes AA)
- Primary #266489 on surface #F7F9FF: contrast ratio ~5.5:1 (passes AA for large text/UI)
- Snackbar text #EEF1F6 on #2D3135: contrast ratio ~14:1 (exceeds AAA)

Minimum touch targets for all interactive elements: 48dp × 48dp. The transaction rows are 72dp
tall, the download button is 48dp tall, the retry button is 48dp tall — all compliant.

All icons must have explicit `contentDescription` values or be marked as decorative:

- `arrow_back` (top app bar): "Navigate back" (not decorative)
- `download` (button icon): decorative (label "Download PDF" provides context)
- `receipt_long` (empty state): "No transactions this period" (not decorative)
- `error_outline` (error state): "Error loading statement" (not decorative)

For TalkBack (Android) and VoiceOver (iOS), the transaction rows should announce as a single
unit: "[description], [polarity] [amount] [currency], on [date]". Configure the row's
`semantics {}` block to merge descendants and provide a custom content description combining all
three text fields in reading order: date → description → amount.

The snackbar appears at the bottom of the screen above the navigation bar. Its 4000ms auto-
dismiss timer should be paused for users who have accessibility services (TalkBack, Switch Access)
active, as these users may need more time to interact with the action.

Reduce-motion compliance: when the user enables "Reduce motion" in OS accessibility settings, the
circular progress indicator should use a pulsing opacity animation (0.4 → 1.0 → 0.4 at 1.5s
cycle) rather than rotation. The linear progress indicator should use a fill animation instead of
a sweeping gradient. All page transitions should use Dissolve (fade) instead of Push Left slide.
