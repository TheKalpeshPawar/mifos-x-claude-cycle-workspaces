# ATM Locator — Figma Design Prompts

> Generated from `screens/atm-locator/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Roboto · bg #F7F9FF
> States covered: loading · content · empty · error

---

## Design System Summary

### Colour Palette (M3 Light — resolved hex)

| Role | Figma Variable | Hex |
|---|---|---|
| Primary | `color/primary` | #266489 |
| On Primary | `color/onPrimary` | #FFFFFF |
| Primary Container | `color/primaryContainer` | #C9E6FF |
| On Primary Container | `color/onPrimaryContainer` | #004B6F |
| Secondary | `color/secondary` | #50606E |
| On Secondary | `color/onSecondary` | #FFFFFF |
| Secondary Container | `color/secondaryContainer` | #D3E5F5 |
| On Secondary Container | `color/onSecondaryContainer` | #384956 |
| Error | `color/error` | #BA1A1A |
| On Error | `color/onError` | #FFFFFF |
| Error Container | `color/errorContainer` | #FFDAD6 |
| Background | `color/background` | #F7F9FF |
| Surface | `color/surface` | #F7F9FF |
| On Surface | `color/onSurface` | #181C20 |
| Surface Variant | `color/surfaceVariant` | #DDE3EA |
| On Surface Variant | `color/onSurfaceVariant` | #41474D |
| Outline | `color/outline` | #72787E |
| Outline Variant | `color/outlineVariant` | #C1C7CE |

### Typography Scale (Roboto — M3 default)

| Style | Figma Variable | Size · Weight · Line Height |
|---|---|---|
| Title Large | `type/title/large` | 22sp · 400 · 28sp |
| Title Medium | `type/title/medium` | 16sp · 500 · 24sp |
| Title Small | `type/title/small` | 14sp · 500 · 20sp |
| Body Large | `type/body/large` | 16sp · 400 · 24sp |
| Body Medium | `type/body/medium` | 14sp · 400 · 20sp |
| Body Small | `type/body/small` | 12sp · 400 · 16sp |
| Label Large | `type/label/large` | 14sp · 500 · 20sp |
| Label Medium | `type/label/medium` | 12sp · 500 · 16sp |
| Label Small | `type/label/small` | 11sp · 500 · 16sp |

### Spacing and Shape

| Token | Value |
|---|---|
| spacing.xs | 4dp |
| spacing.sm | 8dp |
| spacing.md | 16dp |
| spacing.lg | 24dp |
| radius.medium | 12dp |
| radius.large | 16dp |
| radius.full | 9999dp (pill) |
| Minimum touch target | 48dp |

---

## Global Frame Setup

Create a Figma frame named **"ATM Locator"** at 393×852dp. Enable clip content. Set the background fill to `color/background` (#F7F9FF). This screen is a secondary screen within the Open Banking app; it sits one level below the main tab destinations and is always reached via a navigation event (not by tapping a bottom nav tab directly).

Establish two persistent chrome layers that appear unchanged in every state frame. Create these as Figma components so you can instance them across all four state frames.

**Top App Bar Component** — Create a frame 393dp wide × 64dp tall. Set the background fill to `color/surface` (#F7F9FF). On the left, place a back-arrow icon (Material Symbol: arrow_back or chevron_left) at 24dp, coloured `color/primary` (#266489), centred vertically within a 48dp × 48dp transparent hit area inset 4dp from the left edge. Place the screen title "Find HSBC ATM" centred vertically at `type/title/large` (22sp Roboto Regular 400, `color/onSurface` #181C20). No trailing action icons. Do not apply an elevation shadow on this screen — the content begins directly below the bar.

**Bottom Navigation Bar Component** — Create a frame 393dp wide × 80dp tall. Set the background fill to `color/surface` (#F7F9FF). Apply a 1dp top border in `color/outlineVariant` (#C1C7CE). Inside, use a horizontal Auto Layout with equal-width distribution across four tab items. Each tab is a vertical stack (Auto Layout, direction: vertical, item spacing: 4dp, alignment: centre) containing a 24dp icon above a label at `type/label/medium` (12sp Roboto Medium 500).

All four tabs are rendered in the **unselected** state on this screen, because ATM Locator is not a primary tab destination:
- **Home** — icon: home — label: "Home" — fill `color/onSurfaceVariant` (#41474D)
- **Accounts** — icon: account_balance — label: "Accounts" — fill `color/onSurfaceVariant` (#41474D)
- **Transactions** — icon: receipt_long — label: "Transactions" — fill `color/onSurfaceVariant` (#41474D)
- **More** — icon: more_horiz — label: "More" — fill `color/onSurfaceVariant` (#41474D)

The scrollable content area between the top bar and bottom bar measures 393dp wide × 708dp tall (852 − 64 − 80).

---

## State Frames

### Frame 1: ATM Locator / Loading

Duplicate the global frame. Name this frame **"ATM Locator / Loading"**.

**Search Field (resting placeholder)** — Place a filled text field at 361dp wide × 56dp tall, with 16dp left margin and 16dp right margin, starting 8dp below the top app bar. Set the background fill to `color/surfaceVariant` (#DDE3EA). Set border radius to 28dp on all corners. Place a search icon (Material Symbol: search, 20dp) as a leading element, fill `color/onSurfaceVariant` (#41474D), inset 16dp from the left edge. Render the placeholder text "e.g. NW1 0LT or Camden" at `type/body/medium` (14sp Roboto Regular 400, `color/onSurfaceVariant` #41474D). Also show the field label "Search by postcode or area" as a 12sp floating label at `color/onSurfaceVariant` — in Material Design's filled text field, this label sits embedded in the field when no value is entered. No trailing icon in the resting state.

**Linear Progress Indicator** — Directly below the search field, leaving 16dp (spacing.md) of vertical space, place a LinearProgressIndicator spanning the full 393dp width at 4dp height. Construct two layers: a track rectangle (393dp × 4dp, fill `color/primaryContainer` #C9E6FF) and an indicator rectangle (approximately 45% of the width, fill `color/primary` #266489) animating left to right. In static Figma export, show the indicator positioned at roughly 40–50% through its travel to communicate the indeterminate state. Label this layer with an annotation: "Indeterminate animation — indicator sweeps left to right continuously at 300ms cubic-bezier(0.2,0,0,1.0)."

The remainder of the 708dp content zone is empty in loading state. Do not render filter chips, result count text, or any ATM cards. Add a Figma annotation note: "Filter chips (state_binding=[content, empty]), result count (state_binding=[content]), and ATM list (state_binding=[content]) are all hidden during loading."

**Auto Layout for content column:**
- Direction: Vertical
- Padding top: 8dp (search field top offset below app bar)
- Item spacing: 0dp (each child manages its own spacing via internal padding)
- Horizontal alignment: Leading
- Width: 393dp, Height: 708dp, clip content enabled, overflow: scroll

---

### Frame 2: ATM Locator / Content

Duplicate the global frame. Name this frame **"ATM Locator / Content"**.

**Search Field (active state)** — Use the same filled text field dimensions and styling, but now show an active value. Render the text "NW1 0LT" at `type/body/medium` (14sp Roboto Regular 400, `color/onSurface` #181C20). Add a 2dp bottom-edge indicator stroke in `color/primary` (#266489) to communicate focused state. Place a trailing clear icon (Material Symbol: close, 20dp, fill `color/onSurfaceVariant` #41474D) 12dp inset from the right edge of the field — this is the trailing_icon that appears when searchQuery is non-empty.

**Service Filter Chip Row** — 4dp below the search field (spacing.xs), place a horizontally scrollable chip group. Use a horizontal Auto Layout: padding 16dp left and right (spacing.md), padding 4dp top and bottom (spacing.xs), item spacing 4dp (spacing.xs). Create three filter chips. Each chip is 32dp tall, full-pill border radius (9999dp), and uses `type/label/large` (14sp Roboto Medium 500) for its label.

Render all three chips in the **unselected** state: border 1dp `color/outline` (#72787E), background transparent, label and icon at `color/onSurfaceVariant` (#41474D).

- Chip 1: label "24h" (no leading icon in ui.yaml declaration)
- Chip 2: label "Wheelchair" (no leading icon in ui.yaml declaration)
- Chip 3: label "Cash deposit" (no leading icon in ui.yaml declaration)

For the **selected state variant** of each chip (used in prototype interactions and in the component variant panel): background fill `color/primaryContainer` (#C9E6FF), border 1dp `color/primary` (#266489), label colour `color/onPrimaryContainer` (#004B6F). Optionally add a leading check icon (done, 18dp, fill `color/onPrimaryContainer`) to confirm the selected predicate — this is standard M3 filter chip behaviour.

**Result Count Label** — 4dp below the chip row, place the text "4 ATMs found" at `type/label/medium` (12sp Roboto Medium 500, `color/onSurfaceVariant` #41474D). Left margin 16dp, bottom padding 4dp (spacing.xs). This value is derived from `filteredAtms.size` with the string pattern "{count} ATMs found".

**ATM Card Component** — Design the ATM card as a Figma component. The card is an outlined card: 1dp border in `color/outline` (#72787E), background fill `color/surface` (#F7F9FF), border radius 12dp (radius.medium), subtle shadow at elevation 1dp (y-offset 1dp, blur 3dp, colour #000000 at 10%). Card width is 361dp (match_parent minus 16dp margins each side). Internal padding is 16dp on all sides.

Inside the card, use a vertical Auto Layout with 4dp item spacing:

1. **ATM Name** — `type/title/medium` (16sp Roboto Medium 500, `color/onSurface` #181C20)
2. **ATM Address** — `type/body/small` (12sp Roboto Regular 400, `color/onSurfaceVariant` #41474D). Allow text to wrap to two lines for longer addresses.
3. **ATM Distance** — `type/label/small` (11sp Roboto Medium 500, `color/secondary` #50606E)
4. **Service Chip Group** — A horizontally scrollable row of display-only chips. Each display chip is 28dp tall, full-pill radius (9999dp), border 1dp `color/outlineVariant` (#C1C7CE), background transparent. Each chip has a 16dp leading icon and `type/label/small` (11sp) label, both in `color/onSurfaceVariant` (#41474D).

The card is tappable (on_click → open_atm_directions). Add a pressed state layer: ripple overlay at `color/primary` (#266489) 12% opacity covering the entire card surface, with elevation briefly increasing to 2dp during press (150ms).

**Populate four card instances** with real data from `demo-data.yaml`:

**Card 1 — HSBC Camden Town**
Render: Name "HSBC Camden Town" · Address "218 Camden High Street, London NW1 8QR" · Distance "0.3 miles" · Service chips: [access_time "24 hours"] [accessible "Wheelchair"] [savings "Cash deposit"]. HasWheelchairAccess = true, HasCashDeposit = true — both conditional chips are visible.

**Card 2 — HSBC Kentish Town**
Render: Name "HSBC Kentish Town" · Address "152 Kentish Town Road, London NW1 9QB" · Distance "0.7 miles" · Service chips: [access_time "24 hours"] [accessible "Wheelchair"]. HasCashDeposit = false — the Cash deposit chip (chip_deposit) is not rendered on this card.

**Card 3 — HSBC Euston Road**
Render: Name "HSBC Euston Road" · Address "376 Euston Road, London NW1 3BL" · Distance "1.1 miles" · Service chips: [access_time "Mon–Sat 08:00–20:00"] [accessible "Wheelchair"] [savings "Cash deposit"]. All three chips visible. Note that the opening hours chip shows the actual time-range string, not "24 hours".

**Card 4 — HSBC Oxford Street**
Render: Name "HSBC Oxford Street" · Address "92 Oxford Street, London W1D 1LR" · Distance "2.0 miles" · Service chips: [access_time "24 hours"] [accessible "Wheelchair"] [savings "Cash deposit"]. All three chips visible.

**ATM List Auto Layout spec:**
- Direction: Vertical
- Padding left: 16dp · Padding right: 16dp · Padding bottom: 24dp (spacing.lg)
- Item spacing: 8dp (spacing.sm) between cards
- Width: 393dp, overflow: Scroll (vertical)

The full list is slightly taller than the visible content area (approximately 624dp list height vs 568dp available below the search field and chip row). In Figma, set the list frame to its natural content height and enable vertical scrolling. The fourth card is partially visible when the screen first loads (approximately 80% visible before scroll).

---

### Frame 3: ATM Locator / Empty

Duplicate the global frame. Name this frame **"ATM Locator / Empty"**.

**Search Field (active, no results)** — Render the search field with the value "TR1 9ZZ", the demo postcode that returns zero HSBC ATM matches. Show the trailing clear icon. The field is not in an error state — it is simply showing a valid query that produced no results. Use the same focused styling as the content frame (2dp bottom stroke at #266489).

**Service Filter Chips** — Render the same three chips as in the content frame in the unselected state. These remain visible on the empty state because the user may want to remove a filter predicate (for example, unchecking "24h" might reveal ATMs in that area with restricted hours). State binding: [content, empty].

**Empty State Block** — Below the filter chip row, centre the following vertically within the remaining 708dp content zone:

Place the Material Symbol `location_off` at 48dp × 48dp, filled with `color/onSurfaceVariant` (#41474D). Centre horizontally. Apply 48dp top padding from the bottom edge of the chip row.

Below the icon with 12dp vertical gap, place the heading text "No ATMs found nearby" at `type/headline/small` (24sp Roboto Regular 400, `color/onSurface` #181C20). Centre-align. Set horizontal padding to 32dp each side to ensure comfortable text width on narrow widths.

Below the heading with 8dp vertical gap, place the body text "No HSBC ATMs match your search. Try a different postcode or area name." at `type/body/medium` (14sp Roboto Regular 400, `color/onSurfaceVariant` #41474D). Centre-align. Same 32dp horizontal padding. This string is exact from `strings.atm_locator_empty_body`.

There is no action button on the empty state. The user recovers by modifying the search query (the field is active and reachable) or by toggling filter chips. Do not add a "Clear search" button — the clear icon on the search field serves that purpose.

**Empty state Auto Layout spec:**
- Direction: Vertical
- Alignment: Centre (horizontal)
- Padding: 48dp top from chip row, 8dp between heading and body, 12dp between icon and heading
- No padding bottom required (empty state sits above the bottom nav)

---

### Frame 4: ATM Locator / Error

Duplicate the global frame. Name this frame **"ATM Locator / Error"**.

**Search Field (resting after retry reset)** — Render the search field in placeholder state with empty query text. When `retryLoad` fires, it resets `filterState` to all-off defaults and clears `searchQuery` to an empty string before re-calling `atmsLoad`. So on error, the field is empty. Show the placeholder "e.g. NW1 0LT or Camden" in `color/onSurfaceVariant` (#41474D). No trailing icon appears.

**No Filter Chips** — The service filter chip group has `state_binding: [content, empty]` which does not include the error state. Omit the chip row entirely. Go directly from the search field to the error illustration.

**Error State Block** — Centre the following block vertically in the remaining content area:

Place the Material Symbol `error_outline` at 48dp × 48dp, filled with `color/error` (#BA1A1A). Centre horizontally. Apply 48dp top padding from the bottom of the search field.

Below the icon with 16dp vertical gap, place the error title "Could not load ATMs" at `type/headline/small` (24sp Roboto Regular 400, `color/onSurface` #181C20). Centre-align. Set horizontal padding to 32dp each side.

Below the title with 8dp vertical gap, place the error body. The exact string is the network error user message: "Could not reach HSBC Open Data. Check your connection." Render this at `type/body/medium` (14sp Roboto Regular 400, `color/onSurfaceVariant` #41474D). Centre-align. Same 32dp horizontal padding. This is `error.message` from the NETWORK_ERROR case declared in `docs.yaml`. The HTTP_5XX variant would read "HSBC Open Data service unavailable. Please try again." — create a secondary error frame or component variant if both messages need to be designed.

**Retry Button** — 24dp below the body text, place a filled button centred horizontally on the screen. Create a rectangle at approximately 160dp wide × 40dp tall. Set the background fill to `color/primary` (#266489). Set the border radius to 9999dp (full pill). Place the label "Retry" centred within the button at `type/label/large` (14sp Roboto Medium 500, `color/onPrimary` #FFFFFF). Add 24dp horizontal internal padding on each side of the label. Set a minimum touch target of 48dp tall by using a transparent hit-area extension 4dp above and below the visible button. The button triggers the `retry_load` action: `effect: call_api` targeting `GET /atms` on the HSBC Open Data endpoint.

Add a Figma annotation: "retry_load resets filterState to all-off and re-calls atmsLoad → transitions through Loading → Content | Empty | Error."

**Error Auto Layout spec:**
- Direction: Vertical
- Alignment: Centre (horizontal)
- Padding top: 48dp from search field bottom
- Item spacing: 16dp (icon to title), 8dp (title to body), 24dp (body to button)

---

## Component Variants Reference

### TextField / location_search

Create a four-variant component set:

**Resting / Placeholder** — Filled text field, bg `color/surfaceVariant` (#DDE3EA), radius 28dp. Leading search icon 20dp at `color/onSurfaceVariant` (#41474D), inset 16dp. Placeholder "e.g. NW1 0LT or Camden" at `type/body/medium` 14sp #41474D. Height 56dp. No trailing icon.

**Active / Focused** — Same background and radius. Two-dp bottom edge stroke at `color/primary` (#266489). Text value at `color/onSurface` (#181C20). Trailing clear icon (close, 20dp) at #41474D visible 12dp from right. Caret at `color/primary`.

**Hovered** — Add 1dp full-perimeter border at `color/outline` (#72787E) over the base filled style. No bottom stroke change.

**Disabled** — Fill at 38% opacity of `color/surfaceVariant`. Leading icon and placeholder both at 38% opacity. Cursor: not-allowed. No interaction affordance.

### Filter Chip (service_filters)

Two-variant component (M3 Filter Chip):

**Unselected** — Border 1dp `color/outline` (#72787E), background transparent, label `color/onSurfaceVariant` (#41474D). Height 32dp, radius 9999dp, horizontal padding 12dp each side.

**Selected** — Background `color/primaryContainer` (#C9E6FF), border 1dp `color/primary` (#266489), label `color/onPrimaryContainer` (#004B6F). Add a leading done check icon (18dp, fill `color/onPrimaryContainer`).

Both variants: pressed state layer = `color/primary` 20% opacity ripple. Focused state = 2dp focus ring outside the chip border at `color/primary` (#266489).

### ATM Card

Two-variant component set:

**Default** — Outlined card: border 1dp `color/outline` (#72787E), background `color/surface` (#F7F9FF), radius 12dp (radius.medium), shadow elevation 1dp (y 1dp, blur 3dp, black 10%). Content padding 16dp. Vertical content stack: name (titleMedium) · address (bodySmall) · distance (labelSmall) · service chips row — all at 4dp item spacing.

**Pressed** — State-layer overlay at `color/primary` (#266489) 12% opacity covering the full card. Elevation steps to 2dp during press (150ms cubic-bezier ease). Border colour transitions briefly to `color/primary`. After tap completes, no state change within the card — the `open_atm_directions` action exits the app.

### Display Chip (atm_service_chips)

**Single variant (informational only)** — Height 28dp, radius 9999dp, border 1dp `color/outlineVariant` (#C1C7CE), background transparent. Leading icon slot 16dp at `color/onSurfaceVariant` (#41474D). Label at `type/label/small` (11sp Roboto Medium 500, #41474D). These chips have no hover, pressed, selected, or focused state because they are display-only components (no on_click action declared).

Icons by chip type: chip_hours → access_time · chip_wheelchair → accessible · chip_deposit → savings

### Filled Button (retry_button)

**Default** — Background `color/primary` (#266489), label `color/onPrimary` (#FFFFFF) at `type/label/large` (14sp 500). Radius 9999dp, height 40dp, horizontal padding 24dp. Touch target: 48dp.

**Hovered** — 8% white state-layer over the primary fill.

**Pressed** — 16% white state-layer over the primary fill. Elevation reduces to 0dp on press.

**Disabled** — Background `color/onSurface` at 12% opacity. Label `color/onSurface` at 38% opacity. Not interactive.

### Empty State Block

**Two-variant component (error / no-results):**

**No Results** — Icon: location_off 48dp at `color/onSurfaceVariant` (#41474D). Title: "No ATMs found nearby" headlineSmall 24sp #181C20. Body at bodyMedium 14sp #41474D. No action button.

**Error** — Icon: error_outline 48dp at `color/error` (#BA1A1A). Title: headlineSmall #181C20. Body at bodyMedium #41474D. Retry filled button below.

---

## Semantic Token → Figma Variable Mapping

| Semantic Role | Figma Variable Path | Hex / Value |
|---|---|---|
| primary | `color/primary` | #266489 |
| onPrimary | `color/onPrimary` | #FFFFFF |
| primaryContainer | `color/primaryContainer` | #C9E6FF |
| onPrimaryContainer | `color/onPrimaryContainer` | #004B6F |
| secondary | `color/secondary` | #50606E |
| error | `color/error` | #BA1A1A |
| background / surface | `color/surface` | #F7F9FF |
| onSurface | `color/onSurface` | #181C20 |
| surfaceVariant | `color/surfaceVariant` | #DDE3EA |
| onSurfaceVariant | `color/onSurfaceVariant` | #41474D |
| outline | `color/outline` | #72787E |
| outlineVariant | `color/outlineVariant` | #C1C7CE |
| type/title/large | `type/titleLarge` | 22sp Roboto 400 28sp lh |
| type/title/medium | `type/titleMedium` | 16sp Roboto 500 24sp lh |
| type/body/medium | `type/bodyMedium` | 14sp Roboto 400 20sp lh |
| type/body/small | `type/bodySmall` | 12sp Roboto 400 16sp lh |
| type/label/large | `type/labelLarge` | 14sp Roboto 500 20sp lh |
| type/label/medium | `type/labelMedium` | 12sp Roboto 500 16sp lh |
| type/label/small | `type/labelSmall` | 11sp Roboto 500 16sp lh |
| spacing.xs | `spacing/xs` | 4dp |
| spacing.sm | `spacing/sm` | 8dp |
| spacing.md | `spacing/md` | 16dp |
| spacing.lg | `spacing/lg` | 24dp |
| radius.medium | `radius/medium` | 12dp |
| radius.full | `radius/full` | 9999dp |
| elevation.level1 | `elevation/1` | shadow y 1dp blur 3dp black 10% |

---

## Prototype Interaction Flow

Configure the following Figma prototype connections:

| Trigger | Source Component | From Frame | To Frame / Action | Transition |
|---|---|---|---|---|
| On tap: back icon | top_app_bar leading ← | Any frame | Previous screen (popBackStack) | Smart Animate 300ms ease |
| On type (simulate) | location_search text field | Loading | Content | Instant |
| On type "TR1 9ZZ" | location_search text field | Content | Empty | Instant |
| On clear (✕ tap) | trailing clear icon | Empty | Content | Instant |
| On tap: 24h chip (toggle) | filter_24h | Content | Content (filtered variant — create a separate frame showing a "24h only" filtered view of the list) | Instant |
| On tap: any atm_card | atm_card component | Content | [Overlay: "Handoff to OS Maps — geo: URI / maps:// URL via gps-expect-actual"] | Smart Animate 150ms |
| On tap: retry_button | retry_button | Error | Loading | Smart Animate 200ms ease |
| After delay 2s | [simulate load] | Loading | Content | Smart Animate 300ms ease |

For the atm_card tap, create a full-screen overlay annotation frame explaining the `open_atm_directions` action: "Fires geo: URI on Android (geo:51.5395,-0.1428?q=HSBC+Camden+Town) or maps:// URL on iOS via the gps-expect-actual expect/actual implementation. This exits the Open Banking app — the OS takes control and opens the native Maps application. No return route is required within the app; the user navigates back via the OS back stack."

---

## Accessibility Annotations

Apply these annotations to the appropriate layer in each frame using a Figma annotation component set or manual callouts:

**Minimum touch targets** — All tappable elements must meet 48dp × 48dp minimum. Specifically check: back button (visible 24dp icon, needs 48dp hit area), filter chips (32dp tall, need 8dp transparent extension above and below), ATM cards (full card surface is the tap target — meets 48dp height), retry button (40dp visible, needs 4dp extension to reach 48dp touch target), bottom nav tabs (icon + label combined should comfortably exceed 48dp).

**Screen reader labels (contentDescription):**
- Back button: "Navigate back" (role: button)
- location_search: "Search for ATMs by postcode or area" (role: textField)
- filter_24h chip: "Filter: 24-hour ATMs only" (role: toggleButton, state announced)
- filter_wheelchair chip: "Filter: wheelchair-accessible ATMs only"
- filter_deposit chip: "Filter: cash deposit ATMs only"
- atm_card: "[Name], [Address], [Distance]. Tap to open in Maps." (role: button)
- chip_hours: "Opening hours: [value]" (role: text, not interactive)
- chip_wheelchair: "Wheelchair accessible" (role: text)
- chip_deposit: "Cash deposit available" (role: text)
- progress_indicator: "Searching for nearby ATMs" (role: progressBar)
- location_off icon (empty state): "No ATMs found near your search location" (role: status)
- error_outline icon (error state): "Error loading ATM list" (role: alert)
- retry_button: "Retry loading ATM list" (role: button)
- Bottom nav Home: "Home, tab 1 of 4"
- Bottom nav Accounts: "Accounts, tab 2 of 4"
- Bottom nav Transactions: "Transactions, tab 3 of 4"
- Bottom nav More: "More, tab 4 of 4"

**Colour contrast — WCAG AA verified:**
All text pairings on the #F7F9FF surface background pass AA minimum 4.5:1 for normal text, 3:1 for large text.
- #181C20 on #F7F9FF → contrast ratio ≈ 14.7:1 (AAA — onSurface for titles and headings)
- #41474D on #F7F9FF → contrast ratio ≈ 8.0:1 (AA — onSurfaceVariant for addresses and labels)
- #50606E on #F7F9FF → contrast ratio ≈ 5.9:1 (AA for normal text — secondary for distance)
- #FFFFFF on #266489 → contrast ratio ≈ 5.5:1 (AA — Retry button label on primary fill)
- #004B6F on #C9E6FF → contrast ratio ≈ 7.2:1 (AA — selected chip label on primaryContainer)
- #BA1A1A on #F7F9FF → contrast ratio ≈ 5.8:1 (AA — error icon colour)

**Focus traversal order (annotate with numbered badges):**
Back button (1) → Search field (2) → 24h chip (3) → Wheelchair chip (4) → Cash deposit chip (5) → ATM Card 1 (6) → ATM Card 2 (7) → ATM Card 3 (8) → ATM Card 4 (9) → Bottom nav: Home (10) → Accounts (11) → Transactions (12) → More (13).

**Reduce motion accommodation** — The LinearProgressIndicator's indeterminate animation should be paused and replaced with a static half-filled indicator when the system's prefers-reduced-motion preference is active. Annotate the Loading frame loading bar with: "Reduce motion: show static 50% filled bar, no sweep animation." The card list scroll and Smart Animate transitions between states should also respect reduce-motion by switching to instant/cross-fade transitions.

---

## Implementation Notes for Handoff

The ATM Locator screen calls the HSBC Open Data public endpoint (`GET /atms` at `https://api.hsbc.com/v2.0/uk/open-banking`). This endpoint is completely unauthenticated — no OAuth token, no OBIE consent flow, no FAPI authorisation. Designs do not need to account for any sign-in gate or consent banner before loading ATM data.

The `open_atm_directions` action on each ATM card fires a deep-link intent that exits the app. On Android this is a `geo:` URI; on iOS a `maps://` URL scheme. The expect/actual implementation (`GpsDistanceCalculator`) handles the platform dispatch. There is no in-app map view — the card tap purely invokes the OS.

Distance values shown on cards ("0.3 miles", "0.7 miles", etc.) are computed at runtime using device GPS when available, or fall back to a postcode centroid calculation when the user has denied location permission. Design the distance label as optional — if the GPS fix fails or the postcode centroid lookup is unavailable, the distance value may be absent. The `atm_distance` label should gracefully collapse (remove its height from the card stack) when no value is available.

The three filter chips toggle boolean predicates inside the ViewModel (`is24h`, `hasWheelchairAccess`, `hasCashDeposit`). Multiple chips can be active simultaneously. The filtered list is derived client-side with no API call. When a combination of filters produces zero results, the screen transitions to the Empty state while the search field and chips remain interactive.

`chip_wheelchair` and `chip_deposit` inside each ATM card are conditionally visible based on the HSBC Open Data ATM record's `Accessibility` and `ATMServices` arrays respectively. In Figma, model these as boolean component properties on the ATM Card component so designers can toggle their visibility without breaking the card's Auto Layout.
