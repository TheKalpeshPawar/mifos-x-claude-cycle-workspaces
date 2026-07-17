# Home — Figma Design Prompts

> Generated from: `screens/home/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) · Material 3 light theme · Roboto typeface · No top app bar · Bottom nav visible
> Design system: Open Banking — Trust Blue (seed #266489, M3 dynamic colour)

---

## Design System Summary

Before building frames, establish the following local styles and variables in Figma. Every colour name below maps to a Figma variable in the `color/` collection.

### Semantic Token → Figma Variable Mapping

| Token name | Figma variable path | Hex (light mode) |
|---|---|---|
| primary | color/primary | #266489 |
| onPrimary | color/onPrimary | #FFFFFF |
| primaryContainer | color/primaryContainer | #C9E6FF |
| onPrimaryContainer | color/onPrimaryContainer | #004B6F |
| secondary | color/secondary | #50606E |
| onSecondary | color/onSecondary | #FFFFFF |
| secondaryContainer | color/secondaryContainer | #D3E5F5 |
| onSecondaryContainer | color/onSecondaryContainer | #384956 |
| error | color/error | #BA1A1A |
| onError | color/onError | #FFFFFF |
| errorContainer | color/errorContainer | #FFDAD6 |
| background | color/background | #F7F9FF |
| surface | color/surface | #F7F9FF |
| onSurface | color/onSurface | #181C20 |
| surfaceVariant | color/surfaceVariant | #DDE3EA |
| onSurfaceVariant | color/onSurfaceVariant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outlineVariant | #C1C7CE |
| surfaceContainerLow | color/surfaceContainerLow | #F1F4F9 |
| surfaceContainer | color/surfaceContainer | #EBEEF3 |

### Type Scale — Roboto (create as Figma text styles)

| Style name | Size / Line | Weight | Usage |
|---|---|---|---|
| Display/Small | 36 / 44 | 400 Regular | Hero balance amount |
| Headline/Medium | 28 / 36 | 400 Regular | Spending amount |
| Headline/Small | 24 / 32 | 400 Regular | Empty/error titles |
| Title/Large | 22 / 28 | 400 Regular | Account nickname |
| Title/Small | 14 / 20 | 500 Medium | Section headers |
| Body/Medium | 14 / 20 | 400 Regular | Transaction descriptions, amounts |
| Body/Small | 12 / 16 | 400 Regular | Labels, dates, secondary info |
| Label/Medium | 12 / 16 | 500 Medium | Account subtype chip |
| Label/Small | 11 / 16 | 500 Medium | Quick-action icon labels |

### Spacing Reference

All spacing values are multiples of 4dp. Use Figma's spacing variable collection `spacing/`:
- `spacing/xxs` = 4dp
- `spacing/xs` = 8dp
- `spacing/sm` = 12dp
- `spacing/md` = 16dp
- `spacing/lg` = 24dp
- `spacing/xl` = 32dp

### Shape Tokens

- `radius/sm` = 8dp — transaction rows
- `radius/md` = 12dp — action cards, quick-action card
- `radius/lg` = 16dp — hero card, skeleton
- `radius/full` = 9999dp — chips, filled buttons, circular icon buttons

---

## Frame: Home — Loading State

Create a new frame named **"Home / Loading"** at 393×852. Set the background fill to `color/background` (#F7F9FF). Apply a vertical Auto Layout with 0 padding and no gap — child frames will control their own spacing.

### Skeleton stack

Inside the frame, create a vertical stack child named **"Skeleton Stack"** with Auto Layout: direction vertical, item spacing 12dp, padding top 32dp, padding left and right 16dp, padding bottom 16dp, horizontal sizing fill container.

Add six children to Skeleton Stack in order:

**Skeleton Hero Card**: Create a rectangle 361dp wide × 180dp tall. Set corner radius to 16dp. Fill with `color/surfaceVariant` (#DDE3EA). Add a shimmer animation overlay — use a linear gradient from transparent to white at 30% opacity to transparent, animated left-to-right over 1.5 seconds on loop. Name this layer "skeleton_hero". Set Figma's "Layer blur" to 0 — keep fill sharp.

**Skeleton Actions Card**: Create a rectangle 361dp wide × 80dp tall. Set corner radius to 12dp. Fill with `color/surfaceVariant` (#DDE3EA). Apply the same shimmer gradient. Name it "skeleton_actions".

**Skeleton Transaction Header**: Create a rectangle 140dp wide × 20dp tall. Fill `color/surfaceVariant`. Name it "skeleton_tx_header". This represents the "Recent transactions" label placeholder.

**Skeleton Transaction Row 1**: Create a rectangle matching the container width × 64dp tall. Set corner radius to 8dp. Fill `color/surfaceVariant`. Apply shimmer. Name "skeleton_tx_1".

**Skeleton Transaction Row 2**: Duplicate skeleton_tx_1. Rename "skeleton_tx_2".

**Skeleton Transaction Row 3**: Duplicate. Rename "skeleton_tx_3".

For reduced-motion accessibility: provide a static variant where the shimmer gradient is replaced with a flat `color/surfaceVariant` fill at full opacity, no animation.

### Bottom Navigation Bar

Below the skeleton stack, place a Bottom Navigation component 393dp wide × 80dp tall. Background: `color/surface` (#F7F9FF). Add a top divider line 1dp thick, fill `color/outlineVariant` (#C1C7CE).

Arrange four equally spaced tab items using horizontal Auto Layout with equal distribution:
- **Home tab**: icon `home` 24dp, label "Home" Label/Small, indicator pill 56dp wide × 32dp tall behind icon, fill `color/secondaryContainer` (#D3E5F5), icon and label tint `color/primary` (#266489) — this is the selected state.
- **Accounts tab**: icon `account_balance` 24dp, label "Accounts" Label/Small, icon and label tint `color/onSurfaceVariant` (#41474D) — unselected.
- **Transactions tab**: icon `receipt_long` 24dp, label "Transactions" Label/Small, tint #41474D — unselected.
- **More tab**: icon `more_horiz` 24dp, label "More" Label/Small, tint #41474D — unselected.

All tab touch areas must be at minimum 48dp tall.

---

## Frame: Home — Content State

Create a frame named **"Home / Content"** at 393×852. Background: `color/background` (#F7F9FF). Use a vertical Auto Layout with fill sizing, content scrollable vertically (the frame clips overflow below the bottom nav).

### Account Switcher

Create a row component named **"Account Switcher"** using horizontal Auto Layout, height 48dp, horizontal padding 16dp, top padding 16dp, bottom padding 8dp, item spacing 8dp, horizontal overflow: scroll.

Add three chip components. Each chip uses horizontal Auto Layout, padding horizontal 16dp vertical 8dp, corner radius 9999dp (full pill shape), height 32dp:

- **Everyday Current chip (selected)**: Fill background `color/primaryContainer` (#C9E6FF). Label "Everyday Current" using Label/Medium style, fill `color/onPrimaryContainer` (#004B6F). No border.
- **ISA Saver chip (unselected)**: No fill background (transparent). Stroke 1dp `color/outline` (#72787E). Label "ISA Saver" Label/Medium, fill `color/onSurfaceVariant` (#41474D).
- **Platinum Mastercard chip (unselected)**: Same styling as ISA Saver. Label "Platinum Mastercard".

For the prototype: each chip has a tap trigger connected to the "Home / Content" frame, simulating account selection. In real implementation the tap calls `selectAccount(accountId)`.

### Hero Balance Card

Create a card component named **"Hero Balance Card"** using vertical Auto Layout. Sizing: fill width minus 32dp margin (set horizontal margin 16dp on each side). Corner radius 16dp. Background fill `color/primaryContainer` (#C9E6FF). Drop shadow: offset Y 2dp, blur 4dp, colour #000000 10% — representing M3 elevation 2. Padding: all sides 24dp. Item spacing 12dp. This entire card is tappable.

Inside the card, place the following layers in order:

**Account type row**: Horizontal Auto Layout, alignment center vertical, item spacing 0:
- Text layer "CurrentAccount" using Label/Medium (12sp/16sp weight 500), fill `color/onPrimaryContainer` (#004B6F), flex grow 1.
- Icon layer `account_balance` 24dp×24dp, fill `color/onPrimaryContainer` (#004B6F). Mark as decorative in accessibility annotation.

**Account nickname**: Text "Everyday Current", style Title/Large (22sp/28sp weight 400), fill `color/onPrimaryContainer` (#004B6F).

**Hero balance**: Text "£2,847.63", style Display/Small (36sp/44sp weight 400), fill `color/onPrimaryContainer` (#004B6F). Note: use Roboto Mono for the numeric portion to ensure aligned decimal rendering; in Figma apply a mixed-style span or a separate text layer for the currency symbol vs the amount. Accessibility label: "Balance two thousand eight hundred forty-seven pounds sixty-three pence".

**Available balance row**: Horizontal Auto Layout, alignment center vertical, item spacing 8dp:
- Text "Available" Body/Small (12sp/16sp weight 400), fill `color/onPrimaryContainer` (#004B6F).
- Text "£2,847.63" Body/Small, same fill.

**Account identifier**: Text "40-05-15 12345678", Body/Small (12sp/16sp weight 400), fill `color/onPrimaryContainer` (#004B6F). This is a sort code + account number in UK.OBIE.SortCodeAccountNumber format.

Prototype: tap the entire card → navigate to "Account Detail" frame.

### Component Variants for the Hero Card

Create a component with the following variants:
- **Default**: Background #C9E6FF, no highlight.
- **Pressed**: Apply a 12% black scrim overlay on top of the card — use a rectangle with same shape, fill black 12% opacity, placed above content.
- **Focused** (keyboard/accessibility): Add a 2dp outline ring in `color/primary` (#266489) around the card exterior, with 2dp offset gap.

### Quick Actions Card

Create a card named **"Quick Actions Card"** with horizontal Auto Layout. Sizing: fill width minus 32dp (margin 16dp each side). Height: 80dp. Corner radius 12dp. Background `color/surface` (#F7F9FF). Drop shadow: Y 1dp blur 2dp black 8% (M3 elevation 1). Padding 16dp. Item spacing 8dp. Alignment: center vertical.

Place four action slots inside, each a vertical Auto Layout with center horizontal alignment, item spacing 4dp, weight 1 (equal distribution), height fill:

**Pay slot** (disabled state):
- Icon button 48dp×48dp, icon `send` 24dp. Background fill `color/secondaryContainer` (#D3E5F5) at 38% opacity to indicate disabled. Icon tint `color/onSecondaryContainer` (#384956) at 38% opacity. Corner radius 9999dp.
- Label "Pay", Label/Small (11sp/16sp weight 500), fill `color/onSurfaceVariant` (#41474D) at 38% opacity, center aligned.
- Apply a "disabled" variant flag. Tap is intercepted but produces no navigation.

**Transactions slot** (enabled):
- Icon button 48dp×48dp, icon `receipt_long` 24dp, background #D3E5F5, icon tint #384956. Corner radius 9999dp.
- Label "Transactions", Label/Small, fill #41474D, center aligned.
- Prototype: tap → navigate to "Transactions" frame.

**Statements slot** (enabled):
- Icon button 48dp×48dp, icon `description` 24dp, same colours.
- Label "Statements", Label/Small, #41474D.
- Prototype: tap → navigate to "Statements" frame.

**Consents slot** (enabled):
- Icon button 48dp×48dp, icon `shield` 24dp, same colours.
- Label "Consents", Label/Small, #41474D.
- Prototype: tap → navigate to "Consent List" frame.

Each enabled icon button should have pressed and focused variants: pressed darkens background to `color/secondaryContainer` at full opacity; focused adds a 2dp outline ring in `color/primary`.

### Recent Transactions Section

Create a vertical stack named **"Recent Transactions Section"** using vertical Auto Layout, padding horizontal 16dp, padding bottom 16dp, item spacing 8dp, fill width.

**Section header row**: Horizontal Auto Layout, alignment center vertical, no item spacing:
- Text "Recent transactions", Title/Small (14sp/20sp weight 500), fill `color/onSurface` (#181C20), flex grow 1.
- Text button "View all", Label/Medium (12sp/16sp weight 500), fill `color/primary` (#266489). Min touch 48dp tall, extend the tap area with padding. Prototype: tap → navigate to "Transactions" frame.

**Transaction list**: A vertical stack with item spacing 4dp. Add five transaction row cards in chronological descending order:

For each transaction row, create a card component named **"Transaction Row"** using horizontal Auto Layout. Width: fill container. Height: 64dp minimum (hug content with minimum 64dp). Corner radius 8dp. Background: `color/surface` (#F7F9FF). No elevation. Padding vertical 12dp, horizontal 16dp. Item spacing 16dp. Alignment center vertical.

Transaction row internal layout:
- **Category icon** (left): Icon 24dp×24dp, fill `color/secondary` (#50606E). Mark decorative.
- **Description + date column** (centre): Vertical Auto Layout, item spacing 4dp, flex grow 1:
  - Description text: Body/Medium (14sp/20sp weight 400), fill `color/onSurface` (#181C20), max lines 1, text overflow ellipsis.
  - Date text: Body/Small (12sp/16sp weight 400), fill `color/onSurfaceVariant` (#41474D).
- **Amount** (right): Body/Medium (14sp/20sp weight 400), align end. Colour: `color/error` (#BA1A1A) for debits, `color/primary` (#266489) for credits.

The five rows with concrete content:

Row 1: icon `shopping_cart`, description "AMAZON UK MARKETPLACE", date "27 Jun", amount "- £31.99" in #BA1A1A.
Row 2: icon `restaurant`, description "PRET A MANGER 083 LONDON", date "27 Jun", amount "- £8.45" in #BA1A1A.
Row 3: icon `local_grocery_store`, description "TESCO STORES 3476 LONDON", date "26 Jun", amount "- £42.17" in #BA1A1A.
Row 4: icon `directions_bus`, description "TFL TRAVEL CHARGE", date "26 Jun", amount "- £6.80" in #BA1A1A.
Row 5: icon `work`, description "SALARY ACME LTD", date "25 Jun", amount "+ £2,400.00" in #266489.

Create a component with pressed and focused variants for each row. Pressed: overlay a black 8% scrim across the card. Focused: 2dp outline ring in `color/primary`.

Prototype: tap any row → navigate to "Transaction Detail" frame, passing the corresponding transaction.

### Spending Snapshot Card

Create a card named **"Spending Snapshot Card"** with horizontal Auto Layout. Width: fill minus 32dp (margin 16dp each side). Height: hug content, minimum 96dp. Corner radius 12dp. Background `color/surface` (#F7F9FF). Shadow Y 1dp blur 2dp black 8% (M3 elevation 1). Padding 16dp. Item spacing 16dp. Alignment center vertical. Bottom margin 32dp. This card is tappable.

Inside the card:

**Text column** (flex grow 1): Vertical Auto Layout, item spacing 4dp:
- "Spending this month": Title/Small (14sp/20sp weight 500), fill `color/onSurface` (#181C20).
- "This month": Body/Small (12sp/16sp weight 400), fill `color/onSurfaceVariant` (#41474D).
- "£167.41": Headline/Medium (28sp/36sp weight 400), fill `color/error` (#BA1A1A). The error colour communicates spending as an outflow. Accessibility label: "You have spent one hundred sixty-seven pounds forty-one pence this month".
- "Top category: Groceries": Body/Small (12sp/16sp weight 400), fill `color/onSurfaceVariant` (#41474D).

**Chevron** (right): Icon `chevron_right` 24dp×24dp, fill `color/onSurfaceVariant` (#41474D). Accessibility label: "View spending breakdown".

Component variants: Default, Pressed (black 8% scrim overlay), Focused (2dp primary outline).

Prototype: tap card → navigate to "PFM Dashboard" frame.

---

## Frame: Home — Empty State

Create a frame named **"Home / Empty"** at 393×852. Background: `color/background` (#F7F9FF). Use a vertical Auto Layout with center horizontal alignment and center vertical alignment — the entire content block is centered on screen.

### Empty Content Block

Create a vertical stack named **"Empty Content"** with Auto Layout: direction vertical, item spacing 16dp, padding horizontal 32dp, alignment center horizontal. Sizing: hug width and height.

**Icon**: Place a Material icon `account_balance_wallet` rendered at 48dp×48dp. Tint: `color/onSurfaceVariant` (#41474D). contentDescription for accessibility: "No bank accounts connected". Do not mark as decorative — screen readers announce this icon in the context of the empty state.

**Title text**: "No accounts connected yet". Style Headline/Small (24sp/32sp weight 400), fill `color/onSurface` (#181C20). Alignment: center. Max width: 280dp to ensure comfortable line wrapping on 393dp canvas.

**Body text**: "Connect your bank via Open Banking to see your balances and recent transactions." Style Body/Medium (14sp/20sp weight 400), fill `color/onSurfaceVariant` (#41474D). Alignment: center. Max width: 280dp.

**CTA Button**: Create a filled button component 56dp tall. Width: fill container (inherits 280dp from parent constraint, minus padding). Corner radius 9999dp (full pill). Background: `color/primary` (#266489). Label "Connect with Open Banking", Style Label/Large (14sp/20sp weight 500), fill `color/onPrimary` (#FFFFFF). Min touch height: 56dp (meets WCAG 2.5.8 level AA 24dp extended to accessible minimum). Top margin: 8dp extra for visual breathing room above the button.

Component variants for the button:
- **Default**: fill #266489, label #FFFFFF.
- **Hovered**: overlay white 8% over the fill.
- **Pressed**: overlay white 12% over the fill.
- **Disabled**: fill #41474D at 12% opacity, label #181C20 at 38% opacity — not applicable here (always enabled in empty state).
- **Focused**: 2dp outline ring `color/primary` at 2dp offset.

Prototype: tap "Connect with Open Banking" → navigate to "Login" frame.

### Bottom Navigation Bar

Reuse the bottom navigation component from the loading state frame. Home tab remains selected.

---

## Frame: Home — Error State

Create a frame named **"Home / Error"** at 393×852. Background `color/background` (#F7F9FF). Vertical Auto Layout with center alignment, same approach as empty state.

### Error Content Block

Create a vertical stack named **"Error Content"** with item spacing 16dp, padding horizontal 32dp, alignment center horizontal.

**Icon**: Material icon `error_outline` at 48dp×48dp. Tint: `color/error` (#BA1A1A). contentDescription: "Error loading your accounts". The red tint immediately communicates a problem state without relying on text alone (WCAG 1.4.1 use of colour).

**Title text**: "Unable to load your accounts". Style Headline/Small (24sp/32sp weight 400), fill `color/onSurface` (#181C20). Alignment center, max width 280dp.

**Body text (dynamic)**: Displays `error.userMessage` at runtime. For the demo frame, render: "Your session has expired. Please sign in again." Style Body/Medium (14sp/20sp weight 400), fill `color/onSurfaceVariant` (#41474D). Alignment center, max width 280dp. Note in the annotation layer: for EC-HOME-002 (403 non-recoverable), this message would read "Your consent doesn't include balance access. Manage your consents to restore access."

**Retry button** (conditional visibility): Render a filled button identical in dimensions and style to the empty state CTA but with label "Try again". This button is **visible when `error.recoverable == true`**. In Figma, create two variants of the error state: one with the button visible (for 401, 429, network errors) and one without it (for 403 non-recoverable). Label the variants "Error / Recoverable" and "Error / Non-recoverable". Min touch 56dp.

Prototype for "Error / Recoverable": tap "Try again" → transition to "Home / Loading" frame (simulates the retry API call).

### Bottom Navigation Bar

Reuse bottom navigation component. Home tab remains selected.

---

## Auto Layout Specifications Per Frame

### Home / Loading

Frame level: Vertical Auto Layout, clip content enabled, no padding, no item spacing.
- Skeleton Stack: Vertical Auto Layout, padding top 32 left 16 right 16 bottom 16, item spacing 12dp, horizontal sizing fill.
  - skeleton_hero: fixed 180dp tall, width fill, corner 16dp.
  - skeleton_actions: fixed 80dp tall, width fill, corner 12dp.
  - skeleton_tx_header: fixed 140dp wide × 20dp tall, no corner.
  - skeleton_tx_{1,2,3}: fixed 64dp tall, width fill, corner 8dp.
- Bottom Nav: fixed 80dp tall, width fill, pinned to frame bottom.

### Home / Content

Frame level: Vertical Auto Layout, scrollable content, clip content enabled.
- Account Switcher: Horizontal scroll container, fixed 48dp tall, width fill, padding h 16dp.
- Hero Balance Card: Vertical Auto Layout, width fill minus 32dp margin (set 16dp left/right margin), hug height, corner 16dp, padding 24dp, gap 12dp.
- Quick Actions Card: Horizontal Auto Layout, fixed 80dp tall, width fill minus 32dp, corner 12dp, padding 16dp, gap 8dp.
- Recent Transactions Section: Vertical Auto Layout, width fill, hug height, padding h 16dp bottom 16dp, gap 8dp.
  - Section header row: Horizontal Auto Layout, alignment center vertical, width fill, hug height.
  - Transaction list: Vertical Auto Layout, width fill, hug height, gap 4dp.
    - Each transaction row: Horizontal Auto Layout, width fill, min height 64dp, corner 8dp, padding v 12dp h 16dp, gap 16dp, alignment center vertical.
- Spending Snapshot Card: Horizontal Auto Layout, width fill minus 32dp, hug height min 96dp, corner 12dp, padding 16dp, gap 16dp, margin bottom 32dp.
- Bottom Nav: fixed 80dp tall, width fill, pinned to frame bottom.

### Home / Empty and Home / Error

Frame level: Vertical Auto Layout, centered vertically and horizontally, clip content.
- Content block: Vertical Auto Layout, hug width/height, padding h 32dp, gap 16dp, alignment center horizontal.
  - Icon: fixed 48dp × 48dp.
  - Title: max width 280dp, hug height.
  - Body: max width 280dp, hug height.
  - Button: fixed height 56dp, width fill (capped by content block width).
- Bottom Nav: fixed 80dp tall, width fill, pinned to frame bottom, overlapping the content (content scrolls independently but the nav is always visible).

---

## Prototype Interaction Flow

The following interaction connections model the `action_contract` declarations from `ui.yaml`.

From **Home / Loading** → after a simulated 1.5s delay → **Home / Content** (Smart Animate, 300ms ease).

From **Home / Content**:
- Tap `Everyday Current` chip → Smart Animate dissolve to **Home / Loading** (simulating re-fetch) → then to **Home / Content** (same screen, account switching in place).
- Tap `Hero Balance Card` → push transition → **Account Detail** frame (pass accountId = "40051512345678").
- Tap `Pay` icon button → no connection (disabled; prototype shows a tooltip overlay "Coming soon — PISP payments are not available in this release").
- Tap `Transactions` icon button → push → **Transactions** frame (accountId).
- Tap `Statements` icon button → push → **Statements** frame (accountId).
- Tap `Consents` icon button → push → **Consent List** frame.
- Tap any `Transaction Row` → push → **Transaction Detail** frame (transactionId, accountId).
- Tap `View all` → push → **Transactions** frame (accountId).
- Tap `Spending Snapshot Card` → push → **PFM Dashboard** frame.

From **Home / Empty**:
- Tap `Connect with Open Banking` → push → **Login** frame.

From **Home / Error / Recoverable**:
- Tap `Try again` → Smart Animate dissolve → **Home / Loading** (simulates retry API call chain).

Bottom navigation taps:
- Tap `Accounts` → push → **Accounts** frame.
- Tap `Transactions` → push → **Transactions** frame.
- Tap `More` → push → **Settings** frame.

---

## Accessibility Notes

### Touch Target Sizes

Every interactive element must meet WCAG 2.5.8 (Level AA) minimum 24dp target and recommended 48dp target:
- Account chips: set a 48dp tall invisible tap area extending above and below the 32dp chip pill.
- Icon buttons in quick actions: already 48dp × 48dp — compliant.
- Transaction rows: 64dp height — compliant.
- "View all" text button: add 8dp padding vertically to reach 48dp touch height.
- Spending snapshot card: at least 96dp height — compliant.
- Filled buttons (Connect, Try again, Retry): 56dp height — compliant.

### Content Descriptions and Screen Reader Flow

Design annotation layer: add a pink sticky note style for each interactive and meaningful non-decorative element listing its contentDescription value:
- `hero_balance`: "Balance £2,847.63" — avoid announcing the currency symbol literally; screen reader should say "two thousand eight hundred forty-seven pounds sixty-three pence".
- `hero_available_amount`: "Available balance £2,847.63".
- `hero_identification`: "Account number 40 dash 05 dash 15 12345678" — note that OBIE sort code format should be announced digit-by-digit for screen reader clarity.
- `account_chip[selected]`: "Everyday Current, selected, double tap to switch account".
- `tx_amount` (debit): "Minus £31.99" — prefix "minus" for debits.
- `tx_amount` (credit): "Plus £2,400.00".
- `spending_chevron`: "View spending breakdown" (non-decorative; its parent card is tappable so announce the CTA).
- `pay_button` (disabled): "Pay, disabled, coming soon" — still announced but action is blocked.

### Colour Contrast

All text must achieve WCAG AA minimum 4.5:1 contrast ratio:
- #004B6F on #C9E6FF (hero card body text): contrast 6.1:1 — passes AA.
- #181C20 on #F7F9FF (section headers, tx descriptions): contrast 17.4:1 — passes AAA.
- #41474D on #F7F9FF (secondary labels, dates): contrast 8.6:1 — passes AA.
- #BA1A1A on #F7F9FF (debit amounts, spending total): contrast 5.9:1 — passes AA.
- #266489 on #F7F9FF (primary actions, credit amounts): contrast 4.6:1 — passes AA.
- #FFFFFF on #266489 (button labels): contrast 4.6:1 — passes AA.

For the disabled pay button, the 38% opacity on `color/onSecondaryContainer` on `color/secondaryContainer` achieves approximately 1.5:1 contrast — intentionally below AA to signal non-interactivity; the component's disabled semantic role communicates this to screen readers without relying on contrast alone.

### Reduced Motion

For the shimmer animation in the loading state, provide a reduced-motion variant with no animated gradient — use a static `color/surfaceVariant` (#DDE3EA) fill. Figma prototype: add an interaction trigger based on the OS `prefers-reduced-motion` media query in the prototype settings, switching between the animated and static variants.

### Focus Order

Design the logical focus traversal for keyboard / switch access users in this order:
1. Account switcher chips (left to right, loop).
2. Hero balance card (single focusable unit; announces full account summary).
3. Pay icon button (announced as disabled).
4. Transactions icon button.
5. Statements icon button.
6. Consents icon button.
7. "View all" text button.
8. Transaction row 1 through 5 (each announced with description, date, and amount).
9. Spending snapshot card.
10. Bottom navigation tabs (Home, Accounts, Transactions, More).

Annotate this focus order in Figma using the Focus Order plugin numbering overlay (blue circles 1–10+) so handoff engineers implement the correct `semanticsOrder` in Jetpack Compose.

---

## Component Variants Reference

### Account Chip (chip component)

| Variant | Background | Text colour | Border |
|---|---|---|---|
| Selected | #C9E6FF | #004B6F | none |
| Unselected / Default | transparent | #41474D | 1dp #72787E |
| Unselected / Pressed | #C9E6FF at 50% | #41474D | 1dp #72787E |
| Unselected / Focused | transparent | #41474D | 2dp #266489 |

### Transaction Row (list_item component)

| Variant | Background | Amount colour |
|---|---|---|
| Default / Debit | #F7F9FF | #BA1A1A |
| Default / Credit | #F7F9FF | #266489 |
| Pressed / Debit | #EBEEF3 (surfaceContainer) | #BA1A1A |
| Pressed / Credit | #EBEEF3 | #266489 |
| Focused | #F7F9FF + 2dp outline #266489 | as above |

### Filled Button (connect / retry)

| Variant | Background | Label colour |
|---|---|---|
| Default | #266489 | #FFFFFF |
| Hovered | #266489 + white 8% | #FFFFFF |
| Pressed | #266489 + white 12% | #FFFFFF |
| Focused | #266489 + 2dp outline ring offset 2dp | #FFFFFF |
| Disabled | #41474D 12% | #181C20 38% |

### Icon Button — Tonal (quick actions)

| Variant | Container background | Icon colour |
|---|---|---|
| Default / Enabled | #D3E5F5 | #384956 |
| Hovered | #D3E5F5 + black 8% | #384956 |
| Pressed | #D3E5F5 + black 12% | #384956 |
| Focused | #D3E5F5 + 2dp outline #266489 | #384956 |
| Disabled | #D3E5F5 at 12% | #384956 at 38% |

---

## Handoff Checklist

Before marking these frames ready for engineering handoff:

- All colour fills replaced with Figma variable references (no hard-coded hex in layers).
- All text styles are Figma text style references (not overridden locally).
- All spacing set via variable tokens or layout grid constraints, not manual nudges.
- Auto Layout set on every frame and component group — no absolute positioning except for the bottom nav pin.
- Component variants published to the project library for transaction rows, chips, buttons, and icon buttons.
- Prototype connections from this set of four frames link correctly to all target screen frames.
- Accessibility annotations layer is unlocked and visible; contains focus order numbering, contentDescription values, and contrast pass/fail badges.
- Both animated and reduced-motion variants of the loading skeleton exist.
- Error state has two sub-variants: recoverable (retry button visible) and non-recoverable (retry button hidden).
