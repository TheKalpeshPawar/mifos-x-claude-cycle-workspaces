# Party — Figma Design Prompts

> Generated from: `screens/party/ui.yaml` + `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Canvas: 393×852dp (Pixel 5) · Material Design 3 · Light theme · Roboto font family
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

### Resolved Colour Palette

The Open Banking app uses a Trust Blue palette derived from seed colour #266489, generated via the
Material Theme Builder. All colours below are the resolved light-mode values that should be imported
as Figma variables under a collection named `Open Banking / Light`.

Primary is #266489 (Trust Blue). It appears on filled buttons, the active bottom-nav indicator, the
top-app-bar back icon tint, and the circular loading indicator. On-primary is #FFFFFF.

Primary container is #C9E6FF — a soft sky-blue used for chip selected backgrounds and hero card
backgrounds in other screens. On-primary-container is #004B6F, a deep teal used for prominent text
inside primary-container surfaces.

Secondary is #50606E — a muted blue-grey used for section-header text, leading icons in list rows,
and overline party-type labels. On-secondary is #FFFFFF.

The surface and background both resolve to #F7F9FF — a near-white with a faint blue cast. All
cards and the app background use this colour. On-surface is #181C20 (near-black).

On-surface-variant is #41474D, used for body text in secondary roles such as the legal name,
address country, section dividers, and body text in empty/error/consent states.

Outline-variant is #C1C7CE — used for divider lines under section headers and card borders at
elevation 1.

Error is #BA1A1A — used exclusively for the error_outline icon in the error state. On-error is
#FFFFFF.

Surface-variant is #DDE3EA — available for skeleton shimmer or subtle fills; not used directly on
the party screen.

### Roboto Type Scale (resolved dp/sp)

headlineMedium: Roboto, 28sp, weight 400, line-height 36dp — party holder name.
headlineSmall: Roboto, 24sp, weight 400, line-height 32dp — empty/error/consent titles.
titleLarge: Roboto, 22sp, weight 400, line-height 28dp — top app bar title.
bodyMedium: Roboto, 14sp, weight 400, line-height 20dp — legal name, address lines, trailing row values.
bodySmall: Roboto, 12sp, weight 400, line-height 16dp — address country, secondary body text.
labelLarge: Roboto, 14sp, weight 500, line-height 20dp — section header labels.
labelMedium: Roboto, 12sp, weight 500, line-height 16dp — party type overline.
labelSmall: Roboto, 11sp, weight 500, line-height 16dp — address type chip, list-item support labels.

### Semantic Token → Figma Variable Mapping

| Semantic Token | Figma Variable (collection: Open Banking) | Resolved Hex |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/on-primary | #FFFFFF |
| primaryContainer | color/primary-container | #C9E6FF |
| onPrimaryContainer | color/on-primary-container | #004B6F |
| secondary | color/secondary | #50606E |
| onSecondary | color/on-secondary | #FFFFFF |
| surface | color/surface | #F7F9FF |
| onSurface | color/on-surface | #181C20 |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outline-variant | #C1C7CE |
| error | color/error | #BA1A1A |
| onError | color/on-error | #FFFFFF |
| background | color/background | #F7F9FF |
| scrim | color/scrim | #000000 |
| surfaceContainer | color/surface-container | #EBEEF3 |
| surfaceContainerLow | color/surface-container-low | #F1F4F9 |

### Shape Scale (corner radius)

extra_large: 28dp — used for pill buttons.
large: 16dp — not used on this screen.
medium: 12dp — party_header_card and all address_card instances.
small: 8dp — not used on this screen.
extra_small: 4dp — not used on this screen.
full (9999dp) — retry_button and reauthorise_button, creating fully rounded pills.

### Spacing Baseline

All horizontal screen padding is 16dp. Cards and list items sit within this boundary.
Internal card padding is 16dp on all sides.
Gap between stacked child text nodes inside cards is 4dp.
Gap between top-level scrollable children (cards, headers, list rows) is 16dp.
Gap between consecutive address cards inside the address list is 8dp.
List-item rows have a minimum height of 56dp with vertical padding of 12dp.
The bottom navigation bar height is 80dp.
The top app bar height is 56dp.
The minimum interactive touch target for all tappable elements is 48dp × 48dp.

---

## Frame: Loading State

Create a frame named "Party / Loading" at 393×852dp. Set the fill to #F7F9FF (surface / background).

### Top App Bar

At the top of the frame, place a component named "Top App Bar — Small" spanning the full 393dp width
at 56dp height. Fill it with #F7F9FF. Use Auto Layout with horizontal direction, centre-vertical
alignment, padding of 4dp on all sides, and an item spacing of 0dp.

Place a back-arrow icon button on the leading side. Use the Material Symbols icon `navigate_before`
at 24dp, coloured #41474D (on-surface-variant). Wrap the icon in a 48dp × 48dp container with
transparent fill to guarantee the WCAG-compliant minimum touch target. Set contentDescription to
"Back".

Place a text label to the right of the back button. Style it as titleLarge: Roboto, 22sp, weight
400, colour #181C20. The label reads "Account Holder". Left-align the text relative to the remaining
space.

Do not add elevation or a visible shadow to the top app bar in its default resting state.

### Loading Indicator

In the body area (below the top app bar, above the bottom navigation), centre a circular progress
indicator both horizontally and vertically within the remaining 716dp of height. The circle should
be 48dp in diameter with a stroke width of 4dp, coloured #266489 (primary). Add 24dp padding on
all sides around this element. In Figma, render this as a circle outline with a partial arc to
convey the spinning animation metaphor; the arc can represent a 270° sweep. Label this layer
"loading_indicator".

Add a hidden accessibility annotation layer reading "Loading account holder details" to document
the TalkBack/VoiceOver label.

### Bottom Navigation Bar

At the very bottom of the frame, place a component named "Bottom Nav" spanning the full 393dp width
at 80dp height. Fill it with #F7F9FF. Use Auto Layout with horizontal direction, space-between
distribution, padding 12dp vertical and 0dp horizontal, item spacing 0dp.

Create four tab items. Each tab item uses Auto Layout vertically, centred horizontally, gap 4dp
between icon and label. Icon size 24dp, label is labelSmall (11sp, weight 500).

Tab 1 — Home: icon `home`, label "Home", default state, icon and label colour #41474D.
Tab 2 — Accounts: icon `account_balance`, label "Accounts", selected state, colour #266489. Show
the M3 active indicator pill behind the icon: a rounded rectangle 64dp × 32dp, fill #C9E6FF
(primary-container), radius 9999dp.
Tab 3 — Transactions: icon `receipt_long`, label "Transactions", default, colour #41474D.
Tab 4 — More: icon `more_horiz`, label "More", default, colour #41474D.

Accounts is the active tab because the party screen is accessed from account-detail, which lives
under the Accounts navigation rail.

---

## Frame: Content State

Create a frame named "Party / Content" at 393×852dp, fill #F7F9FF.

Replicate the top app bar and bottom navigation components described in the Loading frame above.
The top app bar title remains "Account Holder" and the back button navigates to account-detail.
The Accounts tab remains selected in the bottom nav.

### Scrollable Body

Create an Auto Layout frame named "scrollable_column" with vertical direction, fill-container width,
wrap-height. Set padding to 16dp on all sides and item spacing to 16dp. Place this frame between
the top app bar and the bottom navigation.

#### Party Header Card

Create a Card component named "party_header_card". Set width to 361dp (fill with 0dp margin — the
16dp padding on each side is supplied by the scrollable_column). Set height to hug contents. Apply
a background fill of #F7F9FF (surface). Apply an elevation of 2dp: in Figma, translate this as a
drop-shadow with Y offset 1dp, blur 3dp, spread 0dp, colour #000000 at 15% opacity. Apply corner
radius 12dp on all four corners. Set internal padding to 16dp on all sides.

Inside the card, use Auto Layout in vertical direction, gap 4dp, alignment: leading.

The first child is the party type overline. Style it as Roboto 12sp, weight 500, colour #50606E
(secondary). The text reads "Sole" — sourced from OBParty2.PartyType. This field is the
`party_type_label` component. PII note: PartyType is a classification label only, not a PII field.

The second child is the party name. Style it as Roboto 28sp, weight 400, colour #181C20 (on-surface).
The text reads "Priya Sharma". This is the `party_name` component, sourced from OBParty2.Name.
Apply contentDescription: "Name: Priya Sharma".

The third child is the full legal name. Style it as Roboto 14sp, weight 400, colour #41474D
(on-surface-variant). The text reads "Priya Anjali Sharma". This is the `party_full_legal_name`
component, sourced from OBParty2.FullLegalName. PII sensitivity: legal name is personally
identifiable; no masking required in this context as the screen is behind PSU authentication, but
do not cache or share this value. Apply contentDescription: "Legal name: Priya Anjali Sharma".

#### Contact Section Header

Place a section header component named "contact_header" below the party header card. This is a
horizontal divider row: a text label reading "Contact" in Roboto 14sp, weight 500, colour #41474D,
followed by a horizontal rule spanning the remaining width at 1dp height, colour #C1C7CE
(outline-variant). The row height is 40dp. Align the text vertically centred, with 0dp horizontal
padding (padding already applied by the parent column).

#### Email Row

Create a list item named "email_row". Width: fill (393dp). Minimum height: 56dp. Use Auto Layout
horizontally, alignment centre-vertical, padding 12dp vertical and 16dp horizontal, gap 16dp.

The leading element is the `email` Material Symbols icon at 24dp, colour #50606E (secondary).
Wrap in a 40dp × 40dp invisible container for alignment consistency.

In the centre, stack two text nodes vertically with gap 2dp:
- Support label: Roboto 11sp, weight 500, colour #41474D. Text: "Email".
- (No second line — support label is the only visible label; the trailing text carries the value.)

The trailing element is a text node right-aligned: Roboto 14sp, weight 400, colour #181C20. Text:
"priya.sharma@example.co.uk". Apply a max-width constraint so this truncates with an ellipsis if
the email is very long. The full value is available in the contentDescription:
"Email address: priya.sharma@example.co.uk".

Visibility rule: this row is visible only when party.EmailAddress is non-empty.

#### Mobile Row

Create a list item named "mobile_row" identical in structure to email_row. Use the
`phone_android` icon at 24dp, colour #50606E. Support label text: "Mobile". Trailing text:
"+44 7700 900482". contentDescription: "Mobile number: +44 7700 900482". E.164 format as
returned from the HSBC OBIE sandbox. Visibility: show only when party.Mobile is non-empty.

#### Phone Row

Create a list item named "phone_row". Use the `phone` icon at 24dp, colour #50606E. Support
label text: "Phone". Trailing text: "+44 20 7946 0301". contentDescription:
"Phone number: +44 20 7946 0301". Visibility: show only when party.Phone is non-empty.

#### Address Section Header

Place a section header component named "address_header" identical in structure to contact_header.
Label text: "Address".

#### Address Card — Residential

Create a Card named "address_card_residential". Width: fill (361dp). Height: hug. Background:
#F7F9FF. Apply elevation 1dp: drop-shadow Y 1dp, blur 1dp, spread 0dp, #000000 at 10% opacity.
Corner radius: 12dp. Padding: 16dp all sides. Internal Auto Layout: vertical, gap 4dp.

The first child is the address type label. Style as Roboto 11sp, weight 500, colour #50606E.
Text: "RESIDENTIAL". This renders OBPostalAddress8.AddressType uppercased. Layer name: `address_type`.

The second child is address line 1. Style as Roboto 14sp, weight 400, colour #181C20.
Text: "48 Camden High Street". Derived from BuildingNumber "48" concatenated with StreetName
"Camden High Street". Layer name: `address_line_1`.

The third child is address line 2 (optional). Style as Roboto 14sp, weight 400, colour #181C20.
Text: "Flat 12". Sourced from AddressLine[0]. This layer is visible only when AddressLine is
non-empty. Layer name: `address_line_2`.

The fourth child is the town and postcode. Style as Roboto 14sp, weight 400, colour #181C20.
Text: "London, NW1 0LT". Derived from TownName + ", " + PostCode. Layer name: `address_town_postcode`.

The fifth child is the country. Style as Roboto 12sp, weight 400, colour #41474D. Text: "GB".
ISO 3166 alpha-2 country code as returned by the API. contentDescription: "Country: GB".
Layer name: `address_country`.

Add a screen-reader-only annotation layer reading the full concatenated address:
"Address: 48 Camden High Street, Flat 12, London, NW1 0LT, GB". This corresponds to the
`address_full_card` invisible text node declared in ui.yaml.

#### Address Card — Business

Create a second Card named "address_card_business" identical in structure. Width: fill. Margin
top: 8dp (address_list gap). Contents:

address_type: "BUSINESS"
address_line_1: "1 Canada Square"
address_line_2: "Suite 400"
address_town_postcode: "London, E14 5AB"
address_country: "GB"
Screen-reader annotation: "Address: 1 Canada Square, Suite 400, London, E14 5AB, GB"

---

## Frame: Error State

Create a frame named "Party / Error" at 393×852dp, fill #F7F9FF.

Replicate the top app bar and bottom navigation. Accounts tab remains selected.

### Error State View

In the body region, place an Auto Layout container named "error_state" centred both horizontally
and vertically within the 716dp body height. Set padding to 24dp on all sides, item spacing to
16dp, direction vertical, alignment centred.

Place the `error_outline` Material Symbols icon at 48dp, colour #BA1A1A (error). Set
decorative:false with contentDescription "Error loading account holder data".

Below the icon, place the error title. Style as Roboto 24sp, weight 400, colour #181C20, centre-
aligned. Text: "Unable to load account holder". Sourced from strings.party.error_title.

Below the title, place the error body. Style as Roboto 14sp, weight 400, colour #41474D, centre-
aligned, line-height 20dp. Text: "Request timed out. Please check your connection and try again."
This is the dynamic error.message from the ViewModel. In the NETWORK_ERROR fixture, this message
is produced by a network timeout. For the AUTH error (HTTP 401), this would render "Session
expired. Please re-authenticate."

Below the body, place the retry button. Use a filled button variant: background fill #266489,
label colour #FFFFFF, corner radius 9999dp (full pill), height 56dp, horizontal padding 24dp,
minimum touch target 56dp. Label text: "Try again". accessibility_label: "Retry loading account
holder details". This button triggers the `retry_load` action which delegates to `partyLoad`,
re-issuing the parallel GET /party + GET /parties calls via ktorfit and transitioning the screen
back through Loading to Content, Empty, or ConsentRequired.

### Button Variants for retry_button

Default state: fill #266489, label #FFFFFF, no border.
Hovered: fill tinted 8% lighter — overlay #FFFFFF at 8% opacity on top of #266489.
Pressed: fill tinted 12% darker — overlay #000000 at 12% opacity on top of #266489.
Disabled: fill #1C2024 at 12% opacity (approx #E0E3E8 equivalent), label #181C20 at 38% opacity.
Focused: same as default with a 3dp focus ring in #266489 offset 2dp.

---

## Frame: Empty State

Create a frame named "Party / Empty" at 393×852dp, fill #F7F9FF.

Replicate the top app bar and bottom navigation. Accounts tab selected.

### Empty State View

In the body region, place an Auto Layout container named "empty_state_view" centred both
horizontally and vertically within the 716dp body height. Padding 24dp all sides, item spacing
16dp, direction vertical, alignment centred.

Place the `person_off` Material Symbols icon at 48dp, colour #41474D (on-surface-variant). Set
decorative:false with contentDescription "No account holder data for this account".

The empty state uses an info variant (not error). The icon colour is on-surface-variant (#41474D)
rather than error red, signalling that the absence of data is expected behaviour for some account
types rather than a failure.

Below the icon, place the empty title. Style as Roboto 24sp, weight 400, colour #181C20, centre-
aligned. Text: "No account holder details". Sourced from strings.party.empty_title.

Below the title, place the empty body. Style as Roboto 14sp, weight 400, colour #41474D, centre-
aligned, line-height 20dp. Text: "No party record found for this account. This is typical for
business accounts where PSU identity is not exposed." Sourced from strings.party.empty_body and
informed by the demo-data.yaml empty state description (accountId 40051999000001).

There is no CTA button in the empty state. The state is non-recoverable from within the screen —
the user can only navigate back via the back button or the system gesture. Do not add a dummy
button; the visual must reflect the declared ui.yaml component list for this state.

---

## Frame: Consent Required State

Create a frame named "Party / Consent Required" at 393×852dp, fill #F7F9FF.

Replicate the top app bar and bottom navigation. Accounts tab selected.

### Consent Required View

In the body region, place an Auto Layout container named "consent_required_view" centred both
horizontally and vertically within the 716dp body height. Padding 24dp all sides, item spacing
16dp, direction vertical, alignment centred.

Place the `lock_person` Material Symbols icon at 48dp, colour #50606E (secondary). This uses the
warning variant palette: the secondary colour (a muted blue-grey) is chosen over error red to
signal that the restriction is a consent configuration issue rather than a system failure. Set
decorative:false, contentDescription "Permission required to view account holder data".

Below the icon, place the consent title. Style as Roboto 24sp, weight 400, colour #181C20, centre-
aligned. Text: "Permission not granted". Sourced from strings.party.consent_title.

Below the title, place the consent body. Style as Roboto 14sp, weight 400, colour #41474D, centre-
aligned, line-height 20dp. Text: "Your consent does not include access to account holder details.
Please re-authorise to grant ReadParty permission." Sourced from strings.party.consent_body.

Below the body, place the reauthorise button. Use the same filled button spec as retry_button:
background #266489, label colour #FFFFFF, corner radius 9999dp, height 56dp, horizontal padding
24dp, minimum touch target 56dp. Label text: "Manage consents". accessibility_label: "Manage your
Open Banking consent permissions". The button label deliberately uses "Manage consents" to align
with the target screen's branding (consent-list screen is named "Manage consents" in the
navigation structure).

On tap, this button triggers the `navigate_to_consent` action, routing the user to the
consent-list screen (idea-layer/screens/consent-list/). The user can then re-grant the ReadParty
permission in their active Open Banking consent, after which returning to the party screen will
trigger a fresh load and transition to Content.

---

## Auto Layout Specifications per Frame

### scrollable_column (content state body)

Direction: vertical. Alignment: leading (left). Width: fill container. Height: hug contents.
Padding: top 16dp, bottom 16dp, left 16dp, right 16dp. Item spacing: 16dp.
Overflow: scroll (clip contents, allow vertical scroll). Clip content: true.

### party_header_card

Direction: vertical. Alignment: leading. Width: fill (child of 16dp-padded column). Height: hug.
Padding: 16dp all sides. Item spacing: 4dp.
Corner radius: 12dp (all corners). Shadow: Y +1dp, blur 3dp, colour #000000 at 15%, to represent
Material elevation 2 (3dp tonal shadow in M3). Resizing: fixed width, hug height.

### email_row / mobile_row / phone_row (list items)

Direction: horizontal. Alignment: centre-vertical. Width: fill. Min height: 56dp.
Padding: top 12dp, bottom 12dp, left 16dp, right 16dp. Item spacing: 16dp.
Leading icon container: 40dp × 40dp, auto layout centred. Icon: 24dp.
Centre text stack: direction vertical, gap 2dp, weight 1 (flex grow). Fill remaining width.
Trailing text: right-aligned, max width ≈ 180dp, single line with ellipsis overflow.

### address_card (both instances)

Direction: vertical. Alignment: leading. Width: fill. Height: hug. Padding: 16dp. Item spacing: 4dp.
Corner radius: 12dp. Shadow: Y +1dp, blur 1dp, colour #000000 at 10%, representing elevation 1.

### error_state / empty_state_view / consent_required_view

Direction: vertical. Alignment: centre. Width: fill. Height: hug. Padding: 24dp all sides.
Item spacing: 16dp. Parent frame aligns this container to vertical centre using absolute position
centred in the 716dp body region.

### retry_button / reauthorise_button

Direction: horizontal. Alignment: centre. Height: 56dp. Width: fill (constrained by 24dp parent
padding, net ≈ 345dp). Corner radius: 9999dp. Padding: 0dp vertical, 24dp horizontal.
Fill: #266489. Label: Roboto 14sp, weight 500, #FFFFFF, centre-aligned.

---

## Component Variants

### Filled Button (retry_button, reauthorise_button)

Create a 5-variant component set:

**Default** — Fill #266489, label #FFFFFF, no border, corner 9999dp, height 56dp.

**Hovered** — Fill #266489 with an 8% white overlay layer on top
(rectangle same size, fill #FFFFFF at opacity 8%). Conveys hover highlight on web/desktop.

**Pressed** — Fill #266489 with a 12% black overlay layer
(rectangle same size, fill #000000 at opacity 12%). Conveys press ripple.

**Disabled** — Container fill: #E0E3E8 (#181C20 at 12%). Label colour: #181C20 at 38%.
No pointer-cursor. Do not apply pointer interaction tokens.

**Focused** — Same as Default. Add a focus ring: 3dp stroke #266489, offset 2dp outside the button
boundary. This represents keyboard/a11y focus in the Figma prototype.

### List Item Row (email_row, mobile_row, phone_row)

Create a 3-variant component set for list items:

**Default** — White/surface fill (#F7F9FF), icon #50606E, support label #41474D, trailing #181C20.
No border. No elevation.

**Hovered** — Same with a state-layer overlay: fill #266489 at 8% opacity over the row. Used for
web/pointer interactions.

**Pressed** — State-layer overlay: fill #266489 at 12% opacity. Used for tap feedback.

Note: list rows in this screen are display-only (no `on_click` declared in ui.yaml). They render
in Default state only; Hovered and Pressed variants are included in the component set for design
system completeness but are inactive in the prototype.

### Address Card

Create a 2-variant component set:

**Default** — Fill #F7F9FF, elevation 1 shadow, corner 12dp.

**Hovered** — Same fill with state-layer #266489 at 8% opacity. Address cards are also display-only
in this screen (no on_click), so this variant is for completeness only.

---

## Prototype Interaction Flow

Configure the following prototype connections in Figma Prototype mode:

**Back button (all frames)** — On Tap → Navigate to "Account Detail" frame. Animation: Slide Left,
Ease Out, 300ms. This simulates the system back navigation returning to the parent account-detail
screen, which supplies the accountId as a navigation argument.

**retry_button (Party / Error frame)** — On Tap → Navigate to "Party / Loading". Animation: Dissolve,
Ease In-Out, 150ms. This simulates the retry_load action re-triggering partyLoad, putting the
screen back into the Loading state before resolving to Content.

**reauthorise_button (Party / Consent Required frame)** — On Tap → Navigate to "Consent List" frame
(or create a placeholder frame if consent-list frames are not yet in the file). Animation: Slide Left,
Ease Out, 300ms. This simulates the navigate_to_consent action, routing to consent-list to re-grant
ReadParty. The action_contract effect is `navigate`, target `consent-list`.

**Back button on Party / Loading** — On Tap → Navigate to "Account Detail". Party / Loading is the
initial state; tapping back during loading should dismiss and return to the caller without waiting
for the API result.

---

## Accessibility Annotations

Add a dedicated "Accessibility" page or annotation layer group to the file. Document the following:

**Minimum touch targets**: All interactive elements (back_button, retry_button, reauthorise_button,
bottom nav tabs) must have a minimum tappable area of 48dp × 48dp. Where the visual size is smaller
(e.g. the 24dp icon), pad with an invisible 48dp × 48dp touch rectangle.

**Content descriptions for icons**: back_button → "Back". loading_indicator → "Loading account holder
details". error_outline → "Error loading account holder data". person_off → "No account holder data
for this account". lock_person → "Permission required to view account holder data". email icon →
decorative (suppressed from screen reader). phone_android icon → decorative. phone icon → decorative.

**PII fields and screen reader**: party_name contentDescription = "Name: Priya Sharma".
party_full_legal_name contentDescription = "Legal name: Priya Anjali Sharma".
email_row trailing contentDescription = "Email address: priya.sharma@example.co.uk".
mobile_row trailing contentDescription = "Mobile number: +44 7700 900482".
phone_row trailing contentDescription = "Phone number: +44 20 7946 0301".
address_full_card (screen_reader_only, invisible text): "Address: 48 Camden High Street, Flat 12,
London, NW1 0LT, GB" and "Address: 1 Canada Square, Suite 400, London, E14 5AB, GB".

**WCAG AA contrast**: Verify the following pairs pass 4.5:1 for normal text and 3:1 for large text.
#181C20 on #F7F9FF: passes AA (contrast ~17.5:1). #41474D on #F7F9FF: passes AA (~9.6:1).
#50606E on #F7F9FF: passes AA (~5.5:1). #FFFFFF on #266489: passes AA (~4.6:1).
#BA1A1A on #F7F9FF: passes AA (~5.8:1). #266489 on #C9E6FF: passes AA for large text (~3.5:1).

**Reduce motion**: The circular progress indicator and any shimmer animations should respect the
system prefers-reduced-motion setting. At reduced motion, the loading indicator renders as a static
partial arc rather than a spinning animation.

**Reading order**: Ensure the layer order in Figma matches the intended TalkBack/VoiceOver reading
order: top app bar → body content (top-to-bottom) → bottom navigation.

**Focus management**: On state transitions (Loading → Content, Error → Loading, ConsentRequired →
consent-list), the accessibility focus must be re-announced. The top app bar title or the first
visible content element should receive focus on state settle.

---

## Design Quality Checklist

Before finalising the Figma file, verify:

1. All five states are present as top-level frames: Party / Loading, Party / Content, Party / Error,
   Party / Empty, Party / Consent Required.

2. No placeholder text or Lorem ipsum is present in any frame. All text values are sourced from
   demo-data.yaml: "Priya Sharma", "Priya Anjali Sharma", "Sole", "priya.sharma@example.co.uk",
   "+44 7700 900482", "+44 20 7946 0301", "48 Camden High Street", "Flat 12", "London, NW1 0LT",
   "GB", "1 Canada Square", "Suite 400", "London, E14 5AB".

3. The bottom navigation bar in all frames shows exactly four tabs: Home (home icon), Accounts
   (account_balance icon), Transactions (receipt_long icon), More (more_horiz icon). The "Accounts"
   tab is active (tint #266489 with primaryContainer indicator pill). The old "PFM" tab must not
   appear — it was removed from the app shell in the 2026-06-30 update.

4. All filled buttons (retry_button, reauthorise_button) use corner radius 9999dp (full pill) and
   height 56dp. They do not use the default 8dp corner radius.

5. party_header_card uses corner radius 12dp and elevation 2. address_card instances use corner
   radius 12dp and elevation 1. These are distinct elevations producing different shadow depths.

6. The consent_required state's icon is lock_person in #50606E (secondary), not #BA1A1A (error).
   This is a deliberate design decision: a 403 permission issue is a configuration state, not an
   application error.

7. The empty state has no button. The component list for the empty state in ui.yaml declares only
   icon, title, and body. Do not add a "Reconnect" or "Try again" button.

8. The address list in the content state renders two cards: Residential (48 Camden High Street,
   Flat 12, London NW1 0LT, GB) and Business (1 Canada Square, Suite 400, London E14 5AB, GB).
   These are the two OBPostalAddress8 entries from demo-data.yaml.

9. Semantic token names are used for all colour references in Figma variable bindings rather than
   raw hex values, to enable one-click dark mode switching via the variable collection.

10. All components are connected to the Figma component library (buttons, list items, cards, bottom
    nav) and not rendered as flat groups. This enables design token propagation and component updates.
