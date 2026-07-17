# Direct Debits — Figma Design Prompts

> Generated from `screens/direct-debits/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) — Material Design 3 light theme
> Design system: Open Banking — Trust Blue (seed #266489)

---

## Design System Foundation

### Canvas and Grid Setup

Create a Figma frame sized 393×852dp to represent a Pixel 5 physical device. Set the fill to the surface colour #F7F9FF. Apply an 8-column grid with 16dp margins on each side and 8dp gutters. Add a baseline grid at 4dp to align spacing increments. Enable safe-area guides: 64dp top (top app bar) and 80dp bottom (navigation bar), both inset from the frame edges.

This screen always includes two persistent chrome components: a Material Design 3 small top app bar at the top of the frame and a navigation bar at the bottom. These sit outside the scrollable content area and appear in every state variant.

### Semantic Token → Figma Variable Mapping

Create a Figma variable collection named `Open Banking / Trust Blue` with a single mode called `Light`. Map each semantic token to a Figma variable so that swapping modes automatically updates all components.

| Semantic Token | Hex Value | Figma Variable Path |
|---|---|---|
| primary | #266489 | `color/primary` |
| onPrimary | #FFFFFF | `color/on-primary` |
| primaryContainer | #C9E6FF | `color/primary-container` |
| onPrimaryContainer | #004B6F | `color/on-primary-container` |
| secondary | #50606E | `color/secondary` |
| onSecondary | #FFFFFF | `color/on-secondary` |
| secondaryContainer | #D3E5F5 | `color/secondary-container` |
| surface | #F7F9FF | `color/surface` |
| onSurface | #181C20 | `color/on-surface` |
| surfaceVariant | #DDE3EA | `color/surface-variant` |
| onSurfaceVariant | #41474D | `color/on-surface-variant` |
| surfaceContainerLow | #F1F4F9 | `color/surface-container-low` |
| outline | #72787E | `color/outline` |
| outlineVariant | #C1C7CE | `color/outline-variant` |
| error | #BA1A1A | `color/error` |
| onError | #FFFFFF | `color/on-error` |
| background | #F7F9FF | `color/background` |
| scrim | #000000 | `color/scrim` |

### Typography Scale

Set up a Figma text style collection named `Open Banking / Roboto` using Roboto as the font family throughout. Create the following named text styles:

- **headlineSmall** — Roboto Regular, 24sp, line-height 32sp. Used for previous payment amounts within mandate cards. Colour: `color/on-surface` (#181C20).
- **titleMedium** — Roboto Medium, 16sp, line-height 24sp. Used for originator names (mandate card headings). Colour: `color/on-surface` (#181C20).
- **titleLarge** — Roboto Regular, 22sp, line-height 28sp. Used for the top app bar title "Direct Debits". Colour: `color/on-surface` (#181C20).
- **bodyMedium** — Roboto Regular, 14sp, line-height 20sp. Used for the empty state body and error body text. Colour: `color/on-surface-variant` (#41474D).
- **bodySmall** — Roboto Regular, 12sp, line-height 16sp. Used for the last-collected date label. Colour: `color/on-surface-variant` (#41474D).
- **labelLarge** — Roboto Medium, 14sp, line-height 20sp. Used for button labels ("Try again"). Colour: `color/on-primary` (#FFFFFF) on filled buttons.
- **labelMedium** — Roboto Medium, 12sp, line-height 16sp. Used for chip labels in the summary chip group.
- **labelSmall** — Roboto Medium, 11sp, line-height 16sp. Used for mandate reference IDs (dd_mandate_id). Colour: `color/on-surface-variant` (#41474D).

### Spacing and Shape

Define a spacing variable collection with the following values sourced from `design-tokens.yaml`:

The base unit is 4dp. Common multiples used in this screen are 8dp (gap between mandate cards and between chip group items), 12dp (card corner radius), 16dp (screen horizontal padding and card internal padding), 24dp (badge and chip internal horizontal padding), and 32dp (empty/error state horizontal padding). The navigation bar and top app bar use 0dp corner radius as they span the full width.

Pills (chips, badges, retry button) use `radius/full` which equals 9999dp, producing a fully rounded shape at any height.

---

## Frame: Loading State

Create a frame named `DirectDebits/Loading` at 393×852dp. Set the background fill to `color/surface` (#F7F9FF).

### Top App Bar

Place a small Material Design 3 top app bar across the full width of the frame at the top, spanning 393dp wide and 64dp tall. Set its background fill to `color/surface` (#F7F9FF) with no elevation tint. Add a navigation icon on the left edge: use the Material Symbols `arrow_back` icon at 24dp, filled with `color/on-surface` (#181C20). Expand the touch target for this icon to 48×48dp using Auto Layout padding so it meets the minimum accessibility target. Title this component `back_button` and give it an accessibility label "Back to account details". Place the text "Direct Debits" centred vertically in the bar using the `titleLarge` text style (22sp Roboto Regular, `color/on-surface` #181C20).

### Skeleton Placeholder Cards

Below the top app bar, create a vertical Auto Layout column (direction: vertical, item spacing: 8dp, padding: 16dp horizontal, 16dp top). Name it `loading_skeleton`. Inside this column, place four identical skeleton card frames.

Each skeleton card should be 361dp wide (full width minus 32dp screen margins) and 80dp tall, with a corner radius of 12dp. Fill each card with the `color/surface-variant` (#DDE3EA). Apply a shimmer animation effect by setting the fill opacity to animate between 30% and 60% over 1.5 seconds in a repeating loop — in Figma, represent this with a gradient shimmer overlay using a linear gradient from transparent to `color/surface-variant` (#DDE3EA) at 60% opacity and back to transparent, sweeping left to right. For designers using Figma's smart animate, add a flow trigger that loops between two variant positions of the skeleton. Label the four frames `skeleton_card_1` through `skeleton_card_4`.

Add a group-level accessibility annotation: "Loading direct debits". Note in a design comment that for users with reduced motion preferences, the shimmer animation should be replaced with a static fill at 50% opacity.

### Navigation Bar (Loading)

At the bottom of the frame, place the navigation bar spanning 393dp wide and 80dp tall. Set its fill to `color/surface` (#F7F9FF). It contains four navigation items evenly spaced using an Auto Layout row with equal distribution. Label and icon each item:

- **Home** — icon `home` 24dp, label "Home" using `labelMedium` style. This item is in its default (unselected) state: icon tint `color/on-surface-variant` (#41474D), indicator absent.
- **Accounts** — icon `account_balance` 24dp, label "Accounts". This item is in the **selected** state because the user arrived from the account-detail screen (which is within the Accounts flow): icon tint `color/primary` (#266489), apply a pill-shaped indicator behind the icon using `color/secondary-container` (#D3E5F5) at 64dp wide and 32dp tall.
- **Transactions** — icon `receipt_long` 24dp, label "Transactions". Default, unselected. Icon tint #41474D.
- **More** — icon `more_horiz` 24dp, label "More". Default, unselected. Icon tint #41474D. Target screen: settings.

---

## Frame: Content State

Create a frame named `DirectDebits/Content` at 393×852dp with fill `color/surface` (#F7F9FF). Use the same top app bar and navigation bar design described in the loading state. The body area between the top app bar (bottom edge at y=64dp) and the navigation bar (top edge at y=772dp) contains a vertically scrollable region. Model this as an Auto Layout column (direction: vertical, item spacing: 0dp, padding: 0dp) that clips content and supports vertical scrolling.

### Mandate Summary Chip Group

At the top of the scrollable body, place a horizontal Auto Layout row named `mandate_summary_chips`. Set its padding to 16dp left, 16dp right, 16dp top, 8dp bottom. Set item spacing to 8dp. This chip group is purely informational — it has no tap interaction.

Create two chips inside this row:

The first chip is `active_count_chip`, representing three active direct debit mandates. Design it as an assist chip with a filled container. Set the container fill to `color/primary-container` (#C9E6FF) and the label text colour to `color/on-primary-container` (#004B6F). The chip label reads "Active (3)" using `labelMedium` text style (12sp Roboto Medium). Set the chip height to 32dp and corner radius to 9999dp (full pill). Set horizontal internal padding to 12dp on each side. Give this chip an accessibility label "3 Active direct debits".

The second chip is `inactive_count_chip`, representing one inactive mandate. Design it as an outlined chip. Set the container fill to transparent, add a 1dp border stroke using `color/outline` (#72787E), and set the label text colour to `color/on-surface-variant` (#41474D). The label reads "Inactive (1)" using `labelMedium`. Same height (32dp), corner radius (9999dp), and internal horizontal padding (12dp) as the first chip. Accessibility label: "1 Inactive direct debit".

### Mandate Card List

Below the chip group, create a vertical Auto Layout column named `direct_debits_list`. Set its padding to 0dp top, 16dp horizontal, 16dp bottom, with 8dp item spacing between cards. This list renders four cards based on the demo data from `demo-data.yaml`, sorted Active-first by the ViewModel.

**Card Design — DirectDebitCard Component**

Design a reusable component named `DirectDebitCard` with two variants: `status=Active` and `status=Inactive`. Each card is 361dp wide (fill to container minus 16dp padding on each side). Set Auto Layout direction to vertical, padding 16dp on all sides, item spacing 8dp between each child text element. Set the card fill to `color/surface-container-low` (#F1F4F9) and apply a Material Design 3 Level 1 elevation effect — a subtle drop shadow with 1dp blur radius, Y offset 1dp, and the shadow colour set to #000000 at approximately 15% opacity. Apply a corner radius of 12dp.

Inside each card, stack these five elements vertically:

1. **dd_originator_name** — A text element using the `titleMedium` style (16sp Roboto Medium, `color/on-surface` #181C20). Set this as a heading within the card for screen reader navigation. The text wraps to a maximum of 2 lines before truncating with an ellipsis.

2. **dd_status_badge** — A compact badge element. For the Active variant, fill the badge container with `color/primary-container` (#C9E6FF), set label text colour to `color/on-primary-container` (#004B6F), apply corner radius 9999dp (pill). For the Inactive variant, leave the container transparent, add a 1dp border stroke in `color/outline` (#72787E), and set label text colour to `color/on-surface-variant` (#41474D). Both variants: height 24dp, horizontal internal padding 8dp, label using `labelSmall` style (11sp Roboto Medium). Accessibility label prefix "Status: " followed by the status value.

3. **dd_previous_amount** — A prominent text element using the `headlineSmall` style (24sp Roboto Regular, `color/on-surface` #181C20). This displays the last collected payment amount in locale-formatted GBP. Critically, this amount field uses the neutral `onSurface` colour (#181C20), not the error colour — direct debit amounts are not inherently negative spending from the user's perspective.

4. **dd_previous_date** — A smaller supporting text element using `bodySmall` style (12sp Roboto Regular, `color/on-surface-variant` #41474D). Prefixed with the label "Last collected: " followed by the locale-formatted date.

5. **dd_mandate_id** — The smallest text in the card, using `labelSmall` style (11sp Roboto Medium, `color/on-surface-variant` #41474D). Prefixed with "Mandate: " followed by the mandate reference identifier.

**Populating the Four Cards (from demo-data.yaml)**

Place four instances of the `DirectDebitCard` component in the list, using the real data from the sandbox fixture:

Card 1 — Active, originator "British Gas", amount "£78.00", date "Last collected: 15 Jun 2026", mandate "Mandate: DD-BG-44120". Use the `status=Active` variant: badge fills #C9E6FF, text #004B6F. Card accessibility label: "British Gas, Active".

Card 2 — Active, originator "Vodafone", amount "£29.00", date "Last collected: 20 Jun 2026", mandate "Mandate: DD-VF-88301". Use the `status=Active` variant. Card accessibility label: "Vodafone, Active".

Card 3 — Active, originator "Aviva Insurance", amount "£41.50", date "Last collected: 05 Jun 2026", mandate "Mandate: DD-AV-10293". Use the `status=Active` variant. Card accessibility label: "Aviva Insurance, Active".

Card 4 — Inactive, originator "TV Licensing", amount "£13.25", date "Last collected: 01 Mar 2026", mandate "Mandate: DD-TVL-55667". Use the `status=Inactive` variant: badge transparent container, 1dp border #72787E. Card accessibility label: "TV Licensing, Inactive". Note in a design annotation that the ViewModel sorts Active mandates to the top and Inactive mandates to the bottom, so this card always appears last regardless of the order returned by the HSBC OBIE API.

---

## Frame: Empty State

Create a frame named `DirectDebits/Empty` at 393×852dp with fill `color/surface` (#F7F9FF). Use the same top app bar and navigation bar as all other states.

In the body region between the two chrome bars, create a vertical Auto Layout column centred both horizontally and vertically within the available 708dp body height (852 minus 64 top bar minus 80 bottom nav). Set padding to 32dp horizontal and 0dp vertical. Set item spacing to 16dp between the icon, title, and body text.

Place the Material Symbols icon `subscriptions` at 48dp by 48dp, coloured with `color/on-surface-variant` (#41474D). This icon is not decorative — give it a contentDescription of "No direct debit mandates" for screen readers.

Below the icon, add a headline text element using the `headlineSmall` style (24sp Roboto Regular, `color/on-surface` #181C20) centred horizontally. The text reads "No direct debit mandates registered". Set maximum lines to 2 with centred text alignment.

Below the headline, add a body text element using the `bodyMedium` style (14sp Roboto Regular, `color/on-surface-variant` #41474D) centred horizontally. The text reads "No direct debit mandates are registered for this account." This is the resolved string from `docs.yaml` error_cases EmptyResult user_message. Set maximum lines to 3 with centred text alignment.

There are no action buttons in this state. The user can only press the back button in the top app bar to return to account-detail. Note in a design comment that this state occurs when the OBIE API returns HTTP 200 with an empty `Data.DirectDebit` array — it is a valid response, not an error.

---

## Frame: Error State

Create a frame named `DirectDebits/Error` at 393×852dp with fill `color/surface` (#F7F9FF). The error frame requires two variants: `retriable=true` (shown for 401 TokenExpired, 429 RateLimited, and network errors) and `retriable=false` (shown for 403 ConsentRevoked only). Use the same top app bar and navigation bar as all other states.

In the body region, use the same centred vertical Auto Layout column as the empty state, with 32dp horizontal padding and 16dp item spacing.

Place the Material Symbols icon `error_outline` at 48dp by 48dp, coloured with `color/error` (#BA1A1A). This icon is not decorative — give it a contentDescription of "Error loading direct debits".

Below the icon, add a headline using `headlineSmall` style (24sp Roboto Regular, `color/on-surface` #181C20) centred. Text: "Unable to load direct debits".

Below the headline, add a body text element using `bodyMedium` style (14sp Roboto Regular, `color/on-surface-variant` #41474D) centred. This field is bound to `error.userMessage` and changes based on the error type. For the primary demo variant (401 TokenExpired), the text reads "Session expired. Please log in again." For the 403 ConsentRevoked variant, it reads "Account access consent has been revoked. Re-authorise in Consents." For the 429 RateLimited variant: "Too many requests. Please wait a moment and try again." For a network error: "No network connection. Check your connection and retry." Add all four text variants as overrideable string properties on the Figma component.

**Retry Button — Retriable Variant**

For the `retriable=true` component variant, add a filled button below the body text. Create a button component named `retry_button` with Auto Layout (direction: horizontal, padding: 16dp vertical 20dp horizontal, centred alignment). Set the fill to `color/primary` (#266489) and the corner radius to 9999dp (full pill). Set the minimum width to 56dp and ensure the height is 56dp to meet the 48dp minimum touch target requirement with an additional visual weight. The label text reads "Try again" using `labelLarge` style (14sp Roboto Medium, `color/on-primary` #FFFFFF). The button spans match_parent minus 32dp horizontal padding from the screen edges (265dp wide). Accessibility label: "Retry loading direct debits".

**Retry Button — Non-Retriable Variant**

For the `retriable=false` component variant (403 ConsentRevoked), hide the retry button entirely. The user cannot retry because their consent does not include the ReadDirectDebits permission. They must navigate to the consent-list screen to re-authorise — this is communicated through the body text. No secondary action button exists in the current ui.yaml specification.

---

## Component Variants

### DirectDebitCard Variants

Design the `DirectDebitCard` Figma component with a `status` property containing two options: `Active` and `Inactive`. The structural layout (Auto Layout vertical, padding 16dp, item spacing 8dp, card bg #F1F4F9, elevation 1, radius 12dp) is identical between variants. Only the `dd_status_badge` child changes:

- **Active badge**: container fill `color/primary-container` (#C9E6FF), label colour `color/on-primary-container` (#004B6F), no border stroke.
- **Inactive badge**: container fill transparent, border stroke 1dp `color/outline` (#72787E), label colour `color/on-surface-variant` (#41474D).

The `dd_originator_name`, `dd_previous_amount`, `dd_previous_date`, and `dd_mandate_id` fields are identical in colour and style across both variants; only their text content changes per instance.

### Status Badge Variants

Design a standalone `StatusBadge` component with two variants matching the two status codes in the OBIE OBReadDirectDebit2 schema:

- **Active** (primary tonal): height 24dp, corner radius 9999dp, fill `color/primary-container` (#C9E6FF), label `color/on-primary-container` (#004B6F), `labelSmall` text style.
- **Inactive** (outline): height 24dp, corner radius 9999dp, transparent fill, 1dp border `color/outline` (#72787E), label `color/on-surface-variant` (#41474D), `labelSmall` text style.

Both variants use 8dp horizontal internal padding and wrap their width to content. These badges are not interactive — they do not have hover or pressed states.

### Summary Chip Variants

The `mandate_summary_chips` chip group uses two chip variants, both at 32dp height with corner radius 9999dp:

- **active_count_chip (tonal)**: fill `color/primary-container` (#C9E6FF), label `color/on-primary-container` (#004B6F), no border. Uses `labelMedium` style. Displays the ViewModel-computed active mandate count.
- **inactive_count_chip (outline)**: transparent fill, 1dp border `color/outline` (#72787E), label `color/on-surface-variant` (#41474D), no fill. Uses `labelMedium` style.

Neither chip has a hover or pressed state because they are display-only components with no `on_click` interaction.

### Retry Button States

Design the `retry_button` filled pill button with the following interactive states for prototyping:

- **Default**: bg `color/primary` (#266489), label `color/on-primary` (#FFFFFF).
- **Hovered**: bg `color/primary` (#266489) with a white overlay at 8% opacity.
- **Pressed**: bg `color/primary` (#266489) with a white overlay at 12% opacity, scale transform 0.98.
- **Disabled**: bg `color/on-surface` (#181C20) at 12% opacity, label `color/on-surface` (#181C20) at 38% opacity. Used internally; this button is simply hidden (not disabled) for the 403 error case.

---

## Auto Layout Specifications

### Screen-Level Layout

The overall screen uses a fixed frame (393×852dp) as the container. It is not Auto Layout at the screen level — instead it contains three fixed-position elements: the top app bar pinned to the top edge (y=0, h=64dp), the navigation bar pinned to the bottom edge (y=772dp, h=80dp), and a scrollable body content frame spanning y=64dp to y=772dp (708dp tall, full width).

### Scrollable Body

The scrollable body frame uses a clip-content Auto Layout column with direction: vertical, item spacing: 0dp, no padding at the frame level (padding is handled within each child section). Overflow: scroll vertically.

### Chip Group Auto Layout

`mandate_summary_chips`: direction horizontal, item spacing 8dp, padding-left 16dp, padding-right 16dp, padding-top 16dp, padding-bottom 8dp. Width: fill container. Height: hug contents (approximately 64dp total including padding).

### Card List Auto Layout

`direct_debits_list`: direction vertical, item spacing 8dp, padding-left 16dp, padding-right 16dp, padding-top 0dp, padding-bottom 16dp. Width: fill container. Height: hug contents.

### Card Auto Layout

Each `DirectDebitCard`: direction vertical, padding 16dp on all sides, item spacing 8dp. Width: fill container (361dp when the list has 16dp horizontal padding). Height: hug contents (approximately 168dp given the five stacked text elements). Corner radius: 12dp.

### Empty / Error State Body Auto Layout

The centred body for empty and error states: direction vertical, item spacing 16dp, padding-left 32dp, padding-right 32dp, vertical alignment centre (use Figma's align-to-frame option). Width: fill container. Height: 708dp (full body height) to ensure vertical centring works correctly.

### Navigation Bar Auto Layout

`bottom_nav`: direction horizontal, item spacing 0dp, no padding (equal distribution between four items). Width: fill container (393dp). Height: 80dp fixed. Each tab item: direction vertical, item spacing 4dp, padding-top 12dp, padding-bottom 16dp, width fill with equal weight. Icon 24dp, label `labelMedium` text style.

---

## Prototype Interaction Flow

Set up Figma prototype connections between the four state frames using the following rules derived from the `action_contract` declarations in `ui.yaml`:

### Back Button → account-detail

From any state frame (`DirectDebits/Loading`, `DirectDebits/Content`, `DirectDebits/Empty`, `DirectDebits/Error`), connect the `back_button` (arrow_back icon in the top app bar) with a tap trigger to the `AccountDetail` screen. Use the "Navigate to" action with a slide-out-right transition at 300ms emphasised easing (cubic-bezier 0.2, 0.0, 0, 1.0). This represents `action_contract.effect: navigate` for `navigate_back` targeting `account-detail`.

### Error Screen → Loading (Retry)

From the `DirectDebits/Error` frame, connect the `retry_button` (only present in the `retriable=true` variant) with a tap trigger to the `DirectDebits/Loading` frame, then continue to `DirectDebits/Content` after a 1.5 second delay (simulating the API call). Use a "Navigate to" action with a dissolve transition at 300ms. This models `action_contract.effect: call_api` for `retry_load` which re-issues `GET /accounts/{AccountId}/direct-debits`.

### Loading → Content (Success Path)

Add a prototype animation from `DirectDebits/Loading` to `DirectDebits/Content` with a 2-second delay after reaching the loading frame (simulating a successful API response). Use a dissolve transition at 300ms. This simulates `DirectDebitsUiState.Loading` transitioning to `DirectDebitsUiState.Content`.

### Loading → Error (Failure Path)

Create an alternate connection from `DirectDebits/Loading` to `DirectDebits/Error` (retriable=true variant) to demonstrate the 401 TokenExpired error scenario. This can be triggered by a keyboard shortcut key in the prototype to switch between the happy and failure paths during user testing.

### Loading → Empty (Empty Data Path)

Create a connection from `DirectDebits/Loading` to `DirectDebits/Empty` to demonstrate the scenario where the OBIE API returns HTTP 200 with an empty `Data.DirectDebit` array.

---

## Accessibility

The Direct Debits screen must meet WCAG AA contrast requirements as specified in `design-tokens.yaml`. Review the following contrast ratios for the key colour pairs used on this screen:

The primary text colour `onSurface` (#181C20) on the surface background (#F7F9FF) achieves a contrast ratio of approximately 18.5:1, well above the 4.5:1 AA requirement for normal text. The `onSurfaceVariant` (#41474D) on `surface` (#F7F9FF) achieves approximately 7.8:1, meeting AA for normal text. The primary chip/badge text `onPrimaryContainer` (#004B6F) on `primaryContainer` (#C9E6FF) achieves approximately 5.2:1, meeting AA. The outline chip text `onSurfaceVariant` (#41474D) on the transparent (surface) background achieves approximately 7.8:1.

Minimum touch target size is 48×48dp as declared in `design-tokens.yaml#accessibility.min_touch_target_dp`. The `back_button` must have a 48×48dp touch target even though the icon is only 24dp. Achieve this by adding invisible padding around the icon or by using a 48dp minimum frame. The `retry_button` is 56dp tall, exceeding the 48dp minimum.

Every non-decorative icon and component must carry a `contentDescription` in the implementation. The `back_button` uses accessibility_label "Back to account details". The `subscriptions` icon in the empty state uses "No direct debit mandates". The `error_outline` icon in the error state uses "Error loading direct debits". The status badges carry "Status: Active" and "Status: Inactive" labels.

The mandate card list must support TalkBack / VoiceOver navigation by card. Each `DirectDebitCard` carries a group-level `accessibility_label` combining the originator name and status (for example, "British Gas, Active"). Inside the card, the heading role on `dd_originator_name` allows screen readers to navigate by headings within the list. The amount field `dd_previous_amount` should not be announced as a debit or negative amount — it represents the last collected amount, which is neutral financial information.

In Figma, annotate each interactive component with a red accessibility annotation marker indicating the contentDescription, the role (button, heading, image), and the minimum touch target size. Use the Figma Accessibility Annotation Kit plugin if available, or create manual annotation stickers in a dedicated `A11y` layer group that sits above the design layers but below the delivery handoff export slice.

For the retry button, add a disabled state annotation explaining that the button is hidden (not disabled) for the 403 ConsentRevoked error. This distinction is intentional: a disabled button implies the user could eventually tap it, whereas hiding it entirely correctly signals there is no retry path for a revoked consent.

---

## Component Anatomy Guide

### Top App Bar — Anatomy

The small top app bar on this screen is a single-row chrome element. From left to right: a 12dp left inset, then the navigation icon container (48×48dp, centred on the icon), then a 4dp gap, then the title text using `titleLarge` style that fills the remaining horizontal space, then optional trailing actions (none on this screen), then a 12dp right inset. The total bar height is 64dp including safe-area alignment at the top. The divider below the bar is absent in the loading, content, and empty states — a subtle bottom shadow or surface tint change from `color/surface` to `color/surface-container-low` is used to separate the bar from the scrollable content below. This matches Material Design 3's guidance for elevated top app bars on scroll.

The back arrow icon is `arrow_back` from the Material Symbols rounded variant at 24dp, using fill value 0 (outlined), weight 400, optical size 24. The icon colour maps to `color/on-surface` (#181C20) in the default state.

### DirectDebitCard — Anatomy Breakdown

Understanding the full anatomy of the `DirectDebitCard` component is essential for pixel-accurate implementation. The card contains five vertically stacked child elements within a 16dp padded container:

The first element, `dd_originator_name`, uses the largest type in the card at `titleMedium` (16sp). It is a semi-bold heading that uniquely identifies who is collecting the direct debit payment. Constrain it to a maximum of 2 lines with end-ellipsis overflow. This heading is announced first by screen readers when focus enters the card.

The second element, `dd_status_badge`, is a compact inline pill positioned directly below the originator name. It occupies the minimum width needed to contain its label text ("Active" or "Inactive") with 8dp horizontal padding. The badge height is fixed at 24dp — shorter than the 32dp chip height used in the chip group — because it is a secondary decorative indicator rather than a primary user action element. The two badge variants (primary tonal and outline) signal the mandate lifecycle state at a glance: teal-tinted fill for Active mandates, grey outline for Inactive ones.

The third element, `dd_previous_amount`, uses `headlineSmall` at 24sp — the largest text on the card. This deliberate sizing makes the monetary amount the most visually prominent piece of information within each mandate card. The amount should be formatted by the ViewModel as a locale-aware GBP currency string (e.g., "£78.00") rather than the raw API value "78.00 GBP". The colour is `color/on-surface` (#181C20) — the same neutral dark colour used for all primary text — because this is a collection amount, not an outgoing expense from the user's perspective.

The fourth element, `dd_previous_date`, uses `bodySmall` at 12sp in `color/on-surface-variant` (#41474D). The label prefix "Last collected: " is followed by the ISO-8601 date formatted by the ViewModel into a locale-aware short date (e.g., "15 Jun 2026"). This label provides the recency context for the amount shown above it.

The fifth element, `dd_mandate_id`, uses `labelSmall` at 11sp — the smallest type on screen — in `color/on-surface-variant` (#41474D). The prefix "Mandate: " followed by the mandate reference identifier (e.g., "DD-BG-44120") provides a reference number for support enquiries. This field is the least visually prominent because most users will never need it during normal browsing.

### Chip Group — Anatomy

The `mandate_summary_chips` chip group is positioned at the very top of the scrollable content body, just below the top app bar divider. It serves as a visual data summary — users can immediately see how many mandates are in each status category before reading the individual cards. The two chips sit in a horizontal row with 8dp spacing between them. Both chips hug their content width — the "Active (3)" chip will be slightly narrower than "Inactive (1)" in practice because "Active" is a shorter word.

The chip group carries a group-level accessibility label of "3 active, 1 inactive direct debit mandates". This allows screen readers to announce the summary in a single reading before the user moves on to the individual cards. Individual chip accessibility labels are "3 Active direct debits" and "1 Inactive direct debit".

### Empty State — Anatomy

The `empty_direct_debits` component follows the Material Design 3 empty state pattern: a centred icon at the top, a bold headline below it, and supporting body copy beneath the headline. There are no action buttons because the user has no actions available in this state — the account genuinely has no direct debit mandates registered.

The icon choice `subscriptions` from Material Symbols represents recurring payment arrangements, which is conceptually aligned with direct debit mandates. The icon renders at 48dp at `color/on-surface-variant` (#41474D) — a medium-weight grey that distinguishes it from primary actions without appearing broken or errored.

The vertical centring of this component within the 708dp body area is important. If the content is allowed to top-align, the empty state will appear visually unbalanced and users may mistake the blank space below for a loading failure. Figma's align-to-frame vertical centring mode achieves this automatically.

### Error State — Anatomy

The `error_state` component shares the same structural layout as the empty state (centred icon → headline → body) but uses the error colour token for its icon. The icon `error_outline` at 48dp in `color/error` (#BA1A1A) clearly communicates a failure condition. The icon uses the outlined variant rather than the filled variant to reduce visual aggression — the outlined error_outline feels informational rather than alarming.

The headline "Unable to load direct debits" is static (always the same regardless of error type). The body text is dynamic, bound to `error.userMessage` from the ViewModel. The ViewModel maps each HTTP status code to a distinct user-facing message that explains what happened and implicitly suggests next steps (logging in again for 401, waiting for 429, checking connection for network errors).

The `retry_button` appears only when `error.isRetriable` is true. For the three retriable errors (401, 429, network), the retry button is shown as a full-width pill button below the body text. For 403 ConsentRevoked, it is completely hidden — not disabled. This aligns with WCAG guidance that disabled interactive elements can confuse users who do not understand why they cannot proceed. A fully hidden button removes the false affordance entirely.

---

## Motion and Animation Specifications

### Loading State Skeleton Shimmer

The skeleton shimmer animation runs at low intensity per the `design-tokens.yaml#motion.intensity: low` setting. The shimmer gradient sweeps left to right across each skeleton card over a 1.5-second cycle time, using the `design-tokens.yaml#motion.durations.long: 450ms` value for the fade-in and fade-out of the gradient ends, while the sweep itself occupies the central 600ms. The animation eases using the `emphasis_easing: cubic-bezier(0.2, 0.0, 0, 1.0)` curve for a natural feel. For users who have enabled the system's reduced-motion setting, all animation is suppressed and the skeleton fills are displayed as static #DDE3EA without any sweep.

### State Transitions

When the ViewModel emits a new `DirectDebitsUiState`, the screen transitions between frames using a cross-dissolve at 300ms using the emphasis easing curve. This matches the `design-tokens.yaml#motion.durations.medium: 300ms` value. The cross-dissolve is chosen over a slide transition because the content is not hierarchically navigating deeper — it is updating in place as data loads. In Figma prototypes, model this as a "Dissolve" smart animate with 300ms duration.

The back navigation (back_button tap) uses a slide-out-right transition, consistent with the Material Design 3 shared-axis forward/back navigation pattern. The Direct Debits screen slides out to the right while the account-detail screen slides in from the left.

### Card List Entry Animation

When the content state first appears (transitioning from loading), each `DirectDebitCard` in the list should enter with a staggered fade-in animation. The first card fades in at 0ms, the second at 50ms, the third at 100ms, and the fourth at 150ms. Each fade-in uses `design-tokens.yaml#motion.durations.short: 150ms` duration with the emphasis easing curve. In Figma, model this with Smart Animate on a multi-frame prototype flow showing skeleton cards transforming into content cards.

---

## Dark Mode Considerations

The `design-tokens.yaml` file includes a complete dark mode colour set under `colors.dark`. While the primary design deliverable for this sprint is the light theme, the Figma component library should be built with mode support from the beginning to avoid costly retrofitting.

For dark mode, the key token substitutions that affect the Direct Debits screen are:

The surface background changes from #F7F9FF to #101417, making all card fills and the screen background substantially darker. The `surfaceContainerLow` token (card background) changes from #F1F4F9 to #181C20, maintaining the tonal distinction between card and background. The `primaryContainer` token (Active badge fill) changes from #C9E6FF to #004B6F, converting the light teal badge to a dark teal badge while retaining the brand colour family. The `onPrimary` text on the primary badge changes from #004B6F to #C9E6FF to maintain contrast on the dark container.

The `error` token changes from #BA1A1A to #FFB4AB in dark mode, converting the deep red to a lighter coral that maintains AA contrast on dark backgrounds. The retry button background uses `color/primary` which changes from #266489 to #95CDF7 in dark mode.

In Figma, set all colour fills and strokes to use the variable references from the `Open Banking / Trust Blue` collection. Switching the collection mode from `Light` to `Dark` should update every component automatically if the variables are correctly wired.

---

## Design Handoff Annotations

### Layer Naming Convention

Adopt the following layer naming convention in Figma to match the component IDs declared in `ui.yaml`. This allows engineers to map design layers directly to ViewModel binding targets:

- `back_button` — the back arrow icon button in the top app bar
- `mandate_summary_chips` — the chip group Auto Layout container
- `active_count_chip` — the first chip inside mandate_summary_chips
- `inactive_count_chip` — the second chip inside mandate_summary_chips
- `direct_debits_list` — the scroll container holding all cards
- `direct_debit_card` — each individual mandate card instance
- `dd_originator_name` — the originator name text inside each card
- `dd_status_badge` — the Active / Inactive badge inside each card
- `dd_previous_amount` — the amount text inside each card
- `dd_previous_date` — the date text inside each card
- `dd_mandate_id` — the mandate reference text inside each card
- `empty_direct_debits` — the empty state container
- `error_state` — the error state container
- `retry_button` — the retry call-to-action button in the error state
- `loading_skeleton` — the skeleton list container

### Export Specifications

For the four state frames, export as PNG at 3× resolution for device screenshots and as SVG for any icon assets. The navigation bar icons (home, account_balance, receipt_long, more_horiz) should be sourced from the Material Symbols icon font rather than exported as SVG files — import the TTF/variable font into Figma and use text nodes with the Symbols font.

For the `DirectDebitCard` component, export the component itself (not a frame instance) so engineers receive the component definition rather than a flattened snapshot.

Annotate the design with red-line spacing annotations covering: 16dp horizontal screen padding, 8dp card list gap, 12dp card corner radius, 16dp card internal padding, 8dp intra-card item spacing, 32dp empty/error state horizontal padding.

### Developer Notes

Add a developer notes section as a sticky note component in Figma near the content state frame:

The ViewModel sorts the directDebits list Active-first before it reaches the Compose LazyColumn. The UI layer does not need to handle sorting — it renders items in the order provided by DirectDebitsState. The activeCount and inactiveCount values are pre-computed by the ViewModel from the sorted list, not derived in the UI layer. The status_variant field on each OBDirectDebit2 object is added by the ViewModel's withStatusVariant() extension function and maps DirectDebitStatusCode "Active" to variant "primary" and "Inactive" to variant "outline". The badge component consumes this variant string directly to select its visual style.

The retry_button visibility is controlled by the error.isRetriable boolean on the DirectDebitsUiState.Error sealed class variant. The 403 ConsentRevoked error has isRetriable set to false because the ReadDirectDebits permission has been removed from the user's AISP consent. No retry is possible until the user re-authorises through the consent-list screen, which they reach by navigating away via the back button.
