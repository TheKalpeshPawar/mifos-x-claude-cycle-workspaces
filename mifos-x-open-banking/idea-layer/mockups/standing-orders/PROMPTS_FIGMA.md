# Standing Orders — Figma Design Prompts

> Generated from `screens/standing-orders/ui.yaml` + `design-tokens.yaml` + `demo-data.yaml`
> Design system: Open Banking — Trust Blue (seed #266489, Material 3 light)
> Generated: 2026-07-16T00:00:00Z

---

## Canvas Specification

All frames: 393×852dp (Pixel 5 — M3 reference phone). Grid: 4-column, 16dp gutter, 16dp margin. Density: comfortable (4dp base unit). Font: Roboto (all weights from system). Theme: Material 3 light, dynamic-color disabled in Figma for design-system consistency.

---

## Design System Summary

### Resolved Colour Palette

| Token | Hex | Usage |
|---|---|---|
| primary | #266489 | Filled buttons, active nav icons, progress spinner, back icon |
| onPrimary | #FFFFFF | Label colour on filled buttons and primary surfaces |
| primaryContainer | #C9E6FF | Active standing-order badge background (chip tonal) |
| onPrimaryContainer | #004B6F | Active standing-order badge label text |
| secondary | #50606E | Category icons, secondary chrome |
| onSecondary | #FFFFFF | Label on secondary-filled surfaces |
| secondaryContainer | #D3E5F5 | Inactive standing-order badge background |
| onSecondaryContainer | #384956 | Inactive standing-order badge label text |
| error | #BA1A1A | Error icon tint |
| onError | #FFFFFF | Label on error-filled surfaces |
| background / surface | #F7F9FF | Screen background, top app bar, bottom nav |
| onSurface | #181C20 | Primary text (payee name, amount, title) |
| onSurfaceVariant | #41474D | Secondary text (frequency, dates, sort-code, ref, summary) |
| surfaceVariant | #DDE3EA | Dividers, disabled fills |
| outline | #72787E | Card outline when border-style elevation is used |
| outlineVariant | #C1C7CE | Subtle dividers |
| surfaceContainerLow | #F1F4F9 | Card surface (elevation 1) |

### Roboto Type Scale (Material 3)

| Role | Size / Line-height / Weight | Usage in this screen |
|---|---|---|
| titleLarge | 22sp / 28sp / 400 | Top app bar title |
| titleMedium | 16sp / 24sp / 500 | Payee name (so_payee_name) |
| headlineSmall | 24sp / 32sp / 400 | Next payment amount (so_amount), empty/error title |
| labelMedium | 12sp / 16sp / 500 | Summary row (active/inactive count), status badge label |
| labelLarge | 14sp / 20sp / 500 | Retry button label |
| bodyMedium | 14sp / 20sp / 400 | Error body text |
| bodySmall | 12sp / 16sp / 400 | Frequency, dates, sort-code, reference (Roboto Mono for sort-code) |

### Spacing Scale

Base unit: 4dp. Comfortable density. Screen padding: 16dp horizontal. Card internal padding: 16dp. Gap between list items: 8dp. Gap between card rows: 4dp.

---

## Frame 1 — Loading State

Create a frame named "Standing Orders / Loading" at 393×852dp. Fill the frame background with #F7F9FF.

At the top of the frame, place the M3 Small Top App Bar component. Set its height to 64dp and background to #F7F9FF with no elevation shadow. Place a leading icon button using the Material Symbol `arrow_back` at 24dp, tinted with primary #266489, inside a 48×48dp touch target. Set the bar title text to "Standing Orders" using titleLarge (Roboto 22sp/28sp weight 400) in #181C20. Align the title to the left of the leading icon with 16dp spacing from the icon.

In the main content area between the top bar and bottom navigation, place a single circular progress indicator at the exact centre of the available height. Size the indicator at 40×40dp. Set its colour to primary #266489 with a stroke width of 4dp. Do not add any label text near the indicator. The surrounding area should be entirely empty, reinforcing the unloaded state.

At the bottom of the frame, place the persistent bottom navigation bar at height 80dp, filled with #F7F9FF. It contains four tabs in order: Home (icon: `home`), Accounts (icon: `account_balance`), Transactions (icon: `receipt_long`), More (icon: `more_horiz`). Each icon is 24dp. All icon tints use #41474D for unselected tabs. Set the Accounts tab tint to #266489 and its label to weight 500 to reflect the active navigation hierarchy (standing-orders is reached via Accounts → account-detail).

**Auto Layout — Loading frame:**
- Direction: vertical
- Top app bar: fixed height 64dp, hug width fill
- Content area: fill width, fill remaining height, content centred both axes
- Bottom nav: fixed height 80dp, fill width
- No padding or gap between these three regions; each fills its layer

---

## Frame 2 — Content State

Create a frame named "Standing Orders / Content" at 393×852dp, background #F7F9FF.

**Top App Bar:** Same as the Loading frame — 64dp, #F7F9FF, back icon #266489, title "Standing Orders" titleLarge #181C20.

**Summary Row:** Directly below the top bar, place a single text element reading "4 Active · 1 Inactive". Style it as labelMedium (Roboto 12sp/16sp weight 500) in #41474D. Apply horizontal padding of 16dp and vertical padding of 8dp (making the row 32dp tall). Do not add a background or divider to this row.

**Scrollable List:** Below the summary row, create a vertically scrollable content area with horizontal padding of 16dp and bottom padding of 16dp. Populate it with five standing order cards, each separated by a vertical gap of 8dp. The list supports pull-to-refresh: display the standard M3 pull-to-refresh indicator with primary tint #266489 when the gesture is active.

**Standing Order Card — Design Specification:**

Each card uses the M3 ElevatedCard component (elevation 1, equivalent tonal surface is surfaceContainerLow #F1F4F9). Set corner radius to 12dp (medium shape). Internal padding is 16dp on all sides. Card width fills the column (393 − 32dp horizontal padding = 361dp). Height wraps content.

Inside each card, lay out content using vertical Auto Layout with item spacing of 4dp.

The first row is a horizontal Auto Layout: place the payee name text on the left (weight 1, flex-expand) and the status badge on the right, aligned centre-vertical, with a gap of 8dp. The payee name uses titleMedium (16sp/24sp w500 #181C20) with single-line overflow ellipsis. The status badge is a chip shape: pill corners (radius 9999), height 24dp, horizontal padding 8dp. Active badges use background #C9E6FF and label text #004B6F. Inactive badges use background #D3E5F5 and label text #384956. Label text is labelSmall (11sp/16sp w500).

The second row is the next payment amount. Use headlineSmall (24sp/32sp w400 #181C20). For an Inactive order where NextPaymentDateTime is null, show only the currency amount without the "Next:" prefix (the amount still reflects the originally configured recurring amount).

The third row is the frequency label. Use bodySmall (12sp/16sp w400 #41474D).

The fourth row is the next payment date, prefixed with "Next: " and formatted as "dd MMM yyyy". Use bodySmall (12sp/16sp w400 #41474D). Omit this row entirely for Inactive orders where NextPaymentDateTime is null (SO-004 in the demo data).

The fifth row is the final payment date. This row is conditional: render it only when `hasFinalPayment` is true. Prefix with "Final: " and format as "dd MMM yyyy". Use bodySmall (12sp/16sp w400 #41474D). In Figma, model this as a hidden variant that becomes visible. Both SO-004 (Inactive, Final: 28 Dec 2025) and SO-005 (Active, Final: 25 Dec 2026) display this row.

The sixth row is the creditor sort-code and account number. Use Roboto Mono bodySmall (12sp/16sp w400 #41474D) to convey the monospaced, machine-readable nature of the identifier (for example: "40-12-09 65872310"). Roboto Mono improves scanability and aligns digit widths.

The seventh row is the payment reference, prefixed with "Ref: ". Use bodySmall (12sp/16sp w400 #41474D).

**The five cards in order:**

Card 1 — Jameson Lettings: badge Active (#C9E6FF/#004B6F), amount £1,200.00 GBP, frequency "Monthly on the 1st", next date "Next: 01 Jul 2026", no final date row, sort-code "40-12-09 65872310", ref "Ref: RENT-FLAT12".

Card 2 — ISA Saver: badge Active (#C9E6FF/#004B6F), amount £200.00 GBP, frequency "Monthly on the 1st", next date "Next: 01 Jul 2026", no final date row, sort-code "60-16-13 31926819", ref "Ref: ISA-TOPUP".

Card 3 — PureGym: badge Active (#C9E6FF/#004B6F), amount £24.99 GBP, frequency "Monthly on the 15th", next date "Next: 15 Jul 2026", no final date row, sort-code "20-00-00 55512345", ref "Ref: GYM-MBR".

Card 4 — Oxfam GB: badge Inactive (#D3E5F5/#384956), amount £10.00 GBP, frequency "Monthly on the 28th", no next-date row (NextPaymentDateTime is null), final date row visible "Final: 28 Dec 2025", sort-code "08-60-01 20321982", ref "Ref: CHARITY-DON". The Inactive badge should appear visually subdued relative to the Active badge — the lighter background (#D3E5F5) and muted text (#384956) achieve this without requiring explicit opacity reduction.

Card 5 — Marcus Savings: badge Active (#C9E6FF/#004B6F), amount £50.00 GBP, frequency "Weekly every Friday", next date "Next: 04 Jul 2026", final date row visible "Final: 25 Dec 2026", sort-code "30-96-22 41227714", ref "Ref: SAVINGS-SWEEP".

**Bottom Nav:** Same as Loading frame. Accounts tab tinted #266489.

**Auto Layout — Content frame:**
- Direction: vertical
- Top app bar: fixed 64dp, fill width
- summary_row: fixed 32dp, fill width, padding h 16dp
- standing_orders_list: fill width, fill remaining height, clipped, scrollable vertically
  - Internal vertical Auto Layout: padding 16dp all sides, item-spacing 8dp
  - Each card: fill width, hug height, radius 12dp
    - Internal vertical Auto Layout: padding 16dp, item-spacing 4dp
    - name+badge row: horizontal, space-between, item-spacing 8dp
- Bottom nav: fixed 80dp, fill width

---

## Frame 3 — Empty State

Create a frame named "Standing Orders / Empty" at 393×852dp, background #F7F9FF.

**Top App Bar:** 64dp, #F7F9FF, back icon #266489, title "Standing Orders" titleLarge #181C20.

**Empty State Body:** In the remaining content area (852 − 64 − 80 = 708dp tall), vertically centre an empty-state composition. Horizontal padding is 32dp on each side, leaving 329dp of content width.

Place the Material Symbol `autorenew` at 48×48dp, tinted #41474D. Set contentDescription to "No standing orders" for accessibility export annotations.

Below the icon with a vertical gap of 16dp, place the title text "No standing orders" using headlineSmall (24sp/32sp w400 #181C20), centred, with a maximum width of 329dp.

Below the title with a vertical gap of 8dp, place the body text "No standing orders are set up for this account." using bodyMedium (14sp/20sp w400 #41474D), centred, with a maximum width of 329dp, allowing wrapping to two lines.

Do not place any call-to-action button on this empty state. Standing orders are read-only AIS data — there is no create action in this AISP app.

**Bottom Nav:** Same persistent bar, Accounts tab #266489.

**Auto Layout — Empty frame:**
- Direction: vertical
- Top app bar: fixed 64dp
- Content area: fill width, fill remaining height
  - Inner column: vertically centred within content area, horizontally centred, gap 16dp, padding h 32dp
    - icon: 48dp×48dp, centred
    - title: fill width, hug height, text-align centre
    - body: fill width, hug height, text-align centre
- Bottom nav: fixed 80dp

---

## Frame 4 — Error State

Create a frame named "Standing Orders / Error" at 393×852dp, background #F7F9FF.

**Top App Bar:** 64dp, #F7F9FF, back icon #266489, title "Standing Orders" titleLarge #181C20.

**Error State Body:** In the remaining 708dp content area, vertically centre the error composition. Horizontal padding is 32dp (329dp content width).

Place the Material Symbol `error_outline` at 48×48dp, tinted with error #BA1A1A. Set contentDescription to "Error loading standing orders".

Below the icon with a 16dp gap, place the title "Unable to load standing orders" using headlineSmall (24sp/32sp w400 #181C20), centred.

Below the title with an 8dp gap, place the error body text using bodyMedium (14sp/20sp w400 #41474D), centred. In the primary Figma frame, show the TokenExpiredError message as representative content: "Session expired. Please log in again." The design must accommodate any of the five error messages defined in `docs.yaml#error_cases` — the longest is "Too many requests. Please wait a moment and try again." which spans two lines at this width, so set the text height to hug content with a minimum of two lines reserved.

Below the error body with a 16dp gap, place the retry button. Use the M3 Filled Button component. Background: primary #266489. Label: "Try again" in labelLarge (14sp/20sp w500 #FFFFFF). Height: 48dp. Corner radius: 9999dp (full pill). Horizontal padding: 24dp inside the button. Minimum width: 200dp. Minimum touch target: 48dp height satisfied by the button itself.

**Component Variants for retry_button:**
- Default: bg #266489, label #FFFFFF
- Hovered: bg #266489 with an 8% #FFFFFF (onPrimary) state-layer overlay
- Pressed: bg primary at 88% opacity — M3 pressed state ripple in #FFFFFF at 12% opacity
- Focused: bg #266489 with 3dp focus ring in outline #72787E at 1dp offset
- Disabled: bg #41474D at 12% opacity, label #41474D at 38% opacity (not applicable here — button is always enabled in the error state)

**Bottom Nav:** Same persistent bar, Accounts tab #266489.

**Auto Layout — Error frame:**
- Identical structure to Empty frame
- Replace icon + texts + add retry_button below body with 16dp gap

---

## Component Variants Reference

### standing_order_card

Create a Figma component named `StandingOrderCard`. Expose the following properties:

- `payeeName` (text): the creditor name
- `status` (variant enum): `Active` | `Inactive`
- `amount` (text): formatted amount with currency, e.g. "£1,200.00 GBP"
- `frequency` (text): human-readable frequency string
- `showNextDate` (boolean): true for Active orders with a non-null NextPaymentDateTime
- `nextDate` (text): formatted next payment date
- `showFinalDate` (boolean): true when hasFinalPayment=true
- `finalDate` (text): formatted final payment date
- `sortCode` (text): Roboto Mono sort-code/account-number string
- `reference` (text): payment reference string

The `status` variant controls the badge appearance: Active uses #C9E6FF/#004B6F, Inactive uses #D3E5F5/#384956. No other structural change between variants — only the badge colours and text differ.

The card itself has no hover, pressed, or selected state — it is a read-only display component (AIS data, not interactive).

### so_status_badge

Create a Figma component named `StatusBadge`. Two variants: `Active` and `Inactive`. Both use pill shape (radius 9999). Internal horizontal padding 8dp. Height 24dp. The Active variant uses fill #C9E6FF and text #004B6F (labelSmall Roboto 11sp w500). The Inactive variant uses fill #D3E5F5 and text #384956 (labelSmall Roboto 11sp w500).

### progress_indicator (circular)

Use the standard M3 CircularProgressIndicator component. Set colour to primary #266489, stroke width 4dp, size 40dp. In Figma, create an indeterminate variant (rotating arc). No determinate variant needed for this screen.

### bottom_nav (persistent component)

Create a reusable `BottomNav` component used across all frames. Four tabs in a horizontal Auto Layout, space-between distribution, height 80dp, fill width, background #F7F9FF, top border 1dp #C1C7CE (outlineVariant). Each tab: vertical stack, centred, icon 24dp + label labelSmall 11sp, width 25% of parent. Selected tab: icon and label tinted primary #266489. Unselected: tinted #41474D.

For the standing-orders screen, the Accounts tab is set to selected state since the user arrived via the Accounts navigation hierarchy.

---

## Semantic Token → Figma Variable Mapping

Create a Figma variable collection named "Open Banking — Trust Blue" with the following bindings. All colour variables are in the `Color` group.

| Semantic token | Figma variable path | Resolved value |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/on-primary | #FFFFFF |
| primaryContainer | color/primary-container | #C9E6FF |
| onPrimaryContainer | color/on-primary-container | #004B6F |
| secondary | color/secondary | #50606E |
| onSecondary | color/on-secondary | #FFFFFF |
| secondaryContainer | color/secondary-container | #D3E5F5 |
| onSecondaryContainer | color/on-secondary-container | #384956 |
| error | color/error | #BA1A1A |
| onError | color/on-error | #FFFFFF |
| surface | color/surface | #F7F9FF |
| onSurface | color/on-surface | #181C20 |
| surfaceVariant | color/surface-variant | #DDE3EA |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outline-variant | #C1C7CE |
| surfaceContainerLow | color/surface-container-low | #F1F4F9 |

Create a separate `Typography` variable group with number variables for type sizes and line heights (sp values used directly as px in Figma at 1:1):

| Token | Figma variable | Value |
|---|---|---|
| titleLarge/size | typography/title-large-size | 22 |
| titleMedium/size | typography/title-medium-size | 16 |
| headlineSmall/size | typography/headline-small-size | 24 |
| bodyMedium/size | typography/body-medium-size | 14 |
| bodySmall/size | typography/body-small-size | 12 |
| labelMedium/size | typography/label-medium-size | 12 |
| labelLarge/size | typography/label-large-size | 14 |
| labelSmall/size | typography/label-small-size | 11 |

Create a `Shape` variable group:

| Token | Figma variable | Value (dp) |
|---|---|---|
| shape/medium | shape/corner-medium | 12 |
| shape/full | shape/corner-full | 9999 |
| screen/padding | layout/screen-padding | 16 |
| card/padding | layout/card-padding | 16 |
| list/gap | layout/list-gap | 8 |
| card/row-gap | layout/card-row-gap | 4 |

---

## Prototype Interaction Flow

Set up the following connections in Figma Prototype mode across the four frames:

**back_button (arrow_back icon, all frames):** On tap, navigate to the `account-detail` screen frame (Smart Animate, 300ms, ease-out). This reflects the `navigate_back` action with effect `navigate` declared in `ui.yaml`.

**pull-to-refresh gesture (standing_orders_list, Content frame):** Model as a drag-down interaction starting from the top of the list. On release, transition to the Loading frame (300ms dissolve), then back to Content after 1.5s. In Figma, use an Interaction of type "Drag" pointing to the Loading frame. This reflects the `retry_load` action triggered by `pull_to_refresh_action` on the list.

**retry_button (Error frame):** On tap, navigate to the Loading frame (Smart Animate, 150ms ease). After the loading animation, transition to the Content frame. This reflects the `retry_load` action with effect `call_api` re-triggering GET /accounts/{AccountId}/standing-orders via ktorfit.

**bottom_nav — Home tab:** On tap, navigate to the `home` screen frame (Smart Animate, 300ms ease-in-out).

**bottom_nav — Accounts tab:** On tap, navigate to the `accounts` screen frame (Smart Animate, 300ms ease-in-out).

**bottom_nav — Transactions tab:** On tap, navigate to the `transactions` screen frame (Smart Animate, 300ms ease-in-out).

**bottom_nav — More tab:** On tap, navigate to the `settings` screen frame (Smart Animate, 300ms ease-in-out).

The standing order cards themselves have no tap interaction — they are read-only AIS data display components. Do not add any tap interaction to card bodies.

---

## Accessibility Annotations

Annotate the Figma frames using the Figma Accessibility plugin or equivalent annotation layer with the following notes:

**back_button:** contentDescription = "Back" (or localised equivalent). Role: Button. Minimum touch target enforced at 48×48dp.

**progress_indicator (Loading):** Role: ProgressBar (indeterminate). contentDescription = "Loading standing orders". Set `importantForAccessibility = true`.

**summary_row:** Role: Text. Read by TalkBack/VoiceOver as "4 Active, 1 Inactive" (dot separator → comma for TTS clarity). Mark `importantForAccessibility = true`.

**standing_order_card:** Role: none (non-interactive). TalkBack merges all child text into a single traversal node. contentDescription on the card itself = "Standing order for {payeeName}". Inner text elements each have their own `contentDescription` as declared in `ui.yaml`.

**so_status_badge:** contentDescription = "Status: Active" or "Status: Inactive". Ensure WCAG AA contrast ratio ≥ 4.5:1 for text against badge background. Active badge: #004B6F on #C9E6FF = contrast ratio 7.2:1 (passes AA large and normal). Inactive badge: #384956 on #D3E5F5 = contrast ratio 5.1:1 (passes AA).

**so_sort_code:** contentDescription = "Sort code and account number: {value}". Roboto Mono prevents screen readers from reading run-together digits.

**empty_state icon (autorenew):** contentDescription = "No standing orders". Do not mark as decorative.

**error_state icon (error_outline):** contentDescription = "Error loading standing orders". Do not mark as decorative.

**retry_button:** contentDescription = "Try again to load standing orders". Role: Button. Minimum touch target: 48dp height (satisfied). Ensure contrast: #FFFFFF on #266489 = 4.8:1 (passes AA for large text; label is 14sp which qualifies as large per WCAG at w500).

**bottom_nav tabs:** Each tab: Role: Tab. Selected state announced as "selected". Minimum touch target per tab: 48dp height (satisfied by 80dp bar height).

All interactive touch targets must be at minimum 48×48dp per Material 3 accessibility guidelines and WCAG 2.1 Success Criterion 2.5.5.

---

## Additional Design Notes

**Elevation treatment:** Cards use M3 elevation level 1 (tonal elevation via surfaceContainerLow #F1F4F9). Avoid hard drop shadows on cards — tonal elevation matches the Open Banking minimalist-ui aesthetic (design_read.aesthetic_family = minimalist-ui, motion intensity = low).

**Roboto Mono for sort-codes:** Apply Roboto Mono to the `so_sort_code` field only. All other text uses Roboto. This aligns with the design-tokens.yaml declaration of Roboto Mono for amounts and account numbers, and aids scanability of the hyphenated UK sort-code format (e.g. "40-12-09 65872310").

**Status badge placement:** The badge floats right within the first card row, aligned to the centre of the payee name's line height. This avoids the badge anchoring to the top or bottom of the row regardless of payee name length.

**Final payment date row visibility:** The `so_final_date` row is conditionally rendered (Figma: use `showFinalDate` boolean component property to toggle). Never show a placeholder row or dash for orders without a final date — omit the row entirely. This keeps cards for indefinite standing orders compact.

**Inactive card treatment:** Inactive cards (SO-004) do not dim or grey-out the entire card. Only the badge colour changes (#D3E5F5/#384956). The payee name, amount, and other fields remain at full contrast — users may want to review past/inactive orders and should be able to read them clearly. This is intentional and aligns with the WCAG AA commitment in `design-tokens.yaml`.

**Pull-to-refresh colour:** The Material 3 `PullRefreshIndicator` uses primary #266489. No custom spinner artwork needed.

**Motion:** All transitions use the M3 emphasis easing `cubic-bezier(0.2, 0.0, 0, 1.0)` at 300ms (medium duration from design-tokens.yaml). `reduce_motion_supported: true` — in Figma prototype mode, note that production will substitute an instant cross-fade when the OS "Reduce Motion" setting is enabled.
