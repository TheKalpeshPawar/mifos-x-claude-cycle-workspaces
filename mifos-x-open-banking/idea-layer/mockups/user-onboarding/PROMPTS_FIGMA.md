# User Onboarding — Figma Design Prompts

> Auto-generated from `screens/user-onboarding/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Canvas Specification

Create a Figma page named **User Onboarding — Open Banking**. Set the default frame dimensions to **393 × 852** (Pixel 5, dp units). Use Material 3 light theme throughout. The background fill for all frames is `#F7F9FF` (surface token). This screen has no top app bar, no bottom navigation bar, and no FAB — the shell is fully suppressed via `ui.yaml#shell` overrides. All seven state frames sit on this page side-by-side at 40dp horizontal spacing.

---

## Design System Foundation

### Semantic Token → Figma Variable Mapping

Create a Figma variable collection named **Open Banking / M3 Light** with these bindings. Reference these variables throughout every frame rather than hardcoding hex values.

| Semantic Token | Figma Variable Path | Resolved Hex |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `secondary` | `color/secondary` | #50606E |
| `onSecondary` | `color/on-secondary` | #FFFFFF |
| `secondaryContainer` | `color/secondary-container` | #D3E5F5 |
| `error` | `color/error` | #BA1A1A |
| `errorContainer` | `color/error-container` | #FFDAD6 |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/on-surface` | #181C20 |
| `surfaceVariant` | `color/surface-variant` | #DDE3EA |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `surfaceContainerLowest` | `color/surface-container-lowest` | #FFFFFF |
| `outline` | `color/outline` | #72787E |
| `outlineVariant` | `color/outline-variant` | #C1C7CE |
| `scrim` | `color/scrim` | #000000 |

### Typography Scale

Create a Figma text style collection named **Open Banking / Type**. All styles use Roboto. Add these text styles:

| Style Name | Size | Line Height | Weight |
|---|---|---|---|
| `headlineMedium` | 28 | 36 | Regular (400) |
| `headlineSmall` | 24 | 32 | Regular (400) |
| `titleLarge` | 22 | 28 | Regular (400) |
| `titleMedium` | 16 | 24 | Medium (500) |
| `titleSmall` | 14 | 20 | Medium (500) |
| `bodyMedium` | 14 | 20 | Regular (400) |
| `bodySmall` | 12 | 16 | Regular (400) |
| `labelLarge` | 14 | 20 | Medium (500) |
| `labelMedium` | 12 | 16 | Medium (500) |
| `labelSmall` | 11 | 16 | Medium (500) |

### Shape / Spacing Tokens

The corner radius scale used in this screen: `extra-large = 28dp` (filled/outlined buttons, bottom sheet top corners), `full = 9999dp` (assist chips, dots), `small = 8dp` (generic cards). Screen padding is 16dp on each side. Item spacing within lists is 0dp (dividers separate items). Gap between section elements is 12–24dp.

---

## Frame 1 — State: loading

Create a frame named **`user-onboarding/loading`** at 393 × 852dp, fill `#F7F9FF`. This frame represents the initial microsecond while the ViewModel reads the DataStore `onboarding_completed` flag.

Place a single **Circular Progress Indicator** component at the exact center of the frame (x = 196dp, y = 426dp, anchor center). The indicator circle is 48 × 48dp. The track is invisible; the active arc uses `color/primary` (#266489) with a 4dp stroke width. In Figma prototype mode, the component should loop its rotation animation at 1200ms per revolution, matching Material 3 indeterminate behavior.

There is no text, no illustration, no navigation chrome on this frame. The background communicates openness and trust through its plain `#F7F9FF` wash.

### Auto Layout — loading

This frame uses a simple fill layout. The progress indicator is placed with Constraints: Center/Center so it recenters if the frame size changes. No Auto Layout container is needed for the frame root itself — only the single centered indicator.

---

## Frame 2 — State: error

Create a frame named **`user-onboarding/error`** at 393 × 852dp, fill `#F7F9FF`. This frame is shown when the DataStore throws an IOException reading the `onboarding_completed` flag.

Start from the vertical center of the frame (y ≈ 360dp) and build a vertical Column Auto Layout group with alignment Center Horizontal, gap 16dp, padding horizontal 32dp.

First, place an icon using the **Material Symbols** library: `error_outline`, size 48 × 48dp, tint `color/error` (#BA1A1A). This communicates a recoverable system error without alarming the user.

Directly below the icon, add a Text layer with the content **"Something went wrong"** using the `headlineSmall` text style (24sp, Regular, #181C20). Set horizontal alignment to Center.

Below that, add a second Text layer with **"Could not load the onboarding flow. Please try again."** using `bodyMedium` (14sp, Regular, #41474D), horizontal alignment Center, max width 329dp (393 − 64dp padding).

Below the body text, create a Button component with the **Filled** variant. The button label reads **"Try again"** in `labelLarge` style (#FFFFFF). Set the button container color to `color/primary` (#266489), corner radius 28dp, height 56dp, minimum width 180dp. Center it horizontally within the column.

This button maps to the `retry_onboarding_init` action — annotate it with a Figma prototype interaction: On Tap → Navigate to **`user-onboarding/loading`** (representing the retry attempt).

### Auto Layout — error

The root Column container has: direction Vertical, align Center, gap 16dp, padding horizontal 32dp, sizing Hug × Hug. Place this container with Constraints: Center/Center on the parent frame so it sits vertically centered. No scroll needed — the content fits within 852dp at this density.

---

## Frame 3 — State: empty

Create a frame named **`user-onboarding/empty`** at 393 × 852dp, fill `#F7F9FF`. This state appears when onboarding is disabled by a remote feature flag.

Build a vertical Column Auto Layout group, center-aligned, gap 16dp, padding horizontal 32dp, anchored to vertical center of the frame.

Place a Material Symbols icon `info_outline`, 48 × 48dp, tinted `color/on-surface-variant` (#41474D). Below it place the title **"Setup not available"** in `headlineSmall` style, color `color/on-surface` (#181C20), center-aligned.

Below the title add the body **"Guided onboarding is currently unavailable. You can still sign in."** in `bodyMedium`, color #41474D, center-aligned, max-width 329dp.

Finally add a Filled Button labeled **"Go to sign in"** — container color #266489, text #FFFFFF, height 56dp, corner radius 28dp, minimum width 180dp, center-aligned. This maps to `navigate_to_login → login`. Add a Figma prototype arrow: On Tap → Navigate to the login screen frame (or mark as External Navigation to `user-onboarding → login`).

### Auto Layout — empty

Same layout structure as the error frame: vertical Column, Hug × Hug, centered on the parent frame. Gap 16dp between all items.

---

## Frame 4 — State: intro

Create a frame named **`user-onboarding/intro`** at 393 × 852dp, fill `#F7F9FF`. This is Step 1 of the three-step educational pager.

**Step Indicator** — At the top of the frame, 24dp below the safe area edge (typically at y=24dp), place a horizontal row of three dots left-aligned at x=16dp. The active dot (step 1) is a 10 × 10dp filled circle, fill `color/primary` (#266489). The two inactive dots are 8 × 8dp circles, stroke 1.5dp `color/outline-variant` (#C1C7CE), no fill. The dots are spaced 8dp apart. Group this as **`step_indicator_intro`**.

**Hero Illustration** — Below the stepper (margin-top 24dp), center a 240 × 200dp frame named **`hero_illustration`**. Fill this frame with a vertical linear gradient from `color/primary-container` (#C9E6FF) at top to `color/surface` (#F7F9FF) at bottom. Inside, place the illustration asset `ic_open_banking_hero` — depicting a stylized bank building, a security shield, and a smartphone in a clean line-art style consistent with the minimalist-ui aesthetic family. The illustration itself should occupy roughly 200 × 160dp centered within the frame, leaving gradient visible at the edges. Set the image's content description (alt text annotation) to "UK Open Banking — secure, regulated data sharing".

**Headline** — Below the illustration (margin-top 24dp), place a Text layer: **"Share your HSBC data securely with Open Banking"**. Use `headlineMedium` (28sp, Regular, #181C20). Horizontal padding 16dp on each side. Allow two lines — the natural line break should fall after "securely".

**Body Text** — Below the headline (margin-top 12dp), place a Text layer: **"UK Open Banking is a regulated framework overseen by the Financial Conduct Authority. It lets you share your account information with authorised apps — without sharing your password."** Use `bodyMedium` (14sp, Regular, #41474D). Horizontal padding 16dp. Set to auto-height (wraps across approximately 4 lines at 361dp content width).

**Trust Badges** — Below the body (margin-top 16dp), create a horizontal Wrap (Flex) Auto Layout row at x=16dp. Add two Assist Chip components:

- First chip `fapi_security_badge`: Leading icon `verified_user` (18dp, tint #41474D), label **"Secured by FAPI 1.0 Advanced"**. Container fill `color/surface-container-low` (#F1F4F9), border 1dp `color/outline` (#72787E), height 32dp, corner radius 9999 (full pill), label color #41474D using `labelMedium`.

- Second chip `fca_regulated_badge`: Leading icon `account_balance` (18dp, tint #41474D), label **"FCA Regulated"**. Same styling. Gap between chips: 8dp.

**Primary CTA** — At the bottom of the frame (16dp from bottom safe area edge), place a full-width Filled Button with 16dp horizontal margins on each side. Label: **"Get started"**. Container fill `color/primary` (#266489), text color #FFFFFF using `labelLarge`. Height 56dp, corner radius 28dp. The button spans 361dp (393 − 32dp margins). Add Figma prototype: On Tap → Navigate to **`user-onboarding/permissions_overview`**, transition Smart Animate 300ms standard easing.

### Auto Layout — intro

Use a vertical Column Auto Layout for the full frame content: direction Vertical, alignment Start Horizontal, padding top=24dp h=16dp bottom=16dp, gap=0dp (individual gaps handled by padding on each item). Frame sizing: Fill × Fixed 852dp. The hero illustration is Center Horizontal. The "Get started" button is Spacer-pushed to the bottom by placing a Spacer with Flex Grow between the body/chips group and the button.

### Component Variants — intro

- **Step indicator dot**: Create a component with props: `state = active | inactive`, `size = 10 | 8`. Active: fill circle. Inactive: stroke circle.
- **Assist Chip**: Create a component with states: Default, Hovered (#266489 at 8% overlay on #F1F4F9), Pressed (#266489 at 12% overlay), Focused (4dp focus ring #266489), Disabled (container #DDE3EA, label #72787E opacity 38%).
- **Button Filled**: states: Default (bg #266489), Hovered (`onPrimary` #FFFFFF at 8% state-layer over `primary` #266489), Pressed (`onPrimary` #FFFFFF at 12% state-layer over `primary` #266489), Disabled (bg #DDE3EA, label #72787E opacity 38%), Focused (focus ring 3dp #266489).

---

## Frame 5 — State: permissions_overview

Create a frame named **`user-onboarding/permissions_overview`** at 393 × 852dp, fill `#F7F9FF`. This is Step 2 of 3, showing the six OBIE ReadX permission scopes in plain English.

**Step Indicator** — Same three-dot row as intro, but now dots 1 and 2 are active (#266489 filled, 10dp) and dot 3 is inactive (#C1C7CE outline, 8dp). Place at y=24dp, x=16dp. Group as `step_indicator_permissions`.

**Section Header** — Below the stepper (margin-top 20dp), place a Text layer: **"What we'll read"** using `labelLarge` (14sp, Medium, #181C20). Add a 1dp bottom border using a Rectangle beneath it, fill `color/outline-variant` (#C1C7CE), full width (361dp). Group as `what_we_read_header`.

**Permissions List** — Below the section header (margin-top 12dp), create a vertical Auto Layout container named `permissions_list`, full width, gap 0dp between items. Add HorizontalDivider separators (1dp, #C1C7CE) between each list item. Create six ListItem components of type 3-line:

- `perm_accounts`: Leading icon `manage_accounts` (24dp, #41474D). Headline **"Account details"** in `titleSmall` (#181C20). Supporting text **"Account names, sort codes, IBANs, and currency for your HSBC accounts"** in `bodySmall` (#41474D). Minimum height 88dp. Horizontal padding 16dp. Icon positioned at 16dp from left, vertically centered in the first line.

- `perm_balances`: Icon `account_balance`. Headline **"Account balances"**. Supporting **"Current, available, and credit-limit balances across all authorised accounts in real time"**.

- `perm_transactions`: Icon `receipt_long`. Headline **"Transaction history"**. Supporting **"Up to 90 days of debits and credits, merchant names, and transaction references"**.

- `perm_standing_orders`: Icon `autorenew`. Headline **"Standing orders"**. Supporting **"Scheduled recurring payment mandates you have set up on your HSBC accounts"**.

- `perm_direct_debits`: Icon `subscriptions`. Headline **"Direct debits"**. Supporting **"Active direct-debit mandates and the most recent amounts collected on your accounts"**.

- `perm_statements`: Icon `description`. Headline **"Statements"**. Supporting **"Monthly statement summaries, opening and closing balances, and available PDF references"**.

**Consent Duration Note** — Below the list (margin-top 12dp, padding horizontal 16dp), place a Text layer: **"Your consent lasts up to 90 days. You can revoke it at any time from Settings → Manage consents."** Using `bodySmall` (12sp, Regular, #41474D), auto-height.

**Navigation Row** — At the bottom of the frame, 16dp above the safe area edge, place a horizontal Row containing two buttons:

- Left: Outlined Button `permissions_back_button`, label **"Back"**, border 1dp #72787E, text #266489, height 48dp, corner radius 24dp, minimum width 120dp. Prototype: On Tap → Navigate to `user-onboarding/intro` with reverse Smart Animate.

- Right: Filled Button `permissions_next_button`, label **"Next: Guarantees →"**, container #266489, text #FFFFFF, height 56dp, corner radius 28dp, minimum width 180dp. Prototype: On Tap → Navigate to `user-onboarding/consent_explainer`.

Arrange buttons with SpaceBetween alignment, horizontal padding 16dp.

### Auto Layout — permissions_overview

Root frame: vertical Auto Layout, padding h=16dp top=24dp bottom=16dp, gap=12dp between major sections. The permissions list container is full-width with gap=0. A Spacer with Flex Grow sits between the consent duration note and the navigation row to push the buttons to the bottom. The frame should be scrollable in prototype if content overflows at smaller heights — use an overflow container of exactly 720dp (852 − 24dp top − 16dp bottom − 56dp nav row − 16dp gap) for the scrollable region.

---

## Frame 6 — State: consent_explainer

Create a frame named **`user-onboarding/consent_explainer`** at 393 × 852dp, fill `#F7F9FF`. This is Step 3 of 3 — the AIS trust guarantees and primary connect CTA.

**Step Indicator** — All three dots filled #266489. Place at y=24dp, x=16dp. Group as `step_indicator_trust`.

**Section Header** — Margin-top 20dp: Text **"What we never do"**, `labelLarge`, #181C20, with 1dp underline in #C1C7CE. Group as `what_we_never_do_header`.

**Reassurance List** — Three ListItem 3-line components separated by 1dp HorizontalDividers (#C1C7CE). Group as `reassurance_list`.

- `never_payments`: Leading icon `money_off` (24dp, **tint #BA1A1A — the error color signals impossibility**). Headline **"No payments or transfers"** (`titleSmall`, #181C20). Supporting **"This app is Account Information only (AISP). We have no permission to initiate payments or move money from your account."** (`bodySmall`, #41474D).

- `never_password`: Leading icon `lock` (24dp, **tint #266489 — primary color signals security**). Headline **"We never see your password"**. Supporting **"You authenticate directly on HSBC's secure portal using their Strong Customer Authentication (SCA). Your credentials never leave HSBC."**.

- `never_locked_in`: Leading icon `cancel` (24dp, **tint #266489**). Headline **"Revoke access anytime"**. Supporting **"You can disconnect HSBC data sharing at any time from Settings → Manage consents, or directly from your HSBC app."**.

The deliberate use of the error color (#BA1A1A) on the `money_off` icon is intentional — it creates a visual association between "payments" and "not permitted," reinforcing the AISP-only constraint at a glance. The two primary-colored icons (#266489) signal the positive security and freedom-from-lock-in properties.

**Legal Section** — Below the reassurance list, place a HorizontalDivider (1dp, #C1C7CE) as `legal_divider`. Below it, add the `legal_footer` Text: **"Regulated by the Financial Conduct Authority under the Payment Services Regulations 2017. Powered by UK Open Banking Read/Write API v4.0 (OBIE)."** Using `labelSmall` (11sp, Medium, #41474D), horizontal padding 16dp, margin-top 8dp.

**Navigation Controls** — Three interactive elements stacked near the bottom of the frame:

First, a horizontal Row with SpaceBetween alignment and 16dp horizontal padding:
- `trust_back_button` (Outlined): label **"Back"**, border #72787E, text #266489, h=48dp, radius 24dp. Prototype: On Tap → `user-onboarding/permissions_overview`.
- `connect_hsbc_button` (Filled + trailing icon): label **"Connect to HSBC"**, trailing icon `open_in_new` (18dp, #FFFFFF), container #266489, text #FFFFFF, h=56dp, radius 28dp. Prototype: On Tap → Navigate to `login/home` (External). This is the primary conversion action — it triggers the FAPI 1.0 Advanced OBReadConsent1 flow on the login screen.

Below this row (margin-top 8dp), place a Text Button `how_ob_works_button` with label **"How does Open Banking work?"**, text color #266489, full-width, height 40dp. Prototype: On Tap → Open overlay `user-onboarding/ob_explainer_open` using a Bottom Sheet transition.

### Auto Layout — consent_explainer

Root: vertical Auto Layout, padding h=16dp top=24dp bottom=16dp, gap=12dp. Use Flex Grow spacer between the legal footer and the navigation row to push controls toward the bottom. The reassurance list is a sub-container with gap=0 and dividers.

---

## Frame 7 — State: ob_explainer_open

Create a frame named **`user-onboarding/ob_explainer_open`** at 393 × 852dp. This frame shows the `consent_explainer` content dimmed behind a modal bottom sheet overlay explaining the FAPI consent journey in plain English.

**Background** — Place a copy of the `consent_explainer` frame content as a group behind the sheet. Apply a Rectangle overlay (393 × 852dp) filled `#000000` at **40% opacity** — this is the scrim. All elements beneath the scrim should appear desaturated and non-interactive in the Figma prototype.

**Modal Bottom Sheet** — Create a Frame named `ob_explainer_sheet` sized 393 × 540dp. Position it anchored to the bottom of the parent frame (y = 852 − 540 = 312dp, x = 0). Apply corner radius 28dp to the top-left and top-right corners only; bottom corners are 0. Set fill to `color/surface-container-lowest` (#FFFFFF). Add a drop shadow: y = −4dp, blur = 12dp, color #000000 at 15%.

Inside the bottom sheet frame, use a vertical Auto Layout Column with padding horizontal=24dp, top=0, bottom=24dp, gap=0.

**Drag Handle** — At the very top of the sheet content, center a 32 × 4dp rectangle, fill `color/outline-variant` (#C1C7CE), corner radius 2dp. Add 16dp padding above and below the handle.

**Sheet Title** — Below the drag handle, place `ob_explainer_title`: Text **"How UK Open Banking works"**, `titleLarge` (22sp, Regular, #181C20), padding-bottom 16dp.

**Three FAPI Steps** — Create three ListItem 3-line components. There are no dividers between these steps to keep the reading flow continuous.

- `ob_step1`: Leading icon `how_to_reg` (24dp, tint #41474D). Headline **"You approve the permission request"** (`titleSmall`, #181C20). Supporting **"We ask HSBC to prepare a consent with the list of data categories we want to read. You are then redirected to HSBC's secure app or website to review and approve it — choosing which accounts to include."** (`bodySmall`, #41474D). Padding-bottom 12dp after each item.

- `ob_step2`: Leading icon `login` (24dp, #41474D). Headline **"You authenticate directly with HSBC"**. Supporting **"You log in on HSBC's portal using your own HSBC credentials and complete Strong Customer Authentication (SCA). Mifos Open Banking never sees your password, card number, or security codes at any point."**

- `ob_step3`: Leading icon `shield` (24dp, #41474D). Headline **"A secure token is returned to us"**. Supporting **"Once you approve, HSBC sends a short-lived, signed access token back to this app using FAPI 1.0 Advanced — a banking-grade security protocol. We use this token to read the account information you approved; it cannot be used to move money."**

**Revoke Note** — Below the three steps (padding-top 16dp), `ob_explainer_revoke_note`: Text **"You can revoke this access at any time from Settings → Manage consents, or directly from your HSBC app or HSBC online banking."** `bodySmall` (12sp, Regular, #41474D). Full width within sheet padding.

**Close Button** — At the bottom of the sheet (padding-top 24dp), `ob_explainer_close_button` Filled Button, label **"Got it"**, container #266489, text #FFFFFF, height 56dp, corner radius 28dp, full-width (393 − 48dp = 345dp). Prototype: On Tap → Close Overlay (returns to `consent_explainer` frame), transition: Slide Up 300ms standard ease.

### Auto Layout — ob_explainer_open

The scrim rectangle is a flat layer with no Auto Layout. The `ob_explainer_sheet` frame uses vertical Auto Layout: padding h=24dp top=0 bottom=24dp, gap=0. Individual gaps are achieved via padding modifiers on child Text and ListItem components. The sheet frame itself is pinned to the bottom of the parent via Constraints Bottom/Stretch. In prototype, configure this frame as a Component Set overlay variant using Bottom Sheet behavior (draggable, max height 540dp, handle visible).

---

## Prototype Interaction Flow

The following interactions wire the seven frames into a complete prototype flow. Use Smart Animate transitions at 300ms with standard M3 easing (`cubic-bezier(0.2, 0.0, 0, 1.0)`) for state changes within the onboarding pager. Use Slide transitions for bottom sheet and navigation.

| From Component | Event | To Frame | Transition |
|---|---|---|---|
| Frame auto-advance (loading) | After delay 1500ms | `intro` | Dissolve 150ms |
| `onboarding_error_retry_button` | On Tap | `loading` → (simulate) `intro` | Smart Animate 300ms |
| `onboarding_empty_skip_button` | On Tap | login (External) | Push Left 300ms |
| `intro_next_button` | On Tap | `permissions_overview` | Smart Animate 300ms (dots progress) |
| `permissions_back_button` | On Tap | `intro` | Smart Animate 300ms (reverse) |
| `permissions_next_button` | On Tap | `consent_explainer` | Smart Animate 300ms |
| `trust_back_button` | On Tap | `permissions_overview` | Smart Animate 300ms (reverse) |
| `connect_hsbc_button` | On Tap | login (External) | Push Left 300ms |
| `how_ob_works_button` | On Tap | `ob_explainer_open` overlay | Slide Up 300ms |
| `ob_explainer_close_button` | On Tap | Close overlay → `consent_explainer` | Slide Down 300ms |

The Smart Animate on the stepper dots should be the primary animated element: the active dot expands from 8dp to 10dp and transitions its fill from #C1C7CE to #266489 while its neighboring dots deactivate.

---

## Accessibility Annotations

Apply the following accessibility annotations as a Figma annotation layer group named **A11Y** on each frame. Use the Material Design accessibility annotation kit if available.

Every interactive element must meet the **48 × 48dp minimum touch target** requirement. The filled buttons (56dp height, full-width) already comply. The back outlined buttons (48dp height) meet the minimum. The Assist Chips (32dp height) require a 48dp invisible tap zone overlay — add a transparent rectangle above each chip of 48dp height centered on the chip, with the annotation "Tap target: 48dp".

All icons that convey meaningful content must have a `contentDescription` annotation. The `hero_illustration` carries alt text: **"UK Open Banking — secure, regulated data sharing"**. The action icons on buttons (`open_in_new` on Connect, `verified_user` on FAPI chip) should be marked `contentDescription = null` (decorative) since the button label already communicates their purpose.

Every state frame must be annotated with its **accessibility role** at the frame level: `"Screen — Onboarding, Step X of 3"` for intro/permissions_overview/consent_explainer. The loading frame is `"Alert — Loading"`. The error and empty frames are `"Alert — Error"` and `"Alert — Information"` respectively.

Contrast ratios (WCAG AA minimum 4.5:1 for normal text, 3:1 for large text and UI components):
- `#181C20` on `#F7F9FF` = 18.3:1 (passes AAA)
- `#41474D` on `#F7F9FF` = 9.1:1 (passes AAA)
- `#266489` on `#F7F9FF` = 6.1:1 (passes AA)
- `#FFFFFF` on `#266489` = 6.1:1 (passes AA — button labels)
- `#BA1A1A` on `#F7F9FF` = 5.8:1 (passes AA — error icon)
- `#41474D` on `#F1F4F9` = 8.7:1 (passes AAA — chip labels)

All text in the design exceeds WCAG AA contrast thresholds against their respective backgrounds.

Screen readers should announce the stepper as: `"Step 1 of 3"`, `"Step 2 of 3"`, `"Step 3 of 3"` using a live region announcement when state changes. The bottom sheet (`ob_explainer_sheet`) should be annotated as an `AlertDialog` role so TalkBack/VoiceOver focuses it on open.

Form elements: this screen contains no form inputs. All interactions are navigation and state transitions only. No keyboard focus traps exist outside the modal bottom sheet.

Reduce Motion: when the system `reduce motion` preference is active, the loading indicator should display as a static partial arc rather than animating. The stepper dots should cross-dissolve instead of Smart Animate. The bottom sheet should appear instantly (0ms) rather than sliding up. Annotate this with a `Reduced Motion` variant layer group on the component set.

---

## Component Specifications

### HorizontalStepper Component

Create a shared Figma component named **HorizontalStepper** with the following properties:
- Property `totalSteps` (number, options: 2, 3, 4)
- Property `currentStep` (number, options: 1, 2, 3, 4)
- Property `alignment` (string: Start | Center)

Internally it renders a horizontal Row Auto Layout with gap=8dp. Each dot is rendered as a component instance of **StepDot** (see below). Dots whose index ≤ `currentStep` receive the active fill; dots whose index > `currentStep` receive the inactive outline style.

**StepDot** sub-component: single variant property `state = active | inactive`.
- Active: 10 × 10dp ellipse, fill `color/primary` (#266489), no stroke.
- Inactive: 8 × 8dp ellipse, no fill, stroke 1.5dp `color/outline-variant` (#C1C7CE).

The entire stepper group has no background and aligns to the start of the content area at x=16dp, y=24dp from the top safe area edge.

### AssistChip Component

Create a component named **AssistChip** with variant property `state = default | hovered | pressed | focused | disabled`.

Structure: horizontal Row Auto Layout, height 32dp, corner radius 9999 (full pill), border 1dp.
- Leading icon slot: 18 × 18dp icon, tint `color/on-surface-variant` (#41474D).
- Label slot: `labelMedium` text (12sp, Medium, #41474D).
- Internal padding: left 8dp before icon, 8dp between icon and label, 16dp after label.

State fills:
- Default: container `color/surface-container-low` (#F1F4F9), border `color/outline` (#72787E).
- Hovered: container overlay `color/on-surface-variant` (#41474D) at 8% state-layer over `surfaceContainerLow` (#F1F4F9) — M3 state layer blend, no new hex.
- Pressed: container overlay `color/on-surface-variant` (#41474D) at 12% state-layer over `surfaceContainerLow` (#F1F4F9) — M3 state layer blend, no new hex.
- Focused: default container + 4dp focus ring `color/primary` (#266489) outside the border.
- Disabled: container `color/on-surface` (#181C20) at 12% opacity, label and icon at 38% opacity.

### ListItem3Line Component

Create a component named **ListItem3Line** with variant property `hasLeadingIcon = true | false` and `iconColor = default | error | primary`.

Structure: horizontal Row Auto Layout, min-height 88dp, padding horizontal 16dp vertical 12dp, align items Start.
- Leading icon region: 40 × 40dp container (centered icon, 24 × 24dp). Icon tint controlled by `iconColor` variant: default=#41474D, error=#BA1A1A, primary=#266489.
- Text region: vertical Column Auto Layout, gap=2dp, Flex Grow.
  - Headline: `titleSmall` text (14sp, Medium, #181C20), max 2 lines.
  - Supporting: `bodySmall` text (12sp, Regular, #41474D), max 3 lines.
- No trailing region on this screen (all list items are display-only in this flow).

The component fills the parent width (match_parent behavior via Fill Horizontal sizing in Auto Layout). Items are separated by a HorizontalDivider sub-component (1dp, fill `color/outline-variant` #C1C7CE) inserted between instances in the parent container.

### FilledButton Component

Create a component named **FilledButton** with variant property `state = default | hovered | pressed | focused | disabled | withIcon`.

Structure: horizontal Row Auto Layout, height 56dp, corner radius 28dp (extra_large), padding horizontal 24dp.
- Label: `labelLarge` (14sp, Medium, #FFFFFF).
- Optional trailing icon: 18 × 18dp icon slot (visible only in `withIcon` variant), tint #FFFFFF, 8dp gap before icon.

State fills (container):
- Default: `color/primary` (#266489).
- Hovered: `onPrimary` (#FFFFFF) at 8% state-layer overlay on `primary` (#266489).
- Pressed: `onPrimary` (#FFFFFF) at 12% state-layer overlay on `primary` (#266489).
- Focused: default + 3dp focus ring #266489 offset 3dp.
- Disabled: `color/on-surface` (#181C20) at 12% opacity. Label uses #181C20 at 38%.

The `connect_hsbc_button` uses the `withIcon` variant; `intro_next_button`, `permissions_next_button`, and `ob_explainer_close_button` use the default variant.

### OutlinedButton Component

Create a component named **OutlinedButton** with variant property `state = default | hovered | pressed | focused | disabled`.

Structure: horizontal Row Auto Layout, height 48dp, corner radius 24dp, padding horizontal 24dp, border 1dp.
- Label: `labelLarge` (14sp, Medium, `color/primary` #266489).

State borders:
- Default: `color/outline` (#72787E).
- Hovered: `color/on-surface` (#181C20) at 8% overlay on transparent.
- Pressed: `color/on-surface` at 12%.
- Focused: border changes to `color/primary` (#266489), 3dp focus ring.
- Disabled: border `color/on-surface` at 12%, label `color/on-surface` at 38%.

Used for `permissions_back_button` and `trust_back_button`.

---

## Design Rationale

### Why no chrome on onboarding?

The `ui.yaml#shell` suppresses all persistent chrome (top app bar, bottom navigation, FAB) for this screen. This is intentional: showing the bottom nav tabs during onboarding would let the PSU jump to the Home screen before they have consented, creating an incomplete AISP consent state. The full-screen pager commands focused attention and prevents premature navigation away from the regulatory disclosure flow.

### Color semantics in the reassurance list

The `never_payments` item uses icon `money_off` tinted with `color/error` (#BA1A1A). This is the only place on the screen where the error palette appears. The design choice is deliberate: the error red is not communicating a failure — it is repurposed to signal "forbidden by design" (no PISP capability), leveraging the universal stop/prohibited association of red to make the AIS-only guarantee legible at a glance. The two remaining reassurance items use `color/primary` (#266489), the trust-blue palette, to frame the password and revoke guarantees as positive security features rather than limitations.

### Trust hierarchy across the three steps

The three steps build trust in a deliberate funnel: Step 1 (intro) establishes the framework's regulatory legitimacy (FCA + FAPI badges). Step 2 (permissions_overview) shows exactly what data will be read, removing the fear of the unknown. Step 3 (consent_explainer) addresses the three core anxieties PSUs have about Open Banking: payment risk, password exposure, and lock-in. Only after all three steps does the primary CTA appear, ensuring the user makes an informed consent decision.

### The OB Explainer as a non-blocking deep-dive

The `ob_explainer_sheet` is triggered by the `how_ob_works_button` text button, which sits below the primary CTA rather than above it. This placement ensures users who simply trust the guarantees and want to proceed can tap "Connect to HSBC" without encountering the technical explainer. The plain-language FAPI walkthrough is available for more technically-minded PSUs or those with concerns, but it never blocks the primary conversion flow. The bottom sheet pattern (rather than a new screen) means the PSU never loses their place in the onboarding journey.

### Stepper vs. progress bar

A three-dot stepper is used rather than a percentage progress bar. The reason: a progress bar implies an unknown total, while three distinct dots make the finite three-step structure immediately clear. PSUs can see that they are 33%, 66%, or 100% through onboarding at a glance, and the discrete dots map exactly to the three content categories (what it is / what we read / what we never do). The dot size difference between active (10dp) and inactive (8dp) provides additional affordance beyond color alone, supporting color-blind users.

---

## Figma Handoff Checklist

Before handing off these frames to engineering, verify each item:

1. All frames use Figma Variables from the **Open Banking / M3 Light** collection — no hardcoded hex values anywhere.
2. All text layers use Figma Text Styles from **Open Banking / Type** — no ad-hoc font-size or weight overrides.
3. All button, chip, and list item instances are detached from their base components and replaced with named component instances from your local design system library so engineers can identify them in code by component name.
4. Every interactive element has a 48dp minimum tap target (use the accessibility overlay group to verify).
5. The `ob_explainer_sheet` frame is configured as an Overlay in Prototype mode with Bottom Sheet behavior (not a new screen push).
6. Export the `ic_open_banking_hero` illustration as an SVG at 1x and as a PNG at 1x, 2x, 3x for Android drawable density buckets.
7. The loading frame is connected in prototype with an After Delay → 1500ms → intro transition to simulate the DataStore read latency.
8. The `consent_explainer` and `ob_explainer_open` frames share the same Figma frame base — use the overlay mechanic rather than duplicating the consent explainer content.
9. Annotate the `connect_hsbc_button` with a red-line note: "Navigates to login screen where OBReadConsent1 payload is staged. Not a direct HSBC link — the FAPI redirect happens on the login screen."
10. Verify all 7 states are present: loading, error, empty, intro, permissions_overview, consent_explainer, ob_explainer_open.
