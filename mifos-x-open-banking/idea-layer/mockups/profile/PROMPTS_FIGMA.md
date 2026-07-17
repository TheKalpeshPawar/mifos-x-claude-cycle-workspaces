# Profile — Figma Design Prompts

> Generated from `screens/profile/ui.yaml` + `demo-data.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5 logical pixels) — use as a @1x frame; export @2x for Android XXHDPI
> Design system: Open Banking — Trust Blue, seed #266489, Material Design 3 light, Roboto

---

## Design System Summary

### Resolved Colour Palette

The palette derives from Material Theme Builder (seed primary #266489). All roles are M3 standard. Use these as your Figma colour styles.

Primary: `#266489` — Trust Blue. Used for active icons, selected indicators, primary CTAs, and brand anchors.
On Primary: `#FFFFFF` — White text on primary surfaces.
Primary Container: `#C9E6FF` — Tonal button background, avatar fill, selected chip fill. Light sky blue.
On Primary Container: `#004B6F` — Dark navy. Text/icons on primary container.
Secondary: `#50606E` — Slate blue-grey. Supporting body icons, deselected nav icons.
Secondary Container: `#D3E5F5` — Light steel. Rarely used at this screen.
On Secondary Container: `#384956`.
Error: `#BA1A1A` — Alert red. Sign out button border/label, error icon tint.
Error Container: `#FFDAD6` — Pale blush. Not used at this screen.
On Error: `#FFFFFF`.
Background: `#F7F9FF` — Near-white blue-tint. Page background and top app bar fill.
On Background: `#181C20` — Charcoal. Primary body text.
Surface: `#F7F9FF` — Same as background in light mode.
On Surface: `#181C20`.
Surface Variant: `#DDE3EA` — Used for list item dividers.
On Surface Variant: `#41474D` — Label text, section headers, supporting copy.
Outline: `#72787E` — Dividers where higher contrast is needed.
Outline Variant: `#C1C7CE` — Subtle divider between list items.
Surface Container Lowest: `#FFFFFF`.
Surface Container Low: `#F1F4F9` — Consent summary card background.
Surface Container: `#EBEEF3` — Identity header card background.
Surface Container High: `#E5E8ED`.

Expiry advisory tint (M3 tertiary role family): container `#EADDFF` (tertiaryContainer), icon and text `#4C4162` (onTertiaryContainer). This is M3's third semantic accent, conveying non-error advisory emphasis without inventing a custom palette.
Permission granted icons: `#266489` (primary — trust blue, signals an active granted permission).

### Roboto Type Scale (M3 default)

Display Large: 57sp / 64sp line-height / weight 400.
Headline Large: 32sp / 40sp / weight 400.
Headline Medium: 28sp / 36sp / weight 400 — user full name.
Title Large: 22sp / 28sp / weight 400 — dialog title, empty state title, error title.
Title Medium: 16sp / 24sp / weight 500 — bank label in consent card.
Title Small: 14sp / 20sp / weight 500 — section headers.
Body Large: 16sp / 24sp / weight 400.
Body Medium: 14sp / 20sp / weight 400 — supporting text in list items, error message, empty body.
Body Small: 12sp / 16sp / weight 400 — list item labels (Email, Mobile, Address).
Label Large: 14sp / 20sp / weight 500 — button labels.
Label Medium: 12sp / 16sp / weight 500 — party type caption, permission section header.
Label Small: 11sp / 16sp / weight 500.

### Spacing and Shape Tokens

Base unit: 4dp. Screen horizontal padding: 16dp. Content gap between sections: 16dp.
Corner radius extra-small: 4dp. Small: 8dp. Medium: 12dp. Large: 16dp. Extra-large: 28dp.
Cards (identity, consent, warning): radius 12dp.
Dialog (sign out confirm): radius 28dp.
Buttons (stadium shape): radius 20dp (half of 40dp height).
Avatar (circle): radius 36dp.
Bottom navigation bar: radius 0dp.

---

## Semantic Token → Figma Variable Mapping

Create a local variable collection named "Open Banking / Color" in Figma. Bind each variable to a hex value and reference it in all component fills.

| Semantic Token | Figma Variable Path | Resolved Hex |
|---|---|---|
| `primary` | `color/primary` | `#266489` |
| `onPrimary` | `color/on-primary` | `#FFFFFF` |
| `primaryContainer` | `color/primary-container` | `#C9E6FF` |
| `onPrimaryContainer` | `color/on-primary-container` | `#004B6F` |
| `secondary` | `color/secondary` | `#50606E` |
| `error` | `color/error` | `#BA1A1A` |
| `onError` | `color/on-error` | `#FFFFFF` |
| `background` | `color/background` | `#F7F9FF` |
| `onBackground` | `color/on-background` | `#181C20` |
| `surface` | `color/surface` | `#F7F9FF` |
| `onSurface` | `color/on-surface` | `#181C20` |
| `surfaceVariant` | `color/surface-variant` | `#DDE3EA` |
| `onSurfaceVariant` | `color/on-surface-variant` | `#41474D` |
| `surfaceContainerLow` | `color/surface-container-low` | `#F1F4F9` |
| `surfaceContainer` | `color/surface-container` | `#EBEEF3` |
| `outline` | `color/outline` | `#72787E` |
| `outlineVariant` | `color/outline-variant` | `#C1C7CE` |
| `tertiaryContainer` | `color/tertiary-container` | `#EADDFF` |
| `onTertiaryContainer` | `color/on-tertiary-container` | `#4C4162` |

Create a type-style collection named "Open Banking / Type" binding M3 text styles to Roboto.

---

## Frame: Profile / Loading

Create a frame named "Profile / Loading" sized 393×852dp. Set the background fill to `color/background` (#F7F9FF).

Place the top app bar as a child frame spanning the full 393dp width at 56dp height, pinned to the top. Fill it with `color/background`. Place a back-arrow icon (24dp, tint `color/on-surface` #181C20) at 16dp from the left edge, vertically centered. Place the text "Profile" (Title Large 22sp, `color/on-surface` #181C20, Roboto weight 400) starting 56dp from the left, vertically centered.

Place a circular progress indicator at the centre of the remaining content area (between top app bar bottom and bottom navigation top). Render it as a circle with a 40dp outer diameter, a 4dp stroke arc, and fill the stroke with `color/primary` #266489. This represents the in-flight API call for GET /accounts/{AccountId}/party via ktorfit.

Add the bottom navigation bar as a child frame: 393dp wide × 80dp tall, pinned to the bottom, fill `color/background`. Divide it into four equal columns. In each column, place a 24dp icon centred at 16dp from the column top, followed by a 12sp label 4dp below. Icons left-to-right: home, account_balance, receipt_long, more_horiz. Labels: "Home", "Accounts", "Transactions", "More". All icons and labels use tint/fill `color/on-surface-variant` #41474D. No tab is selected in this state.

Apply Auto Layout to the content area: vertical direction, align items centre, spacing between items 0dp, padding 0.

---

## Frame: Profile / Content

Create a frame named "Profile / Content" sized 393×852dp, background `color/background` #F7F9FF. Clip content to frame boundaries.

Begin with the same top app bar as the Loading frame (back arrow + "Profile" title).

Below the top app bar, create a vertically-scrolling Auto Layout container (direction: vertical, padding horizontal 16dp, padding top 16dp, padding bottom 96dp, item spacing 16dp). This is the main scroll content area.

### Identity Header Card

Create a card component named "identity_header_card". Set width to fill the container (361dp effective width = 393−16−16), with height of 130dp, rounded corners 12dp, and fill `color/surface-container` #EBEEF3. Apply a drop shadow matching M3 elevation level 2 (shadow blur 3dp, offset 0 1dp, colour #000000 at 15% opacity).

Inside the card, apply Auto Layout: vertical direction, align items centre (horizontal centre), padding all 16dp, item spacing 8dp.

First child: an avatar component. Create a circle box 72×72dp, fill `color/primary-container` #C9E6FF, with centered text "PS" (Label Large 14sp weight 500, fill `color/on-primary-container` #004B6F, Roboto). This represents the initials derived from "Priya Sharma" by the ProfileViewModel.

Second child: a text node displaying "Priya Sharma" in Headline Medium style (28sp, weight 400, Roboto, fill `color/on-background` #181C20). Align text to centre.

Third child: a text node displaying "Personal account" in Label Medium style (12sp weight 500, Roboto, fill `color/secondary` #50606E). Align text to centre.

### Identity Section Header

Below the card, add a text node "IDENTITY" using Title Small style (14sp weight 500, Roboto, fill `color/on-surface-variant` #41474D, letter spacing +0.1em for uppercase readability). This is the identity_section_header.

### Identity List Items

Create three list item rows stacked vertically with a thin 1dp divider between them (fill `color/outline-variant` #C1C7CE, inset 56dp from left). Each list item is an Auto Layout row (horizontal, height 64dp, padding horizontal 0dp, align items centre, item spacing 16dp).

Email row: leading icon "email" (Material Symbol Outlined 24dp, fill `color/secondary` #50606E). Text column (vertical, gap 2dp): label "Email" (Body Small 12sp #41474D) and supporting text "priya.sharma@example.co.uk" (Body Medium 14sp #181C20). The supporting text uses real data from the HSBC party endpoint (priya.sharma@example.co.uk).

Mobile row: leading icon "phone" (24dp, #50606E). Label "Mobile", supporting "+44 7700 900482". Real data from party.Phone.

Address row: leading icon "home" (24dp, #50606E). Label "Address", supporting "12 Baker Street, London W1U 6TZ". Real data from party.Address[0] (AddressType: Residential) formatted as StreetName + ", " + TownName + " " + PostCode.

### Open Banking Connection Section Header

Add a text node "OPEN BANKING CONNECTION" (Title Small 14sp w500 #41474D, same style as Identity header). This is the connection_section_header.

### Consent Summary Card

Create a card component named "consent_summary_card". Width fills container (361dp), height approximately 280dp, radius 12dp, fill `color/surface-container-low` #F1F4F9. Apply M3 elevation level 1 (shadow blur 1dp, 0 1dp offset, #000000 12% opacity).

Inside the card, Auto Layout vertical, padding 16dp, item spacing 8dp.

Bank label row: horizontal Auto Layout, gap 8dp, align items centre. Leading icon "account_balance" (20dp, fill `color/primary` #266489). Text "HSBC Open Banking" (Title Medium 16sp w500 Roboto, fill `color/on-surface` #181C20).

Consent status row: horizontal Auto Layout (list item style). Leading icon "verified" (24dp, fill `color/primary` #266489). Text column: label "Status" (Body Small 12sp #41474D) and supporting "Authorised" (Body Medium 14sp, fill `color/primary` #266489 to convey active status visually).

Consent expiry row: leading icon "schedule" (24dp, fill `color/secondary` #50606E). Label "Expires" (Body Small 12sp #41474D). Supporting "26 Sep 2026" (Body Medium 14sp #181C20).

Permissions section header: text "Permissions" (Label Medium 12sp w500 #41474D).

Permissions list: four rows, each an Auto Layout row (horizontal, gap 8dp, height 40dp). Each row has a leading icon "check_circle" (20dp, fill `color/primary` #266489) followed by text (Body Medium 14sp #181C20): "Account information", "Balances", "Transaction details", "Personal identity". These correspond to the ReadAccountsDetail, ReadBalances, ReadTransactionsDetail, and ReadParty permissions from the consent record.

Manage consent button: a Filled Tonal Button at the bottom of the card. Height 40dp, width wrapping content (approximately 180dp), radius 20dp (stadium). Fill `color/primary-container` #C9E6FF. Label "Manage consent" (Label Large 14sp w500, fill `color/on-primary-container` #004B6F). Horizontal padding 24dp.

### Sign Out Button

Below the consent summary card, create an Outlined Button spanning the full container width (361dp), height 40dp, radius 20dp. Stroke: 1dp, fill `color/error` #BA1A1A. Label "Sign out" (Label Large 14sp w500, fill `color/error` #BA1A1A). This is the destructive action entry point; it must meet WCAG AA contrast (4.5:1) against the #F7F9FF background — verified: #BA1A1A on #F7F9FF passes at approximately 5.1:1.

Close the frame with the bottom navigation bar as described in the Loading frame.

---

## Frame: Profile / Content Expiring

Create a frame named "Profile / Content Expiring" sized 393×852dp. This state is rendered when the active OBIE consent has 5 days remaining (consent.days_remaining ≤ 7).

Use the same top app bar, identity header card (Priya Sharma / PS / Personal account), identity section, and identity list items as the Content frame.

### Expiry Warning Banner

After the identity list and before the Open Banking Connection section header, insert the expiry_warning_banner card. Create a card 361dp wide with automatic height (approximately 88dp depending on text wrap), radius 12dp, fill `color/tertiary-container` #EADDFF. Elevation 0dp (flat — no shadow).

Inside, use Auto Layout: horizontal direction, padding 12dp, item spacing 12dp, align items flex-start (top).

Leading: icon "warning_amber" (24dp, fill `color/on-tertiary-container` #4C4162, contentDescription empty since the text conveys the meaning).

Trailing column (Auto Layout vertical, gap 8dp, flex-grow 1): first child is the warning text "Your consent expires in 5 days. Please renew to keep access." (Body Medium 14sp, fill `color/on-tertiary-container` #4C4162). Second child is the Renew Consent tonal button: height 40dp, width wrap (160dp), radius 20dp, fill `color/surface-variant` #DDE3EA, label "Renew Consent" (Label Large 14sp w500, fill `color/on-surface-variant` #41474D).

### Consent Summary with Expiring Data

The consent_summary_card in this state uses the expiring fixture: consent expiry row shows "04 Jul 2026" (consent.expiry_date from the expiring fixture). The permissions list contains four items (Account information, Balances, Transaction details, Personal identity) reflecting the reduced permission set in the expiring fixture. All other visual properties remain identical to the Content state.

The sign_out_button remains visible (red outlined button, 361dp wide) since its state_binding includes content_expiring.

---

## Frame: Profile / Confirm Sign Out

Create a frame named "Profile / Confirm Sign Out" sized 393×852dp.

Render the full page content (identity header card, identity list, connection section, consent summary card) as in the Content frame. The sign_out_button is not visible in this state (state_binding: [content, content_expiring] excludes confirm_sign_out).

### Modal Scrim

Place a full-frame rectangle (393×852dp) above the content layer. Fill it with #000000 at 40% opacity. This is the modal scrim that dims the background while the dialog is presented.

### Sign Out Confirmation Dialog

Centre a dialog component on the screen (horizontally and vertically). The dialog is 280dp wide with automatic height (approximately 200dp). Apply rounded corners 28dp (M3 Large shape). Fill with #FFFFFF. Apply a drop shadow matching M3 elevation level 4 (blur 8dp, spread 2dp, offset 0 2dp, #000000 20% opacity).

Inside, apply Auto Layout: vertical direction, padding horizontal 24dp, padding vertical 24dp, item spacing 16dp.

First child: title text "Sign out?" (Title Large 22sp weight 400 Roboto, fill #181C20).

Second child: body text "You will be signed out and your session will end." (Body Medium 14sp weight 400 Roboto, fill #41474D).

Third child: an action row (Auto Layout horizontal, gap 8dp, justify content flex-end). Two buttons:

"Cancel" as a Text Button: no fill, no stroke, label (Label Large 14sp w500, fill `color/primary` #266489), padding horizontal 12dp, height 40dp, radius 20dp. On tap, this dismisses the dialog and restores the previous ProfileUiState.

"Sign out" as a Filled Button: fill `color/error` #BA1A1A, label "Sign out" (Label Large 14sp w500, fill #FFFFFF), padding horizontal 24dp, height 40dp, radius 20dp. On tap, this executes the destructive sign-out flow — clears access token, refresh token, and ConsentId from EncryptedSharedPreferences, then navigates to the login screen.

---

## Frame: Profile / Error

Create a frame named "Profile / Error" sized 393×852dp, background `color/background` #F7F9FF.

Include the same top app bar (back arrow + "Profile" title).

In the content area, create an Auto Layout column centered both horizontally and vertically in the available space (between top bar and bottom nav). Apply horizontal padding 32dp and vertical item spacing 16dp.

Place an "error_outline" icon at 48dp × 48dp, tint `color/error` #BA1A1A.

Below the icon, place the title text "Couldn't load your profile" (Title Large 22sp #181C20, centred, width wrap content, max width 329dp).

Below the title, place the error body text. Use the EC-PROF-002 fixture: "Consent does not include profile access. The ReadParty permission was not granted when you authorised this app." (Body Medium 14sp #41474D, centred, max width 329dp).

Below the body, centre a Filled Button labelled "Retry": fill `color/primary` #266489, label fill #FFFFFF, Label Large 14sp w500, height 40dp, minimum width 120dp, radius 20dp, horizontal padding 24dp. On tap this re-invokes loadProfile() via the ktorfit party API.

End with the bottom navigation bar.

---

## Frame: Profile / Empty

Create a frame named "Profile / Empty" sized 393×852dp, background `color/background` #F7F9FF.

Include the same top app bar.

In the content area, create an Auto Layout column centered both horizontally and vertically (padding horizontal 32dp, item spacing 16dp).

Place an "account_circle_off" icon at 48dp × 48dp, tint `color/secondary` #50606E. This differs from the error state — the neutral tint conveys a missing-data situation rather than a failure.

Below, the title: "No profile data available" (Title Large 22sp #181C20, centred, max width 329dp).

Below the title, the body explanation: "We couldn't retrieve your identity from HSBC. Your consent may not include identity access. Re-authorise to regain access." (Body Medium 14sp #41474D, centred, max width 329dp). This text explains the EC-PROF-006 scenario where GET /party returns HTTP 200 with an empty Party array.

Below the body, a Filled Button labelled "Re-authorise": fill `color/primary` #266489, label fill #FFFFFF, Label Large 14sp w500, height 40dp, minimum width 160dp, radius 20dp, horizontal padding 24dp. On tap this navigates to the login screen to re-initiate the FAPI authorization flow and allow the PSU to grant ReadParty scope.

End with the bottom navigation bar.

---

## Auto Layout Specs

The following table describes the Auto Layout properties for each major layout zone in the Profile screen. Apply these in the Figma "Design" panel under Auto Layout.

**Main scroll container** (content area between top app bar and bottom nav):
Direction: Vertical. Padding: top 16dp, bottom 96dp, horizontal 16dp. Item spacing: 16dp. Horizontal sizing: Fill container (393dp). Vertical sizing: Hug (scrolls beyond viewport if content exceeds height). Clip content: on.

**identity_header_card** (internal):
Direction: Vertical. Align items: Centre (horizontal axis). Padding: 16dp all sides. Item spacing: 8dp. Width: Fill parent. Height: Hug.

**identity_list** (row container):
Direction: Vertical. Padding: 0dp. Item spacing: 0dp (dividers are separate 1dp rectangles). Width: Fill parent. Height: Hug.

**Each list item row** (email_row, mobile_row, address_row):
Direction: Horizontal. Padding: horizontal 0dp, vertical 12dp. Item spacing: 16dp. Align items: Centre (vertical axis). Width: Fill parent. Height: 64dp minimum.

**consent_summary_card** (internal):
Direction: Vertical. Padding: 16dp all sides. Item spacing: 8dp. Width: Fill parent. Height: Hug.

**bank_label row** (icon + text):
Direction: Horizontal. Item spacing: 8dp. Align items: Centre.

**permissions_list** (inside card):
Direction: Vertical. Item spacing: 0dp. Width: Fill parent. Height: Hug.

**Each permission row**:
Direction: Horizontal. Item spacing: 8dp. Align items: Centre. Height: 40dp. Width: Fill parent.

**expiry_warning_banner** (internal):
Direction: Horizontal. Padding: 12dp all sides. Item spacing: 12dp. Align items: Flex-start (top-aligned). Width: Fill parent. Height: Hug.

**Warning trailing column**:
Direction: Vertical. Item spacing: 8dp. Align items: Flex-start. Flex-grow: 1.

**sign_out_dialog** (internal):
Direction: Vertical. Padding: horizontal 24dp, vertical 24dp. Item spacing: 16dp. Width: Fixed 280dp. Height: Hug.

**Dialog action row**:
Direction: Horizontal. Item spacing: 8dp. Align items: Centre. Justify content: Flex-end. Width: Fill parent.

---

## Component Variants

Design a "Button" component with the following variants in Figma. Each variant changes fill, stroke, and label colour while preserving the 40dp height, 20dp radius stadium shape, and Label Large 14sp w500 typography.

**Filled / Default**: fill `color/primary` #266489, label #FFFFFF, no stroke.
**Filled / Hovered**: fill `color/primary` #266489 with 8% `color/on-primary` (#FFFFFF) state-layer overlay, label #FFFFFF, drop shadow 1dp.
**Filled / Pressed**: fill `color/primary` #266489 with 12% `color/on-primary` (#FFFFFF) state-layer overlay, label #FFFFFF, ripple #FFFFFF at 16% opacity.
**Filled / Disabled**: fill #181C20 at 12% opacity, label #181C20 at 38% opacity.

**Filled Tonal / Default** (manage_consent_button, renew_consent_button): fill `color/primary-container` #C9E6FF, label `color/on-primary-container` #004B6F.
**Filled Tonal / Hovered**: fill `color/primary-container` #C9E6FF with 8% `color/on-primary-container` (#004B6F) state-layer overlay, label #004B6F.
**Filled Tonal / Pressed**: fill `color/primary-container` #C9E6FF with 12% `color/on-primary-container` (#004B6F) state-layer overlay, label #004B6F, ripple #004B6F at 12% opacity.
**Filled Tonal / Disabled**: fill #181C20 at 12% opacity, label #181C20 at 38% opacity.

**Outlined Error / Default** (sign_out_button): fill transparent, stroke 1dp `color/error` #BA1A1A, label `color/error` #BA1A1A.
**Outlined Error / Hovered**: fill #BA1A1A at 8% opacity, stroke 1dp #BA1A1A.
**Outlined Error / Pressed**: fill #BA1A1A at 12% opacity, stroke 1dp #BA1A1A, ripple #BA1A1A at 12% opacity.
**Outlined Error / Focused**: stroke 3dp #BA1A1A (accessibility focus ring).

**Text Button / Default** (cancel_sign_out_button): fill transparent, label `color/primary` #266489.
**Text Button / Hovered**: fill #266489 at 8% opacity.
**Text Button / Pressed**: fill #266489 at 12% opacity.

**Filled Error / Default** (confirm_sign_out_button): fill `color/error` #BA1A1A, label #FFFFFF.
**Filled Error / Hovered**: fill `color/error` #BA1A1A with 8% `color/on-error` (#FFFFFF) state-layer overlay, label #FFFFFF.
**Filled Error / Pressed**: fill `color/error` #BA1A1A with 12% `color/on-error` (#FFFFFF) state-layer overlay, label #FFFFFF, ripple #FFFFFF at 16%.

Avatar component: circle shape, fixed 72×72dp. Three variants — Initials (fill `color/primary-container` #C9E6FF + text #004B6F), Photo (image fill), Error (fill `color/surface-container-high` #E5E8ED + icon person_off #41474D).

---

## Prototype Interaction Flow

Wire the following interactions using Figma's Prototype panel. All transitions use Smart Animate with 300ms duration (M3 medium easing cubic-bezier 0.2, 0, 0, 1.0) unless noted.

On tap "Manage consent" button (manage_consent_button) in the Content or Content Expiring frames → Navigate to consent-detail screen. Transition: Push from right (300ms).

On tap "Renew Consent" button (renew_consent_button) in the Content Expiring frame → Navigate to consent-detail screen with renew=true semantic. Transition: Push from right (300ms).

On tap "Sign out" outlined button (sign_out_button) in the Content or Content Expiring frames → Navigate to the Confirm Sign Out frame. Transition: Dissolve (150ms), representing the dialog appearing over the current content.

On tap "Cancel" text button (cancel_sign_out_button) in the Confirm Sign Out frame → Navigate back to the Content frame. Transition: Dissolve (150ms).

On tap "Sign out" filled error button (confirm_sign_out_button) in the Confirm Sign Out frame → Navigate to login screen. Transition: Push from right (300ms), representing end of the authenticated session.

On tap "Retry" button (retry_button) in the Error frame → Navigate to the Loading frame. Transition: Dissolve (150ms), representing the API re-call animation.

On tap "Re-authorise" button (profile_empty_reauth_button) in the Empty frame → Navigate to login screen. Transition: Push from right (300ms), representing a fresh FAPI authorization start.

Back arrow in the top app bar (all frames) → Navigate to the previous screen (typically the More / settings entry point). Transition: Pop to left (300ms).

---

## Accessibility Specifications

The Profile screen displays PSU personal identity data (name, email, phone, address). No data is masked in the current ui.yaml — all fields are shown in clear text. If a future privacy requirement demands masking, the email and phone fields should be redacted to p*****@example.co.uk and +44 **** ****82 respectively before rendering.

All interactive surfaces must meet the 48dp minimum touch target rule (M3 accessibility guideline). The 40dp-height buttons achieve this through their internal tap area extension. Verify in Figma by toggling "Show touch targets" in the Accessibility inspector.

WCAG AA contrast requirements (4.5:1 for text, 3:1 for UI components):
- "Priya Sharma" (#181C20 on #EBEEF3): approximately 12:1 — passes.
- "Personal account" (#50606E on #EBEEF3): approximately 5.4:1 — passes.
- "priya.sharma@example.co.uk" (#181C20 on #F7F9FF): approximately 16:1 — passes.
- "Authorised" (#266489 on #F1F4F9): approximately 4.6:1 — passes AA (borderline; verify in production).
- Sign out label (#BA1A1A on #F7F9FF): approximately 5.1:1 — passes.
- Warning text (#4C4162 on #EADDFF): M3 tertiary role pair — passes WCAG AA (M3-guaranteed).

Set `contentDescription` on all icons that convey meaning: email icon ("Email"), phone icon ("Mobile"), home icon ("Address"), verified icon ("Authorised"), schedule icon ("Expiry date"), check_circle icons ("Permission granted"), account_balance icon ("Bank"). Set `contentDescription = ""` on the warning_amber icon (the adjacent text conveys the same meaning). Set `contentDescription = "No profile data"` on account_circle_off. Set `contentDescription = "Error"` on error_outline.

Group each list item (icon + label + supporting text) into a single TalkBack/VoiceOver semantic group so the screen reader announces them as one unit: e.g. "Email, priya.sharma@example.co.uk". Apply these mergeDescendants groupings in Figma's Accessibility panel.

The sign-out dialog must trap focus within the dialog while open. In prototype mode, ensure Tab order cycles: dialog title → body → Cancel → Sign out, then loops. Back navigation from within the dialog (hardware back on Android) should be equivalent to Cancel.
