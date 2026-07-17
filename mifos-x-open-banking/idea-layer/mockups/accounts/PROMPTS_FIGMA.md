# Accounts — Figma Design Prompts

> Generated from `screens/accounts/ui.yaml` (status: approved, quality_score: 95)
> Design system: Open Banking — Trust Blue (seed #266489, Material 3 light, Roboto)
> Canvas: 393×852dp (Pixel 5 equivalent) · All frames use the same canvas size
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

The Open Banking — Trust Blue design system is built on Material Design 3 using seed colour
`#266489` (trust blue). All colour roles are derived from the Material Theme Builder export and
resolve to the hex values below. Every frame must reference Figma variables (not inline hex) so
that dark-mode variants and dynamic-colour overrides flow through automatically.

### Semantic Token → Figma Variable Mapping

| Semantic token | Figma variable name | Light-mode hex |
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
| errorContainer | color/error-container | #FFDAD6 |
| onErrorContainer | color/on-error-container | #93000A |
| surface | color/surface | #F7F9FF |
| onSurface | color/on-surface | #181C20 |
| surfaceVariant | color/surface-variant | #DDE3EA |
| onSurfaceVariant | color/on-surface-variant | #41474D |
| surfaceContainerLowest | color/surface-container-lowest | #FFFFFF |
| outline | color/outline | #72787E |
| outlineVariant | color/outline-variant | #C1C7CE |

### Type Scale (Roboto)

| Role | Figma text style | Size / Line / Weight |
|---|---|---|
| headlineLarge | typography/headline-large | 32sp / 40sp / 400 |
| headlineSmall | typography/headline-small | 24sp / 32sp / 400 |
| titleMedium | typography/title-medium | 16sp / 24sp / 500 |
| titleSmall | typography/title-small | 14sp / 20sp / 500 |
| bodyLarge | typography/body-large | 16sp / 24sp / 400 |
| bodyMedium | typography/body-medium | 14sp / 20sp / 400 |
| bodySmall | typography/body-small | 12sp / 16sp / 400 |
| labelMedium | typography/label-medium | 12sp / 16sp / 500 |
| labelSmall | typography/label-small | 11sp / 16sp / 500 |
| labelLarge | typography/label-large | 14sp / 20sp / 500 |

Account numbers and sort codes use **Roboto Mono** at bodySmall size (12sp / 16sp / 400) to
maintain character-width stability across different identification strings.

### Shape Scale

| Token | Figma corner style | Radius |
|---|---|---|
| shape/none | Sharp | 0dp |
| shape/extra-small | Rounded | 4dp |
| shape/small | Rounded | 8dp |
| shape/medium | Rounded | 12dp |
| shape/large | Rounded | 16dp |
| shape/extra-large | Rounded | 28dp |
| shape/full | Full / Pill | 9999dp |

### Spacing Scale

| Token | Value | Figma spacing variable |
|---|---|---|
| spacing/xs | 4dp | spacing/xs |
| spacing/sm | 8dp | spacing/sm |
| spacing/md | 16dp | spacing/md |
| spacing/lg | 24dp | spacing/lg |
| spacing/screen-padding | 16dp | spacing/screen-padding |

---

## App Shell (Applied to All Frames)

Every Accounts frame carries a standard chrome that must be placed in a shared component
library and used as an instance, not a manual copy.

**Top App Bar** — Use the Material 3 Small Top App Bar component. Set background fill to
`color/surface` (#F7F9FF). Set the title text to "Accounts" using `typography/title-medium`
(16sp, weight 500) in `color/on-surface` (#181C20). No leading icon for the primary
bottom-nav tab. No trailing icons on this screen.

**Bottom Navigation Bar** — Use the Material 3 Navigation Bar component at 80dp height. Apply
`color/surface` (#F7F9FF) background. The four destinations are: Home (home icon, label
"Home"), Accounts (account_balance icon, label "Accounts", **active/selected**), Transactions
(receipt_long icon, label "Transactions"), and More (more_horiz icon, label "More"). The
selected indicator pill uses `color/secondary-container` (#D3E5F5) with the active icon in
`color/on-secondary-container` (#384956) per M3 navigation bar spec. The selected tab for
all Accounts frames is **Accounts** (tab index 1).

---

## Frame 1 — Loading State

Create a frame named **"Accounts / Loading"** at 393×852dp. Apply `color/surface` (#F7F9FF)
as the frame fill. Place the shared Top App Bar at the top (64dp height, title "Accounts").
Place the shared Bottom Navigation Bar pinned to the bottom (80dp height, Accounts selected).

The content area between top app bar and bottom nav is filled by a vertical Auto Layout
container. Set the Auto Layout to vertical direction, padding of 16dp on all sides, item
spacing of 8dp. The frame background remains `color/surface`.

Inside this container, create three shimmer skeleton cards. Each skeleton card is a rectangle
at full width (361dp, accounting for 16dp padding each side) by 96dp height. Apply
`color/surface-variant` (#DDE3EA) as the fill and corner radius of 12dp matching
`shape/medium`. Add a shimmer animation overlay: a linear gradient transitioning from
`color/surface-variant` at 0% opacity through `color/surface-container-lowest` (#FFFFFF) at
50% opacity back to `color/surface-variant`, animated horizontally at a 1.5-second ease cycle.
This communicates that account data is being fetched in parallel from the HSBC AIS endpoint.

**Auto Layout — Loading container:**
- Direction: Vertical
- Padding: 16dp (all four sides)
- Item spacing: 8dp
- Horizontal sizing: Fill container
- Vertical sizing: Hug contents

**Component variants for shimmer card:**
- Default: fill #DDE3EA, corner 12dp
- Animating: shimmer overlay active (prototype animation)

---

## Frame 2 — Content State

Create a frame named **"Accounts / Content"** at 393×852dp. Apply `color/surface` (#F7F9FF).
Place the Top App Bar and Bottom Navigation Bar as described above.

The content area between app bar and nav is a vertically scrolling column. In Figma, use an
Auto Layout frame with vertical direction, horizontal padding of 0dp (inner components manage
their own horizontal padding), vertical padding of 0dp top, and clip content enabled for
overflow scrolling.

### Total Balance Summary (stat_block)

At the top of the scrollable content, place a stat block component. This is a simple vertical
stack with padding: 16dp top, 16dp left and right, 4dp bottom. Background inherits from the
parent frame fill.

Place a label text "Total balance" using `typography/label-medium` (12sp, weight 500) in
`color/on-surface-variant` (#41474D). Directly below, place the primary balance value
"£15,797.63" using `typography/headline-large` (32sp, weight 400) in `color/on-surface`
(#181C20). Below that, add the supporting count "5 accounts" using `typography/body-small`
(12sp, weight 400) in `color/on-surface-variant` (#41474D).

**Auto Layout — stat_block:**
- Direction: Vertical
- Padding: 16dp top, 16dp horizontal, 4dp bottom
- Item spacing: 2dp
- Width: Fill container

### Account Type Filter Chips

Below the stat block, place a horizontally scrolling chip group. This is an Auto Layout frame
set to horizontal direction with horizontal padding of 16dp left and right, bottom padding of
8dp, gap of 8dp between chips, and horizontal overflow set to Scroll.

Create five filter chips with these exact labels: **All**, **Current**, **Savings**, **Credit**,
**Global**. Each chip is 32dp tall with horizontal padding of 12dp each side, full pill corner
radius (9999dp), and uses `typography/label-large` (14sp, weight 500).

The **All** chip starts selected. Selected chip appearance: fill `color/primary-container`
(#C9E6FF), label text `color/on-primary-container` (#004B6F). Unselected chip appearance: no
fill (transparent), 1dp stroke `color/outline` (#72787E), label text `color/on-surface-variant`
(#41474D).

**Component variants for each filter chip:**
- Default (unselected): transparent fill, outline #72787E, text #41474D
- Selected: fill #C9E6FF, text #004B6F, no stroke
- Hovered (unselected): fill `color/surface-variant` (#DDE3EA) at 8% opacity overlay
- Pressed (unselected): fill `color/surface-variant` at 12% opacity overlay
- Focused: 2dp outline #266489 ring outside chip boundary
- Disabled: opacity 38%

**Auto Layout — chip group row:**
- Direction: Horizontal
- Padding: 0dp top, 16dp horizontal, 8dp bottom
- Item spacing: 8dp
- Overflow: Horizontal scroll
- Height: Hug contents

### Account Card List

Below the chip group, place a vertical Auto Layout container for the account cards. Set
horizontal padding to 16dp each side, gap of 8dp, and clip content. This list is the
primary scrollable region.

Create five account cards. Each card is a Material 3 Elevated Card with corner radius 12dp
(`shape/medium`), elevation level 1 (M3 tonal shadow), fill `color/surface-container-lowest`
(#FFFFFF), and padding of 16dp on all four sides. Cards are full width within the padding
container.

**Inside each card**, use a horizontal Auto Layout row with vertical alignment center, gap of
16dp between the icon and the text column, and between the text column and the balance column.

**Left: Account type icon** — Place a 24dp Material icon at the left. Icon colour is
`color/primary` (#266489). Icons per account type: CurrentAccount uses `account_balance`,
Savings uses `savings`, CreditCard uses `credit_card`, GlobalMoney uses `public`, GlobalWallet
uses `currency_exchange`. This icon is decorative and requires no content description.

**Centre: Account text column** — A vertical Auto Layout column with gap of 4dp and
horizontal sizing set to Fill (weight 1 in the parent row). Three text layers stack vertically:
1. Account subtype label using `typography/label-small` (11sp, weight 500) in
   `color/secondary` (#50606E). Examples: "CurrentAccount", "Savings", "CreditCard",
   "GlobalMoney", "GlobalWallet".
2. Account nickname using `typography/title-medium` (16sp, weight 500) in `color/on-surface`
   (#181C20). Examples: "Everyday Current", "ISA Saver", "Platinum Mastercard", "Global Money",
   "Global Wallet — USD".
3. Account identification using `typography/body-small` (12sp, weight 400) in
   `color/on-surface-variant` (#41474D) and **Roboto Mono** typeface. Examples:
   "40-05-15 12345678", "60-16-13 31926819", "xxxx xxxx xxxx 7654",
   "GB29HBUK40051512340001", "GB29HBUK40051512340002". Mask sensitive card
   numbers as shown.

**Right: Balance column** — A vertical Auto Layout column aligned to the right edge, gap of
2dp. Two elements: the balance amount and an optional badge.

Balance amount uses `typography/headline-small` (24sp, weight 400). Colour rule: for all
accounts except CreditCard with CreditDebitIndicator=Debit, use `color/on-surface` (#181C20).
For the Platinum Mastercard (balance owed), use `color/error` (#BA1A1A). Format examples:
"£2,847.63", "£12,450.00", "£342.18" (in error colour), "£500.00", "USD 250.00" (GlobalWallet
uses native currency code prefix, not £ symbol).

Below the balance amount, conditionally show a tonal badge labelled **"Balance owed"** for the
Platinum Mastercard. The badge has fill `color/error-container` (#FFDAD6), text
`color/on-error-container` (#93000A), `typography/label-small` (11sp, weight 500), horizontal
padding 6dp each side, height 20dp, full pill corners (9999dp). Hide this badge on all other
accounts by setting the layer visibility to false.

**Auto Layout — account_card:**
- Direction: Horizontal
- Alignment: Center vertical
- Padding: 16dp all sides
- Item spacing: 16dp
- Width: Fill container (361dp within 16dp screen padding each side)
- Height: 96dp (fixed)
- Corner radius: 12dp
- Elevation: Level 1 (M3 tonal overlay + shadow)

**Component variants for account_card:**
- Default: fill #FFFFFF, elevation 1
- Hovered: fill #FFFFFF, elevation 2, state-layer overlay `color/on-surface` 8% opacity
- Pressed: fill #FFFFFF, elevation 0, state-layer overlay `color/on-surface` 12% opacity
- Focused: fill #FFFFFF, elevation 1, 2dp outline `color/primary` (#266489) inset

The five cards in order are:
1. CurrentAccount / "Everyday Current" / 40-05-15 12345678 / £2,847.63 / icon: account_balance
2. Savings / "ISA Saver" / 60-16-13 31926819 / £12,450.00 / icon: savings
3. CreditCard / "Platinum Mastercard" / xxxx xxxx xxxx 7654 / £342.18 [error] + "Balance owed" badge / icon: credit_card
4. GlobalMoney / "Global Money" / GB29HBUK40051512340001 / £500.00 / icon: public
5. GlobalWallet / "Global Wallet — USD" / GB29HBUK40051512340002 / USD 250.00 / icon: currency_exchange

**Auto Layout — accounts_list:**
- Direction: Vertical
- Padding: 0dp top, 16dp horizontal, 16dp bottom
- Item spacing: 8dp
- Width: Fill container
- Clip content: true (enables scroll in prototype)

---

## Frame 3 — Consent Expiring State

Create a frame named **"Accounts / Consent Expiring"** at 393×852dp. The content area is
identical to Frame 2 (Content), with the same stat block, chip group, and five account cards.
The unique addition is a warning banner component pinned to the bottom of the content area,
above the Bottom Navigation Bar.

### Consent Expiry Warning Banner

Create a banner component at the bottom of the scrollable content region, configured as
sticky (it does not scroll away with the card list). The banner is full width (393dp), height
approximately 72dp, with no corner radius (flat edges flush to screen width).

Set the banner background fill to `color/error-container` (#FFDAD6). Draw a 3dp left-border
line in `color/error` (#BA1A1A) to reinforce the warning severity.

Inside the banner, use a horizontal Auto Layout row with 16dp padding all around and 12dp
item spacing. On the left, place the `warning_amber` Material icon at 24dp in
`color/on-surface-variant` (#41474D).

To the right of the icon, use a vertical Auto Layout column (weight: Fill) with 2dp gap. Place
a title text "Consent expires in 14 days" using `typography/title-small` (14sp, weight 500) in
`color/on-surface` (#181C20). Below it, place body text "Re-confirm to keep your accounts
connected." using `typography/body-small` (12sp, weight 400) in `color/on-surface-variant`
(#41474D).

At the right edge of the banner row, place a text button labelled **"Reconfirm"** using
`typography/label-large` (14sp, weight 500) in `color/primary` (#266489). No background, no
border — pure text button. Minimum touch target: 48dp height × 48dp width.

**Component variants for consent_expiry_banner:**
- Default: fill #FFDAD6, left border #BA1A1A 3dp
- Banner hover (desktop preview): overlay `color/on-surface` at 8% opacity
- Banner pressed: overlay `color/on-surface` at 12% opacity

**Reconfirm button variants:**
- Default: text #266489, no fill
- Hovered: state-layer `color/primary` (#266489) at 8% opacity under the label
- Pressed: state-layer `color/primary` at 12% opacity
- Focused: 2dp ring #266489 around the text label

**Auto Layout — consent_expiry_banner:**
- Direction: Horizontal
- Alignment: Center vertical
- Padding: 16dp all sides
- Item spacing: 12dp
- Width: Fill container (393dp)
- Height: ~72dp (hug contents with min 72dp constraint)
- Position: Sticky bottom, z-index above scroll content, below Bottom Navigation Bar

---

## Frame 4 — Empty State

Create a frame named **"Accounts / Empty"** at 393×852dp. Apply `color/surface` (#F7F9FF).
Place the Top App Bar and Bottom Navigation Bar (Accounts selected) as usual. The content
area uses a centred vertical Auto Layout column.

In the centre of the available content region (between top app bar and bottom nav), place a
vertically centred stack with horizontal padding of 32dp each side. Inside, arrange three
elements in a vertical Auto Layout column with gap of 16dp and horizontal alignment centred.

Start with the `account_balance_wallet` Material icon at 48dp, colour `color/on-surface-variant`
(#41474D). Below it, place the title text "No accounts found" using `typography/headline-small`
(24sp, weight 400) in `color/on-surface` (#181C20), text alignment centred. Below the title,
place the body text "There are no accounts linked to your Open Banking consent. Contact your
bank or re-authorise access." using `typography/body-medium` (14sp, weight 400) in
`color/on-surface-variant` (#41474D), text alignment centred, with a max width of 280dp to
ensure comfortable line length.

This empty state design deliberately omits a primary CTA because the consent authorisation
pathway is managed through the consent-list screen, accessible via the Home screen's
"Manage consents" quick action. The icon size of 48dp at `color/on-surface-variant` is
intentionally subdued to avoid alarming the user.

**Auto Layout — empty_state container:**
- Direction: Vertical
- Alignment: Center horizontal and vertical within the available content area
- Padding: 32dp horizontal, 0dp vertical (parent centres this group vertically)
- Item spacing: 16dp
- Width: Fill container
- Height: Fill container (stretches between top app bar and bottom nav)

---

## Frame 5 — Error State

Create a frame named **"Accounts / Error"** at 393×852dp. Apply `color/surface` (#F7F9FF).
Place the Top App Bar and Bottom Navigation Bar (Accounts selected) as usual. The content
area uses a centred vertical Auto Layout column, mirroring the empty state layout approach.

In the centre of the content area, place a vertical Auto Layout column with 32dp horizontal
padding, gap of 24dp between the icon, title, body, and CTA, and horizontal alignment centred.

Start with the `error_outline` Material icon at 48dp, colour `color/error` (#BA1A1A). The
error colour here is intentional — it signals a recoverable technical failure, distinguishable
from the neutral empty state. Below the icon, place the title "Unable to load accounts" using
`typography/headline-small` (24sp, weight 400) in `color/on-surface` (#181C20), text alignment
centred.

Below the title, add body text "We couldn't retrieve your accounts. Check your connection and
try again." using `typography/body-medium` (14sp, weight 400) in `color/on-surface-variant`
(#41474D), centred, max width 280dp.

Below the body text, create a primary filled button labelled **"Try again"**. The button fill
is `color/primary` (#266489), label text `color/on-primary` (#FFFFFF), `typography/label-large`
(14sp, weight 500). Horizontal padding 24dp each side, height 48dp (minimum touch target),
full pill corner radius (9999dp). Minimum width 120dp to maintain comfortable tap target.

**Component variants for retry_button:**
- Default: fill #266489, text #FFFFFF
- Hovered: fill `color/primary` (#266489), state-layer overlay `color/on-primary` (#FFFFFF) at 8% opacity — M3 hover is an onPrimary layer on the unchanged primary fill; the container colour does not change
- Pressed: fill `color/primary` (#266489), state-layer overlay `color/on-primary` (#FFFFFF) at 12% opacity — M3 pressed deepens the same overlay to 12%; no new hex
- Focused: fill #266489, 2dp focus ring `color/primary` (#266489) outside button boundary
- Disabled: fill `color/on-surface` at 12% opacity, text `color/on-surface` at 38% opacity

**Auto Layout — error_state container:**
- Direction: Vertical
- Alignment: Center horizontal and vertical within the available content area
- Padding: 32dp horizontal, 0dp vertical
- Item spacing: 24dp
- Width: Fill container
- Height: Fill container

---

## Prototype Interaction Flow

Wire these interactions in Figma Prototype mode. Each source component triggers a navigation
to the named destination frame or screen:

| Source frame | Source component | Trigger | Destination |
|---|---|---|---|
| Accounts / Loading | (automatic — no user action) | After delay 0ms → API response | Accounts / Content OR Accounts / Error |
| Accounts / Content | filter_all chip | On tap | Accounts / Content (re-filter, same frame) |
| Accounts / Content | filter_current chip | On tap | Accounts / Content (filter to CurrentAccount) |
| Accounts / Content | filter_savings chip | On tap | Accounts / Content (filter to Savings) |
| Accounts / Content | filter_credit chip | On tap | Accounts / Content (filter to CreditCard) |
| Accounts / Content | filter_global chip | On tap | Accounts / Content (filter to GlobalMoney+GlobalWallet) |
| Accounts / Content | account_card (Everyday Current) | On tap | Account Detail screen (AccountId: 40051512345678) |
| Accounts / Content | account_card (ISA Saver) | On tap | Account Detail screen (AccountId: 60161331926819) |
| Accounts / Content | account_card (Platinum Mastercard) | On tap | Account Detail screen (AccountId: 40060512987654) |
| Accounts / Content | account_card (Global Money) | On tap | Account Detail screen (AccountId: 59001234000001) |
| Accounts / Content | account_card (Global Wallet — USD) | On tap | Account Detail screen (AccountId: 59001234000002) |
| Accounts / Consent Expiring | All account_cards | On tap | Account Detail screen (respective AccountId) |
| Accounts / Consent Expiring | reconfirm_button (banner) | On tap | Consent Detail screen (ConsentId: aac-7f3b9d2e-1a4c-4f8e-b3d1-9e2a5c6f0d4b) |
| Accounts / Error | retry_button | On tap | Accounts / Loading (simulate retry) |

All transitions between Accounts frames use the M3 **Fade through** motion pattern (duration
300ms, `cubic-bezier(0.2, 0.0, 0, 1.0)` emphasis easing) to match the app's low-intensity
motion configuration (`design_read.dials.motion = 2`).

Navigation from an account_card to Account Detail uses a **Forward** / **Push right** (Slide
in from right) transition at 300ms. Navigation from the Reconfirm banner CTA to Consent Detail
uses the same Forward push. Pressing the system back button reverses with **Backward** /
Slide in from left.

For the filter chip interactions, use **Smart Animate** at 150ms (short duration) to animate
the selected chip's colour fill and the account list content fade. This communicates the
instant client-side nature of the filter — no loading indicator is shown because no API call
is made.

---

## Accessibility Notes

Apply the following accessibility properties to components in Figma. When handing off to
engineers, these map directly to Compose `Modifier.semantics {}` declarations.

**Minimum touch targets** — Every interactive component (account_card, filter chips, retry
button, reconfirm button) must have a minimum tappable area of 48×48dp. For filter chips at
32dp height, add 8dp invisible padding outside the visible chip boundary. Account cards at
96dp height already exceed the minimum.

**Content descriptions** — The `account_type_icon` is decorative and must receive
`contentDescription = null` in Compose (`decorative: true` in ui.yaml). The
`account_balance_wallet` icon in the empty state and `error_outline` in the error state are
informational and must receive a meaningful content description matching the screen title or
state.

**Screen-reader reading order** — In Figma's Layer panel, maintain this top-to-bottom order
within each card: account_type_icon → account_subtype → account_nickname → account_number →
balance_amount → balance_type_badge. Screen readers must announce the balance in context with
the account name. An example announcement: "Everyday Current, CurrentAccount, 40-05-15
12345678, £2,847.63 available."

**Colour contrast** — All text colour pairs meet WCAG AA minimum (4.5:1 for normal text,
3:1 for large text). Verified pairs: `color/on-surface` (#181C20) on `color/surface` (#F7F9FF)
= 16.7:1 ✓. `color/error` (#BA1A1A) on `color/surface` (#F7F9FF) = 5.9:1 ✓.
`color/on-primary-container` (#004B6F) on `color/primary-container` (#C9E6FF) = 9.3:1 ✓.
`color/on-secondary` (#FFFFFF) on `color/secondary` (#50606E) = 4.6:1 ✓.

**Focus indicators** — All interactive elements show a 2dp `color/primary` (#266489) focus
ring when navigated via keyboard or accessibility switch. In Figma, add a focused variant to
each interactive component showing this ring. The ring is drawn outside the component boundary,
never inside, to avoid disrupting layout.

**Banner accessible name** — The `consent_expiry_banner` has role Alert in the accessibility
tree. Its accessible name is the concatenation of title and body: "Consent expires in 14 days.
Re-confirm to keep your accounts connected." The Reconfirm button's accessible name is
"Reconfirm consent connection".

**Dynamic text size** — Design the content state account card at 16sp `titleMedium` for
nickname. At maximum accessibility text size (200%), the nickname may wrap to two lines and
the card height will expand beyond the 96dp design specification. In Figma, create an
**accessibility-xl** variant of the account card with increased height (~120dp) and wrapped
nickname text to preview this case.

**Reduced motion** — The shimmer animation in the loading state must respect the system-level
reduce motion preference. Create a static variant of the skeleton cards (flat #DDE3EA fill,
no animation) for this mode. In prototype settings, link `prefers-reduced-motion: reduce` to
the static variant.

---

## Component Library Recommendations

When creating reusable components in the Figma library for this screen, structure the
component set as follows:

**AccountCard** component with properties: AccountSubType (text), Nickname (text),
Identification (text), BalanceFormatted (text), BalanceColor (enum: default/error),
ShowBadge (boolean), IconName (enum: account_balance/savings/credit_card/public/
currency_exchange). Variants: Default, Hovered, Pressed, Focused, Accessibility-XL.

**FilterChip** component with properties: Label (text), Selected (boolean). Variants:
Default-Unselected, Default-Selected, Hovered-Unselected, Hovered-Selected, Pressed,
Focused, Disabled. Attach chip to a ChipGroup auto-layout wrapper that supports horizontal
overflow scrolling.

**ConsentExpiryBanner** component with property: DaysRemaining (text — drives the title).
Variants: Default, Hovered-CTA. This is a one-off warning component specific to the OBIE
consent lifecycle.

**AccountsStatBlock** component with properties: TotalBalance (text), AccountCount (text).
No interactive variants needed — this is display-only.

**SkeletonCard** component. Variants: Static (for reduced-motion), Animated (shimmer). Use
instance swap in the loading frame to allow toggling between the two.

---

## Handoff Checklist

Before marking this spec complete in Figma:

- [ ] All five state frames created and named with "Accounts /" prefix
- [ ] Shared App Shell (Top App Bar + Bottom Nav) components used as instances, not copies
- [ ] All colour fills reference Figma variables from the `color/` namespace, not inline hex
- [ ] All text layers reference Figma text styles from the `typography/` namespace
- [ ] All spacing values use Figma spacing tokens from the `spacing/` namespace
- [ ] AccountCard created as a Figma component with all five icon variants and Default/Hovered/Pressed/Focused/Accessibility-XL state variants
- [ ] FilterChip created as a Figma component with selected/unselected × interaction variants
- [ ] Prototype connections wired for all interactive components per the Interaction Flow table
- [ ] Accessibility annotations added (touch targets, content descriptions, focus rings, reading order)
- [ ] Dark-mode sibling frames created by swapping the Figma variable collection to the dark-mode set (seed #266489 dark roles from design-tokens.yaml)
- [ ] ConsentExpiry banner uses error-container (#FFDAD6) fill — not a custom colour
- [ ] CreditCard "Balance owed" badge uses error-container fill (#FFDAD6) and on-error-container text (#93000A)
- [ ] Account identification strings use Roboto Mono, not Roboto
- [ ] GlobalWallet balance "USD 250.00" uses native currency prefix, not £ symbol
