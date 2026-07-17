# Product Terms — Figma Design Prompts

> Generated from `screens/product/ui.yaml` + `demo-data.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Roboto · bg #F7F9FF
> Design system: Open Banking — Trust Blue (seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

### Resolved Colour Palette

Create a Figma colour library with the following styles under a collection named "Open Banking / Trust Blue (Light)":

The primary brand colour is Trust Blue at #266489. Use this for the top app bar back arrow, circular progress indicator fill, check_circle feature icons, and the filled retry button background. Its container pair, #C9E6FF, serves as the selected tab indicator background and elevated card tints where a brand wash is desired.

The surface system uses #F7F9FF as the page background and top app bar background. Cards at Material 3 elevation level 2 adopt #EBEEF3 (surfaceContainer) as their background, giving a subtle lift without heavy shadow. Use #F1F4F9 (surfaceContainerLow) for any divider regions or subtle inset panels.

For text, apply #181C20 (onSurface) to all primary body copy, product names, trailing amounts, and feature text. Secondary descriptive labels — product type overline, section subheadings, supporting list text — use #41474D (onSurfaceVariant). The secondary semantic colour #50606E applies specifically to the product type overline label to give it a de-emphasised badge feel.

Financial risk indicators — overdraft EAR rates — use #BA1A1A (error), which passes WCAG AA contrast against both white and the #F7F9FF background. Apply this colour only to the trailing EAR percentage text in overdraft rows, signalling high-cost credit to the user.

Outline and divider lines use #C1C7CE (outlineVariant) at 1dp height. Do not use border-heavy separators; rely on a single thin line between section header and list content.

### Roboto Type Scale

Set up the following text styles in Figma using Roboto (auto-imported from Google Fonts):

titleLarge / 22sp / line-height 28sp / weight 400 — used for the top app bar title.
headlineMedium / 28sp / line-height 36sp / weight 400 — used for the product name.
titleMedium / 16sp / line-height 24sp / weight 500 — used for all trailing amount and rate values (£0.00, 0.15% AER, 39.9% EAR).
bodyMedium / 14sp / line-height 20sp / weight 400 — used for supporting text in list items and feature strings.
labelMedium / 12sp / line-height 16sp / weight 500 — used for the product type overline (PCA / BCA).
labelSmall / 11sp / line-height 16sp / weight 500 — used for the product ID caption and section header labels (FEES, CREDIT INTEREST, OVERDRAFT, FEATURES).
headlineSmall / 24sp / line-height 32sp / weight 400 — used for the empty and error state titles.

### Semantic Token → Figma Variable Mapping

Create a Figma variable collection named "Tokens / Open Banking Light" with the following bindings:

| Token name | Figma variable | Hex value |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/onPrimary | #FFFFFF |
| primaryContainer | color/primaryContainer | #C9E6FF |
| onPrimaryContainer | color/onPrimaryContainer | #004B6F |
| secondary | color/secondary | #50606E |
| onSecondary | color/onSecondary | #FFFFFF |
| background | color/background | #F7F9FF |
| surface | color/surface | #F7F9FF |
| surfaceContainer | color/surfaceContainer | #EBEEF3 |
| surfaceContainerLow | color/surfaceContainerLow | #F1F4F9 |
| onSurface | color/onSurface | #181C20 |
| onSurfaceVariant | color/onSurfaceVariant | #41474D |
| outlineVariant | color/outlineVariant | #C1C7CE |
| error | color/error | #BA1A1A |
| onError | color/onError | #FFFFFF |

---

## Frame 1 — Loading State

### Frame Setup

Create a frame named "Product Terms / Loading" sized 393×852. Set the background fill to #F7F9FF. Apply Auto Layout with vertical direction, zero item spacing, and no padding — this frame is the outermost shell.

### Top App Bar Region

Within the frame, add a top region 393 wide and 56 tall with a #F7F9FF fill and no visible border. Inside this region, place a back-arrow icon (Material Symbols "arrow_back") at 24×24dp, tinted #266489, sitting 12dp from the left edge and vertically centred. Give the back arrow a 48×48dp invisible tap target layer behind it.

Place a Text element labelled "Product Terms" using titleLarge (Roboto 22sp weight 400 #181C20) centred vertically in the app bar, positioned 72dp from the left edge (after the 48dp icon touch zone and a 4dp gap). Do not truncate.

Add a 1dp horizontal Divider line at y=56 in outlineVariant #C1C7CE to separate the app bar from the scrollable content below.

### Loading Indicator

Create a centred Auto Layout frame that fills the remaining 716dp (852 minus 56 app bar minus 80 bottom nav). Inside it, place a Circular Progress component. Draw this as a circle, outer diameter 40dp, stroke width 4dp, colour #266489 (primary), with a 270-degree arc suggesting an in-progress spinner. Centre it exactly in the available content area both horizontally and vertically.

Add a 0-opacity text layer "Loading product terms" beneath the spinner — this represents the accessibility announcement that screen readers will speak; it is not visible to sighted users.

### Bottom Navigation Region

Add a 393×80 region at the bottom of the frame, fill #F7F9FF, with a 1dp top border in #C1C7CE. Inside it, arrange four navigation items in equal-width columns (each 393÷4 ≈ 98dp wide). Each item is a vertical stack with a 24dp icon above a label in labelMedium (12sp).

The Home item uses icon "home" tinted #41474D with label "Home" in #41474D. The Accounts item uses icon "account_balance" tinted #266489 (selected state) with label "Accounts" in #266489 — apply a selected indicator pill 64dp wide × 32dp tall in #C9E6FF (primaryContainer) centred behind the icon. The Transactions item uses icon "receipt_long" #41474D with label "Transactions". The More item uses icon "more_horiz" #41474D with label "More". All touch areas are 48dp minimum.

---

## Frame 2 — Content State

### Frame Setup

Create a frame named "Product Terms / Content" sized 393×852, background #F7F9FF. Use Auto Layout vertical, zero item spacing. The body region between app bar and bottom nav is a scrollable LazyColumn — use Figma's scrollable frame feature with clip content enabled and overflow: vertical.

### Top App Bar

Reproduce the same top app bar as in Frame 1 (back arrow #266489, title "Product Terms" titleLarge #181C20, 1dp divider below at y=56).

### Scrollable Content Column

Create a scrollable frame 393×716 (remaining space) with vertical overflow. Inside, use Auto Layout vertical with 0 item spacing and padding: top 16, left 16, right 16, bottom 32.

#### Product Header Card

Add a Card component 361dp wide (fill minus 0dp since we're inside a 16dp padded column — the column padding handles margins). Set the card background to #EBEEF3 (surfaceContainer), elevation shadow at 3dp (Material level 2 tonal shadow), and corner radius 12dp. Inside the card, apply Auto Layout vertical, padding 16dp on all sides, gap 4dp between children.

Place a Text element "PCA" using labelMedium (Roboto 12sp weight 500 #50606E) at the top. This is the product type overline — keep it uppercase as it is an OBIE enum value. Below it, place "HSBC Advance Account" using headlineMedium (28sp weight 400 #181C20). Below that, place "Product ID: HSBC-ADVANCE-PCA-001" using labelSmall (11sp weight 500 #41474D).

Add 16dp vertical space below the card.

#### Fees Section

Create a section header component: a horizontal row 361dp wide, with "FEES" as a Text in labelSmall (11sp weight 500 #41474D uppercase letter-spacing 0.5), aligned leading. Below the text row, add a 1dp horizontal Divider in #C1C7CE spanning the full 361dp width. Total height of section header: 40dp including the divider.

Add a ListItem for the monthly maximum charge. It is 361dp wide and 56dp tall. On the left, a supporting Text "Monthly maximum charge" in bodyMedium (14sp weight 400 #181C20) vertically centred. On the right edge, a trailing Text "£0.00" in titleMedium (16sp weight 500 #181C20), right-aligned. Both texts sit in a horizontal row with weight distribution: supporting text fills remaining space, trailing text hugs its content. Minimum touch area is the full 56dp height row.

Add 16dp vertical gap before the next section.

#### Credit Interest Section

Repeat the section header pattern with label "CREDIT INTEREST" in labelSmall #41474D with a divider below.

Add two ListItem rows representing the AER tier bands from the HSBC Advance PCA data:

The first row is 361dp × 56dp. Supporting text "Up to £1,000 · paid Monthly" in bodyMedium 14sp #41474D. Trailing text "0.00% AER" in titleMedium 16sp weight 500 #181C20. This band represents the standard low-balance tier where no interest is paid.

The second row is also 361dp × 56dp. Supporting text "Up to £10,000 · paid Monthly" in bodyMedium 14sp #41474D. Trailing text "0.15% AER" in titleMedium 16sp weight 500 #181C20. This is the premium tier for HSBC Advance customers holding £1,000–£10,000.

Add 16dp vertical gap before the next section.

#### Overdraft Section

Add a section header "OVERDRAFT" in the same style as above.

Add two ListItem rows for overdraft tiers:

The first row represents the Arranged overdraft tier: supporting text "Arranged overdraft" in bodyMedium 14sp #181C20, trailing "39.9% EAR" in titleMedium 16sp weight 500 #BA1A1A. Use the error colour #BA1A1A deliberately — this signals to users that this is a high-cost borrowing rate and draws attention to it as required by FCA fair value and consumer duty obligations. The contrast ratio of #BA1A1A on #F7F9FF is approximately 5.1:1, exceeding WCAG AA 4.5:1.

The second row represents the Unarranged overdraft: supporting text "Unarranged overdraft" in bodyMedium 14sp #181C20, trailing "49.9% EAR" in titleMedium 16sp weight 500 #BA1A1A. This is the higher-risk charge that applies when the customer exceeds their arranged limit.

Add 16dp vertical gap before the next section.

#### Features Section

Add a section header "FEATURES" with the same style.

Add six ListItem rows, each 361dp × 48dp. Each row contains a leading icon and supporting text. On the left, place the Material Symbols "check_circle" icon at 20×20dp, tinted #266489 (primary), with 16dp left padding and vertical centering. Use contentDescription "Feature confirmed" for accessibility. The icon is followed by 16dp horizontal gap, then supporting text in bodyMedium 14sp weight 400 #181C20.

The six feature rows display these strings from the product data:
Row 1: "No monthly maintenance fee"
Row 2: "Mobile and online banking included"
Row 3: "Arranged overdraft buffer up to £25"
Row 4: "HSBC Rewards cashback on eligible spend"
Row 5: "Preferential rates on HSBC savings and mortgages"
Row 6: "24/7 telephone banking support"

All feature text is single-line at 14sp. If the feature string exceeds the available width (361 minus 52dp icon zone = ~309dp of text), allow wrapping to a second line and increase the row height to 64dp. Keep the check_circle icon top-aligned in that case.

### Auto Layout Specification — Content Frame

The outer scrollable column uses: direction Vertical, padding 16/16/16/32 (top/right/bottom/left), item spacing 0. The product_header_card uses: direction Vertical, padding 16 all sides, item spacing 4. Section headers use: direction Vertical, padding-top 16, item spacing 4. The bottom nav uses: direction Horizontal, distribution Space Between, padding 8/16/8/16. Each nav tab child uses: direction Vertical, item spacing 4, alignment Center.

### Bottom Navigation

Same as Frame 1, Accounts tab selected with #C9E6FF indicator pill.

---

## Frame 3 — Empty State

### Frame Setup

Create a frame named "Product Terms / Empty" sized 393×852, background #F7F9FF.

### Top App Bar

Same as other frames — back arrow #266489, title "Product Terms" titleLarge #181C20, 1dp divider.

### Empty Content Area

In the 393×716 content region, create a Box (Figma Auto Layout with horizontal and vertical centring). Apply padding of 32dp on left and right. Inside, stack vertically with gap 16dp and centre alignment.

Place the Material Symbols icon "info_outline" at 48×48dp, tinted #41474D (onSurfaceVariant). The info icon communicates that this is a neutral informational state, not an error. Set contentDescription to "Information — no product terms available for this account type." The icon must not be decorative here — it carries semantic meaning for screen reader users.

Below the icon, place a Text element using headlineSmall (24sp weight 400 #181C20, textAlign Centre): "No product information available".

Below that, place a bodyMedium Text (14sp weight 400 #41474D, textAlign Centre, max width 329dp): "Product terms are not available for this account type."

Do not add a call-to-action button in this state. The empty state is informational, not recoverable — it represents accounts such as GlobalMoney, Savings, or CreditCard that do not have a corresponding OBProduct2 PCA or BCA entry in the OBIE catalogue. Adding a retry button would confuse users into thinking this is a network failure.

### Auto Layout Specification — Empty Frame

The centred content stack uses: direction Vertical, padding horizontal 32, item spacing 16, horizontalAlignment Centre, verticalAlignment Centre, fillAvailable true (or use absolute centering with constraints set to centre both axes).

### Bottom Navigation

Same as previous frames, Accounts tab selected.

---

## Frame 4 — Error State

### Frame Setup

Create a frame named "Product Terms / Error (HTTP 403)" sized 393×852, background #F7F9FF. The HTTP 403 scenario represents the most instructive error case (ReadProducts consent missing) — also design a variant for HTTP 401 in the same frame as a variant property.

### Top App Bar

Same as other frames — back arrow #266489, title "Product Terms" titleLarge #181C20.

### Error Content Area

In the 393×716 content region, use the same centred Auto Layout stack pattern as the empty state, padding horizontal 32dp, gap 16dp between elements.

Place the Material Symbols icon "error_outline" at 48×48dp, tinted #BA1A1A (error). Use contentDescription "Error loading product terms." Unlike the empty state's neutral #41474D icon, the error red immediately signals a recoverable failure.

Place a Text element using headlineSmall (24sp weight 400 #181C20, textAlign Centre): "Unable to load product terms".

Place a bodyMedium Text (14sp weight 400 #41474D, textAlign Centre): add a Figma property "errorMessage" so the string is swappable in prototypes. Default value for the HTTP 403 variant: "Consent does not include ReadProducts." For the HTTP 401 variant: "Session expired. Please re-authenticate." For the network error variant: "Unable to connect. Check your internet connection."

Below the message text, add 8dp extra gap (total gap from message to button = 24dp) for breathing room before the primary action.

Place a Button component. Set the variant to Filled. Width: 329dp (match_parent minus 32dp each side). Height: 56dp. Corner radius: 9999 (full pill). Background fill: #266489 (primary). Label "Try again" in labelLarge (14sp weight 500 #FFFFFF). Minimum touch target 56dp (button height already satisfies this).

This button represents the retry_load action: on tap, the ViewModel re-triggers productLoad(accountId), which re-issues GET /accounts/{AccountId}/product via ktorfit, returning to the Loading state and then resolving to Content, Empty, or Error.

### Component Variants for the Retry Button

Add the following variants to the Button component in the error state:

The Default state shows a solid #266489 background with "Try again" label in #FFFFFF at full opacity. The Pressed state lightens the background slightly to #004B6F (onPrimaryContainer used as pressed overlay) and adds a ripple effect at 12% opacity. The Focused state adds a 3dp focus ring in #266489 around the button perimeter. The Loading state (after the user taps and the retry is in flight) replaces the label with a small 20dp circular progress indicator in #FFFFFF, centred. This prevents double-taps. All variants maintain the same 56dp height and 9999 corner radius.

### Auto Layout Specification — Error Frame

The centred content stack uses: direction Vertical, padding horizontal 32, item spacing 16, horizontalAlignment Centre, verticalAlignment Centre. The button is sized: width Fixed 329, height Fixed 56.

### Bottom Navigation

Same as other frames, Accounts tab selected.

---

## Prototype Interaction Flow

Wire the following interactions in Figma Prototype mode:

From Frame 1 (Loading), after a 1200ms delay (simulating API response time), auto-navigate to Frame 2 (Content) with a Fade transition, duration 300ms, easing ease-out. This simulates the successful loading path.

Add a second prototype path from Frame 1 after a 2000ms delay navigating to Frame 4 (Error) with the same Fade transition. Annotate this path as "Error path — tap Loading to see Error state".

On Frame 2 (Content), the back_button (arrow_back icon in top app bar) triggers Navigate Back to the originating account-detail frame. Set this as an Instant transition since the OS back-stack handles the animation natively on Android.

On Frame 4 (Error), the retry_button triggers Navigate to Frame 1 (Loading) with a Fade transition at 150ms (short animation). From Frame 1, the auto-navigate paths above complete the loop. This creates a prototype-visible retry cycle.

There are no tap interactions on the product_header_card, list items (monthly_max_charge_row, tier_band_row, overdraft_tier_row, feature_row), or the empty_product_state — all are display-only. Document this explicitly in the component annotations panel: "Display only — no tap target. Screen readers navigate via swipe; no onClick contract."

---

## Component Variants Reference

### TopAppBar — Product Terms Screen

Create a TopAppBar component for this screen with two variants: Scrolled and Default. In Default, the app bar has background #F7F9FF, elevation 0, no shadow visible. In Scrolled, the app bar transitions to background #EBEEF3 (surfaceContainer) with a subtle 2dp drop shadow beneath the bottom edge. The title "Product Terms" and back arrow remain unchanged. This matches Material 3 behaviour where the top app bar gains elevation tint as the user scrolls.

### SectionHeader Component

Create a reusable SectionHeader component with properties: label (string) and showDivider (boolean, default true). The component is 361dp wide and 40dp tall. The label uses labelSmall (11sp weight 500 #41474D), left-aligned with 0dp horizontal padding (the column padding handles the margin). When showDivider is true, a 1dp Divider in #C1C7CE spans the full width below the label, inset 0dp on both sides.

### TierBandListItem Component

Create a reusable TierBandListItem component with properties: supportingText (string), trailingValue (string), trailingColor (colour token defaulting to onSurface #181C20). The component is 361dp wide × 56dp tall with no corner radius. The supporting text uses bodyMedium 14sp #41474D in the left zone (fill remaining). The trailing value uses titleMedium 16sp weight 500 in the specified trailingColor, right-aligned. Apply this component to both credit interest rows (trailingColor = onSurface) and overdraft rows (trailingColor = error #BA1A1A).

### FeatureListItem Component

Create a reusable FeatureListItem component with a single property: featureText (string). Width: 361dp. Height: auto (minimum 48dp, expands on text wrap). The leading icon is check_circle at 20×20dp tinted #266489, left-padded 0dp (inherits column padding), vertically top-aligned when text wraps. The feature text uses bodyMedium 14sp weight 400 #181C20. Gap between icon and text: 16dp. Minimum touch area: 48dp height.

### ProductHeaderCard Component

Create a ProductHeaderCard component with properties: productType (string), productName (string), productId (string). Card background: #EBEEF3. Elevation: shadow 3dp. Corner radius: 12dp. Interior Auto Layout: vertical, padding 16, gap 4. productType uses labelMedium 12sp weight 500 #50606E. productName uses headlineMedium 28sp weight 400 #181C20. productId uses labelSmall 11sp weight 500 #41474D. The card has no tap interaction on this screen (display only).

---

## Accessibility Annotations

Add Figma accessibility annotations (use the Figma Accessibility plugin or manual annotation layers) for the following elements:

The back_button in the top app bar must carry a contentDescription "Go back" in addition to the visual arrow_back icon. Mark it as: Role=Button, Label="Go back". Minimum touch area 48×48dp — draw a transparent 48×48 layer behind the 24dp icon to indicate this.

The product_header_card carries a card-level contentDescription "Product: HSBC Advance Account, type PCA, ID HSBC-ADVANCE-PCA-001". Mark child elements as decorative within the card context since the card-level label encompasses all child content.

Each tier_band_row has a compositeContentDescription derived from its two text elements. Annotate as: "Up to £1,000, paid Monthly: 0.00% AER" for the first band. Avoid reading the trailing and supporting texts as separate focusable elements — merge them at the row level.

Each overdraft_tier_row should have composite annotation: "Arranged overdraft: 39.9% EAR" and "Unarranged overdraft: 49.9% EAR". Importantly, note in the annotation that the red #BA1A1A colour on EAR values is not the sole indicator of high cost — the text itself conveys the rate numerically, satisfying WCAG 1.4.1 (Use of Colour).

Each feature_row should be marked Role=ListItem with Label="Feature: {featureText}". The check_circle icon within each row is decorative (the text already communicates the confirmed feature); mark it as decorative with an empty contentDescription.

The retry_button has Role=Button, Label="Retry loading product terms". After tapping, if a loading state activates, announce "Loading product terms" via accessibility live region.

The circular progress indicator in the loading state has Role=ProgressIndicator (indeterminate), Label="Loading product terms". It is not decorative.

The info_outline icon in the empty state has Role=Image, Label="Information — no product terms available for this account type."

The error_outline icon in the error state has Role=Image, Label="Error loading product terms."

All touch targets meet the 48dp minimum required by both Material 3 and WCAG 2.5.5 (Target Size).

Ensure all text colours pass WCAG AA contrast: #181C20 on #F7F9FF = 17.3:1 (AAA), #41474D on #F7F9FF = 9.9:1 (AAA), #50606E on #F7F9FF = 6.1:1 (AA), #266489 on #FFFFFF = 5.7:1 (AA), #BA1A1A on #F7F9FF = 5.1:1 (AA). All roles satisfy minimum 4.5:1 for normal text.

---

## Spacing and Layout Grid

Set up a 4-column layout grid in Figma with 16dp margins on left and right. All content — the product_header_card, list items, section headers, buttons — aligns to this 16dp margin. This leaves 361dp of usable content width within the 393dp frame.

Vertical rhythm follows a 4dp baseline grid. Section-to-section gaps: 16dp above each section header. Item-to-item within a list section: 0dp gap (the 56dp list item height already provides sufficient breathing room). The product header card has 16dp margin below. Top of scrollable content: 16dp padding from app bar bottom. Bottom of scrollable content: 32dp padding above bottom nav.

The bottom navigation height is 80dp, consistent with Material 3 navigation bar specification. This accounts for the 48dp icon+label composite height plus 16dp padding above and below.

Motion: all state transitions use the Material 3 emphasis easing "cubic-bezier(0.2, 0.0, 0, 1.0)" at 300ms. Loading → Content fades in the product card and list sections with a staggered entrance: card appears at 0ms, FEES section at 50ms, CREDIT INTEREST at 100ms, OVERDRAFT at 150ms, FEATURES at 200ms. This stagger is subtle (5 items × 50ms offset = 250ms total spread) and respects the `reduce-motion: supported` system preference — disable stagger entirely when `prefers-reduced-motion: reduce` is detected.
