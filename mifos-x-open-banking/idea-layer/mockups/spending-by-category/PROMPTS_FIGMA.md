# Spending by Category — Figma Design Prompts

> Generated from `screens/spending-by-category/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) — 1× reference frame (scale to 2× / 3× for delivery assets)
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

The Open Banking app uses Material Design 3 with a Trust Blue primary palette derived from seed colour #266489. All components follow M3 Light theme. Typography is exclusively Roboto (brand, plain, and body roles) with Roboto Mono reserved for monetary amounts and account numbers.

### Resolved Colour Palette (Light Theme)

Primary (#266489) is the action colour for selected chips, progress bar fill, back-arrow tint, and the selected bottom-nav icon. Use it only on white or surface backgrounds to maintain WCAG AA contrast.

Error (#BA1A1A) is used exclusively for debit amounts — the total spend figure on this screen — and for the warning icon in the error state. Never use it for decorative purposes.

OnSurfaceVariant (#41474D) carries secondary text: chip labels when unselected, supporting text in list rows, body copy in empty and error states, and all bottom-nav labels in the unselected state.

Surface (#F7F9FF) is the page background and the card background for the spend summary card. It is near-white, not pure white — use this exact value.

PrimaryContainer (#C9E6FF) is the selected chip fill, the retry button fill (tonal variant), and the hover/pressed overlay on primary-adjacent interactive elements.

OnPrimaryContainer (#004B6F) is the text colour on PrimaryContainer surfaces — selected chip label and retry button label.

SurfaceVariant (#DDE3EA) is the shimmer skeleton fill and the progress bar track. It provides sufficient contrast on the Surface background without being visually heavy.

OnSurfaceVariant (#41474D) is the icon tint for category icons and unselected bottom-nav icons.

OutlineVariant (#C1C7CE) is the 1dp list divider between category rows.

### Semantic Token → Figma Variable Mapping

| Token name | Resolved hex (light) | Figma variable path |
|---|---|---|
| primary | #266489 | color/primary |
| onPrimary | #FFFFFF | color/on-primary |
| primaryContainer | #C9E6FF | color/primary-container |
| onPrimaryContainer | #004B6F | color/on-primary-container |
| error | #BA1A1A | color/error |
| onError | #FFFFFF | color/on-error |
| background | #F7F9FF | color/background |
| surface | #F7F9FF | color/surface |
| onSurface | #181C20 | color/on-surface |
| surfaceVariant | #DDE3EA | color/surface-variant |
| onSurfaceVariant | #41474D | color/on-surface-variant |
| outline | #72787E | color/outline |
| outlineVariant | #C1C7CE | color/outline-variant |
| surfaceContainerHighest | #E0E3E8 | color/surface-container-highest |
| surfaceContainerLow | #F1F4F9 | color/surface-container-low |

### Roboto Type Scale (Figma Text Styles)

Create the following Figma text styles using these exact specifications. All styles use Roboto unless noted.

titleLarge: size 22sp, line-height 28sp, weight Regular (400). Used for the top app bar title.

headlineMedium: size 28sp, line-height 36sp, weight Regular (400). Used for the total spend amount on the summary card. Apply color/error (#BA1A1A) to this style in the spend context.

headlineSmall: size 24sp, line-height 32sp, weight Regular (400). Used for empty state and error state titles.

bodyLarge: size 16sp, line-height 24sp, weight Regular (400). Used for category row name (label) and trailing amount text.

bodyMedium: size 14sp, line-height 20sp, weight Regular (400). Used for supporting text in category rows and body copy in empty/error states.

labelMedium: size 12sp, line-height 16sp, weight Medium (500). Used for the "Total Spend — June 2026" header on the summary card.

labelSmall: size 11sp, line-height 16sp, weight Medium (500). Used for bottom navigation labels.

For monetary amounts displayed at bodyLarge size, switch the font to Roboto Mono to maintain tabular alignment across rows.

### Spacing System

The base unit is 4dp. Common compound values: 8dp (component gap), 16dp (horizontal screen padding, card internal padding), 32dp (double screen padding for centred modals). All values are in density-independent pixels (dp).

---

## Frame 1 — Loading State

Create a frame 393dp wide by 852dp tall. Set the background fill to #F7F9FF (color/background). Name this frame "SBC / Loading".

### Top App Bar

At the top of the frame, create a horizontal layout container 393dp wide by 64dp tall. Fill it with #F7F9FF (color/surface). Add a shadow (elevation 0 — no shadow at rest; the shadow appears on scroll, so keep it at 0 in the static design). Inside this container, place two elements using Auto Layout with horizontal direction, vertical alignment centred, horizontal padding 16dp, and a gap of 8dp between items.

The leading element is an icon button: an arrow_back icon (24dp × 24dp) tinted #266489 (color/primary). This represents the back navigation action. Ensure the touch target is at least 48dp × 48dp by wrapping the icon in a 48dp × 48dp transparent hit area. Set the accessibility annotation to "Navigate back".

The title text reads "Spending by Category" in Roboto, titleLarge style (22sp, weight 400, line 28sp), colour #181C20 (color/on-surface). Left-align this text and let it fill the remaining horizontal space.

### Period Selector

Directly below the top app bar (margin top 0dp, flush), create a horizontal scroll container 393dp wide by 48dp tall. Set horizontal padding to 16dp on each side and use vertical padding of 8dp so each chip sits centred vertically. Place three filter chips in a row with 8dp gap between them.

The first chip reads "This month" and is in the selected state. Create it with a filled background of #C9E6FF (color/primary-container), no outline, text in labelLarge (14sp weight 500) coloured #004B6F (color/on-primary-container), and corner radius 9999dp (full pill). The chip height is 32dp. Include a checkmark icon (check, 18dp) to the left of the label to indicate selection. Minimum touch target: 48dp height by expanding the hit area vertically beyond the visual chip.

The second chip reads "Last month" in the unselected state: no fill, 1dp outline in #72787E (color/outline), label text #41474D (color/on-surface-variant), labelLarge style. Same pill radius, same 32dp height.

The third chip reads "3 months" with identical unselected styling.

### Skeleton Loading Blocks

Below the period selector with 8dp margin top, create a vertical stack Auto Layout container filling the content area (width: match parent with 32dp total horizontal margin, so 361dp wide). Set vertical direction, gap 8dp, padding 0. All skeleton elements use #DDE3EA (color/surface-variant) as fill and should be animated with a left-to-right shimmer sweep in production; in Figma use a static fill.

First skeleton element: a rounded rectangle 361dp wide by 80dp tall with corner radius 12dp, fill #DDE3EA. This represents the spend summary card placeholder.

Second skeleton element: a rounded rectangle 216dp wide (60% of 361dp) by 16dp tall with corner radius 8dp, fill #DDE3EA. This represents a text line placeholder.

Third, fourth, and fifth skeleton elements: three rounded rectangles each 361dp wide by 56dp tall with corner radius 8dp, fill #DDE3EA. These represent the first three category row placeholders.

Add an 8dp gap between each skeleton element.

Set the accessibility annotation on the entire skeleton group to "Computing your spending breakdown".

### Bottom Navigation

At the very bottom of the 852dp frame, create a horizontal layout 393dp wide by 80dp tall, fill #F7F9FF. Use Auto Layout with horizontal direction, items spaced evenly (space-between or fill-width with equal weights). Include safe-area padding at the bottom if targeting devices with a home indicator — add 16dp bottom padding.

Each navigation tab consists of a vertical Auto Layout container with centred horizontal alignment, gap 4dp, containing a 24dp icon and a labelSmall text. All four tabs are in the unselected state on this screen. Unselected tab tint: #41474D (color/on-surface-variant) for both icon and label.

Tab 1: icon home, label "Home".
Tab 2: icon account_balance, label "Accounts".
Tab 3: icon receipt_long, label "Transactions".
Tab 4: icon more_horiz, label "More".

No tab is selected on this sub-screen — spending-by-category is accessed via in-app navigation, not directly from a bottom tab.

---

## Frame 2 — Content State (This Month, June 2026)

Create a frame 393dp wide by 852dp tall. Name this frame "SBC / Content — This Month". Background #F7F9FF. This is the primary state with real data from the Priya Sharma anchor dataset.

### Top App Bar

Identical to the loading frame: 64dp tall, back arrow tinted #266489, title "Spending by Category" titleLarge #181C20.

### Period Selector

Identical shell to the loading frame, but now "This month" chip is selected (fill #C9E6FF, text #004B6F, checkmark visible) and the other two chips remain unselected.

### Total Spend Summary Card

Below the period selector with 8dp margin top, create a card component 361dp wide (16dp margin each side) with corner radius 12dp, surface elevation level 1 (applies a subtle tonal overlay in M3 — use fill #F1F4F9 for the elevated surface or use a shadow: 0dp X, 1dp Y, 3dp blur, #000000 at 15% opacity). Internal padding: 16dp on all sides.

Inside the card, use a vertical Auto Layout container with gap 4dp.

The first text element reads "Total Spend — June 2026" in labelMedium style (12sp, weight 500, line-height 16sp), colour #41474D (color/on-surface-variant). This label interpolates the selected period at runtime; for this frame use "June 2026".

The second text element displays "£1,840.00" in headlineMedium style (28sp, weight 400, line-height 36sp), colour #BA1A1A (color/error). This is the total debit spend for June 2026 from the demo dataset. Use Roboto Mono for this amount to align digits correctly. Set the accessibility annotation to "Total spend £1,840.00".

### Category List

Below the summary card with 8dp margin top, create a vertical list container that fills the remaining width (full width, no horizontal margin — let individual rows manage their own internal padding). Set dividers between rows using a 1dp horizontal line in #C1C7CE (color/outline-variant).

Each category row is a tappable list item. Use the following structure for every row:

Create a vertical Auto Layout container full-width. Inside it, place a horizontal row container 56dp tall with vertical alignment centred, horizontal padding 16dp on each side, and 16dp gap between the leading icon and the text stack. Then below the horizontal row, place the progress bar with 16dp horizontal margin and 8dp bottom margin.

**Row 1 — Bills (highest spend)**

Leading icon: receipt_long (Material Symbols Outlined), 24dp × 24dp, tint #50606E (color/on-surface-variant, secondary tone). Set contentDescription to "Bills" for accessibility.

Text stack (fills remaining width, vertical Auto Layout, gap 2dp): Primary text "Bills" in bodyLarge (16sp weight 400) colour #181C20 (color/on-surface), maxLines 1 with ellipsis. Secondary text "4 transactions · 73.7%" in bodyMedium (14sp weight 400) colour #41474D (color/on-surface-variant). Use Roboto for both.

Trailing text: "£1,356.00" in bodyLarge Roboto Mono, colour #181C20 (color/on-surface), right-aligned. Do not apply the error colour here — category amounts are neutral; only the total is coloured error.

Progress bar directly below the row (not inside the horizontal row container): a horizontal rectangle filling the card width minus 32dp (329dp wide), height 4dp, corner radius 2dp. The track fill is #E0E3E8 (color/surface-container-highest). The indicator fill is #266489 (color/primary) and covers 73.7% of the bar width (approximately 242dp filled out of 329dp total). In Figma, use a progress bar component or simulate with two rectangles clipped inside a container: the track behind, and the indicator on top. Set the accessibility annotation to "Bills spending share".

**Row 2 — Groceries**

Leading icon: shopping_cart 24dp #50606E. Primary "Groceries" bodyLarge #181C20. Supporting "9 transactions · 10.8%" bodyMedium #41474D. Trailing "£198.00" Roboto Mono bodyLarge #181C20. Progress bar fill: 10.8% of 329dp ≈ 36dp indicator width on a 329dp track.

**Row 3 — Dining**

Leading icon: restaurant 24dp #50606E. Primary "Dining". Supporting "5 transactions · 4.8%". Trailing "£88.00". Progress: 4.8% fill ≈ 16dp indicator.

**Row 4 — Subscriptions**

Leading icon: subscriptions 24dp #50606E. Primary "Subscriptions". Supporting "5 transactions · 3.4%". Trailing "£63.00". Progress: 3.4% fill ≈ 11dp indicator.

**Row 5 — Transport**

Leading icon: directions_transit 24dp #50606E. Primary "Transport". Supporting "8 transactions · 2.2%". Trailing "£41.00". Progress: 2.2% fill ≈ 7dp indicator.

Separate each row with a divider: a 1dp horizontal line using colour #C1C7CE (color/outline-variant), extending full width. The divider sits between row containers, not inside them.

### Component Variants for Category Row

**Default state**: white/surface background, #181C20 primary text, no elevation.

**Hovered state** (pointer input / large screen): apply a 4–8% onSurface overlay (#181C20 at 8% opacity) as a fill on the row container background.

**Pressed/Ripple state**: apply a circular ripple from the touch point expanding to fill the row. The ripple colour is #C9E6FF (color/primary-container) at 32% opacity. In Figma, use a rectangle overlay matching the row dimensions with fill #C9E6FF at 32% opacity and mark it as the pressed variant.

**Focused state** (keyboard / accessibility): apply a 3dp focus ring in #266489 (color/primary) around the entire row container. In Figma, use a rectangle outline, weight 3dp, colour #266489, no fill.

### Bottom Navigation

Same structure as the loading frame. All tabs unselected.

---

## Frame 3 — Content State (Last Month, May 2026)

Create a frame "SBC / Content — Last Month". This frame is structurally identical to Frame 2, with the following data substitutions from the last_month period in demo-data.yaml.

The "Last month" chip is now selected (bg #C9E6FF, text #004B6F, checkmark). The "This month" chip becomes unselected.

Summary card label: "Total Spend — May 2026". Summary card amount: "£1,851.00" in #BA1A1A headlineMedium.

The category list now contains six rows in this order (sorted by amount descending): Bills (£1,340.00, 72.4%, 4 transactions, progress 72.4%), Groceries (£210.00, 11.3%, 10 transactions, progress 11.3%), Entertainment (£105.00, 5.7%, 3 transactions, icon movie), Dining (£95.00, 5.1%, 6 transactions), Subscriptions (£63.00, 3.4%, 5 transactions), Transport (£38.00, 2.1%, 7 transactions).

Note the Entertainment category uses the movie icon (24dp #50606E) and did not appear in the this_month period — this demonstrates the dynamic nature of the category list.

All row styling, typography, progress bar colours, and spacing are identical to Frame 2.

---

## Frame 4 — Content State (3 Months, Apr–Jun 2026)

Create a frame "SBC / Content — 3 Months". The "3 months" chip is selected. Summary card: "Total Spend — Apr–Jun 2026" / "£5,388.00" headlineMedium #BA1A1A.

Seven category rows: Bills (£4,052.00, 75.2%, 12 tx, receipt_long), Groceries (£588.00, 10.9%, 28 tx), Dining (£263.00, 4.9%, 16 tx), Subscriptions (£189.00, 3.5%, 15 tx), Entertainment (£135.00, 2.5%, 5 tx, movie icon), Transport (£117.00, 2.2%, 23 tx), Other (£44.00, 0.8%, 4 tx, more_horiz icon).

The Bills progress bar at 75.2% extends to approximately 247dp of the 329dp track. The seven rows will push the list below the visible viewport — the screen should scroll vertically. In Figma, set the content frame to extend beyond 852dp and clip with a scroll mask. The top app bar and period selector remain sticky (use Figma's "Fix position when scrolling" for those two layers).

---

## Frame 5 — Empty State

Create a frame 393×852dp named "SBC / Empty". Background #F7F9FF.

### Top App Bar

Identical to other frames: back arrow #266489, title "Spending by Category" titleLarge #181C20.

### Period Selector

The period selector remains fully visible and interactive in the empty state. Per the UX specification (EC-SBC-001), the user must be able to switch to a different period even when no data is found for the current one. Show "This month" selected.

### Empty State Illustration Area

After the period selector, the remaining viewport below the chips and above the bottom nav is vertically centred. Use a vertical Auto Layout container centred both horizontally and vertically in this space, with gap 16dp between children and horizontal padding 32dp.

The illustration is a single Material Symbols icon: pie_chart (Outlined variant), rendered at 48dp × 48dp, tinted #41474D (color/on-surface-variant). Set the icon's contentDescription to "No spending data". Do not use a coloured circle background — keep the icon freestanding.

Below the icon, place the title text "No spending data" in headlineSmall style (24sp, weight 400, line-height 32sp), colour #181C20 (color/on-surface), horizontally centred.

Below the title with 8dp gap, place the body text "No debit transactions were found for this period. Try a different time window or check back later." in bodyMedium style (14sp, weight 400, line-height 20sp), colour #41474D (color/on-surface-variant), centred alignment, padding horizontal 32dp, allowing natural wrapping.

Set the overall empty state group accessibility annotation to "No spending data for this period".

### Bottom Navigation

Identical to other frames.

---

## Frame 6 — Error State

Create a frame 393×852dp named "SBC / Error". Background #F7F9FF.

### Top App Bar

Identical to other frames.

### Period Selector

The period selector is visible in the error state per ui.yaml `state_binding: [loading, content, empty, error]`. Show "This month" selected. The user can still tap a different period chip — this will trigger retryCompute via the selectPeriod action, giving the user an implicit retry path.

### Error State Content

After the period selector, the remaining viewport space is vertically centred. Use a vertical Auto Layout container centred in the space, gap 16dp between elements, horizontal padding 32dp.

The error icon is warning_amber (Material Symbols Outlined) at 48dp × 48dp, tinted #BA1A1A (color/error). Set contentDescription to "Computation error". This is the only use of the error colour on this screen outside the total spend amount — it visually signals severity without being alarmist.

Below the icon, place the title "Unable to compute spending" in headlineSmall (24sp weight 400 line 32sp) colour #181C20, centred.

Below the title, place the body "There was a problem reading your transaction data. Your cached data may be unavailable." in bodyMedium (14sp weight 400 line 20sp) colour #41474D, centred, wrapped at the available width.

### Retry Button

Below the body text with 16dp margin top, place a button using the tonal variant of M3 Button:
- Fill: #C9E6FF (color/primary-container)
- Label colour: #004B6F (color/on-primary-container)
- Label text: "Try again" in labelLarge (14sp weight 500)
- Corner radius: 9999dp (full pill shape per M3 default)
- Height: 48dp (meets the WCAG 2.5.5 AA+ 44dp minimum; we use 48dp for M3 comfortable density)
- Width: fill container minus 64dp horizontal margin (i.e., 265dp on the 393dp canvas)
- Minimum touch target: 48dp height — already met by the 48dp visual height

**Button variants:**

Default: fill #C9E6FF, label #004B6F.

Hovered: apply an 8% onPrimaryContainer (#004B6F at 8%) overlay on the fill — #C9E6FF blended with #004B6F at 8% opacity.

Pressed: apply a 12% overlay. Add a slight scale transform (0.97×) in prototype.

Focused: 3dp focus ring #266489 around the button outline, no fill change.

Disabled: not applicable for this button — it is always shown when the error state is active.

Set the accessibility annotation: label "Try again", role Button, action description "Retry computing spending breakdown for selected period".

### Bottom Navigation

Identical to other frames.

---

## Auto Layout Specifications

This section specifies the Auto Layout settings for every major frame region.

**Outer frame (all states)**: Fixed width 393dp, fixed height 852dp. Overflow: hidden (clip). Background #F7F9FF.

**Top app bar container**: Auto Layout direction horizontal. Width: fill container. Height: fixed 64dp. Alignment: centre vertical. Padding: left 4dp, right 16dp (the icon button itself provides 12dp internal padding making visual leading appear 16dp). Gap between items: 8dp.

**Period chip group container (scroll region)**: Auto Layout direction horizontal. Width: fill container. Height: hug contents (min 48dp). Padding horizontal 16dp, vertical 8dp. Gap between chips: 8dp. Clip content: true (enables horizontal scroll in prototype).

**Individual filter chip**: Auto Layout direction horizontal. Height fixed 32dp. Padding horizontal 12dp. Alignment: centre vertical. Gap between checkmark and label: 4dp. Corner radius 9999.

**Spend summary card outer container**: Auto Layout direction horizontal. Width: fill container with margin 16dp each side (net 361dp). Height: hug contents. Padding: 16dp all sides. Gap between children: 4dp. Background: #F7F9FF. Corner radius 12dp. Effect: elevation level 1 (drop shadow 0×1dp, 3dp blur, #000000 15%).

**Category list container**: Auto Layout direction vertical. Width: fill container (393dp, no side margins). Height: hug contents. Padding: none (rows handle their own padding). Gap: 0 (dividers are separate layers). Overflow visible (for shadow if needed).

**Individual category row (horizontal content area)**: Auto Layout direction horizontal. Width: fill container. Height: fixed 56dp. Padding horizontal 16dp. Alignment: centre vertical. Gap between leading icon and text stack: 16dp.

**Category text stack (within row)**: Auto Layout direction vertical. Width: fill remaining. Height: hug. Gap: 2dp.

**Progress bar row (below each category's content area)**: Fixed height 4dp. Width: fill container minus 32dp (margin 16dp each side). Corner radius 2dp. Two fills: track layer #E0E3E8 below, indicator layer #266489 on top at the appropriate fractional width. Bottom margin: 8dp.

**Empty / Error state centred container**: Auto Layout direction vertical. Width: fill container with horizontal padding 32dp. Height: hug. Alignment: centre horizontal. Gap: 16dp. Positioned with vertical alignment centred in the remaining viewport space.

**Bottom navigation bar**: Auto Layout direction horizontal. Width: fill container. Height: fixed 80dp (includes 16dp safe-area bottom padding). Alignment: distribute (space between or equal weight). Background: #F7F9FF. Each tab item: Auto Layout vertical, centred horizontal, gap 4dp.

---

## Prototype Interaction Flow

Define the following prototype connections in Figma using "On tap" triggers between frames. All transitions use the Material Motion standard curve: ease-in-out, 300ms duration.

**Period chip: "This month" (on any frame)**
On tap → stay on current frame but swap data. In Figma prototype, connect to Frame 2 (SBC / Content — This Month) from all other content frames. Transition: Smart Animate, 200ms ease.

**Period chip: "Last month" (on any frame)**
On tap → connect to Frame 3 (SBC / Content — Last Month). Transition: Smart Animate 200ms.

**Period chip: "3 months" (on any frame)**
On tap → connect to Frame 4 (SBC / Content — 3 Months). Transition: Smart Animate 200ms.

**Category row — Bills**
On tap → navigate to the Transactions screen filtered by Bills. In Figma, create a connection to the Transactions frame or a placeholder screen labelled "Transactions (Bills filter)". Transition: slide left (push), 300ms standard curve. Document the action_contract: effect navigate, target transactions, param category="Bills" URI-encoded.

**Category row — Groceries**
On tap → Transactions (Groceries filter). Same transition as Bills.

**Category row — Dining**
On tap → Transactions (Dining filter). Same transition.

**Category row — Subscriptions**
On tap → Transactions (Subscriptions filter). Same transition.

**Category row — Transport**
On tap → Transactions (Transport filter). Same transition.

**Retry button (error state)**
On tap → Frame 1 (SBC / Loading), then after a simulated 1.5s delay, auto-advance to Frame 2 (SBC / Content — This Month) using an "After delay" trigger. This simulates the retryCompute → loading → content flow. Transition to loading: dissolve 150ms. Transition to content: Smart Animate 300ms.

**Back arrow (all frames)**
On tap → navigate back. Connect to the previous screen in the prototype flow (e.g., PFM Dashboard or Home). Transition: slide right (pop), 300ms standard curve.

---

## Accessibility Annotations

Every interactive element on this screen must meet the following requirements. Add Figma accessibility annotations (using the Figma Accessibility plugin or annotation stickers) to document these for the development handoff.

**Minimum touch target**: All tappable elements must have a touch target of at least 48dp × 48dp per WCAG 2.5.5 (AAA level; our baseline is 48dp for M3 comfortable density). The visual chip is 32dp tall but must have 48dp touch area. Category rows are 76dp tall visually (56dp content + 20dp progress), comfortably exceeding the minimum. The retry button is 48dp tall exactly at the minimum — do not reduce it.

**Colour contrast**: All text must meet WCAG AA minimum contrast ratios. Primary text #181C20 on #F7F9FF background achieves 16.8:1 (well above 4.5:1). Secondary text #41474D on #F7F9FF achieves 7.3:1. Error text #BA1A1A on #F7F9FF achieves 5.6:1 (passes AA at 4.5:1 for normal text). Progress bar fill #266489 on #E0E3E8 track achieves 3.4:1 — the progress bar conveys information redundantly via the percentage text label, so it does not need to meet contrast requirements alone. Selected chip text #004B6F on #C9E6FF achieves 6.4:1 (passes AA).

**Content descriptions for icons**: The back arrow icon must have contentDescription "Navigate back". Category icons (receipt_long, shopping_cart, restaurant, subscriptions, directions_transit) are decorative within their row — the row's own accessibility label provides the semantic content. Set these icons to decorative (contentDescription = null or empty string). The pie_chart icon in the empty state and warning_amber in the error state are not decorative — they carry semantic meaning and must have contentDescriptions: "No spending data" and "Computation error" respectively.

**Screen reader reading order**: The logical reading order for the content state from top to bottom is: top app bar title → back button → period selector chips (in order) → summary card (label then amount) → category row 1 through N (each row: icon label + row label + supporting text + trailing amount + progress bar percentage). The progress bar should surface its value as a percentage via the accessibility label, not just as a visual bar.

**Focus ring**: Any keyboard or D-pad focused element must render a 3dp focus ring in #266489. This applies to: back arrow, each period chip, each category row, and the retry button.

**Reduced motion**: When the system prefers reduced motion (Reduce Motion accessibility setting on device), the shimmer pulse animation in the loading skeleton is replaced with a static #DDE3EA fill. All page transitions drop the slide animation and use a simple dissolve at 150ms. Annotate this in Figma using a "reduced motion" annotation sticker or note.

---

## Design Handoff Notes

The category colour coding on progress bars uses a single primary colour (#266489) for all categories. This is intentional — the screen does not assign per-category colours (e.g., red for Bills, green for Groceries), because the design system does not define a categorical colour scale and arbitrary colour assignment can violate WCAG AA contrast requirements. The percentage text label provides the relative magnitude context. If a future design iteration adds per-category colour coding, each colour must be audited against the #F7F9FF surface background for a minimum 3:1 contrast ratio (graphical object minimum per WCAG 1.4.11).

The trailing monetary amounts in category rows use Roboto Mono to maintain vertical alignment when amounts vary in digit count (e.g., "£1,356.00" vs "£41.00"). The screen reader should announce these as "Bills, £1,356.00, 4 transactions, 73.7%", not by reading out individual characters. Implement this via a merged accessibility label on the row.

The spend_summary_card is display-only (no on_click). Do not add a tap affordance (no hover state, no ripple). The card elevation (level 1) is sufficient to distinguish it from the page background without an outline or stroke.

The period selector chips should not wrap to a second line. They scroll horizontally. In Figma, mark the chip group container as scrollable and ensure the frame clips content. All three chips (including their 16dp end-padding) fit in approximately 300dp — they do not scroll on a 393dp canvas for this locale. However, localised strings (e.g., "This month" in German: "Diesen Monat") may be longer and require scroll; design accordingly.
