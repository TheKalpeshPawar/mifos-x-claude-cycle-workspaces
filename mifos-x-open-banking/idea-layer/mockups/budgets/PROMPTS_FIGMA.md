# Budgets — Figma Design Prompts

> Generated from `screens/budgets/ui.yaml` + `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Canvas: 393×852dp (Pixel 5, 1x dp units) · Material Design 3 · Light theme

---

## Design System Summary

### Resolved Colour Palette

All design work for the Budgets screen uses the following resolved hex values from the Open Banking Trust Blue Material 3 theme (seed #266489):

| Semantic Token | Figma Variable | Hex (light) | Usage in Budgets |
|---|---|---|---|
| primary | color/primary | #266489 | Save button fill, progress bar (under budget), text links |
| onPrimary | color/on-primary | #FFFFFF | Text on filled primary buttons |
| primaryContainer | color/primary-container | #C9E6FF | Chip selections, tonal button backgrounds |
| onPrimaryContainer | color/on-primary-container | #004B6F | Text on primary container surfaces |
| secondary | color/secondary | #50606E | Secondary text, icon decorative fills |
| error | color/error | #BA1A1A | Over-budget progress bars, alert text, error icon |
| onError | color/on-error | #FFFFFF | Text on error-colour fills |
| errorContainer | color/error-container | #FFDAD6 | Over-budget progress track (background fill) |
| onErrorContainer | color/on-error-container | #93000A | Text on error container surfaces |
| background | color/background | #F7F9FF | Screen background, top app bar |
| onBackground | color/on-background | #181C20 | Primary text, card labels |
| surface | color/surface | #F7F9FF | Card and sheet surfaces |
| onSurface | color/on-surface | #181C20 | On-surface text |
| surfaceVariant | color/surface-variant | #DDE3EA | Skeleton shimmer fill, progress track (general) |
| onSurfaceVariant | color/on-surface-variant | #41474D | Secondary labels, placeholder text, icon fills |
| outline | color/outline | #72787E | Dropdown and text field borders |
| outlineVariant | color/outline-variant | #C1C7CE | Dividers, subtle separators |
| surfaceContainer | color/surface-container | #EBEEF3 | Card backgrounds (elevation 1 tint applied by M3) |
| secondaryContainer | color/secondary-container | #D3E5F5 | Tonal button fill (retry), quick-action icon backgrounds |
| onSecondaryContainer | color/on-secondary-container | #384956 | Text on secondary container |

### Typography — Roboto Type Scale

All text uses Roboto. Weights: Regular 400, Medium 500. Use Figma's shared text styles.

| Style | Size | Line Height | Weight | Usage |
|---|---|---|---|---|
| headlineSmall | 24sp | 32sp | Regular 400 | Empty-state title, error-state title |
| titleMedium | 16sp | 24sp | Medium 500 | Top app bar title "Budgets" |
| titleSmall | 14sp | 20sp | Medium 500 | Budget category names inside cards |
| labelLarge | 14sp | 20sp | Medium 500 | Section headers ("Set budget", "June 2026"), button labels |
| labelMedium | 12sp | 16sp | Medium 500 | Text-button labels ("View transactions", "Delete") |
| labelSmall | 11sp | 16sp | Medium 500 | Over-budget alert text, validation error messages |
| bodyLarge | 16sp | 24sp | Regular 400 | Form field input values |
| bodyMedium | 14sp | 20sp | Regular 400 | Error and empty-state body copy |
| bodySmall | 12sp | 16sp | Regular 400 | Supporting text in budget cards (used/limit), storage hint, trailing labels |

### Spacing and Shape

The base spacing unit is 4dp. Standard screen padding is 16dp on all horizontal sides. Cards use 12dp corner radius. Input fields use 4dp corner radius (outlined variant). Buttons use 9999dp (full pill) corner radius. The minimum touch target for all interactive elements is 48dp.

---

## State: Loading

Create a mobile frame at 393×852dp. Apply a background fill of #F7F9FF across the entire frame.

At the top, place a small top app bar spanning the full width at 56dp height. The bar's background matches the screen (#F7F9FF). On the left side of the app bar, place a back arrow icon (arrow_back, 24dp, colour #181C20) with a minimum touch target of 48×48dp. Horizontally centre the title text "Budgets" using titleMedium style (Roboto 16sp/24sp, weight 500, colour #181C20) within the bar, slightly right-of-centre if the back icon is only on the left.

Below the app bar, add 16dp of vertical padding, then place three skeleton placeholder cards stacked vertically with 8dp gaps between them. Each skeleton card is 88dp tall, spans the content width (393 − 32dp = 361dp wide), and has 12dp corner radius. Fill them with #DDE3EA. Apply a Figma shimmer effect using a horizontal linear gradient that sweeps from #DDE3EA to #E5E8ED to #DDE3EA, animated at 1.5 seconds per cycle. For reduced-motion scenarios, the gradient remains static at #DDE3EA without animation.

Auto Layout specs for the skeleton column: direction vertical, item spacing 8dp, padding left 16dp, right 16dp, top 16dp, bottom 16dp, sizing: fill container width, hug height.

At the bottom of the frame, place the bottom navigation bar. It is 393dp wide and 80dp tall, with a background fill of #F7F9FF. The bar contains four equally spaced navigation items: Home (icon: home), Accounts (icon: account_balance), Transactions (icon: receipt_long), and More (icon: more_horiz). Since the Budgets screen is not one of these primary nav destinations, none of the tabs are shown as selected — all four icons and labels render in the default unselected tint (#41474D, #72787E for labels). Each tab item uses labelSmall 11sp text below its 24dp icon, minimum touch target 48×48dp.

Component variants to include: default (shimmer active), reduced-motion (static fill), dark mode (skeleton fill #313539 on background #101417).

---

## State: Content

Create a mobile frame at 393×852dp with background #F7F9FF. This is the primary state showing both the budget creation form and the list of six active budget cards for June 2026.

Begin with the same top app bar as the loading state (56dp, back arrow, title "Budgets").

Directly below the app bar, place a section header label reading "Set budget" in labelLarge style (Roboto 14sp/20sp, weight 500, colour #181C20). Apply 16dp horizontal padding and 16dp top padding, 8dp bottom padding to this label.

Beneath the section header, create a card for the budget creation form. The card uses M3 Elevated Card styling: background tint #EBEEF3 (surface container at elevation level 1), 12dp corner radius, elevation shadow 1dp, horizontal margin 16dp, internal padding 16dp on all sides. Use Auto Layout: direction vertical, item spacing 12dp, sizing fill width (361dp), hug height.

Inside the form card, place first an exposed dropdown menu component for category selection. Create a container 56dp tall with 4dp corner radius and a 1dp outline in #72787E. Inside it, place a floating label in labelSmall style (11sp, weight 500, #41474D) reading "Category" positioned at the top-left of the field. Below the label, place the selected value text in bodyLarge style (16sp, weight 400, #181C20) reading "Groceries" — this matches the demo-data form.category value. On the trailing edge, place a downward chevron icon (arrow_drop_down, 24dp, #41474D). The full dropdown spans match_parent width within the card. On tap this component dispatches the selectBudgetCategory action which updates form.category via transform_state.

Below the dropdown, place an outlined text field for the monthly limit amount. Height 56dp, 4dp corner radius, 1dp outline in #72787E. The floating label reads "Monthly limit (£)" (labelSmall 11sp, weight 500, #41474D). The field value is empty in the default demo state (form.amount is blank). Show the placeholder text "0.00" in bodyLarge (16sp, weight 400, #72787E) when empty. This field uses a decimal keyboard and triggers the updateBudgetAmountField action on every change, performing inline validation. Below the field, reserve 16dp vertical space for an inline validation error message in labelSmall (11sp, weight 400, #BA1A1A) — create this as a hidden layer for the validation-fail variant.

Below the text field, place the primary action button labelled "Set Budget". Use a FilledButton with background #266489, text colour #FFFFFF, label text in labelLarge (14sp, weight 500), 40dp height (minimum touch area 48dp via padding), and 9999dp corner radius (full pill). The button spans match_parent width within the card. It is enabled only when form.category is non-null and form.amount passes validation; create a disabled variant with reduced opacity (38% alpha on the background) for the Figma component. On tap this dispatches the saveBudget action which persists a BudgetEntry to DataStore via androidx.datastore and kotlinx-serialization.

Below the form card, outside it, add the storage transparency hint text in bodySmall style (12sp, weight 400, #41474D): "Budgets are stored locally on your device." Apply 16dp horizontal padding, 8dp vertical padding.

Next, place another section header reading "June 2026" (the currentMonthLabel from demo-data). Same labelLarge style as "Set budget", with 16dp horizontal padding and 8dp top padding.

Now build the budget card list. There are six budget cards stacked vertically with 8dp gaps. Each card has: background tint #EBEEF3, elevation 1dp, 12dp corner radius, 16dp internal padding, horizontal margin 16dp. Auto Layout: direction vertical, item spacing 8dp.

For each card, the layout inside is a vertical Auto Layout with item spacing 8dp:

Row 1 — list item header: a horizontal Auto Layout (direction horizontal, alignment center_vertical, item spacing auto/space-between). Left side: category name in titleSmall (14sp, weight 500, #181C20), supporting text in bodySmall (12sp, weight 400, #41474D) formatted as "£{used} of £{limit}". Right side trailing: the remaining or over amount in bodySmall (12sp, weight 400); for under-budget cards this is #41474D, for over-budget cards this is #BA1A1A. Set the title and supporting text as a vertical stack (gap 2dp) on the left, weight 1 (fill available width). The accessibility label for the whole row item is "{category}: spent £{used} of £{limit} budget".

Row 2 — linear progress bar: a horizontal bar spanning match_parent, height 6dp, corner radius 3dp. For under-budget cards the filled portion colour is #266489 (primary) and the track is #DDE3EA. For over-budget cards (Dining and Shopping), the filled portion is #BA1A1A (error) and the track is #FFDAD6 (error container). The bar fills according to the fraction value — for Dining (fraction 1.0) and Shopping (fraction 1.0), the bar is entirely filled in error red.

Row 3 — over-budget alert text: only visible when is_over_budget is true. Text in labelSmall (11sp, weight 500, #BA1A1A) reading "Over budget by £{amount}". For Groceries, Transport, Bills, and Subscriptions this layer is hidden; for Dining ("Over budget by £18.00") and Shopping ("Over budget by £24.99") it is visible. Create as a conditional layer in the card component.

Row 4 — action buttons row: a horizontal Auto Layout, direction horizontal, gap 8dp, alignment leading. Left: a text button labelled "View transactions" in labelMedium (12sp, weight 500, #266489), minimum touch 48dp. Right: a text button labelled "Delete" in labelMedium (12sp, weight 500, #BA1A1A), minimum touch 48dp. On "View transactions" tap, the navigateSpendingByCategory action fires, navigating to the spending-by-category screen with the category pre-filtered. On "Delete" tap, the deleteBudget action fires, removing the BudgetEntry from DataStore.

The six cards in order are:
Groceries: £198.50 of £400.00, fraction 0.496 (50%), remaining "£201.50 left", progress #266489, no alert.
Dining: £168.00 of £150.00, fraction 1.0 (100%), trailing "£18.00 over" in #BA1A1A, progress #BA1A1A, alert "Over budget by £18.00" visible.
Transport: £41.20 of £80.00, fraction 0.515 (52%), remaining "£38.80 left", progress #266489, no alert.
Bills: £197.40 of £220.00, fraction 0.897 (90%), remaining "£22.60 left", progress #266489, no alert.
Shopping: £124.99 of £100.00, fraction 1.0 (100%), trailing "£24.99 over" in #BA1A1A, progress #BA1A1A, alert "Over budget by £24.99" visible.
Subscriptions: £63.00 of £75.00, fraction 0.84 (84%), remaining "£12.00 left", progress #266489, no alert.

Auto Layout specs for the full screen content column: direction vertical, padding horizontal 16dp, top 8dp, bottom 96dp (clears the nav bar), item spacing 8dp (between major sections), sizing fill container.

Close the frame with the persistent bottom navigation bar identical to the loading state — all tabs unselected (none of Home, Accounts, Transactions, More corresponds to Budgets), all icons #41474D.

Component variants for budget_card: default, over-budget (error colours), hover (elevated shadow 3dp), pressed (ripple scrim #266489 at 12% opacity on card surface).

---

## State: Empty

Create a mobile frame at 393×852dp, background #F7F9FF. This state renders when no budget entries have been saved yet.

Begin with the same top app bar (56dp, back arrow, title "Budgets").

The budget creation form is fully visible in this state — the "Set budget" section header, the form card with category dropdown and amount field, and the "Set Budget" button, all identical to the content state. This allows the user to create their first budget without any separate action. Below the form card, show the storage hint text.

Below the storage hint, instead of the budgets list and its header, render the empty state component, vertically centred within the remaining space below the form (approximately 300dp of vertical space remains after the form and storage hint).

The empty state contains, in vertical sequence centred horizontally:

A Material Symbols icon "savings" at 48dp size, colour #41474D, with content description "No budgets set" for accessibility. The savings icon depicts a piggy bank silhouette — use the outlined variant from Material Symbols.

Below the icon with 16dp gap, the title "No budgets yet" in headlineSmall style (Roboto 24sp, line height 32sp, weight 400, colour #181C20), centre-aligned.

Below the title with 8dp gap, the body copy in bodyMedium style (14sp, line height 20sp, weight 400, colour #41474D, centre-aligned, max width 329dp = 393 − 64dp horizontal padding): "Set monthly spending limits for each category to track your habits against your real Open Banking transactions."

The empty state component has horizontal padding of 32dp on each side and is centred vertically in the available space.

Auto Layout specs for the empty state: direction vertical, alignment center_horizontal, padding horizontal 32dp, top 48dp, bottom 32dp, item spacing 8dp, sizing hug height.

Close the frame with the bottom navigation bar identical to content state.

Component variants: default empty, dark mode (icon #B7C9D9, title #E0E3E8, body #B7C9D9 on #101417 background).

---

## State: Error

Create a mobile frame at 393×852dp, background #F7F9FF. This state renders when the DataStore read fails on mount (EC-BUD-004: IOException).

Begin with the same top app bar (56dp, back arrow, title "Budgets"). Unlike the content and empty states, no form is visible here — the screen is dedicated to the error recovery experience.

Centre the error state component vertically within the 852 − 56 − 80 = 716dp available body space (accounting for top app bar and bottom nav). Apply 32dp horizontal padding.

The error state contains, in vertical sequence centred horizontally:

A Material Icons "error_outline" icon at 48dp size, colour #BA1A1A (error), with content description "Error loading budgets". This icon uses the outlined style and conveys a problem state.

Below the icon with 16dp gap, the title "Couldn't load budgets" in headlineSmall style (Roboto 24sp/32sp, weight 400, colour #181C20, centre-aligned).

Below the title with 8dp gap, the body copy in bodyMedium style (14sp/20sp, weight 400, colour #41474D, centre-aligned, max width 329dp): "Something went wrong reading your saved budget data. Please try again."

Below the body with 24dp gap, the retry button. Use a Tonal Button (M3 FilledTonalButton): background fill #D3E5F5 (secondary container), text colour #266489 (primary), label "Try again" in labelLarge (14sp, weight 500), height 48dp, corner radius 9999dp (full pill). Width: match_parent of the container (329dp after 32dp each side). This button dispatches the retryLoad action which transitions back through the loading state and re-reads DataStore.

Auto Layout specs for error state: direction vertical, alignment center_horizontal, padding horizontal 32dp, sizing hug height, item spacing as described.

Close with the persistent bottom navigation bar.

Component variants for retry_load_button: default (bg #D3E5F5, text #266489), pressed (ripple #266489 12% opacity), disabled (not applicable here — always enabled in error state), dark mode (bg #384956, text #95CDF7).

---

## Prototype Interaction Flow

The following interactions connect the Budgets frames in the Figma prototype:

From any state, tapping the back arrow in the top app bar navigates back to the previous screen in the navigation stack (use Figma Smart Animate → Back gesture, transition: slide-left, duration 300ms ease-in-out).

Loading → Content: after the skeleton animation completes (simulate with a 1.5s delay trigger in Figma prototype or use the "After Delay 1500ms" interaction on the skeleton frame), transition to the content state using a cross-dissolve fade animation (Dissolve, 300ms).

Loading → Empty: same trigger path as loading → content but targets the empty frame.

Loading → Error: same trigger path, targets the error frame.

Error frame: tapping the "Try again" button triggers a transition back to the loading state (Dissolve, 150ms) to simulate the retry attempt.

Content and Empty frames: tapping the "Set Budget" button (when enabled) triggers a brief confirmation flash (the button shows a ripple) and the list refreshes — in the prototype, simulate this as a self-transition on the content frame with a Smart Animate, 300ms ease.

Content frame: tapping "View transactions" on any budget card navigates to the spending-by-category screen. Use Navigate To → spending-by-category frame, slide-up transition (Push, 300ms).

Content frame: tapping "Delete" on any budget card removes that card from the list. In the prototype simulate by linking to a variant of the content frame with that card removed. Use Smart Animate, 200ms ease-out.

Category dropdown: tapping the dropdown opens a bottom sheet overlay listing the seven options (Groceries, Transport, Dining, Bills, Shopping, Subscriptions, Income). Each option when tapped updates the displayed selected value and closes the sheet. Prototype this as an overlay transition (slide-up from bottom, 300ms).

Form validation: create a variant of the form card called "amount-error" where the amount field shows a red outline and an inline error message below it. In the prototype, link the "Set Budget" button when the amount is empty to transition to this variant using Instant to simulate synchronous validation.

---

## Accessibility Specifications

Every interactive element must meet WCAG AA contrast standards. Verify:

The primary button (#266489 on #FFFFFF) achieves 4.88:1 contrast — passes AA for normal text.
The error colour (#BA1A1A on #F7F9FF) achieves 4.72:1 contrast — passes AA.
The secondary text (#41474D on #F7F9FF) achieves 7.54:1 contrast — passes AAA.
The disabled button text if shown (onSurfaceVariant #41474D at 38% alpha on surface) drops below 3:1 — use the M3 disabled alpha convention; screen-reader should announce "disabled".

All interactive components (dropdown, text field, both text buttons, the save button, the retry button, each budget card row) must have a minimum touch target of 48×48dp, enforced via invisible overlay tap zones in Figma if the visible component is smaller.

Content descriptions for screen reader:
- Top app bar back arrow: "Navigate back"
- budget_category_dropdown: "Category — currently Groceries, double tap to change"
- budget_amount_field: "Monthly limit in pounds, enter a number above zero"
- save_budget_button: "Set Budget"
- budget_progress_bar (Groceries): "Groceries budget: 50% used"
- budget_progress_bar (Dining): "Dining budget: 100% used"
- over_budget_alert (Dining): "Dining is over budget"
- view_category_spend_button (Groceries): "View transactions for Groceries"
- delete_budget_button (Groceries): "Delete budget for Groceries"
- empty state icon: "No budgets set"
- retry_load_button: "Try again"

Add a "Reduce Motion" design variant for each animated component. In the reduced-motion variant: skeleton shimmer is a static #DDE3EA fill with no gradient sweep; all transitions use opacity cross-fades at 150ms instead of slides.

---

## Component Library Mapping

Create the following Figma component definitions for the Budgets screen:

BudgetCard — a component with properties: category (string), usedAmount (string), limitAmount (string), fractionValue (number 0–1), remainingLabel (string), isOverBudget (boolean), and overBudgetLabel (string). Wire the isOverBudget boolean to a boolean property that toggles the over_budget_alert text layer and switches the progress bar and trailing label colours between primary (#266489) and error (#BA1A1A) palettes.

BudgetFormCard — a component with properties: selectedCategory (string, default "Groceries"), amountValue (string, default empty), hasValidationError (boolean), validationMessage (string). Wire hasValidationError to show/hide the inline error text layer below the amount field and switch the field outline from #72787E to #BA1A1A.

BudgetProgressBar — a primitive component: width match_parent, height 6dp, radius 3dp. Properties: fillFraction (0–1), isOverBudget (boolean). Fill layer clips to fillFraction × component width. Colour: #266489 when isOverBudget false, #BA1A1A when true. Track: #DDE3EA when not over, #FFDAD6 when over.

BudgetsEmptyState — a component with the savings icon, title, and body. No interactive children.

BudgetsErrorState — a component with error icon, title, body, and the retry tonal button. The retry button is always enabled.

BudgetsTopAppBar — extend the shared OpenBanking TopAppBar component: variant small, title slot "Budgets", leading back_arrow, no trailing actions.

BudgetsBottomNav — use the shared OpenBanking BottomNav component: four tabs (Home, Accounts, Transactions, More), no tab selected (Budgets is not a root nav destination).

---

## Semantic Token — Figma Variable Mapping

Define these in your Figma design system variables panel under the "Open Banking / Trust Blue" collection:

| Token name | Figma variable path | Hex value (light mode) |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/on-primary | #FFFFFF |
| primaryContainer | color/primary-container | #C9E6FF |
| onPrimaryContainer | color/on-primary-container | #004B6F |
| secondary | color/secondary | #50606E |
| secondaryContainer | color/secondary-container | #D3E5F5 |
| onSecondaryContainer | color/on-secondary-container | #384956 |
| error | color/error | #BA1A1A |
| errorContainer | color/error-container | #FFDAD6 |
| background | color/background | #F7F9FF |
| onBackground | color/on-background | #181C20 |
| surface | color/surface | #F7F9FF |
| surfaceContainer | color/surface-container | #EBEEF3 |
| surfaceVariant | color/surface-variant | #DDE3EA |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| outline | color/outline | #72787E |

Bind all colour fills in every component to these Figma variables so that switching the collection mode to "dark" automatically resolves all tokens to the dark-mode values (primary: #95CDF7, error: #FFB4AB, background: #101417, surfaceContainer: #1C2024, onBackground: #E0E3E8, etc.).
