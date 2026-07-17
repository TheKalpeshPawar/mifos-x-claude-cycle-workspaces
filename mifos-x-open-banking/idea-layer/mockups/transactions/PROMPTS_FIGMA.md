# Transactions — Figma Design Prompts

> Auto-generated from `screens/transactions/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Roboto font
> Generated: 2026-07-16T00:00:00Z

These prompts are written as design instructions for Figma AI, a Figma designer, or any handoff consumer.
Each section describes how to construct the frame from scratch, top to bottom, using Auto Layout and
the resolved design-system tokens below. Reference variable names use the Figma variable path convention
`category/role` (e.g. `color/primary`).

---

## Design System Summary

### Colour Palette — Light Mode (resolved hex values)

The Open Banking app uses a Material 3 scheme generated from seed primary #266489 (Trust Blue).
All colour references below are the resolved light-mode hex values. Use these exact values when
creating Figma colour styles or variables.

- **Primary:** #266489 — used for selected chip fills, filled buttons, progress indicators, credit amounts, active navigation icons.
- **On Primary:** #FFFFFF — text / icons placed on primary-coloured surfaces.
- **Primary Container:** #C9E6FF — used for tonal chip backgrounds and hero card backgrounds in account screens.
- **On Primary Container:** #004B6F — text on primary container surfaces.
- **Secondary:** #50606E — secondary actions, category icons, unselected chip icon tints.
- **Secondary Container:** #D3E5F5 — tonal button backgrounds for secondary actions.
- **Error:** #BA1A1A — debit amounts, error state icons, destructive signals.
- **Error Container:** #FFDAD6 — pending badge background, tonal error chip backgrounds.
- **On Error Container:** #93000A — text on error-container-coloured surfaces (pending badge label).
- **Background / Surface:** #F7F9FF — screen and card background.
- **On Surface:** #181C20 — primary text, titles, merchant names.
- **Surface Variant:** #DDE3EA — shimmer skeleton base colour.
- **On Surface Variant:** #41474D — secondary text, date headers, labels, body copy, icon tints.
- **Outline:** #72787E — outlined chip borders, divider strokes.
- **Outline Variant:** #C1C7CE — light dividers, stat-block separators.
- **Surface Container:** #EBEEF3 — search field fill, chip backgrounds in assist and neutral states.
- **Surface Container Low:** #F1F4F9 — subtle card fills where elevation 0 cards need a distinction from the page background.

### Typography Scale (Roboto)

Use Roboto in all text layers. For monetary amounts, use Roboto Mono to align decimal points.

| Role | Size | Line height | Weight | Usage in Transactions |
|---|---|---|---|---|
| titleLarge | 22sp | 28sp | 400 | Top app bar title "Transactions" |
| titleMedium | 16sp | 24sp | 500 | Transaction amounts (credit/debit); stat block values |
| bodyLarge | 16sp | 24sp | 400 | — (reserve for detail screens) |
| bodyMedium | 14sp | 20sp | 400 | Merchant names (tx_merchant), placeholder text, error body |
| bodySmall | 12sp | 16sp | 400 | Stat block labels ("Money in", "Money out") |
| labelLarge | 14sp | 20sp | 500 | Button labels ("Load more transactions", "Clear filters", "Try again") |
| labelSmall | 11sp | 16sp | 500 | Filter chip labels; date group headers; category chip text; pending badge text |

### Spacing & Shape Scale

Use a 4dp base grid throughout. All padding and gap values are multiples of 4.

- Screen horizontal padding: 16dp
- Card internal padding: 12dp vertical × 16dp horizontal
- Gap between filter chips: 8dp
- Corner radius — full pill (chips, badges): 9999dp
- Corner radius — search field: 28dp (extra_large)
- Corner radius — transaction row card: 8dp (small)
- Corner radius — buttons (Load more, Clear filters, Try again): 12dp (medium)
- Corner radius — hero cards on account screens: 16dp (large)
- Minimum touch target for all interactive elements: 48dp

### Token → Figma Variable Mapping

Create a Figma variable collection named "Open Banking / Light" with the following entries.
Reference these variable names in all component fills, strokes, and text colour properties.

| Semantic token | Figma variable path | Resolved hex |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/on-primary | #FFFFFF |
| primaryContainer | color/primary-container | #C9E6FF |
| onPrimaryContainer | color/on-primary-container | #004B6F |
| secondary | color/secondary | #50606E |
| error | color/error | #BA1A1A |
| errorContainer | color/error-container | #FFDAD6 |
| onErrorContainer | color/on-error-container | #93000A |
| background | color/background | #F7F9FF |
| surface | color/surface | #F7F9FF |
| onSurface | color/on-surface | #181C20 |
| surfaceVariant | color/surface-variant | #DDE3EA |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outline-variant | #C1C7CE |
| surfaceContainer | color/surface-container | #EBEEF3 |
| surfaceContainerLow | color/surface-container-low | #F1F4F9 |

For typography, create a text style collection "Open Banking / Type" matching the Roboto scale above.
For monetary values only, override the font to Roboto Mono within the same size/weight spec.

---

## Frame: Transactions / Loading

Create a frame named **Transactions / Loading** at 393×852dp. Set the background fill to `color/background` (#F7F9FF). Apply Auto Layout vertically with no padding and no item spacing.

**Top App Bar:** Place an M3 small top app bar at the top of the frame. Set its height to 64dp and width to fill the frame. Fill the bar with `color/surface` (#F7F9FF). On the left, place a back arrow icon (24dp, tint `color/on-surface` #181C20) with 16dp padding from the left edge. Place the text "Transactions" in titleLarge (22sp, Roboto Regular, `color/on-surface` #181C20) at 56dp from the left. Add a 1dp bottom divider in `color/outline-variant` (#C1C7CE).

**Content Area:** The content area between the app bar and the bottom navigation fills the remaining height. Use a Column Auto Layout, set horizontal alignment to centre and vertical alignment to centre. Inside this centred column place a single M3 CircularProgressIndicator component. Render it as a 48dp circle with a 4dp stroke in `color/primary` (#266489). In Figma, represent this as a ring shape with a 300-degree arc to suggest animation. Label the layer "loading_spinner".

**Bottom Navigation Bar:** Place an M3 navigation bar at the bottom of the frame, height 80dp, width fill frame, background `color/surface` (#F7F9FF). Add a 1dp top separator in `color/outline-variant`. Place four navigation items evenly distributed: Home (icon home), Accounts (icon account_balance), Transactions (icon receipt_long), More (icon more_horiz). The Transactions item is the selected destination — render its icon and label in `color/primary` (#266489) with a pill-shaped indicator behind it (56dp wide × 32dp tall, fill `color/primary-container` #C9E6FF). Unselected items render in `color/on-surface-variant` (#41474D).

---

## Frame: Transactions / Content

Create a frame named **Transactions / Content** at 393×852dp. Background fill `color/background` (#F7F9FF). Apply a vertical Auto Layout with no item spacing (individual sections have their own padding). This is the primary-flow frame and has the most detail.

### Top App Bar

Identical to the Loading frame app bar described above. Title "Transactions", back arrow, 64dp height.

### Period Summary Strip

Immediately below the app bar, create a Row Auto Layout layer named "period_summary". Set width to fill frame, height to 56dp, vertical padding to 8dp, horizontal padding to 16dp. Set the background fill to `color/surface` (#F7F9FF). Add a 1dp bottom divider in `color/outline-variant` (#C1C7CE).

Inside the row, place two Column Auto Layout children with equal weight (each width fills 50% of the available space after subtracting the vertical divider).

The **left column** (total_credit) contains two text layers stacked vertically with 2dp gap. The top layer reads "Money in" in bodySmall (12sp Roboto Regular, `color/on-surface-variant` #41474D). The bottom layer reads "+£2,400.00" in titleMedium (16sp Roboto Mono Medium 500, `color/primary` #266489). The green credit amount uses Roboto Mono to align digits.

The **right column** (total_debit) mirrors the left column. The label reads "Money out" in bodySmall #41474D. The value reads "−£1,394.04" in titleMedium Roboto Mono, fill `color/error` #BA1A1A.

Between the two columns place a 1dp vertical divider line, height 32dp, fill `color/outline-variant` (#C1C7CE), centred vertically in the row.

### Filter Chip Row

Below the period summary, create a horizontal Auto Layout layer named "filter_chips". Set it to Scroll → Horizontal in Figma (overflow: horizontal scroll). Width fills the frame. Height wraps content at approximately 52dp including padding. Padding: 10dp top, 10dp bottom, 16dp left, 16dp right. Gap between chips: 8dp.

Place four M3 FilterChip components in order:

1. **filter_all** "All" — render in the **selected** state. Fill the chip background with `color/primary` (#266489). The label "All" uses labelSmall (11sp Roboto Medium, `color/on-primary` #FFFFFF). No leading icon. Corner radius 9999dp. Height 32dp.

2. **filter_money_in** "Money in" — render in the **unselected** state. Outline stroke 1dp `color/outline` (#72787E). Label "Money in" in labelSmall `color/on-surface-variant` (#41474D). Leading icon arrow_downward 18dp, tint #41474D. Height 32dp. Corner radius 9999dp.

3. **filter_money_out** "Money out" — same style as filter_money_in. Leading icon arrow_upward 18dp.

4. **filter_date_range** "Date range" — same style. Leading icon date_range 18dp.

### Search Field

Below the filter chip row, create an OutlinedTextField layer named "search_field". Width: frame width minus 32dp (361dp). Height: 48dp. Corner radius: 28dp (extra_large — creates a full capsule shape). Fill: `color/surface-container` (#EBEEF3). Stroke: none in default state; add 2dp `color/primary` stroke on focus state. Place 16dp left and right margins to centre it on screen.

Inside the search field, place a leading search icon (20dp, tint `color/on-surface-variant` #41474D) with 12dp leading padding. Place placeholder text "Search transactions" in bodyMedium (14sp Roboto Regular, `color/on-surface-variant` #41474D) centred vertically. Place a trailing clear icon (20dp, tint `color/on-surface-variant` #41474D) with 12dp trailing padding — this icon is only visible when the text field has input; in the default placeholder state, it should be invisible. Add 8dp vertical padding above and below the search row.

### Transaction List — Date Groups

Below the search field, create a vertical Auto Layout container named "transactions_list". Width fills frame. Set padding: 0dp top, 16dp bottom, 16dp left, 16dp right. Gap between items: 0dp (date headers and rows stack flush).

The list is organised into date groups. Each group starts with a **date group header** followed by one or more transaction rows.

**Date Group Header:** Create a text layer for each date header. Use labelSmall (11sp Roboto Medium 500, `color/on-surface-variant` #41474D). Width fills the list container. Height 24dp. Vertical padding 4dp top, 4dp bottom. The text reads the formatted date string, for example "28 Jun 2026". In a real Figma file, these headers should be set to sticky position so they remain visible while the user scrolls through rows within the group.

**Transaction Row:** Create an M3 ListItem layer named "transaction_row". Width fills the list container minus its 16dp horizontal padding (361dp effective). Minimum height 64dp — the row will expand vertically if it contains a pending badge on a separate line. Corner radius 8dp. Background fill `color/surface-container-low` (#F1F4F9) for a card-like separation from the page background (elevation 0). Add 1dp bottom divider in `color/outline-variant` between consecutive rows in the same date group. Padding: 12dp top and bottom, 16dp left and right.

The row is a Row Auto Layout with three zones:

**Leading icon zone (48dp × 48dp):** Place a circle shape 40dp diameter. For Credit (arrow_downward) transactions, fill the circle with `color/primary-container` (#C9E6FF) and place an arrow_downward icon 24dp, tint `color/on-primary-container` (#004B6F). For Debit (arrow_upward) transactions, fill the circle with `color/error-container` (#FFDAD6) and place an arrow_upward icon 24dp, tint `color/on-error-container` (#93000A).

**Body zone (fills remaining width minus trailing zone):** Use a Column Auto Layout with gap 2dp. The top text layer shows the merchant name (tx_merchant) in bodyMedium (14sp Roboto Regular, `color/on-surface` #181C20), single line, ellipsis overflow. Below the merchant name, place a Row Auto Layout (gap 4dp) containing:
- A category chip (tx_category_tag) — render as a small assist chip. Height 24dp, corner radius 9999dp, background `color/surface-container` (#EBEEF3), label in labelSmall (11sp Roboto Medium, `color/on-surface-variant` #41474D).
- A pending badge (tx_pending_badge) — only visible when OBTransaction6.Status=Pending. Render as a tonal chip, height 20dp, corner radius 9999dp, background `color/error-container` (#FFDAD6), label "Pending" in labelSmall (11sp Roboto Medium, `color/on-error-container` #93000A). Include a warning triangle icon 14dp before the text. **This component must be set to hidden by default in Figma** and only made visible via the Pending component variant.

**Trailing amount zone (72dp wide):** Place a Text layer showing the formatted amount. Credit amounts use "+£" prefix and `color/primary` (#266489). Debit amounts use "−£" prefix and `color/error` (#BA1A1A). Both use titleMedium (16sp Roboto Mono Medium 500) to ensure monospace alignment. Right-align the text within this zone.

**Sample rows to create for the Content frame** (use actual HSBC sandbox values from demo-data.yaml):

- 28 Jun 2026 group:
  - NETFLIX.COM | Subscriptions | −£10.99 (Debit, Booked — no badge)
  - COSTA COFFEE 1847 LONDON | Dining | −£3.65 (Debit, Booked — no badge)
  - SPOTIFY AB | Subscriptions | −£11.99 (Debit, **Pending** — show ⚠ Pending badge in #FFDAD6/#93000A)

- 27 Jun 2026 group:
  - PRET A MANGER 083 LONDON | Dining | −£8.45 (Debit, Booked)
  - AMAZON UK MARKETPLACE | Shopping | −£31.99 (Debit, Booked)

- 25 Jun 2026 group:
  - SALARY ACME LTD | Income | +£2,400.00 (Credit, Booked — green amount #266489)

Show the 28 Jun and 27 Jun groups fully; truncate with a fade or ellipsis indicator to imply the 25 Jun and earlier rows scroll below the fold.

### Pagination Footer

Below the visible rows, before the bottom nav, show the **load_more_button** as an M3 TextButton. Width: frame width minus 32dp (361dp). Height: 40dp. Corner radius: 12dp (medium). Label "Load more transactions" in labelLarge (14sp Roboto Medium, `color/primary` #266489), centred. No fill; no stroke. This button is visible only when has_next_page=true and is_paginating=false.

To represent the **pagination_loader** alternative state (visible while is_paginating=true), create a separate variant of the Content frame. In that variant, hide the load_more_button and in its place show an M3 LinearProgressIndicator: a 4dp tall bar, full frame width, with an animated indeterminate fill in `color/primary` (#266489) over a track in `color/primary-container` (#C9E6FF). Label this layer "pagination_loader".

### Bottom Navigation Bar

Identical to the Loading frame bottom nav. The Transactions tab icon receipt_long is selected (#266489 indicator).

---

## Frame: Transactions / Empty

Create a frame named **Transactions / Empty** at 393×852dp. Background `color/background` (#F7F9FF).

Apply the same vertical Auto Layout structure as the Content frame. The top app bar, period summary strip, filter chip row, and search field are all visible and identical to the Content frame — they remain on screen even when the filtered result set is empty, giving the user full access to change or clear the active filter. In the Empty state, the period summary values read "+£0.00" (credit, #266489) and "−£0.00" (debit, #BA1A1A), reflecting that the filtered set contains zero matching transactions.

Below the search field, where the transaction list would appear, render the empty state illustration centred horizontally and vertically in the remaining space.

**Empty state container:** Create a Column Auto Layout layer named "empty_transactions". Set alignment to centre-centre. Padding top 48dp, bottom 48dp, horizontal 32dp.

**Icon:** Place the Material Symbol receipt_long at 48dp × 48dp. Set the icon tint to `color/on-surface-variant` (#41474D) using the outlined variant. Add 16dp bottom margin below the icon.

**Title:** Place a Text layer reading "No transactions found" in headlineSmall (24sp Roboto Regular, `color/on-surface` #181C20). Centre-align. Add 8dp bottom margin.

**Body:** Place a Text layer reading "No transactions match your current filters for this period." in bodyMedium (14sp Roboto Regular, `color/on-surface-variant` #41474D). Centre-align. Max width 280dp. Line wrap enabled. Add 24dp bottom margin.

**Clear Filters Button:** Place an M3 OutlinedButton named "clear_filters_button". Width 200dp. Height 40dp. Corner radius 12dp (medium). Stroke 1dp `color/primary` (#266489). Label "Clear filters" in labelLarge (14sp Roboto Medium, `color/primary` #266489). Centred horizontally. Minimum touch target 48dp in the hit area.

The bottom navigation bar is identical to the other frames with Transactions selected.

---

## Frame: Transactions / Error

Create a frame named **Transactions / Error** at 393×852dp. Background `color/background` (#F7F9FF).

Apply a vertical Auto Layout. The top app bar appears at the top. Unlike the Empty state, the period summary strip, filter chips, and search field are **not** shown in the error state — the full content area between the app bar and bottom nav is used for the error message.

**Error state container:** Create a Column Auto Layout layer named "error_state". Set horizontal alignment to centre and vertical alignment to centre. Fill the available height between the app bar (64dp) and the bottom nav (80dp). Set padding horizontal 32dp.

**Icon:** Place the Material Symbol error_outline at 48dp × 48dp. Set the icon tint to `color/error` (#BA1A1A). Outlined variant. Add 16dp bottom margin.

**Title:** "Unable to load transactions" in headlineSmall (24sp Roboto Regular, `color/on-surface` #181C20). Centre-align. Add 8dp bottom margin.

**Body:** The body message is resolved by the ViewModel from i18n strings based on the HTTP status code. Design four variants of this text layer, one per error type:
- 401 Session expired: "Session expired. Please log in again."
- 403 Consent withdrawn: "Access to transactions has been withdrawn."
- 429 Rate limited: "Too many requests. Please wait a moment and retry."
- Network error (default): "No network connection. Please check your connection and retry."

All error body variants use bodyMedium (14sp Roboto Regular, `color/on-surface-variant` #41474D), centre-aligned, max width 280dp. Use the network error variant as the primary design content for the frame. Add 24dp bottom margin below the body text.

**Retry Button:** Place an M3 FilledButton named "retry_button". Width 200dp. Height 40dp. Corner radius 12dp. Fill `color/primary` (#266489). Label "Try again" in labelLarge (14sp Roboto Medium, `color/on-primary` #FFFFFF). Centred horizontally. Minimum touch target 48dp.

**Visibility rule:** The retry_button must be set to **hidden** in the 403 ConsentWithdrawnError variant (error.recoverable=false). Create a Figma component variant named "Error / Non-Recoverable" where the retry button layer has visibility set to off. For the 401, 429, and Network error variants, the button is visible.

The bottom nav is identical to other frames with Transactions selected.

---

## Auto Layout Specifications — Key Components

Use these Auto Layout settings when building the Figma component library for this screen.

**top_app_bar:** Direction horizontal. Width fill parent. Height 64dp. Padding left 16dp, right 16dp. Alignment: centre vertical. Content: [back_arrow 24dp] [gap 16dp] [title text fill]. Bottom border 1dp `color/outline-variant`.

**period_summary:** Direction horizontal. Width fill parent. Height 56dp. Padding 8dp vertical, 16dp horizontal. Children have equal fill widths. Vertical divider 1dp between children.

**filter_chips:** Direction horizontal. Overflow scroll. Width fill parent. Height wrap (approximately 52dp with padding). Padding 10dp vertical, 16dp horizontal. Gap 8dp. No wrap.

**search_field:** Direction horizontal. Width fixed 361dp. Height 48dp. Corner radius 28dp. Padding 12dp vertical, 16dp horizontal. Gap 8dp between leading icon and text.

**transaction_row:** Direction horizontal. Width fill parent. Min height 64dp (wrap for Pending rows). Padding 12dp vertical, 16dp horizontal. Gap 12dp between zones. Children: leading icon zone (fixed 40dp), body zone (fill), trailing zone (fixed 72dp).

**body zone inside transaction_row:** Direction vertical. Width fill. Gap 4dp. Children: merchant text (fill, single line), chip row (horizontal, gap 4dp, wrap content).

**empty_transactions / error_state:** Direction vertical. Width fill parent. Height fill parent. Alignment centre. Padding 32dp horizontal. Gap: see per-child margins above.

---

## Component Variants — Filter Chip

Create an M3 FilterChip base component with the following named variants. These are reused across the content and empty frames.

- **Default / Unselected:** Transparent fill. Stroke 1dp `color/outline` (#72787E). Label `color/on-surface-variant` (#41474D). Optional leading icon tint #41474D. Height 32dp, corner radius 9999dp.
- **Default / Selected:** Fill `color/primary` (#266489). No stroke. Label `color/on-primary` (#FFFFFF). Optional checkmark icon leading, tint #FFFFFF. Height 32dp.
- **Hovered / Unselected:** Same as Default Unselected but add 8% `color/on-surface` (#181C20) overlay on the fill to suggest hover state. Useful for web/desktop breakpoints.
- **Pressed / Unselected:** Add 12% `color/on-surface` overlay on fill. Scale the chip to 98% in the pressed interaction frame.
- **Focused / Unselected:** Add a 3dp outer focus ring in `color/primary` (#266489) at 2dp offset from the chip border.
- **Disabled:** Reduce opacity of all content to 38%. The fill is `color/surface-container` (#EBEEF3) and the stroke is `color/outline-variant` (#C1C7CE).

---

## Component Variants — Transaction Row

Create a base **TransactionRow** Figma component with these variants:

- **Type = Credit, Status = Booked:** Leading circle fill `color/primary-container` (#C9E6FF), icon arrow_downward `color/on-primary-container` (#004B6F). Amount text `color/primary` (#266489) with "+" prefix. No pending badge.
- **Type = Debit, Status = Booked:** Leading circle fill `color/error-container` (#FFDAD6), icon arrow_upward `color/on-error-container` (#93000A). Amount text `color/error` (#BA1A1A) with "−" prefix. No pending badge.
- **Type = Debit, Status = Pending:** Same as Debit/Booked for leading and amount. Additionally show the tx_pending_badge chip (⚠ Pending, fill #FFDAD6, label #93000A). Min height expands to 80dp to accommodate the extra chip row.
- **Hovered:** Add 8% `color/on-surface` (#181C20) fill overlay on the entire row.
- **Pressed:** Add 12% overlay and reduce row scale to 99%.
- **Focused:** Add a 2dp outer focus ring in `color/primary` (#266489).

---

## Prototype Interaction Flow

Wire the following prototype connections in Figma Prototype view. All interactions are sourced from the `action_contract` declarations in `ui.yaml`. Use "On tap" trigger and "Navigate to" action unless otherwise noted.

**filter_all chip** — On tap → remain on Transactions / Content frame, update the chip row to show filter_all as selected and the others as unselected. Use a "Swap component" interaction or an overlay variant to show the filtered state. The period summary values update to reflect the full unfiltered total.

**filter_money_in chip** — On tap → swap to a "Transactions / Content — Credit only" variant frame where only credit rows appear in the list and the period summary shows only credit totals.

**filter_money_out chip** — On tap → swap to a "Transactions / Content — Debit only" variant where only debit rows appear.

**filter_date_range chip** — On tap → open a bottom sheet overlay frame named "Date Range Picker". Wire the overlay to animate in from the bottom with an ease-out 300ms transition. The bottom sheet should contain a Material 3 Date Range Picker. On "Confirm", navigate back to Transactions / Content with the date range reflected in the filter_date_range chip label (e.g. "23 Jun – 28 Jun"). On "Cancel", dismiss the sheet and return to the current frame.

**search_field** — On tap → switch to "Focused" state of search_field (3dp focus ring in `color/primary`). Use the Figma keyboard simulation to show typed characters. As characters accumulate, simulate list narrowing by creating variant frames with progressively fewer transaction rows visible. For the design handoff, one "Transactions / Content — Search active" frame with a non-empty search string in the field is sufficient to illustrate the pattern.

**transaction_row (any)** — On tap → navigate to **Transaction Detail** frame (screen id: transaction-detail), passing transactionId and accountId as prototype route parameters. Label the connection "navigate_transaction_detail → transaction-detail". Use a "Push right" transition at 300ms ease.

**load_more_button** — On tap → swap to "Transactions / Content — Paginating" variant where load_more_button is hidden and pagination_loader (LinearProgressIndicator) appears in its place at the bottom of the list. After a simulated 1s delay, swap back to the Content frame with additional rows appended and has_next_page set to false (load_more_button hidden, list complete).

**clear_filters_button (Empty frame)** — On tap → navigate to Transactions / Content frame. Use a "Dissolve" transition at 200ms to imply an in-place state change rather than a push.

**retry_button (Error frame)** — On tap → navigate to Transactions / Loading frame first, then after a simulated 1s delay navigate to Transactions / Content (successful retry) or remain on Error (failed retry). Use "Dissolve" 200ms for both transitions. For the 403 non-recoverable variant, there is no retry_button; instead the back arrow navigates to the Accounts screen.

**back arrow (all frames)** — On tap → navigate back to the previous screen (typically account-detail or home depending on navigation entry point). Use "Pop left" slide transition at 300ms ease.

**Bottom nav: Home** — navigate to Home screen.
**Bottom nav: Accounts** — navigate to Accounts screen.
**Bottom nav: Transactions** — no-op (already on this screen).
**Bottom nav: More** — navigate to Settings / More screen.

---

## Accessibility Notes

Apply these annotations to the Figma file for developer handoff. They map directly to the `accessibility_label` values declared in `ui.yaml`.

**Minimum touch targets:** All interactive elements — filter chips, transaction rows, the load_more_button, clear_filters_button, retry_button, and back arrow — must have a minimum touch target of 48dp × 48dp even if the visual size is smaller (e.g. 32dp chips achieve 48dp touch target via invisible padding). Add a red annotation layer (opacity 10%) over any interactive element whose visual bounds are below 48dp to flag it for the engineer.

**Content descriptions:** Every icon used as a standalone interactive element must carry a content description. The back arrow has the label from `strings.transactions.a11y.back` (annotate as "Navigate back"). The search leading icon is decorative (no label needed). The transaction row credit/debit icons are decorative — the full accessibility label is on the row itself, synthesised as "[merchant name], [Credit/Debit], £[amount] [currency][, Pending if applicable]".

**Colour contrast:** All text must meet WCAG AA contrast ratios:
- Body text (#181C20 on #F7F9FF) achieves 16.7:1 — exceeds AAA.
- Secondary text (#41474D on #F7F9FF) achieves 9.3:1 — exceeds AAA.
- Credit amount (#266489 on #F7F9FF) achieves 4.8:1 — passes AA for normal text.
- Debit amount (#BA1A1A on #F7F9FF) achieves 5.9:1 — passes AA.
- Pending badge (#93000A on #FFDAD6) achieves 6.4:1 — passes AA.
- Filter chip selected (white #FFFFFF on #266489) achieves 4.8:1 — passes AA for large text (labelSmall at 11sp is considered large in context of a chip). If strict AA for small text is required, consider using the medium-contrast variant from `design-tokens.yaml#contrast_variants`.

**Screen reader order:** In the content frame, the reading order should follow: top_app_bar → period_summary → filter_chips → search_field → date_group_header (group 1) → transaction_rows (group 1) → date_group_header (group 2) → … → load_more_button or pagination_loader. Use Figma's reading order annotation plugin or the Layer Order to document this for the engineer.

**Pending badge:** The pending badge (⚠ Pending) includes a warning icon before the text. In the Compose implementation, the icon is decorative and the accessibility label on the badge chip is `strings.transactions.a11y.pending_status`, which reads "Transaction pending". Annotate in Figma that the icon alone is not sufficient for screen readers; the label must be present.

**Focus indicators:** The 3dp focus ring in `color/primary` (#266489) must be visible on all interactive elements when navigated via keyboard (web/desktop) or switch access (Android/iOS accessibility). Design both focused and non-focused variants for all chips and buttons as described in the Component Variants sections above.

**Reduce motion:** The pagination_loader LinearProgressIndicator uses an indeterminate animation. When the system's reduce-motion preference is enabled, the animation should reduce to a static fill at 50% rather than an animated sweep. The CircularProgressIndicator in the Loading frame similarly reduces to a static partial arc. Annotate these elements in Figma with a "Reduce motion" note referencing `design-tokens.yaml#motion.reduce_motion_supported: true`.
