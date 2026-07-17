# PFM Dashboard — Figma Design Prompts

> Generated from: `screens/pfm-dashboard/ui.yaml` + `demo-data.yaml` + `design-tokens.yaml`
> Canvas spec: 393×852dp (Pixel 5), Material 3 light theme, Roboto font family
> Generated: 2026-07-17T06:00:00Z

---

## Design System Summary

**Theme:** Open Banking — Trust Blue (seed #266489, Material Theme Builder, M3 light mode)

**Resolved Colour Palette:**

| Role | Hex | Usage |
|---|---|---|
| primary | #266489 | Key actions, selected state, income bar, net worth amount, progress bars |
| onPrimary | #FFFFFF | Text/icons on primary surfaces |
| primaryContainer | #C9E6FF | Selected chip/tab fill |
| onPrimaryContainer | #004B6F | Text on primaryContainer |
| secondary | #50606E | Secondary text, net worth label |
| onSecondary | #FFFFFF | Text on secondary surfaces |
| error | #BA1A1A | Spend bar, credit card debit balance, error icon |
| background | #F7F9FF | Screen background |
| surface | #F7F9FF | Card surface fallback |
| surfaceContainerLow | #F1F4F9 | Card fill (elevation 1) |
| surfaceContainer | #EBEEF3 | Card fill (elevation 2), period selector unselected segment |
| surfaceVariant | #DDE3EA | Shimmer skeleton fill, divider |
| onSurface | #181C20 | Primary body text |
| onSurfaceVariant | #41474D | Secondary/hint text, section headers, unselected nav tabs |
| outline | #72787E | Chip outline, unselected segment border |
| outlineVariant | #C1C7CE | Subtle divider |

**Typography (Roboto):**

| Role | Size | Line | Weight | Usage |
|---|---|---|---|---|
| displaySmall | 36sp | 44sp | 400 | Net worth amount |
| headlineSmall | 24sp | 32sp | 400 | Empty/error state title |
| titleSmall | 14sp | 20sp | 500 | Section headers, insight title |
| bodyMedium | 14sp | 20sp | 400 | Body text |
| bodySmall | 12sp | 16sp | 400 | Account subtitle, insight body |
| labelMedium | 12sp | 16sp | 500 | Net worth label, net cashflow label |
| labelSmall | 11sp | 16sp | 500 | Bar chart axis labels |

**Spacing scale (4dp base):** xs=4dp, sm=8dp, md=12dp, lg=16dp, xl=24dp, 2xl=32dp
**Screen horizontal padding:** 16dp each side → content width 361dp on 393dp canvas
**Corner radius:** card=12dp, chip/pill=9999dp, progress=2dp, category row=8dp
**Minimum touch target:** 48dp (WCAG AA, regulated industry)

---

## Frame: Loading State

Create a frame sized 393×852dp. Set the background fill to #F7F9FF. Name this frame "PFM Dashboard / Loading".

**Top App Bar:** Place a Material 3 Small Top App Bar at the top of the frame spanning full width. Set its height to 56dp. Fill it with #F7F9FF. Add the title "My Finances" centred vertically, using Roboto 16sp/24sp weight 500, colour #181C20. Apply no trailing action icons. This bar should have a subtle bottom separator using outlineVariant #C1C7CE at 1dp thickness.

**Shimmer Skeleton Region:** Below the top app bar, create a vertical Auto Layout column with gap 16dp and horizontal padding of 16dp on each side. This column contains four skeleton placeholder rectangles that simulate the loading state using a shimmer animation.

The first skeleton block represents the net worth card. Draw a rounded rectangle 361dp wide and 120dp tall with corner radius 12dp. Fill it with surfaceVariant #DDE3EA. In production, this will pulse with a left-to-right gradient shimmer at 1.5 second duration. In Figma, represent the pulse using a subtle linear gradient from #DDE3EA to #E5E8ED to #DDE3EA at a 15-degree angle, simulating the mid-shimmer highlight pass.

The second skeleton block represents the spending versus income chart card. Draw a rounded rectangle 361dp wide and 80dp tall, corner radius 12dp, same shimmer fill #DDE3EA.

The third skeleton block represents the top categories list and section header combined. Draw a rounded rectangle 361dp wide and 200dp tall, corner radius 12dp, shimmer fill #DDE3EA. This block is taller to approximate the height of eight category rows plus their progress bars.

The fourth skeleton block represents the insights section. Draw a rounded rectangle 361dp wide and 80dp tall, corner radius 12dp, shimmer fill #DDE3EA.

**Auto Layout — loading skeleton column:**
Direction: vertical. Padding: top 16dp, right 16dp, bottom 16dp, left 16dp. Item spacing: 16dp. Alignment: fill container horizontally. Sizing: hug contents vertically.

**Bottom Navigation Bar:** Place a bottom nav bar at the very bottom of the frame, 393dp wide, 80dp tall. Fill it with #F7F9FF. Apply a 1dp top separator using outlineVariant #C1C7CE. Create four equal-width navigation items: Home (icon: home), Accounts (icon: account_balance), Transactions (icon: receipt_long), More (icon: more_horiz). Because the PFM Dashboard is not a primary navigation tab, none of the four items should be in the selected state. Render all four icons and labels in onSurfaceVariant #41474D. Label text: Roboto 12sp weight 400.

---

## Frame: Content State

Create a frame sized 393×852dp, background #F7F9FF. Name it "PFM Dashboard / Content". Because the content exceeds one screen height, mark this frame as a scrollable prototype screen; the actual rendered content column extends approximately 1400dp tall and clips to the 852dp viewport. The bottom navigation bar is fixed-position at the bottom of the viewport.

### Period Selector

Below the top app bar (56dp), place a segmented button component spanning the full content width (361dp, horizontal padding 16dp from screen edges). Height: 40dp. The segmented button has three segments of equal width.

The leftmost segment is labelled "7 days". The middle segment is labelled "30 days" and is in the selected state. The rightmost segment is labelled "3 months". Use Roboto 14sp weight 500.

For the selected segment ("30 days"): fill primaryContainer #C9E6FF, text colour onPrimaryContainer #004B6F, no outline stroke.
For unselected segments: fill surfaceContainer #EBEEF3, text colour onSurface #181C20, outline stroke 1dp outline #72787E.
Corner radius on the outer edges of the leftmost and rightmost segment: 9999dp (full pill). Interior shared edges: 0dp radius to form a continuous band. Item spacing: 0dp (flush segments).

**Auto Layout — period selector:**
Direction: horizontal. Item spacing: 0dp. Sizing: each segment fills equal width (hug label, then distribute equally). Height: fixed 40dp. Margin below: 12dp.

### Net Worth Card

Place a Material 3 Elevated Card below the period selector. Card width: 361dp (fills content width with 16dp screen padding). Corner radius: 12dp. Background fill: surfaceContainer #EBEEF3. Apply an elevation shadow of 3dp (M3 level 2) using a black scrim at very low opacity (approximately 8% opacity black shadow, 0px vertical offset, 3px blur, 1px spread). Padding inside the card: 16dp all sides.

Inside the card, use a vertical Auto Layout with item spacing 4dp.

Add the label "Net worth" using Roboto 12sp weight 500, colour secondary #50606E. This label has a top margin of 0dp.

Below the label, add the net worth amount "£14,955.45" using Roboto 36sp weight 400, colour primary #266489. This is the largest text element on the screen and serves as the visual anchor of the card.

Below the amount, add the subtitle "Across 3 accounts" using Roboto 12sp weight 400, colour onSurfaceVariant #41474D.

Insert a 1dp horizontal divider using outlineVariant #DDE3EA with vertical margin 8dp above and below.

Below the divider, add the account breakdown section as a vertical Auto Layout with item spacing 4dp. Create three compact list item rows. Each row is a horizontal Auto Layout, height 32dp, alignment center-vertical, with no outer padding (the card padding handles it).

Row one: label "Everyday Current" (Roboto 14sp weight 400 #181C20, flex weight 1) and trailing amount "£2,847.63" (Roboto 14sp weight 400 #181C20, align-end). Accessibility label: "Everyday current account balance £2,847.63".

Row two: label "ISA Saver" (Roboto 14sp weight 400 #181C20, flex weight 1) and trailing amount "£12,450.00" (Roboto 14sp weight 400 #181C20, align-end). Accessibility label: "ISA saver account balance £12,450.00".

Row three: label "Platinum Mastercard" (Roboto 14sp weight 400 #181C20, flex weight 1) and trailing amount "−£342.18" (Roboto 14sp weight 400 #BA1A1A error colour, align-end). The negative sign and the red colour together communicate that this is a liability reducing the total. Accessibility label: "Platinum Mastercard outstanding balance −£342.18".

**Auto Layout — net worth card content column:**
Direction: vertical. Padding: 16dp all sides. Item spacing: 4dp. Width: fixed 361dp. Height: hug contents (approximately 172dp).

### Spending vs Income Section Header

Below the net worth card (gap 16dp), add a section header label "Spending vs Income". Use Roboto 14sp weight 500, colour onSurfaceVariant #41474D. This label sits flush with the left content edge (16dp from screen edge), with margin bottom 8dp.

### Spending vs Income Card

Place an Elevated Card below the section header. Width: 361dp. Corner radius: 12dp. Background fill: surfaceContainerLow #F1F4F9. Elevation shadow: 1dp (M3 level 1). Padding: 16dp all sides.

Inside the card, use a vertical Auto Layout with item spacing 12dp.

**Bar Chart:** Create a horizontal container 329dp wide (card width minus 32dp padding) and 80dp tall for the dual-bar chart. Place two vertical bar groups side by side within a horizontal Auto Layout with item spacing 24dp and horizontal alignment centered.

Income bar group: a vertical stack with the label "Income" (Roboto 11sp weight 500 #41474D) at the bottom, the amount "£2,400.00" (Roboto 11sp weight 500 #41474D) below the label, and a filled rectangle 52dp wide above, filled with primary #266489. The income bar height represents the income value: for the 30-day period, income £2,400 is the taller bar. In the design render, set the income bar height to 56dp. Apply corner radius 4dp to the top two corners only (rounded cap on top).

Spend bar group: a vertical stack with the label "Spend" (Roboto 11sp weight 500 #41474D) at the bottom, the amount "£1,840.00" (Roboto 11sp weight 500 #41474D) below the label, and a filled rectangle 52dp wide above, filled with error #BA1A1A. Set the spend bar height to 43dp (proportional: 1840/2400 × 56dp ≈ 43dp). Apply corner radius 4dp to the top two corners only.

Both bar groups should be bottom-aligned within the chart container so that the baseline of the bars sits at the same y-position, allowing height differences to communicate the income/spend ratio visually.

**Net Cashflow Label:** Below the bar chart, add a single-line label with a leading checkmark icon (check_circle 16dp #266489) followed by the text "You saved £560.00 this period". Use Roboto 12sp weight 500, colour primary #266489. Horizontal Auto Layout, gap 4dp, alignment center-vertical.

**Auto Layout — spending income card:**
Direction: vertical. Padding: 16dp all sides. Item spacing: 12dp. Width: fixed 361dp. Height: hug (approximately 120dp).

### Top Spending Categories Section Header

Below the spending card (gap 16dp), add the section header label "Top spending categories". Roboto 14sp weight 500, colour onSurfaceVariant #41474D. Margin bottom 8dp.

### Category Rows

Create eight category rows in a vertical Auto Layout with item spacing 4dp. Each row is a list item with a tappable touch target. Each row has two parts: the list item row and a progress bar beneath it.

Structure each category row as a vertical Auto Layout containing:

Part one — the list item: a horizontal Auto Layout, height 48dp (minimum touch target), alignment center-vertical, padding left 0dp right 0dp. Contains a label text (Roboto 14sp weight 400 #181C20, flex weight 1), a supporting text showing the transaction count (Roboto 12sp weight 400 #41474D, flex weight 1), and a trailing amount (Roboto 14sp weight 400 #181C20, align-end).

Part two — the progress bar: a 4dp tall horizontal rectangle, corner radius 2dp. The filled portion uses colour primary #266489; the unfilled track uses surfaceVariant #DDE3EA. The filled width is a percentage of the total category row width (361dp content width minus 16dp padding if inside a padded container).

Render the eight category rows with the following data:

**Bills:** label "Bills", supporting "4 transactions", trailing "£1,356.00". Progress bar fill width: 73.7% of track width. This is the dominant category — its progress bar spans nearly three quarters of the available width, giving an immediate visual signal that bills are the primary spend driver.

**Groceries:** label "Groceries", supporting "9 transactions", trailing "£198.00". Progress fill: 10.8%.

**Dining:** label "Dining", supporting "5 transactions", trailing "£88.00". Progress fill: 4.8%.

**Subscriptions:** label "Subscriptions", supporting "5 transactions", trailing "£63.00". Progress fill: 3.4%.

**Transport:** label "Transport", supporting "8 transactions", trailing "£41.00". Progress fill: 2.2%.

**Entertainment:** label "Entertainment", supporting "3 transactions", trailing "£32.00". Progress fill: 1.7%.

**Health:** label "Health", supporting "2 transactions", trailing "£22.00". Progress fill: 1.2%.

**Other:** label "Other", supporting "6 transactions", trailing "£40.00". Progress fill: 2.2%.

For Bills, the five categories below (Subscriptions through Other) with percentages under 4% will have visually short progress bars — 1dp to 14dp filled width — which is intentional and communicates relative magnitude honestly.

**View All Button:** After the last category row, place a text button "View all categories" right-aligned. Roboto 12sp weight 500, colour primary #266489. Height: 36dp, horizontal padding: 8dp. This button navigates to spending-by-category with no category pre-filter.

**Auto Layout — categories column:**
Direction: vertical. Padding: left 16dp, right 16dp. Item spacing: 4dp. Width: match parent. Height: hug.

### Insights Section Header

Below the view all button (gap 8dp), place the section header label "Insights". Roboto 14sp weight 500, onSurfaceVariant #41474D. Margin bottom 8dp.

### Insight Cards

Create three insight cards in a vertical Auto Layout with item spacing 8dp. Each card is an Elevated Card: width 361dp, corner radius 12dp, background surfaceContainerLow #F1F4F9, elevation shadow 1dp. Padding inside: 16dp all sides.

Inside each card, use a horizontal Auto Layout with item spacing 12dp and alignment top.

Place the icon at 20dp × 20dp on the left. All three icons use primary #266489 as the fill colour.

On the right of the icon, use a vertical Auto Layout with item spacing 4dp and flex weight 1.

**Insight card one — Dining is up this month:**
Icon: trending_up (20dp #266489). Title: "Dining is up this month" (Roboto 14sp weight 500 #181C20). Body: "You spent £88 on dining in the last 30 days, 14% more than the prior period (£77)." (Roboto 12sp weight 400 #41474D, max lines: 3).

**Insight card two — Healthy savings rate:**
Icon: thumb_up (20dp #266489). Title: "Healthy savings rate" (Roboto 14sp weight 500 #181C20). Body: "You saved £560 this period — 23% of your income. Great work, Priya!" (Roboto 12sp weight 400 #41474D).

**Insight card three — Transport spending down:**
Icon: trending_down (20dp #266489). Title: "Transport spending down" (Roboto 14sp weight 500 #181C20). Body: "Transport costs fell to £41 from £51 last month — £10 saved on your commute." (Roboto 12sp weight 400 #41474D).

**Auto Layout — each insight card:**
Direction: horizontal. Padding: 16dp all sides. Item spacing: 12dp. Width: fixed 361dp. Height: hug (approximately 80–88dp per card).

### Quick Navigation Chip Group

Below the insight cards (gap 12dp), place a horizontally scrollable chip group. Create three Assist Chips (Material 3) in a horizontal Auto Layout with item spacing 8dp and left padding 16dp. This row overflows the screen width horizontally — clip the right edge to signal horizontal scrollability with a fade gradient (transparent to #F7F9FF, 32dp wide, anchored to the right content edge).

Each chip: height 32dp, horizontal padding 12dp, corner radius 9999dp (full pill). Outline stroke 1dp, colour outline #72787E. Background: transparent. Icon 18dp #41474D, label Roboto 14sp weight 500 #181C20.

**Chip one:** icon pie_chart, label "By category". Accessibility label: "Go to spending by category". Taps navigate to spending-by-category (no category filter).

**Chip two:** icon savings, label "Budgets". Accessibility label: "Go to budgets". Taps navigate to budgets screen.

**Chip three:** icon autorenew, label "Subscriptions". Accessibility label: "Go to recurring subscriptions". Taps navigate to recurring-subscriptions screen.

**Auto Layout — chip group:**
Direction: horizontal. Padding left 16dp, right 16dp. Item spacing: 8dp. Height: hug (32dp chip + 8dp vertical padding = 48dp row). Overflow: horizontal scroll. Bottom margin: 32dp (clears bottom nav bar).

---

## Frame: Empty State

Create a frame 393×852dp, background #F7F9FF. Name it "PFM Dashboard / Empty".

Place the same top app bar (56dp, title "My Finances") and the same bottom nav bar (80dp, unselected) as in the content frame.

Between the top app bar and the bottom nav bar, vertically centre an empty state illustration group. Pad this group 32dp horizontally.

**Empty state icon:** Place a Material icon bar_chart at 48dp × 48dp, colour onSurfaceVariant #41474D, centred horizontally. The icon communicates that this is a data visualisation screen with no data to show yet. Content description: "No spending data available".

**Title:** Below the icon with a gap of 16dp, place the heading "No transaction data yet". Roboto 24sp weight 400, colour onSurface #181C20, text-align centre.

**Body:** Below the title with a gap of 8dp, place the body text: "Your spending overview will appear once your transactions are loaded from the AIS connection." Roboto 14sp weight 400, colour onSurfaceVariant #41474D, text-align centre, max width 329dp (screen width minus 32dp per side).

There is no retry or call-to-action button in the empty state. EC-PFM-001 (empty cache) is not an error condition — data populates automatically as the AIS connection syncs transactions in the background. The design should communicate patience rather than urgency.

**Auto Layout — empty state group:**
Direction: vertical. Alignment: center-horizontal. Item spacing: variable (16dp below icon, 8dp below title). Height: hug. Vertically position this group at the midpoint of the available space between the top app bar and bottom nav bar (approximately y=330dp from top of frame).

---

## Frame: Error State

Create a frame 393×852dp, background #F7F9FF. Name it "PFM Dashboard / Error".

Place the same top app bar (56dp, "My Finances") and bottom nav bar (80dp, unselected) as in other frames.

Between the app bar and the bottom nav, vertically centre the error state group with 32dp horizontal padding.

**Error icon:** Place a Material icon warning_amber at 48dp × 48dp, colour error #BA1A1A, centred horizontally. Content description: "Error loading finances".

**Title:** Below the icon with gap 16dp, place the heading "Could not load your finances". Roboto 24sp weight 400, colour onSurface #181C20, text-align centre.

**Body:** Below the title with gap 8dp, place body text: "Something went wrong while computing your finances overview. Please try again." Roboto 14sp weight 400, colour onSurfaceVariant #41474D, text-align centre, max width 329dp.

**Retry Button — pfm_error_retry_button:** Below the body with gap 24dp, place a filled button. Name this component "pfm_error_retry_button" in the Figma layer panel. Height: 56dp. Width: 261dp (screen width minus 64dp each side). Corner radius: 9999dp (full pill). Background fill: primary #266489. Label: "Try again" (resolves `{strings.pfm_dashboard.error.retry}`), Roboto 14sp weight 500, colour onPrimary #FFFFFF, centred. This button (id: pfm_error_retry_button) triggers the `reloadFinances` action dispatched via kotlinx-coroutines, which re-dispatches `loadFinancesOverview` using the previously selected period, moving the screen from error → loading → content | empty | error. action_contract: effect=transform_state, external_library_refs=[kotlinx-coroutines].

**Auto Layout — error state group:**
Direction: vertical. Alignment: center-horizontal. Item spacing: variable (16dp below icon, 8dp below title, 24dp above button). Width: fixed 329dp. Height: hug. Vertically centre within available viewport space.

---

## Auto Layout Specifications Summary

| Frame / Component | Direction | Padding | Item Spacing | Sizing |
|---|---|---|---|---|
| Screen scroll column | vertical | h:16dp, top:0dp | 16dp between sections | fill width, hug height (scrollable) |
| Period selector | horizontal | v:0dp, h:0dp | 0dp (flush) | fill width, fixed 40dp height |
| Net worth card | vertical | 16dp all | 4dp | fixed 361dp wide, hug height |
| Account breakdown rows | horizontal | 0dp | 8dp | fill width, fixed 32dp height |
| Spending/income card | vertical | 16dp all | 12dp | fixed 361dp wide, hug height |
| Bar chart group | horizontal | 0dp | 24dp | fill width, fixed 80dp height |
| Category rows column | vertical | h:16dp, v:0dp | 4dp | fill width, hug height |
| Category row item | horizontal | v:0dp, h:0dp | 8dp | fill width, fixed 48dp height |
| Insight cards column | vertical | h:16dp, v:0dp | 8dp | fill width, hug height |
| Each insight card | horizontal | 16dp all | 12dp | fixed 361dp wide, hug height |
| Insight text stack | vertical | 0dp | 4dp | fill width, hug height |
| Chip group row | horizontal | h:16dp, v:8dp | 8dp | fill width (h-scroll), hug height |
| Empty / error group | vertical | h:32dp | varies | fixed 329dp wide, hug height |

---

## Component Variants

**Period Selector Segment:**
Default (unselected): bg #EBEEF3, text #181C20, outline #72787E 1dp, corner varies by position.
Hovered: bg #E5E8ED, text #181C20.
Pressed: bg #C9E6FF + 12% onPrimary overlay.
Selected: bg #C9E6FF, text #004B6F, no outline, leading check-mark icon (18dp #004B6F).
Focused: bg #EBEEF3 + 12% primary outline ring #266489 2dp.
Disabled: opacity 38%.

**Category Row:**
Default: bg transparent, text #181C20, supporting text #41474D.
Hovered: bg surfaceContainerHigh #E5E8ED overlay.
Pressed: bg ripple #266489 at 12% opacity.
Focused: outline ring #266489 2dp.
Progress bar unfilled track: #DDE3EA. Filled portion: #266489.

**Insight Card:**
Default: bg #F1F4F9, elevation 1dp shadow.
Pressed: bg #E5E8ED, elevation 0.
Focused: outline ring 2dp #266489.
(Insight cards are display-only — they are not tappable in the current spec.)

**Quick Nav Chip:**
Default: bg transparent, outline #72787E 1dp, icon+label #41474D, radius 9999dp.
Hovered: bg surfaceVariant #DDE3EA.
Pressed: bg surfaceContainerHigh #E5E8ED.
Focused: outline #266489 2dp.
No selected state (these are navigation triggers, not toggles).

**Retry Button — pfm_error_retry_button (error state):**
Default: bg #266489, label #FFFFFF.
Hovered: bg #266489 + 8% onPrimary overlay (#FFFFFF at 8% = lightened).
Pressed: bg #266489 + 12% onPrimary overlay.
Focused: bg #266489 + outline ring 2dp onPrimary #FFFFFF.
Disabled: bg #266489 at 38% opacity, label #FFFFFF at 38% opacity.
Component id: pfm_error_retry_button. action_contract: effect=transform_state, external_library_refs=[kotlinx-coroutines].

---

## Semantic Token → Figma Variable Mapping

Create a Figma local variable collection named "Open Banking / M3 Light" with the following mappings. These variables should be used for all component fills, strokes, and text colours throughout the design file.

| Semantic Token | Figma Variable Name | Hex Value |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/on-primary | #FFFFFF |
| primaryContainer | color/primary-container | #C9E6FF |
| onPrimaryContainer | color/on-primary-container | #004B6F |
| secondary | color/secondary | #50606E |
| error | color/error | #BA1A1A |
| background | color/background | #F7F9FF |
| surface | color/surface | #F7F9FF |
| surfaceContainerLow | color/surface-container-low | #F1F4F9 |
| surfaceContainer | color/surface-container | #EBEEF3 |
| surfaceContainerHigh | color/surface-container-high | #E5E8ED |
| surfaceVariant | color/surface-variant | #DDE3EA |
| onSurface | color/on-surface | #181C20 |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outline-variant | #C1C7CE |

Create a second variable collection "Open Banking / Typography" mapping each type role to the Roboto family with the correct size, line height, and weight as documented in the Design System Summary above.

---

## Prototype Interaction Flow

Set up the following prototype connections in Figma to demonstrate the PFM Dashboard's navigation behaviour.

**On initial load:** The prototype starts on the "PFM Dashboard / Loading" frame. After a simulated 1.5-second delay (or on a tap/click trigger), transition to "PFM Dashboard / Content" using a Dissolve transition, 300ms, standard easing.

**Period selector — tap "7 days":** From "PFM Dashboard / Content", on tap of the "7 days" segment, create a Smart Animate transition to a variant of the content frame where the income and spend bars reflect the 7-day data (£240 income, £184 spend proportionally, or a simplified loading → content loop). Duration: 150ms. This simulates the selectPeriod action re-triggering loadFinancesOverview.

**Period selector — tap "3 months":** Similarly, connect the "3 months" segment to a 3-month variant of the content frame.

**Category row tap (Bills):** On tap of the Bills category row, navigate to the spending-by-category screen prototype frame with an Slide In (right) transition, 300ms. Pass category: "Bills" as a prototype text variable if using Figma's variable-based prototyping.

**Category row tap (all other categories):** Apply the same Slide In (right) transition to all eight category rows, each pointing to the spending-by-category prototype frame. The category parameter differs per row.

**View all categories button:** On tap, navigate to the spending-by-category frame with no category pre-filter. Slide In (right) 300ms.

**Chip — By category:** On tap, navigate to the spending-by-category frame. Slide In (right) 300ms.

**Chip — Budgets:** On tap, navigate to the budgets screen prototype frame. Slide In (right) 300ms.

**Chip — Subscriptions:** On tap, navigate to the recurring-subscriptions prototype frame. Slide In (right) 300ms.

**Error state — pfm_error_retry_button:** On tap of "Try again" (layer: pfm_error_retry_button), transition to "PFM Dashboard / Loading" with a Dissolve 300ms, then auto-advance to "PFM Dashboard / Content" after 1.5 seconds. This simulates the reloadFinances() → loadFinancesOverview(selectedPeriod) retry cycle, dispatched via kotlinx-coroutines (action_contract: effect=transform_state).

**Bottom nav — Home:** On tap of the Home icon, navigate to the Home screen frame with no transition animation (instant) — the PFM Dashboard was reached from the Home screen, so back navigation restores the Home state.

---

## Accessibility Specifications

All interactive components must meet the following requirements. Document these in a dedicated "Accessibility" section on your Figma annotation overlay.

**Minimum touch target:** Every tappable element must have a minimum hit area of 48dp × 48dp. This applies to category rows (which are at least 48dp tall combining the list item row and the progress bar), the view all button (add 6dp invisible padding above and below to reach 48dp), and the chips (add 8dp invisible padding above and below the 32dp chip height).

**Content descriptions:** Every non-decorative icon must have a content description assigned in the accessibility annotation. Use the format listed in the Component Hierarchy sections above. Decorative icons (such as the insight card icons that are adjacent to descriptive text) should be marked as `decorative: false` only when they add semantic meaning beyond the adjacent text — in practice all three insight icons (trending_up, thumb_up, trending_down) convey trend direction that the text also describes, so mark them decorative but retain contentDescription for screen reader verbosity preference.

**Colour contrast:** Verify WCAG AA compliance for all text. Key pairs to check: primary #266489 on background #F7F9FF (contrast ratio ≥ 4.5:1 for small text — #266489 on #F7F9FF achieves approximately 4.6:1, just passing AA); error #BA1A1A on #F7F9FF for the credit card trailing text (contrast ≥ 4.5:1 — #BA1A1A achieves approximately 4.8:1); onSurface #181C20 on all surface backgrounds (high contrast ≥ 10:1 — passes AAA).

**Progress bars:** Each progress bar must have an accessible label describing both the category name and its percentage. Example: "Bills represents 73.7% of total spending". This information should also be conveyed in the list item label and trailing amount text to ensure it is available without requiring the user to navigate to the progress bar separately.

**Segment accessibility:** The period selector segmented button must announce itself as a radio group with three radio buttons. The selected option must announce its selected state. Example VoiceOver announcement: "30 days, selected, 2 of 3".

**Net worth amount:** Announce as "Net worth £14,955.45". The display-size text is intentionally large to draw visual attention, but screen readers must read it as a labelled monetary amount.

**Scrollable region:** Mark the content column as a scrollable region. Screen readers should announce that additional content is available by scrolling.

**Reduce-motion:** When the user has enabled reduced-motion at the OS level, replace the shimmer animation with a static fill at surfaceVariant #DDE3EA. All Dissolve/Slide transitions in the prototype should collapse to an instant swap.
