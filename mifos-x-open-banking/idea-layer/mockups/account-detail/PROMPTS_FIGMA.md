# Account Detail — Figma Design Prompts

> Auto-generated from `screens/account-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-17T00:00:00Z

---

## Canvas Specification

Frame size: 393 × 852dp (Pixel 5 — standard Android reference frame).
All values in dp unless stated. Set the Figma frame to 1× scale (1dp = 1pt in Figma when working at 1×). Clip content to frame: on.

Top chrome: Small Top App Bar — height 64dp, bg `surface` #F7F9FF, elevation 0.
Bottom chrome: Navigation Bar — height 80dp, bg `surface` #F7F9FF, elevation 0.
Content area (between chrome): 852 − 64 − 80 = 708dp of scrollable space.
Screen background fill: `background` #F7F9FF.

---

## Design System Summary

This screen uses the **Open Banking — Trust Blue** Material 3 light theme, seeded from primary #266489.

### Resolved Colour Palette

| Role | Token Name | Hex |
|---|---|---|
| Primary | `primary` | #266489 |
| On Primary | `onPrimary` | #FFFFFF |
| Primary Container | `primaryContainer` | #C9E6FF |
| On Primary Container | `onPrimaryContainer` | #004B6F |
| Secondary | `secondary` | #50606E |
| On Secondary | `onSecondary` | #FFFFFF |
| Secondary Container | `secondaryContainer` | #D3E5F5 |
| On Secondary Container | `onSecondaryContainer` | #384956 |
| Error | `error` | #BA1A1A |
| On Error | `onError` | #FFFFFF |
| Error Container | `errorContainer` | #FFDAD6 |
| On Error Container | `onErrorContainer` | #93000A |
| Background | `background` | #F7F9FF |
| Surface | `surface` | #F7F9FF |
| On Surface | `onSurface` | #181C20 |
| Surface Variant | `surfaceVariant` | #DDE3EA |
| On Surface Variant | `onSurfaceVariant` | #41474D |
| Surface Container Lowest | `surfaceContainerLowest` | #FFFFFF |
| Surface Container Low | `surfaceContainerLow` | #F1F4F9 |
| Surface Container | `surfaceContainer` | #EBEEF3 |
| Surface Container High | `surfaceContainerHigh` | #E5E8ED |
| Surface Container Highest | `surfaceContainerHighest` | #E0E3E8 |
| Outline | `outline` | #72787E |
| Outline Variant | `outlineVariant` | #C1C7CE |
| Inverse Surface | `inverseSurface` | #2D3135 |
| Inverse On Surface | `inverseOnSurface` | #EEF1F6 |
| Inverse Primary | `inversePrimary` | #95CDF7 |
| Surface Dim | `surfaceDim` | #D7DADF |

### Semantic Token → Figma Variable Mapping

| Semantic token | Figma variable path | Resolved hex |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `secondary` | `color/secondary` | #50606E |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `surfaceContainer` | `color/surface-container` | #EBEEF3 |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/on-surface` | #181C20 |
| `outline` | `color/outline` | #72787E |
| `error` | `color/error` | #BA1A1A |
| `surfaceVariant` | `color/surface-variant` | #DDE3EA |

### Typography

All text uses Roboto. Account numbers and amounts use Roboto Mono for numeric clarity.

| Role | Size | Line Height | Weight |
|---|---|---|---|
| headlineMedium | 28sp | 36sp | 400 |
| titleLarge | 22sp | 28sp | 400 |
| titleSmall | 14sp | 20sp | 500 |
| titleMedium | 16sp | 24sp | 500 |
| bodyMedium | 14sp | 20sp | 400 |
| bodySmall | 12sp | 16sp | 400 |
| labelMedium | 12sp | 16sp | 500 |
| labelSmall | 11sp | 16sp | 500 |

### Spacing Scale

Base unit: 4dp. Screen horizontal padding: 16dp each side → content width 361dp.
Content gap: 4dp between list rows, 8dp between chips, 8–16dp vertical between card groups.

### Component State Layers

**All component hover / pressed / focused / dragged states are expressed as opacity overlays using declared token colours. No new hex values are introduced.**

| State | Overlay colour | Opacity |
|---|---|---|
| Hover | `onSurface` #181C20 | 8% |
| Focus | `onSurface` #181C20 | 10% |
| Pressed / Ripple | `onSurface` #181C20 | 12% |
| Dragged | `onSurface` #181C20 | 16% |
| Disabled container | `onSurface` #181C20 | 12% opacity fill |
| Disabled content | `onSurface` #181C20 | 38% opacity text/icon |

For chips (bg `surfaceContainerLow` #F1F4F9, content `onSurfaceVariant` #41474D):
- Hover: `onSurfaceVariant` #41474D at 8% over #F1F4F9
- Pressed: `onSurfaceVariant` #41474D at 12% over #F1F4F9

For filled primary button (bg `primary` #266489, content `onPrimary` #FFFFFF):
- Hover: `onPrimary` #FFFFFF at 8% over #266489
- Focus: `onPrimary` #FFFFFF at 10% over #266489
- Pressed: `onPrimary` #FFFFFF at 12% over #266489

---

## Frame 1 — Loading State

Create an Auto Layout frame (vertical, fill container) at 393 × 852dp named "AccountDetail / Loading".

**Top App Bar:** Create a horizontal Auto Layout row at the top, 393 × 64dp. Fill with `surface` #F7F9FF. Add a back button on the left — an icon button containing the `arrow_back` Material icon at 24dp, tinted `onSurface` #181C20, with a minimum touch target of 48 × 48dp. Leave the title area empty: the account nickname is not available during the concurrent API fetch. Do not add a skeleton placeholder for the title in the app bar.

**Spinner:** In the remaining 708dp of content area, place a single circular progress indicator centred both horizontally and vertically. The spinner is 40 × 40dp. Stroke colour: `primary` #266489. Stroke width: 4dp. Rotation: animated 0→360° with a 1.2-second linear easing in the prototype; in static Figma frames render it at 45° to show motion intent. Add an accessibility annotation: "Loading account details".

**Bottom Navigation Bar:** A persistent 393 × 80dp horizontal row pinned to the bottom. Fill `surface` #F7F9FF. Four tabs evenly distributed: Home (icon `home`), Accounts (icon `account_balance`), Transactions (icon `receipt_long`), More (icon `more_horiz`). The Accounts tab carries the active indicator: a pill shape 64 × 32dp filled `primaryContainer` #C9E6FF centred behind the icon, with the icon and label tinted `primary` #266489. All inactive tabs: icon and label tinted `onSurfaceVariant` #41474D. Label style: labelMedium 12sp. Navigation bar background elevation: 0.

**Auto Layout spec for loading frame:**
- Direction: vertical
- Main axis: space between
- Top padding: 0 (top app bar sits flush to status bar safe area)
- Spinner wrapper: use a filler frame with flex-grow 1, alignment center-center

---

## Frame 2 — Content State

Create an Auto Layout frame (vertical, fill container) at 393 × 852dp named "AccountDetail / Content".

**Top App Bar:** Same 393 × 64dp horizontal row, `surface` #F7F9FF. Back button left, title right of back button. Title text: "Everyday Current" — style titleLarge 22sp/28sp w400, colour `onSurface` #181C20.

**Scrollable Content Column:** An Auto Layout vertical column below the top app bar and above the bottom nav, configured to scroll vertically. Set horizontal padding to 16dp on both sides, top padding 16dp, bottom padding 24dp. Gap between items: 8dp default (overridden per item below).

### Account Header Card

Create a Material 3 Elevated Card (background `surfaceContainer` #EBEEF3, corner radius 12dp, elevation 2dp which renders as a subtle shadow). Width: fill container (361dp). Height: hug contents.

Inside the card, use a vertical Auto Layout column with 16dp padding all sides and an item gap of 8dp.

First child: account subtype label. Text: "CurrentAccount". Style: labelMedium 12sp/16sp weight 500. Colour: `secondary` #50606E. This is the OBIE AccountSubType field — it sits at the top of the card to give users an immediate category signal before reading the nickname.

Second child: account nickname. Text: "Everyday Current". Style: headlineMedium 28sp/36sp weight 400. Colour: `onSurface` #181C20. This is the most prominent piece of text on the screen — give it generous vertical space.

Third child: account identification. Text: "40-05-15 12345678". Style: bodyMedium 14sp/20sp weight 400. Colour: `onSurfaceVariant` #41474D. Use Roboto Mono for this field to align digits and separate the sort code visually. This is the UK.OBIE.SortCodeAccountNumber from the sandbox account.

Fourth child: a horizontal Auto Layout row with a gap of 8dp, vertically aligned to centre. Left element: currency label "GBP" in labelSmall 11sp/16sp weight 500, colour `onSurfaceVariant` #41474D. A subtle dot separator character ·. Right element: servicer BIC "MIDLGB2105V" in bodySmall 12sp/16sp weight 400, colour `onSurfaceVariant` #41474D. The BIC identifies the HSBC UK plc institution managing this sort code.

Fifth child: last-updated row. Text: "Last updated 28 Jun 2026 18:30". Style: labelSmall 11sp/16sp weight 500. Colour: `onSurfaceVariant` #41474D. This surfaces the OBIE StatusUpdateDateTime field — a trust cue that shows data freshness.

The account header card has no interactive behaviour; mark it as a display-only component. Content description for accessibility: "Account: Everyday Current, CurrentAccount, sort code 40-05-15 account 12345678, GBP, servicer MIDLGB2105V."

Spacing after card: 8dp gap before the next element.

### Open Banking Trust Badge

Below the account header card, place a Material 3 Outlined Card (no fill — use `surface` #F7F9FF as background, with a 1dp border in `outline` #72787E). Corner radius: 8dp. Elevation: 0 (no shadow). Width: fill container (361dp). Height: hug contents.

Inside, use a horizontal Auto Layout row with 12dp horizontal padding, 8dp vertical padding, and an 8dp gap. Left element: a lock icon 16dp tinted `primary` #266489. Right element: text "Connected via UK Open Banking" in labelSmall 11sp/16sp weight 500, colour `primary` #266489.

This badge is non-interactive. It conveys regulatory transparency per OBIE Customer Experience Guidelines — users should see a clear indication that data comes from a regulated Open Banking AIS consent, not from credential sharing or screen-scraping. Do not make this badge a button or link.

Content description: "Data sourced via regulated UK Open Banking AIS consent."

Spacing after badge: 16dp gap.

### Balances Section

Add a section header: text "Balances" in titleSmall 14sp/20sp weight 500, colour `onSurface` #181C20. Margin: none horizontal (uses column padding), 4dp below before the list.

Below the section header, place three List Item rows in a vertical column with a gap of 4dp between rows. Each row:
- Background: `surfaceContainerLow` #F1F4F9
- Corner radius: 8dp
- Height: 64dp
- Padding: 16dp horizontal, 12dp vertical
- Layout: horizontal space-between, centre-vertical alignment
- Left side: supporting text — the OBIE balance Type string (labelMedium 12sp/16sp weight 500, `onSurfaceVariant` #41474D)
- Right side: amount — the signed Amount plus Currency code (titleMedium 16sp/24sp weight 500, `onSurface` #181C20). Use Roboto Mono for the numeric part.

The three rows from the demo data:
1. "InterimAvailable" — "2847.63 GBP"
2. "InterimBooked" — "2810.04 GBP"
3. "OpeningBooked" — "3150.00 GBP"

None of these rows are interactive (no on_click defined on balance rows).

Content description per row: "[Type] balance: [Amount] [Currency]".

### Explore / Action Chips Section

Add a section header: text "Explore" in titleSmall 14sp/20sp weight 500, colour `onSurface` #181C20. Top margin: 16dp above this header. Bottom margin: 4dp.

Below the header, place a horizontally scrollable chip row. In Figma, create a horizontal Auto Layout frame set to hug contents in width and 32dp in height, with a gap of 8dp between chips, clipped to the 361dp content width (overflow: visible is fine for prototype scrolling, or use a scroll mask frame).

Create nine suggestion chips in this order: Transactions, Statements, Standing Orders, Direct Debits, Scheduled, Beneficiaries, ATM & Branches, Product, Party.

Each chip:
- Background fill: `surfaceContainerLow` #F1F4F9
- Border: 1dp stroke, `outline` #72787E
- Corner radius: 9999dp (full pill)
- Height: 32dp
- Horizontal padding: 8dp each side
- Inner gap (icon to label): 4dp
- Icon: 18 × 18dp, tinted `onSurfaceVariant` #41474D (see icon list below)
- Label: labelMedium 12sp/16sp weight 500, `onSurfaceVariant` #41474D

Chip icons:
- Transactions: `receipt_long`
- Statements: `description`
- Standing Orders: `autorenew`
- Direct Debits: `subscriptions`
- Scheduled: `schedule`
- Beneficiaries: `people`
- ATM & Branches: `atm`
- Product: `description`
- Party: `person`

All nine chips are interactive and navigate to their corresponding screen with the accountId param. Create a Figma component variant set "Chip" with variants: Default, Hover, Pressed. Default: bg #F1F4F9. Hover: bg #F1F4F9 with `onSurfaceVariant` #41474D at 8% opacity overlay. Pressed: bg #F1F4F9 with `onSurfaceVariant` #41474D at 12% opacity overlay.

**Auto Layout spec for content frame:**
- Outer frame: vertical Auto Layout, fill container
- Top app bar: fixed 64dp, do not stretch
- ScrollColumn: flex-grow 1, horizontal padding 16dp, top padding 16dp, bottom padding 24dp, item gap varies (use explicit spacers or set individual margins below each group)
- Bottom nav: fixed 80dp, do not stretch

---

## Frame 3 — Empty State (Zero Balances)

Create a frame named "AccountDetail / Empty" at 393 × 852dp.

**Top App Bar:** Same 393 × 64dp, `surface` #F7F9FF. Back button left. Title: "Euro Wallet" (titleLarge 22sp/28sp w400 #181C20) — this uses the `empty_scenario.account.Nickname` from the demo data, which represents a GlobalWallet sub-account.

**Content scroll area:** Vertical Auto Layout, padding 16dp horizontal, 16dp top, 24dp bottom.

**Account Header Card:** Same design as the content state but populated with empty-scenario data. Background `surfaceContainer` #EBEEF3, elevation 2dp, radius 12dp.
- account_subtype_label: "GlobalWallet" (labelMedium #50606E)
- account_nickname: "Euro Wallet" (headlineMedium #181C20)
- account_identification: "40-05-15 99999999" (bodyMedium #41474D, Roboto Mono)
- account_currency: "EUR", account_servicer: "MIDLGB2105V" (labelSmall + bodySmall #41474D)
- account_last_updated: "Last updated 28 Jun 2026 12:00" (labelSmall #41474D)

**Open Banking Trust Badge:** Same outlined card as in the content state — border `outline` #72787E, bg `surface` #F7F9FF, radius 8dp. Text: "Connected via UK Open Banking" in labelSmall #266489 with lock icon 16dp #266489. This badge appears even in the empty state because the account data still arrived via a valid Open Banking consent — transparency is unconditional.

**Balances Empty State:** Below the badge, fill the remaining content area vertically. Centre the empty state block both horizontally and vertically within that remaining space (use a filler spacer above and below with flex-grow 1).

The empty state block: vertical Auto Layout, centre-aligned, horizontal padding 32dp (tighter than the usual 16dp to give the text breathing room without stretching too wide), gap 16dp between elements.

Icon: `account_balance_wallet` Material icon, 48 × 48dp, tinted `onSurfaceVariant` #41474D. Content description: "No balance information."

Title: "No balance data available". Style: headlineSmall 24sp/32sp weight 400. Colour: `onSurface` #181C20. Alignment: centre.

Body: "No balance information is available for this account. This may occur for sub-accounts or wallet accounts." Style: bodyMedium 14sp/20sp weight 400. Colour: `onSurfaceVariant` #41474D. Alignment: centre. Max width: 280dp to keep lines short and legible.

Note in Figma annotations: this state represents a valid account (the GET /accounts call succeeded) where the GET /accounts/{id}/balances endpoint returned an empty array. The OBIE spec permits this for Global Wallet sub-accounts where balance permissions are not granted. There is no retry button here because the empty response is not an error — it is an authorised but balance-permission-absent account.

**Bottom Navigation Bar:** Persistent, 393 × 80dp, same spec as content state, Accounts tab active.

---

## Frame 4 — Error State

Create a frame named "AccountDetail / Error" at 393 × 852dp.

**Top App Bar:** Same 393 × 64dp, `surface` #F7F9FF. Back button left. No title — the account nickname was not resolved before the error occurred. The leading `arrow_back` icon gives the user the primary recovery path (go back to accounts list).

**Error State Block:** Fill the remaining 708dp of content area. Centre the block both horizontally and vertically.

Block is a vertical Auto Layout, centre-aligned, horizontal padding 32dp, gap 24dp between elements.

Icon: `error_outline` Material icon, 48 × 48dp, tinted `error` #BA1A1A. Content description: "Error loading account details."

Title: "Something went wrong". Style: headlineSmall 24sp/32sp weight 400. Colour: `onSurface` #181C20. Alignment: centre.

Body: Dynamic text — sourced from `{error.message}`. For the primary demo render (EC-401 TokenExpiredError, recoverable: true), display: "Session expired. Please log in again." Style: bodyMedium 14sp/20sp weight 400. Colour: `onSurfaceVariant` #41474D. Alignment: centre. Max width: 280dp.

Create variant annotations for the four error types:
- EC-401 (recoverable): body "Session expired. Please log in again." · retry button visible
- EC-403 (non-recoverable): body "Access to this account has been withdrawn." · retry button hidden
- EC-404 (non-recoverable): body "Account not found in your authorised account set." · retry button hidden
- EC-network (recoverable): body "No network connection. Please check your connection and retry." · retry button visible

**Retry Button:** A filled M3 button. Background: `primary` #266489. Label colour: `onPrimary` #FFFFFF. Label text: "Try again". Style: labelLarge 14sp/20sp weight 500. Height: 56dp. Width: fill container minus 64dp padding = 265dp (32dp each side). Corner radius: 9999dp (full pill). Minimum touch target: 56dp. Accessibility label: "Retry loading account details."

Visibility: shown when `error.recoverable == true` (EC-401, EC-network). Hidden when `error.recoverable == false` (EC-403, EC-404). In Figma, model this as a component property `showRetry: Boolean` that shows or hides the button with an Auto Layout conditional.

Button state variants for the retry button:
- Default: bg `primary` #266489
- Hover: bg #266489 with `onPrimary` #FFFFFF at 8% overlay
- Pressed: bg #266489 with `onPrimary` #FFFFFF at 12% overlay
- Focus: bg #266489 with `onPrimary` #FFFFFF at 10% overlay + 3dp focus ring in `primary` #266489

**Bottom Navigation Bar:** Persistent, 393 × 80dp, Accounts tab active.

---

## Component Variants

### Suggestion Chip — variant set

Create a Figma component named "Suggestion Chip / Account Detail" with the following variants. Each variant has width hug, height 32dp, radius 9999dp, horizontal padding 8dp, icon-label gap 4dp.

**Default:** Fill `surfaceContainerLow` #F1F4F9. Border 1dp `outline` #72787E. Icon 18dp tint `onSurfaceVariant` #41474D. Label labelMedium 12sp `onSurfaceVariant` #41474D.

**Hover:** Same geometry. Add a rectangle overlay covering the chip at 8% opacity, fill `onSurfaceVariant` #41474D. Do not change the border or icon/label colours.

**Pressed:** Same geometry. Overlay at 12% opacity fill `onSurfaceVariant` #41474D. Ripple colour same token. Animate in Figma prototype: Smart Animate spring on interaction end.

**Focused:** Same geometry as Default. Add a 3dp focus ring in `primary` #266489 offset 2dp from the chip boundary.

**Disabled:** Fill `surfaceContainerLow` #F1F4F9 at 12% opacity. Icon and label tinted `onSurface` #181C20 at 38% opacity. Border `outline` #72787E at 12% opacity. Chips are never disabled in the current design (all chips are always enabled on the content state) but the variant is provided for future product changes.

### Account Header Card — static display

No interactive variant is required. The card is a static display surface. In the Figma component, expose the following as component properties (text overrides):
- `subtypeLabel` (string): e.g. "CurrentAccount"
- `nickname` (string): e.g. "Everyday Current"
- `identification` (string): e.g. "40-05-15 12345678"
- `currency` (string): e.g. "GBP"
- `servicer` (string): e.g. "MIDLGB2105V"
- `lastUpdated` (string): e.g. "Last updated 28 Jun 2026 18:30"

### Open Banking Trust Badge — static display

A separate reusable component at the project library level (applies to all screens that display account data). Expose no overrides — the badge text is static ("Connected via UK Open Banking") and the lock icon is fixed. Background `surface` #F7F9FF, border `outline` #72787E 1dp, radius 8dp.

### List Item — Balance Row

Height 32dp variant does not apply here; use the standard 64dp tall list item. Create a component "Balance Row" with:
- `type` property (string): the OBIE balance Type label
- `amount` property (string): the Amount + Currency string

No interactive states — balance rows are display only.

### Filled Button — Retry

Height 56dp (M3 button recommended minimum for primary actions), radius 9999dp. Standard M3 filled button with the state layer variants described above.

---

## Prototype Interaction Flow

Wire up interactions using Figma prototype connections. All transitions use Move In from Right with duration 300ms (cubic-bezier 0.2, 0, 0, 1.0 — M3 emphasis easing).

**Loading → Content transition:**
- Trigger: After delay (to simulate API response, use 1500ms for Figma preview)
- Action: Navigate to AccountDetail / Content frame
- Animation: Smart Animate, duration 300ms

**Loading → Error transition (EC-401 demo):**
- Trigger: On tap anywhere on the loading frame (alternate prototype flow)
- Action: Navigate to AccountDetail / Error frame

**Back button (all states) → Accounts:**
- Trigger: On tap `back_button`
- Action: Navigate to Accounts screen (link to your Accounts frame)
- Animation: Move Out to Right, 300ms

**chip_transactions → Transactions screen:**
- Trigger: On tap
- Action: Navigate to Transactions frame (param: accountId shown in annotation)
- Animation: Move In from Right, 300ms

**chip_statements → Statements screen:**
- Same as chip_transactions wiring, target Statements frame

**chip_standing_orders → Standing Orders screen:**
- Target: StandingOrders frame, Move In from Right, 300ms

**chip_direct_debits → Direct Debits screen:**
- Target: DirectDebits frame, Move In from Right, 300ms

**chip_scheduled_payments → Scheduled Payments screen:**
- Target: ScheduledPayments frame, Move In from Right, 300ms

**chip_beneficiaries → Beneficiaries screen:**
- Target: Beneficiaries frame, Move In from Right, 300ms

**chip_atm_locator → ATM Locator screen:**
- Target: AtmLocator frame, Move In from Right, 300ms

**chip_product → Product screen:**
- Note: On the Product screen, this triggers GET /accounts/{accountId}/product on mount.
- Target: Product frame, Move In from Right, 300ms

**chip_party → Party screen:**
- Note: On the Party screen, this triggers GET /accounts/{accountId}/party on mount.
- Target: Party frame, Move In from Right, 300ms

**retry_button (Error state) → Loading state:**
- Trigger: On tap
- Action: Navigate to AccountDetail / Loading frame
- Animation: Instant or Dissolve 150ms (re-issuing the API call is fast)

---

## Auto Layout Specifications — Summary

### AccountDetail / Content frame

| Layer | Direction | Padding | Gap | Sizing |
|---|---|---|---|---|
| Outer frame | Vertical | 0 | 0 | Fixed 393 × 852dp |
| top_app_bar | Horizontal | L16 R4 TB12 | 0 | Fixed w393 h64 |
| scroll_column | Vertical | H16 T16 B24 | 0 (manual spacers) | Fill w, flex h |
| account_header_card | Vertical | 16 all | 8 | Fill w, hug h |
| row[currency_servicer] | Horizontal | 0 | 8 | Fill w, hug h |
| open_banking_badge | Horizontal | H12 V8 | 8 | Fill w, hug h |
| balances_list | Vertical | 0 | 4 | Fill w, hug h |
| balance_row | Horizontal | H16 V12 | 0 (space-between) | Fill w, fixed h64 |
| action_chips (LazyRow) | Horizontal | H16 V0 | 8 | Fill w clip, hug h |
| each chip | Horizontal | H8 | 4 | Hug w, fixed h32 |
| bottom_nav | Horizontal | 0 | 0 (space-evenly) | Fixed w393 h80 |

### AccountDetail / Loading frame

| Layer | Direction | Padding | Gap | Sizing |
|---|---|---|---|---|
| top_app_bar | Horizontal | L16 R16 TB12 | 0 | Fixed w393 h64 |
| content_area | Vertical | 0 | 0 | Fill w, flex h |
| spinner_wrapper | — | 0 | — | Fill w+h, centre child |
| bottom_nav | Horizontal | 0 | 0 | Fixed w393 h80 |

### AccountDetail / Empty frame

| Layer | Direction | Padding | Gap | Sizing |
|---|---|---|---|---|
| scroll_column | Vertical | H16 T16 B24 | 0 | Fill w, flex h |
| account_header_card | Vertical | 16 all | 8 | Fill w, hug h |
| open_banking_badge | Horizontal | H12 V8 | 8 | Fill w, hug h |
| empty_spacer_top | — | — | — | Flex h (pushes block to centre) |
| empty_state_block | Vertical | H32 | 16 | Fixed w280 (centred), hug h |
| empty_spacer_bottom | — | — | — | Flex h |

### AccountDetail / Error frame

| Layer | Direction | Padding | Gap | Sizing |
|---|---|---|---|---|
| error_spacer_top | — | — | — | Flex h |
| error_state_block | Vertical | H32 | 24 | Fixed w280 (centred), hug h |
| error_spacer_bottom | — | — | — | Flex h |

---

## Accessibility Annotations

### Minimum Touch Targets

All interactive elements meet the WCAG 2.1 AA / OBIE CX 48dp minimum touch target rule:
- `back_button`: 48 × 48dp touch target (icon is 24dp, surrounded by transparent 12dp padding each side)
- Each chip in `action_chips`: 32dp visible height, wrapped in a 48dp touch target — add a transparent 8dp vertical padding zone above and below each chip in the Figma prototype frame, or set the clickable bounding box to min 48dp in engineering handoff
- `retry_button`: 56dp height satisfies and exceeds the 48dp minimum
- Bottom nav tabs: each tab is ≥ 48dp wide and 80dp tall — satisfies minimum

### Content Descriptions

Annotate the following in Figma's accessibility panel:
- `loading_spinner`: "Loading account details"
- `back_button`: "Navigate back to accounts list"
- `account_header_card`: "Account: Everyday Current, CurrentAccount, sort code 40-05-15 account 12345678, GBP, servicer MIDLGB2105V"
- `open_banking_badge`: "Data sourced via regulated UK Open Banking AIS consent"
- `balances_list`: "Account balances, 3 items"
- `balance_row[0]`: "Interim Available balance: 2847.63 GBP"
- `balance_row[1]`: "Interim Booked balance: 2810.04 GBP"
- `balance_row[2]`: "Opening Booked balance: 3150.00 GBP"
- `action_chips` row: "Account quick actions, 9 options"
- Each chip: "[chip label], navigate to [target screen] for this account"
- `balances_empty_state` icon: "No balance information"
- `error_state` icon: "Error loading account details"
- `retry_button`: "Retry loading account details"

### Colour Contrast

All text/background pairings meet WCAG AA (4.5:1 for small text, 3:1 for large):
- `onSurface` #181C20 on `surface` #F7F9FF: passes AA (high contrast)
- `onSurfaceVariant` #41474D on `surfaceContainerLow` #F1F4F9: passes AA
- `primary` #266489 on `surface` #F7F9FF: passes AA for body text sizes
- `secondary` #50606E on `surfaceContainer` #EBEEF3: passes AA for labelMedium
- `onPrimary` #FFFFFF on `primary` #266489: passes AA (filled button)
- `error` #BA1A1A on `surface` #F7F9FF: passes AA (error icon and state text)

### TalkBack / VoiceOver Reading Order

In the content state, TalkBack should read in this order:
1. "Navigate back to accounts list" (back_button)
2. Screen title "Everyday Current"
3. Account header card (full content description)
4. Open Banking badge
5. "Balances" section header
6. Each balance row in order (InterimAvailable, InterimBooked, OpeningBooked)
7. "Explore" section header
8. Each chip in left-to-right order: Transactions, Statements, Standing Orders, Direct Debits, Scheduled, Beneficiaries, ATM & Branches, Product, Party
9. Navigation bar (persistent, marked as navigation landmark)

Annotate this reading order in Figma using the Accessibility plugin or numeric labels.
