# Recurring Subscriptions — Figma Design Prompts

> Generated from `screens/recurring-subscriptions/ui.yaml`
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Roboto
> Design system: Open Banking — Trust Blue (seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Canvas and Design System Foundation

The Recurring Payments screen targets a 393×852dp canvas, matching the Pixel 5 reference device for the Mifos Open Banking application. All measurements in this document are in density-independent pixels (dp) and scalable pixels (sp). Set up a single Figma frame at 393×852dp for each screen state, enabling Auto Layout in vertical mode. Roboto is the sole type family; import Roboto Regular (400), Roboto Medium (500), and Roboto Mono Regular for currency display.

The Material 3 light theme governs the entire palette. The seed colour is Trust Blue at #266489 (primary). The background is #F7F9FF across all states. This screen does not use any gradients, background imagery, or illustrations — it is a clean data display surface appropriate for a regulated Open Banking AISP context.

---

## Resolved Colour Palette

| Token name | Hex value | Primary usage on this screen |
|---|---|---|
| primary | #266489 | Autorenew icon tint in list rows; back-button active state |
| on-primary | #FFFFFF | Text/icons placed on primary-coloured backgrounds |
| primary-container | #C9E6FF | Pressed state overlay on subscription rows (12% opacity) |
| on-primary-container | #004B6F | Text on primary container surfaces |
| secondary | #50606E | Summary label text ("Estimated monthly spend") |
| error | #BA1A1A | Summary amount (£85.93) and error state icon |
| surface | #F7F9FF | Screen background, top app bar, card fills, bottom nav bar |
| on-surface | #181C20 | Merchant name labels, all primary text, trailing amounts |
| surface-variant | #DDE3EA | Shimmer skeleton base colour; detected-notice banner background |
| on-surface-variant | #41474D | Supporting text (cadence, next date), body copy, inactive nav tabs |
| outline | #72787E | Retry button border, list hairline dividers |
| outline-variant | #C1C7CE | Subtle card borders, divider lines between list items |
| surface-container | #EBEEF3 | Detected badge chip background |
| surface-container-low | #F1F4F9 | Low-elevation card alternative |
| surface-container-highest | #E0E3E8 | Shimmer shimmer highlight end colour |

---

## Roboto Type Scale

| Role | Size | Line height | Weight | Usage |
|---|---|---|---|---|
| titleLarge | 22sp | 28sp | 400 | Top app bar title "Recurring Payments" |
| headlineMedium | 28sp | 36sp | 400 | Summary amount "£85.93" |
| headlineSmall | 24sp | 32sp | 400 | Empty and error state titles |
| titleMedium | 16sp | 24sp | 500 | Subscription row merchant name |
| bodyMedium | 14sp | 20sp | 400 | Detected-notice banner message; error body text; trailing amounts |
| bodySmall | 12sp | 16sp | 400 | Supporting text (cadence + next date); summary count |
| labelMedium | 12sp | 16sp | 500 | Summary card label "Estimated monthly spend" |
| labelLarge | 14sp | 20sp | 500 | Retry button label "Try again" |
| labelSmall | 11sp | 16sp | 500 | Detected badge chip label "Detected" |

---

## Semantic Token to Figma Variable Mapping

In the Figma file, create a local variable collection named `md/sys/color` with the following bindings. This allows the design to be switched between light and dark modes by swapping the variable set without touching any frames.

| Semantic token | Figma variable path | Resolved light value |
|---|---|---|
| color/primary | md/sys/color/primary | #266489 |
| color/on-primary | md/sys/color/on-primary | #FFFFFF |
| color/primary-container | md/sys/color/primary-container | #C9E6FF |
| color/secondary | md/sys/color/secondary | #50606E |
| color/error | md/sys/color/error | #BA1A1A |
| color/background | md/sys/color/background | #F7F9FF |
| color/surface | md/sys/color/surface | #F7F9FF |
| color/on-surface | md/sys/color/on-surface | #181C20 |
| color/surface-variant | md/sys/color/surface-variant | #DDE3EA |
| color/on-surface-variant | md/sys/color/on-surface-variant | #41474D |
| color/outline | md/sys/color/outline | #72787E |
| color/outline-variant | md/sys/color/outline-variant | #C1C7CE |
| color/surface-container | md/sys/color/surface-container | #EBEEF3 |
| radius/small | md/sys/shape/small | 8dp |
| radius/medium | md/sys/shape/medium | 12dp |
| radius/large | md/sys/shape/large | 16dp |
| radius/full | md/sys/shape/full | 9999dp |
| spacing/screen-padding | spacing/screen-padding | 16dp |
| spacing/card-padding | spacing/card-padding | 16dp |
| elevation/level1 | md/sys/elevation/level1 | 1dp (shadow y=1 blur=3 #000000 10%) |

---

## Frame 1 — Recurring Payments: Loading State

Create a new Figma frame at 393×852dp. Set the fill to #F7F9FF. Name this frame "Recurring Payments / Loading".

### Top App Bar

At the very top of the frame, create a horizontal Auto Layout container at full width (393dp) and 64dp in height. Fill it with #F7F9FF. Add no drop shadow on the loading state — the top app bar is flush with the screen. On the leading edge (left, 16dp from the frame edge), place a Material icon button for navigation: use the arrow_back icon at 24×24dp, fill #181C20. Wrap the icon in a transparent 48×48dp bounding box to ensure the minimum touch target. Label this element "back_button" with an accessibility annotation: "Navigate back". To the right of the icon (gap 16dp), add a text label: "Recurring Payments" in Roboto Regular 22sp, line height 28sp, colour #181C20. This is the titleLarge role.

### Shimmer Skeleton

Below the app bar, set up a vertical Auto Layout column taking the remaining height above the bottom navigation bar. Apply 16dp padding on all four sides and set the gap between children to 8dp.

Inside this column, place five skeleton placeholder rows. Each row is a rounded rectangle at full container width minus 32dp of horizontal margin (the column handles this via padding), so effectively 361dp wide, 72dp tall, corner radius 8dp. Fill each row with #DDE3EA.

In Figma, apply a Smart Animate effect that shifts the fill between #DDE3EA and #E5E8ED over a 1.5-second loop using ease-in-out easing, creating the shimmer pulse. Stack all five rows with 8dp vertical gap. These rows simulate the list items that will appear in the loaded content state — they intentionally match the 72dp height of real subscription rows so the transition feels spatially anchored.

Add an annotation to the skeleton group: "For users with Reduce Motion enabled, all five rows render as a static #DDE3EA fill with no animation. A screen-reader-only label announces: 'Loading recurring payments'."

### Bottom Navigation Bar

Anchor a 393×80dp horizontal container to the bottom of the frame. Fill it with #F7F9FF. Inside, place four navigation items with equal weight (each approximately 98dp wide), arranged horizontally with no gap. Each item contains a 24×24dp icon centred above a 12sp label:

Item 1 — Home: icon `home`, label "Home", tint #41474D (on-surface-variant). Not selected.
Item 2 — Accounts: icon `account_balance`, label "Accounts", tint #41474D. Not selected.
Item 3 — Transactions: icon `receipt_long`, label "Transactions", tint #41474D. Not selected.
Item 4 — More: icon `more_horiz`, label "More", tint #41474D. Not selected.

None of these tabs is selected on the Recurring Payments screen. This screen is reached by drilling from the PFM dashboard or the More tab destination, and it does not correspond to a primary tab.

**Auto Layout specification — Frame 1:**
Direction: vertical. No internal padding on the frame itself; the top app bar, scroll body, and bottom nav stack in sequence. The scroll body column: padding 16/16/16/16, gap 8dp. The skeleton column fills the remaining vertical space between app bar and bottom nav.

---

## Frame 2 — Recurring Payments: Content State (7 Subscriptions)

Duplicate Frame 1 and rename to "Recurring Payments / Content". Replace the shimmer skeleton with the content described below. Retain the top app bar and bottom navigation bar unchanged.

### Detected Notice Banner

Immediately below the top app bar (8dp gap), place a horizontal Auto Layout container that functions as an informational banner. Set the fill to #DDE3EA (surfaceVariant). Apply a corner radius of 12dp and 12dp padding on all four sides. Set horizontal margins of 16dp from the frame edges, giving an effective width of 361dp. Allow height to hug its content (approximately 56dp with a single wrapped line of text).

On the leading side, place an `info_outline` icon at 20×20dp using fill colour #41474D. Set gap 8dp between the icon and the text. The text reads: "Detected by analysing your past transactions. Not from the bank." Style it as bodyMedium: Roboto Regular 14sp, line height 20sp, colour #41474D. Allow this text to wrap to two lines if needed at 361dp width. The entire banner is display-only — mark it as not interactive. Add an accessibility label to the banner container: "These payments were detected by analysing your transaction history. They are not bank-registered mandates."

### Summary Card

Below the banner (8dp gap), place a Material 3 card component. Use a fill of #F7F9FF and apply elevation level 1, expressed as a drop shadow: x=0, y=1, blur=3dp, spread=0, colour #000000 at 10% opacity. Set corner radius to 12dp, padding 16dp on all sides, and horizontal margins of 16dp (width 361dp). Height should hug content, approximately 84dp.

Inside the card, create a vertical Auto Layout with a gap of 4dp between the three child text elements.

The first child is the descriptor label: "Estimated monthly spend" in labelMedium — Roboto Medium 12sp, line height 16sp, colour #50606E (secondary). This secondary colour positions the label as a supporting annotation below the main figure.

The second child is the main financial figure: "£85.93" in headlineMedium — Roboto Regular 28sp, line height 36sp, colour #BA1A1A (error). Using the error red for the subscription total is intentional and consistent with how debit amounts appear throughout the Open Banking app: red signals an outgoing cost. This creates cross-screen colour semantics without introducing confusion, because the value is accompanied by the "Estimated monthly spend" label. Consider using Roboto Mono Regular 28sp for this amount if Mono is available in the design system, to align with the monetary typography used in balance displays. Add an accessibility annotation to this element: "Total estimated monthly spend: £85.93 across 7 subscriptions detected."

The third child is the subscription count: "7 subscriptions detected" in bodySmall — Roboto Regular 12sp, line height 16sp, colour #41474D. This grounds the headline figure by providing the number of patterns that contribute to it.

### Subscription List

Below the summary card (8dp gap from the card's bottom edge), render the seven subscription list items as a scrollable vertical list. The list has no explicit padding of its own — each item spans the full 393dp width, relying on internal padding for horizontal breathing room.

Each subscription row is a Material 3 list item using the two-line-with-supporting-text variant. Set each row to a minimum height of 72dp. The row itself is a horizontal Auto Layout with 16dp leading and trailing padding, 12dp top and bottom padding, and a 16dp gap between its three main elements: the leading icon, the content column, and the trailing text. Set alignment to center-vertical across all three elements.

**Leading icon:** Place an `autorenew` icon at 24×24dp using fill #266489 (primary). This icon is decorative in terms of information (the "Detected" badge carries the semantic meaning), but its primary-blue colour creates a visual rhythm down the list that connects all recurring items. Expand the touch area to at least 48×48dp by applying a transparent overlay.

**Content column:** Create a vertical Auto Layout with gap 2dp set to fill remaining horizontal space (use "grow" in Figma's horizontal resizing). Inside, place the merchant name as a single-line text in titleMedium — Roboto Medium 16sp, line height 24sp, colour #181C20 — with max lines set to 1 and end-ellipsis overflow. Below it, add the supporting text combining cadence and next expected date in bodySmall — Roboto Regular 12sp, line height 16sp, colour #41474D. Below the supporting text, place the Detected badge chip.

**Detected badge chip:** This is a Material 3 assist chip used in a display-only capacity. Create a pill-shaped container with fill #EBEEF3 (surfaceContainer), corner radius 9999dp, horizontal padding 8dp, vertical padding 4dp, height 24dp. Inside, add the label "Detected" in labelSmall — Roboto Medium 11sp, line height 16sp, colour #181C20. The chip has no interactive states — it is purely a visual indicator that the pattern was detected algorithmically rather than sourced from the bank's standing-order API. Add an accessibility label: "Detected by in-app analysis". The neutral surfaceContainer fill deliberately avoids primary or secondary tonal colours to signal that this is an inference, not a confirmed bank mandate.

**Trailing amount:** Right-align the subscription amount text in bodyMedium — Roboto Regular 14sp, line height 20sp, colour #181C20. Set horizontal resizing to "fixed" at approximately 64dp to accommodate up to £143.88 without wrapping.

Render all seven subscription rows in the following order, reflecting the sorting by monthly_equivalent descending as computed by the RecurringSubscriptionsViewModel:

Row 1 — PureGym: autorenew icon #266489 | label "PureGym" | supporting "Monthly · Next 15 Jul 2026" | badge "Detected" | trailing "£24.99". Accessibility: "PureGym: £24.99 Monthly, next 15 Jul 2026".

Row 2 — Spotify: label "Spotify" | supporting "Monthly · Next 12 Jul 2026" | trailing "£11.99". Accessibility: "Spotify: £11.99 Monthly, next 12 Jul 2026".

Row 3 — Adobe Lightroom: label "Adobe Lightroom" | supporting "Annual · Next 14 Dec 2026" | trailing "£143.88". Note that this row displays the full annual charge of £143.88, not the monthly equivalent of £11.99. The "Annual" cadence label in the supporting text provides the user with accurate context about what they will actually see debited from their account. Accessibility: "Adobe Lightroom: £143.88 Annual, next 14 Dec 2026".

Row 4 — Netflix: label "Netflix" | supporting "Monthly · Next 8 Jul 2026" | trailing "£10.99". Accessibility: "Netflix: £10.99 Monthly, next 8 Jul 2026".

Row 5 — Amazon Prime: label "Amazon Prime" | supporting "Monthly · Next 20 Jul 2026" | trailing "£8.99". Accessibility: "Amazon Prime: £8.99 Monthly, next 20 Jul 2026".

Row 6 — Apple TV+: label "Apple TV+" | supporting "Monthly · Next 1 Jul 2026" | trailing "£8.99". Accessibility: "Apple TV+: £8.99 Monthly, next 1 Jul 2026".

Row 7 — Disney+: label "Disney+" | supporting "Monthly · Next 3 Jul 2026" | trailing "£7.99". Accessibility: "Disney+: £7.99 Monthly, next 3 Jul 2026".

Between each consecutive pair of rows, optionally insert a hairline divider at 1dp height, fill #C1C7CE (outlineVariant). Inset the divider by 56dp from the left (aligning with the start of the content column, past the autorenew icon and its gap) to follow Material 3 list divider conventions. These dividers are decorative and should be hidden from assistive technologies.

**Auto Layout specification — Content Frame scroll body:**
Direction: vertical. Padding: top 8dp, left 0dp, right 0dp, bottom 24dp. Gap: 0dp between the banner, card, and list (each element manages its own horizontal margin and vertical spacing via its own padding and margin properties). The LazyColumn fills the space between the top app bar and the bottom navigation bar and scrolls vertically when content exceeds the visible area.

---

## Frame 3 — Recurring Payments: Empty State

Duplicate Frame 1 and rename to "Recurring Payments / Empty". Remove the shimmer skeleton and replace the scroll body with a centred empty-state composition. Retain the top app bar and bottom navigation bar.

### Empty State Composition

Create a vertical Auto Layout container that fills the horizontal width of the scroll body (393dp minus 32dp horizontal padding = 329dp effective content width) and is centred vertically within the scroll body area, at approximately y=250dp from the top of the frame (accounting for the 64dp app bar). Apply 32dp left and right padding to the container and set alignment to center-horizontal. Gap between children is 16dp.

First child: an `autorenew` icon at 48×48dp, fill #41474D (on-surface-variant). This is the same icon used in the list rows, intentionally reused to associate the empty state with the concept of recurring payments. It appears at a larger illustrative size here. Mark it as non-decorative with contentDescription "No recurring payments found". Add 16dp bottom margin after the icon.

Second child: the headline title in headlineSmall — Roboto Regular 24sp, line height 32sp, colour #181C20, text alignment centre. Text reads: "No recurring payments found".

Third child: the body paragraph in bodyMedium — Roboto Regular 14sp, line height 20sp, colour #41474D, text alignment centre. Allow wrapping up to 6 lines at the effective content width. Text reads: "We didn't detect any recurring payment patterns in your transactions. Once you have more history, patterns such as streaming, gym, and software subscriptions will appear here."

There are no action buttons in the empty state. The detection algorithm runs automatically over cached data — the user cannot manually trigger a scan. If the cache is genuinely empty, the user needs to navigate to the Transactions screen to initiate a bank sync, which is not an action surfaced from this screen to avoid misattributing responsibility. This deliberate absence of a CTA is a design decision that avoids creating a dead-end experience while keeping the scope of this screen accurately bounded.

**Auto Layout specification — Empty State:**
Direction: vertical. Alignment: center-horizontal. Gap: 16dp between icon and headline; 8dp between headline and body. Padding: left 32dp, right 32dp. Vertical position: centered in the available scroll body height.

---

## Frame 4 — Recurring Payments: Error State

Duplicate Frame 1 and rename to "Recurring Payments / Error". Remove the shimmer skeleton and replace the scroll body with a centred error-state composition. Retain the top app bar and bottom navigation bar.

### Error State Composition

Create a vertical Auto Layout container similar to the empty state layout, centred vertically within the scroll body. Apply 32dp left and right padding, center-horizontal alignment, and a 16dp gap between children by default.

First child: an `error_outline` icon at 48×48dp, fill #BA1A1A (error). The error red is used here to signal a problem, contrasting with the #41474D neutral tone of the empty state icon. Mark it as non-decorative with contentDescription "Error loading recurring payments". Add 16dp bottom margin after the icon.

Second child: the headline title in headlineSmall — Roboto Regular 24sp, line height 32sp, colour #181C20, alignment centre. Text reads: "Unable to load recurring payments".

Third child: the body paragraph in bodyMedium — Roboto Regular 14sp, line height 20sp, colour #41474D, alignment centre, wrapping to up to 4 lines. Text reads: "We couldn't read your cached transaction data. This may be a temporary issue — please try again."

Fourth child: the retry button. Create an outlined button component with 1dp border using #72787E (outline), transparent fill, and the label "Try again" in labelLarge — Roboto Medium 14sp, line height 20sp, colour #266489 (primary). The primary colour on the label signals that this is the singular recommended recovery action. Set button height to 48dp (meeting the minimum touch target requirement from WCAG 2.1 SC 2.5.5). Set button width to fill the error container (match_parent minus 64dp of horizontal padding = 265dp). Apply corner radius 9999dp for a full-pill shape. Set a top margin of 24dp before the button (overriding the 16dp default gap) to create visual breathing room between the explanatory copy and the action.

In Figma component properties, add the following states to the retry button: Default (described above), Hovered (border colour shifts to #41474D, fill #266489 at 8% opacity), Pressed (border #266489, fill #266489 at 12% opacity, scale 0.98 transform), Disabled (border #C1C7CE, label colour #C1C7CE), and Focused (border 2dp #266489 with a 3dp outer focus ring at #C9E6FF). The button is never shown in a disabled state on this screen — it is always active when the error state is visible.

**Auto Layout specification — Error State:**
Direction: vertical. Alignment: center-horizontal. Gap: 16dp between children (24dp override before retry button via margin). Padding: left 32dp, right 32dp. Vertical position: centered in the available scroll body height.

---

## Prototype Interaction Flow

Wire the following connections in the Figma prototype panel to create a navigable prototype:

**Frame 1 (Loading) → Frame 2 (Content):** Use a Smart Animate interaction triggered by an After Delay of 2000ms. Apply a Slide Up transition at 300ms ease-in-out. This simulates the recurring-pattern algorithm completing its analysis and transitioning from the skeleton state to the populated content state.

**Frame 1 (Loading) → Frame 3 (Empty):** Add a second After Delay variant to demonstrate the empty outcome. This is best shown as an interactive variant in a presentation; name the connection "Algorithm finds no patterns".

**Frame 1 (Loading) → Frame 4 (Error):** Add a third After Delay variant to demonstrate the error outcome. Name the connection "DataStore read fails".

**subscription_row (any) in Frame 2 → Transactions placeholder frame:** Wire On Tap to navigate to a placeholder frame representing the Transactions screen (id: transactions). Use a Push Right transition at 300ms ease-in-out. Annotate each row's prototype connection with the note: "Action: navigate_transactions. Effect: navigate. Param: merchant=[merchant name]. TransactionsViewModel applies case-insensitive contains filter on the normalised merchant name." Create seven separate connections, one per row, each with the appropriate merchant annotation.

**retry_button in Frame 4 → Frame 1 (Loading):** Wire On Tap to navigate back to Frame 1 (Loading) using a Dissolve transition at 300ms ease-in-out. This models the UX contract: tapping "Try again" sends the user through the Loading state while the algorithm re-runs. Annotate with: "Action: retry_load_subscriptions. Effect: transform_state. Re-runs recurring-payment detection over locally cached DataStore transactions. No network request issued."

**back_button in all frames → previous screen:** Wire On Tap to navigate to the preceding frame (PFM Dashboard placeholder or the frame that navigated to this screen). Use a Slide Left (reverse push) transition at 250ms ease-in-out. The back button should be wired in all four frames.

**Bottom nav tabs (all frames):** Wire each tab to its respective destination frame: Home → home frame; Accounts → accounts frame; Transactions → transactions frame; More → settings frame. Use a Push Right or Smart Animate transition as consistent with the rest of the app prototype.

---

## Component Variants Guide

### SubscriptionRow Component

Create a Figma component named `SubscriptionRow` with the following variants defined in the component properties panel:

**State=Default:** Background transparent (inherits from screen background), autorenew icon fill #266489, merchant label #181C20, supporting text #41474D, trailing amount #181C20, detected badge fill #EBEEF3 label #181C20. Row has no explicit background fill.

**State=Hovered (desktop/tablet preview):** Apply an overlay fill of #181C20 at 8% opacity directly on the row container. All icon, label, and badge colours remain unchanged. Use this variant to preview hover states in responsive design contexts.

**State=Pressed:** Apply a ripple effect expanding from the centre of the tap point outward. The row overlay fill shifts to #266489 at 12% opacity. The transition animates at 300ms with a dissolve. All content colours remain unchanged. Scale the row container to 0.995 during press to add a subtle depth cue.

**State=Focused:** Apply a 2dp inset border using fill #266489 on the row container. This signals keyboard focus for accessibility. All content colours remain unchanged.

All four state variants share the same internal Auto Layout structure. Use component swapping for the icon, label, supporting text, and badge content to populate individual subscription rows from this single component definition.

### DetectedBadge Component

Create a Figma component named `DetectedBadge`. It has a single Default variant only. Fill #EBEEF3 (surfaceContainer), corner radius 9999dp, horizontal padding 8dp, vertical padding 4dp, fixed height 24dp, width hug content. Label "Detected" in labelSmall (Roboto Medium 11sp/16sp, colour #181C20). No icon. Mark the component as display-only in the component description. The badge is never interactive and has no pressed or focused states.

### RetryButton Component

Create a Figma component named `RetryButton` with the following states:

**State=Default:** Border 1dp #72787E, label "Try again" labelLarge #266489, background transparent, corner radius 9999dp, height 48dp.

**State=Hovered:** Border 1dp #41474D, label #266489, background #266489 at 8% opacity.

**State=Pressed:** Border 1dp #266489, label #266489, background #266489 at 12% opacity, scale 0.98.

**State=Focused:** Border 2dp #266489, outer focus ring 3dp using #C9E6FF. Label #266489.

**State=Disabled:** Border 1dp #C1C7CE, label #C1C7CE, background transparent. (Not used on this screen but included for component completeness.)

---

## Accessibility Annotations Layer

Create a separate Figma layer named "Accessibility" inside each frame. This layer is non-printable and for developer handoff only. Document the following:

**Minimum touch targets:** All interactive elements must have a 48×48dp minimum touch target. Subscription rows at 72dp height and full width comfortably meet this requirement. The 24×24dp back button icon must be wrapped in a transparent 48×48dp bounding box. The retry button at 48dp height meets the requirement; its 265dp width far exceeds it.

**Keyboard focus order (Content state):** back_button → subscription_row[0] PureGym → subscription_row[1] Spotify → subscription_row[2] Adobe Lightroom → subscription_row[3] Netflix → subscription_row[4] Amazon Prime → subscription_row[5] Apple TV+ → subscription_row[6] Disney+ → bottom_nav Home → bottom_nav Accounts → bottom_nav Transactions → bottom_nav More. The detected_notice banner and summary_card are display-only and should be skipped from keyboard focus (role="presentation" in the implementation).

**Keyboard focus order (Error state):** back_button → retry_button → bottom_nav Home → bottom_nav Accounts → bottom_nav Transactions → bottom_nav More.

**Screen reader announcements:** When the screen transitions from Loading to Content, the screen reader should announce: "Recurring Payments loaded. £85.93 estimated monthly spend across 7 subscriptions." When transitioning to Empty: "No recurring payments found." When transitioning to Error: "Unable to load recurring payments." When the retry button resolves: "Loading recurring payments."

**WCAG AA contrast verification:**

Primary text #181C20 on #F7F9FF: contrast ratio 17.1:1 — meets AA and AAA.
Supporting text #41474D on #F7F9FF: contrast ratio 9.5:1 — meets AA and AAA.
Summary label #50606E on #F7F9FF: contrast ratio 6.3:1 — meets AA.
Error amount #BA1A1A on #F7F9FF: contrast ratio 5.7:1 — meets AA.
Primary icon #266489 on #F7F9FF: contrast ratio 4.7:1 — meets AA for non-text (3:1 threshold).
Banner body #41474D on #DDE3EA: contrast ratio 5.6:1 — meets AA.
Badge label #181C20 on #EBEEF3: contrast ratio 14.9:1 — meets AA and AAA.
Retry border #72787E on #F7F9FF: contrast ratio 4.8:1 — meets AA for non-text (3:1 threshold).
Retry label #266489 on #F7F9FF: contrast ratio 4.7:1 — meets AA.

---

## Auto Layout Specification Summary

| Frame / component | Direction | Padding T/R/B/L | Gap | Width sizing |
|---|---|---|---|---|
| Scroll body (Loading) | vertical | 16/16/16/16 | 8dp | fill (361dp usable) |
| Scroll body (Content) | vertical | 8/0/24/0 | 0 | fill (393dp) |
| detected_notice banner | horizontal | 12/12/12/12 | 8dp | fill (−32dp margin = 361dp) |
| summary_card inner column | vertical | 16/16/16/16 | 4dp | fill (−32dp margin = 361dp) |
| subscription_row | horizontal | 12/16/12/16 | 16dp | fill (393dp) |
| row content column | vertical | 0/0/0/0 | 2dp | fill (grows, weight 1) |
| detected_badge chip | horizontal | 4/8/4/8 | 0 | hug content |
| empty_state container | vertical | 0/32/0/32 | 16dp | fill |
| error_state container | vertical | 0/32/0/32 | 16dp | fill |
| retry_button | horizontal | 0/24/0/24 | 0 | fill (265dp at 32dp padding) |
| top_app_bar | horizontal | 0/16/0/0 | 16dp | fill (393dp) |
| bottom_nav | horizontal | 0/0/0/0 | 0 | fill (393dp), fixed 80dp h |

---

## Design Rationale and Notes

The autorenew icon in list rows uses the primary Trust Blue (#266489) rather than the on-surface-variant grey used in other list icon contexts across the app. This intentional deviation creates a consistent visual rhythm — every row in the Recurring Payments list pulses with the same blue, reinforcing the idea that all items share the same recurring quality. The single-colour icon set also reduces visual noise on a screen that is inherently data-dense.

The summary amount uses the error red (#BA1A1A) for the £85.93 figure. This is not an error indicator. It is the same colour applied to debit amounts on the Transactions and Home screens, establishing cross-screen semantics: red means money leaving the account. The "Estimated monthly spend" label above it makes the framing explicit. The choice avoids a separate "cost warning" colour that would expand the palette unnecessarily.

The "Detected" badge chip uses a deliberately neutral fill (#EBEEF3 surfaceContainer) rather than a primary or secondary tonal container. These are algorithmic inferences from transaction patterns — they carry a degree of uncertainty. A primary-tinted badge would suggest the same confidence level as a bank-confirmed standing order or direct debit. The neutral chip colour communicates the distinction without requiring explanatory text beyond the detected_notice banner that anchors the top of the content state.

Annual subscriptions (Adobe Lightroom at £143.88 annual, £11.99 monthly equivalent) display the actual per-charge amount alongside the "Annual" cadence label. This is the correct choice for a transparent financial tool: the user needs to know what will appear on their statement. The summary card normalises all cadences to a monthly total for the aggregate view, providing both the planning figure (£85.93/month equivalent) and the accurate per-charge amounts in the list rows.

The empty state explicitly does not include a call-to-action button. The recurring-payment detection algorithm runs automatically over locally cached transaction data — there is nothing for the user to trigger manually. If the cache is empty, the correct next step is to navigate to the Transactions screen to initiate a bank sync, but surfacing that instruction here would shift accountability incorrectly. The body copy is intentionally forward-looking ("Once you have more history…") to set expectations without making the user feel stuck.
