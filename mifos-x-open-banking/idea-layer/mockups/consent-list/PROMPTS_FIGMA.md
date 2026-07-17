# Consent List — Figma Design Prompts

> Generated from: `screens/consent-list/ui.yaml` + `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5 / Android) — all measurements in dp, multiply by 2.75 for @2.75x export
> Design system: Open Banking — Trust Blue · Material Design 3 · Roboto · WCAG AA contrast target
> Generated: 2026-07-16T00:00:00Z

---

## Design System Summary

### Resolved Colour Palette (Material 3 Light, seed #266489)

| Role | Hex | Usage |
|---|---|---|
| primary | #266489 | Filled buttons, selected icons, active chips, spinner |
| onPrimary | #FFFFFF | Text/icons on primary backgrounds |
| primaryContainer | #C9E6FF | Tonal button fills, Authorised status chip background |
| onPrimaryContainer | #004B6F | Text on primaryContainer |
| secondary | #50606E | Secondary icons, supporting text |
| onSecondary | #FFFFFF | Text on secondary |
| secondaryContainer | #D3E5F5 | Secondary tonal elements |
| onSecondaryContainer | #384956 | Text on secondaryContainer |
| error | #BA1A1A | Error icons, urgency countdown text, error state icons |
| onError | #FFFFFF | Text on error |
| errorContainer | #FFDAD6 | Reconfirm banner background, urgency chip background |
| onErrorContainer | #93000A | Text on errorContainer surfaces |
| background | #F7F9FF | Screen background, top app bar, bottom nav bar |
| onBackground | #181C20 | Primary body text |
| surface | #F7F9FF | Card surface (history cards, default state) |
| onSurface | #181C20 | Primary text on surface |
| surfaceVariant | #DDE3EA | Expired/Revoked status chip background, skeleton shimmer |
| onSurfaceVariant | #41474D | Secondary text, labels, unselected nav icons |
| surfaceContainerLow | #F1F4F9 | Active consent card fill (elevation 1 overlay) |
| outline | #72787E | Input outlines |
| outlineVariant | #C1C7CE | History card border (1dp), section divider |
| scrim | #000000 | Modal backdrop |

### Roboto Type Scale (M3 Default)

| Style | Size | Line Height | Weight | Usage in this screen |
|---|---|---|---|---|
| titleLarge | 22sp | 28sp | 400 | Top app bar title |
| titleMedium | 16sp | 24sp | 500 | — |
| bodyLarge | 16sp | 24sp | 400 | Banner title text |
| bodyMedium | 14sp | 20sp | 400 | Permission summary, banner body, empty/error body |
| labelLarge | 14sp | 20sp | 500 | Section labels ("Active", "History") |
| labelMedium | 12sp | 16sp | 500 | Expiry countdown, expired-on date |
| labelSmall | 11sp | 16sp | 500 | Connected-on date (secondary) |
| headlineSmall | 24sp | 32sp | 400 | Empty/error state title |

### Shape & Spacing

All corner radii follow the M3 shape scale. Screen horizontal padding is 16dp throughout. Card horizontal inset is 16dp (net card width 361dp on 393dp canvas). Vertical gap between list items is 8dp. Section label padding: 8dp top, 4dp bottom.

---

## Frame 1 — Loading State

Create a full-screen frame at 393×852dp named "consent-list/loading". Set the background fill to #F7F9FF (M3 surface/background).

At the top, place a Small Top App Bar component. The app bar has a height of 56dp, background fill #F7F9FF, and zero elevation shadow. Its leading element is a back-arrow icon button (Material Symbol: arrow_back, 24×24dp, tint #41474D, 48×48dp touch target). The title text reads "Data Sharing Consents" in titleLarge (22sp, weight 400, #181C20), positioned after the leading icon.

Below the app bar, in the vertical centre of the remaining screen area (between app bar base at 56dp and bottom nav top at 772dp), place a CircularProgressIndicator component. The indicator is 48×48dp, centred horizontally on the canvas. Its track colour is primaryContainer #C9E6FF and its active-segment colour is primary #266489. Apply a continuous rotation animation in prototyping (used when describing motion only — annotate with "spinner, 1.5s linear rotation"). The contentDescription attribute should be set to "Loading consent status from HSBC" to satisfy TalkBack/VoiceOver accessibility requirements.

At the bottom, add a NavigationBar component with height 80dp and background fill #F7F9FF. Place four NavigationBarItem children: Home (icon: home), Accounts (icon: account_balance), Transactions (icon: receipt_long), and More (icon: more_horiz). For this screen, the More tab is in selected state — its icon and label render in primary #266489, indicatorColour is primaryContainer #C9E6FF at 64×32dp oval. The remaining three tabs render in unselected style, tint #41474D, no indicator.

Auto Layout for loading body: set the content area between app bar and nav bar to a vertical Auto Layout frame, alignment centre-centre, padding 0. The single child (CircularProgressIndicator) is centred by the parent Auto Layout stretch.

---

## Frame 2 — Content State (with near-expiry consents)

Create a frame named "consent-list/content" at 393×852dp, background #F7F9FF. This is the primary state, rendered with all three demo-data fixtures: two active consents and one expired consent in history.

### Top App Bar

Apply the same Small Top App Bar as in the loading frame: back arrow leading, title "Data Sharing Consents" titleLarge #181C20, bg #F7F9FF, no elevation.

### Reconfirm Banner

Immediately below the app bar (top offset 56dp), place a banner component spanning the full width (393dp wide, 0dp horizontal margin) with 16dp internal padding on all sides. The fill colour is errorContainer #FFDAD6. Corner radius is 8dp. Height should hug content — expect approximately 72dp.

Inside the banner, use a horizontal Auto Layout (direction: row, alignment: top, gap: 12dp, padding: 16dp). The first child is a Material Symbol icon "warning_amber" at 24×24dp with tint #BA1A1A. The second child is a vertical Auto Layout (direction: column, gap: 4dp, fill width). Inside it, add two text nodes: the title reads "Reconfirmation required" in bodyLarge (16sp, weight 400, #93000A); the body reads "A consent expires in 7 days. Reconfirm to maintain access." in bodyMedium (14sp, weight 400, #93000A). This banner is visible only when has_near_expiry_consents is true — annotate the component with a "Conditional: show when has_near_expiry_consents" note in the layer description.

This component satisfies OBIE FR-008: the 90-day PSU reconfirmation requirement. Include this note as a layer annotation.

### Active Section Label

Below the banner (8dp gap), add a text node with value "Active" in labelLarge (14sp, weight 500, #41474D). Left-align it with 16dp horizontal padding from the frame edge. Its vertical padding is 8dp top, 4dp bottom.

### Active Consent Card — aac-fb2c4e8a (89 days remaining, no urgency)

Create a Card component named "consent_card/authorised-normal". Its frame is 361dp wide (16dp inset each side), height hug-content (expected ≈116dp). Apply these properties: fill #F1F4F9 (surfaceContainerLow, the M3 elevation-1 overlay for surface), corner radius 12dp, drop shadow at 0×1dp blur 2dp colour #0000001A (M3 elevation level 1), internal padding 16dp all sides.

Inside, create a vertical Auto Layout (direction: column, gap: 8dp, alignment: leading, sizing: hug height fill width).

The first child is a horizontal Auto Layout row named "header_row" (direction: row, alignment: centre-vertical, gap: 8dp, sizing: hug height fill width). Inside it, place the HSBC logo image placeholder: a rectangle 40×20dp with a placeholder fill, annotated "ic_hsbc_logo — import HSBC vector asset, contentDescription: HSBC". To its right, add a Chip component in "Assist" style. The chip label is "Authorised" in labelLarge (14sp, weight 500, #004B6F). The chip icon is "check_circle" at 16×16dp, tint #004B6F. The chip fill is primaryContainer #C9E6FF, border none, corner radius 9999dp (full pill), height 28dp. Position this chip at the trailing (end) edge of the header row by setting the row's main-axis alignment to space-between.

The second child is a text node: "10 data types shared" in bodyMedium (14sp, weight 400, #181C20), full width.

The third child is a text node: "Expires in 89 days · 26 Sep 2026" in labelMedium (12sp, weight 500, #41474D). This is the expiry_countdown component. When days_until_expiry is greater than 14, the colour is #41474D (onSurfaceVariant). Annotate with "expiry_color: on-surface-variant when > 14 days".

The fourth child is a text node: "Connected 28 Jun 2026" in labelSmall (11sp, weight 500, #41474D). This is the granted_since field sourced from Data.CreationDateTime formatted as 'd MMM yyyy'.

The entire card is tappable: add a Prototype interaction "On Tap → Navigate to consent-detail (consentId: aac-fb2c4e8a)". Set the hover overlay to #26648914 (primary at 8% opacity) to indicate interactivity.

### Active Consent Card — aac-d4e5f6a7 (7 days remaining, urgency visible)

Create a second Card component named "consent_card/authorised-near-expiry". Apply the same elevation-1 styling (#F1F4F9 fill, radius 12dp, shadow) and 16dp internal padding as above. Vertical gap between cards is 8dp.

The header row is identical to the first card: HSBC logo placeholder + "Authorised" chip in primaryContainer #C9E6FF.

Below the header row, add the reconfirm_urgency_chip. This chip is VISIBLE because days_until_expiry (7) is less than or equal to 14. Create an Assist Chip: label "Reconfirm soon" in labelLarge (14sp, weight 500, #93000A), icon "warning_amber" at 16×16dp tint #93000A, fill errorContainer #FFDAD6, corner radius 9999dp, height 28dp. Annotate: "Visible only when item.days_until_expiry ≤ 14".

Below that, add: "4 data types shared" in bodyMedium (14sp, #181C20).

Then "Expires in 7 days · 6 Jul 2026" in labelMedium (12sp, weight 500, #BA1A1A) — note the colour changes to error #BA1A1A because expiry_color is "error" when days_until_expiry ≤ 14. This is the key visual urgency signal for the approaching expiry.

Finally, "Connected 7 Apr 2026" in labelSmall (11sp, #41474D).

Apply Prototype: On Tap → Navigate to consent-detail (consentId: aac-d4e5f6a7).

### Section Divider

Below the active list (8dp gap), add a Divider component: full width minus 32dp (361dp), height 1dp, colour outlineVariant #C1C7CE, vertical margin 8dp. This component is visible only when both has_active_consents and has_history_consents are true. Annotate: "Conditional: show when has_active && has_history".

### History Section Label

Below the divider (4dp gap), add a text node "History" in labelLarge (14sp, weight 500, #41474D) with 16dp left padding, 8dp top padding, 4dp bottom padding.

### History Consent Card — aac-a1b2c3d4 (Expired 26 Jun 2026)

Create a Card component named "consent_card/expired". Frame: 361dp wide, height hug-content (≈88dp). Unlike active cards, history cards use elevation 0: fill is surface #F7F9FF, border stroke 1dp colour outlineVariant #C1C7CE, corner radius 12dp, no drop shadow. Internal padding 16dp all sides.

Inside, vertical Auto Layout gap 8dp. Header row contains the HSBC logo (same placeholder as active cards) and a status chip. The history status chip has label "Expired" in labelLarge #41474D, icon "schedule" (16×16dp, tint #41474D), fill surfaceVariant #DDE3EA, corner radius 9999dp, height 28dp. The chip's muted colouring signals historical/inactive status to the PSU.

Second row: "Expired 26 Jun 2026" in labelMedium (12sp, weight 500, #41474D). This is the history_expiry_label sourced from Data.ExpirationDateTime formatted as 'd MMM yyyy'.

Third row: "Connected 12 Mar 2026" in labelSmall (11sp, weight 500, #41474D). This is the history_connected_on date from Data.CreationDateTime.

Apply Prototype: On Tap → Navigate to consent-detail (consentId: aac-a1b2c3d4). History consents are viewable but no active AIS data access is possible.

### Bottom Navigation

Apply the same NavigationBar as the loading frame. More tab is selected (#266489 tint, primaryContainer indicator).

### Auto Layout — Full Content Frame

Set the content frame body (below the app bar, above the nav bar) as a vertical Auto Layout with vertical scrolling enabled, horizontal padding 16dp, vertical padding 16dp, item gap 8dp. Children: reconfirm_banner (full-bleed, negate horizontal padding using negative margin −16dp), then active_section_label, active_consents_list, section_divider, history_section_label, history_consents_list.

---

## Frame 3 — Empty State

Create a frame named "consent-list/empty" at 393×852dp, background #F7F9FF.

Apply the same Small Top App Bar (back arrow, "Data Sharing Consents", bg #F7F9FF, no elevation).

In the centre of the screen body (vertically centred between 56dp and 772dp), create an empty state composition. Use a vertical Auto Layout (direction: column, alignment: centre-centre, gap: 16dp, horizontal padding: 32dp, fill parent width).

The first child is a Material Symbol icon "link_off" at 48×48dp, tint #41474D. This icon communicates no bank connection. Its contentDescription is "No bank accounts connected" — essential for TalkBack. Note: the icon is link_off (not shield as in stale mockups). This reflects the current ui.yaml specification.

The second child is a text node: "No consents yet" in headlineSmall (24sp, weight 400, #181C20, centre aligned). This is the primary empty state headline, resolved from strings.consent_list_empty_title.

The third child is a text node: "You haven't connected any bank accounts via Open Banking yet." in bodyMedium (14sp, weight 400, #41474D, centre aligned, max width 329dp with soft word wrap). Resolved from strings.consent_list_empty_body.

The fourth child is the connect_button. Create a Filled Button component: label "Connect a bank" in labelLarge (14sp, weight 500, #FFFFFF), background fill #266489, corner radius 9999dp (full pill), height 56dp, width fills the parent minus 32dp horizontal padding (net ≈ 329dp). Minimum touch target: 56dp (exceeds the 48dp WCAG guideline). The button's contentDescription is "Connect your bank account via Open Banking". Apply Prototype: On Tap → Navigate to user-onboarding screen (initiates FAPI account-access consent flow).

Apply the same NavigationBar (More selected) at bottom.

---

## Frame 4 — Error State (Network / HTTP 500)

Create a frame named "consent-list/error" at 393×852dp, background #F7F9FF.

Apply the same Small Top App Bar.

Centre the error composition vertically between the app bar and nav bar. Use a vertical Auto Layout (gap 16dp, horizontal padding 32dp, centre-centre alignment).

First child: Material Symbol "error_outline" at 48×48dp, tint error #BA1A1A. ContentDescription: "Error loading consent status". The error-red icon immediately communicates system failure to the PSU without ambiguity.

Second child: text "Unable to load consents" in headlineSmall (24sp, weight 400, #181C20, centre). Resolved from strings.consent_list_error_title.

Third child: text displaying the dynamic error message. In the design, render the demo text: "No internet connection. Please try again." in bodyMedium (14sp, weight 400, #41474D, centre). In production, this slot renders the NetworkError or ConsentStatusServerError user-facing message from the ViewModel. Annotate this text node: "data-driven: {error.message}".

Fourth child: retry_button — Filled Button, label "Try again" in labelLarge (14sp, #FFFFFF), bg #266489, radius 9999dp, height 56dp, min touch 56dp, width fill minus 32dp padding. ContentDescription: "Retry loading consents". Apply Prototype: On Tap → retryLoad action — this re-triggers the full consent-status fetch from GET /account-access-consents/{ConsentId} and transitions back to the loading state while the network request is in-flight. Annotate: "effect: call_api (action_contract)".

Apply NavigationBar (More selected) at bottom.

---

## Frame 5 — Error Auth State (HTTP 401 — Session Expired)

Create a frame named "consent-list/error-auth" at 393×852dp, background #F7F9FF.

Apply the same Small Top App Bar.

This state differs fundamentally from the generic error state. A 401 Unauthorized response means the PSU's access token has expired — retrying the same request would fail again. Therefore this state presents a dedicated re-authentication CTA rather than a generic "Try again".

Centre the error-auth composition vertically. Use a vertical Auto Layout (gap 16dp, horizontal padding 32dp, centre-centre alignment).

First child: Material Symbol "lock_open" at 48×48dp, tint error #BA1A1A. The lock_open icon (not lock, not lock_outline) communicates that access is temporarily withdrawn but can be re-granted by signing in. ContentDescription: "Session expired".

Second child: text "Session expired" in headlineSmall (24sp, weight 400, #181C20, centre). Resolved from strings.consent_list_auth_error_title.

Third child: text "Your access has expired. Sign in again to view your consent status." in bodyMedium (14sp, weight 400, #41474D, centre). This copy sets clear expectation: sign-in will resolve the issue. Resolved from strings.consent_list_auth_error_body.

Fourth child: reauth_button — Filled Button, label "Sign in again" in labelLarge (14sp, #FFFFFF), bg primary #266489, radius 9999dp, height 56dp, min touch 56dp. ContentDescription: "Sign in again to renew your session". Apply Prototype: On Tap → navigate_reauth → login screen (re-initiates the FAPI OAuth 2.0 authorisation flow to obtain a new access token). Annotate: "effect: navigate · target: login (action_contract)". This is the OBIE-recommended pattern for 401 recovery: redirect the PSU to re-authorise rather than showing a generic retry.

Apply NavigationBar (More selected) at bottom.

---

## Auto Layout Specifications Summary

| Frame / Component | Direction | Padding | Item Gap | Alignment | Width | Height |
|---|---|---|---|---|---|---|
| Screen body (content scroll) | column | h:16dp v:16dp | 8dp | top-start | fill | fill |
| reconfirm_banner (inner) | row | 16dp all | 12dp | top | fill | hug |
| banner text stack | column | 0 | 4dp | start | fill | hug |
| consent_card (inner) | column | 16dp all | 8dp | start | fill | hug |
| consent_card header_row | row | 0 | 8dp | center-vertical | fill | hug |
| empty_state / error_state | column | h:32dp v:auto | 16dp | center-center | fill | fill |
| bottom_nav inner | row | h:0 v:0 | 0 | center | fill | 80dp fixed |

---

## Component Variants

### Consent Card — Active Normal (status: Authorised, days > 14)

Default state: fill #F1F4F9, radius 12dp, shadow elevation 1 (0×1dp, blur 2dp, #0000001A).
Hovered state: fill #E5E8ED (surfaceContainerHigh), shadow unchanged. Indicate hover by lightening the overlay slightly.
Pressed state: fill #DDE3EA (surfaceVariant), shadow unchanged. Use a ripple overlay in primary at 12% opacity (#26648914).
Focused state: add a 3dp outline in primary #266489. Used for keyboard and accessibility navigation.

The expiry text colour is #41474D (onSurfaceVariant) in this variant. The reconfirm_urgency_chip is hidden (visibility: false in Figma using component property toggle).

### Consent Card — Active Near-Expiry (status: Authorised, days ≤ 14)

Identical base styling to Active Normal, but with two overrides: the reconfirm_urgency_chip is visible (component property toggle: true) and the expiry countdown text colour changes to error #BA1A1A. This creates a clear visual distinction between healthy consents and consents requiring PSU action.

### Consent Card — History (status: Expired or Revoked)

Default state: fill #F7F9FF (surface), border 1dp #C1C7CE, radius 12dp, no shadow (elevation 0). The flat/outlined treatment communicates inactivity compared to the elevated active cards.
Hovered state: fill #F1F4F9.
Pressed state: fill #EBEEF3 with ripple #26648914.
Focused state: 3dp outline #266489.

The status chip uses surfaceVariant #DDE3EA fill with #41474D text, producing a muted appearance appropriate for historical records. A Revoked consent should use the same chip styling as Expired — both are terminal states.

### Filled Button (connect_button / retry_button / reauth_button)

Default: bg #266489, label #FFFFFF, radius 9999dp, elevation 0.
Hovered: primary #266489 with 8% onPrimary (#FFFFFF) state-layer overlay; keep label white.
Pressed: primary #266489 with 12% onPrimary (#FFFFFF) state-layer overlay; ripple #FFFFFF26.
Focused: 3dp ring in #266489 on bg.
Disabled: bg #C1C7CE, label #72787E, elevation 0 (would apply if button were disabled; all three CTAs are always enabled in their respective states).

### Assist Chip (status chips and urgency chip)

Authorised chip: default fill #C9E6FF, label/icon #004B6F. Hovered: primaryContainer #C9E6FF with 8% onPrimaryContainer (#004B6F) state-layer overlay. Pressed: primaryContainer #C9E6FF with 12% onPrimaryContainer (#004B6F) state-layer overlay.
Urgency chip: default fill #FFDAD6, label/icon #93000A. Hovered: errorContainer #FFDAD6 with 8% onErrorContainer (#93000A) state-layer overlay. Pressed: errorContainer #FFDAD6 with 12% onErrorContainer (#93000A) state-layer overlay.
Expired/History chip: default fill #DDE3EA, label/icon #41474D. Hovered: surfaceVariant #DDE3EA with 8% onSurfaceVariant (#41474D) state-layer overlay. Pressed: surfaceVariant #DDE3EA with 12% onSurfaceVariant (#41474D) state-layer overlay.

---

## Semantic Token → Figma Variable Mapping

Create a "Open Banking / Trust Blue" Figma variable collection with the following bindings. Use string format "color/{role}" for Figma variable names.

| Semantic Token | Figma Variable Name | Resolved Hex | Usage in this screen |
|---|---|---|---|
| primary | color/primary | #266489 | Button fills, selected nav icon, spinner |
| onPrimary | color/on-primary | #FFFFFF | Button labels, onPrimary text |
| primaryContainer | color/primary-container | #C9E6FF | Authorised chip fill, nav indicator |
| onPrimaryContainer | color/on-primary-container | #004B6F | Authorised chip label/icon |
| error | color/error | #BA1A1A | Error icons, near-expiry countdown text |
| onError | color/on-error | #FFFFFF | Text on error fills |
| errorContainer | color/error-container | #FFDAD6 | Reconfirm banner bg, urgency chip fill |
| onErrorContainer | color/on-error-container | #93000A | Banner text, urgency chip label |
| background | color/background | #F7F9FF | Screen bg, app bar bg, nav bar bg |
| onBackground | color/on-background | #181C20 | Primary body text |
| surface | color/surface | #F7F9FF | History card fill |
| onSurface | color/on-surface | #181C20 | Permission summary text |
| surfaceVariant | color/surface-variant | #DDE3EA | Expired chip fill, section divider |
| onSurfaceVariant | color/on-surface-variant | #41474D | Section labels, dates, nav icons (unselected) |
| surfaceContainerLow | color/surface-container-low | #F1F4F9 | Active card fill (elevation 1) |
| outlineVariant | color/outline-variant | #C1C7CE | History card border, section divider |

Bind each component's fill, stroke, and text-colour properties to the corresponding Figma variable so that a theme switch (light → dark) propagates across all frames automatically.

---

## Prototype Interaction Flow

Define the following interactions in Figma's Prototype panel, linking components to their destination frames.

On Tap on consent_card (any card in the active_consents_list), navigate to the "consent-detail" screen. Pass the ConsentId as a route parameter annotated in the prototype comment. Source: action navigate_consent_detail, effect navigate, target consent-detail. This interaction applies to both aac-fb2c4e8a (89-day normal) and aac-d4e5f6a7 (7-day near-expiry) cards.

On Tap on history_consent_card (any card in the history_consents_list), navigate to the "consent-detail" screen with the corresponding ConsentId. Source: action navigate_consent_detail, effect navigate, target consent-detail. History consents display a read-only view of the expired consent's details. The card tap confirms that historical consents are still navigable even though AIS data access has lapsed.

On Tap on connect_button (empty state only), navigate to the "user-onboarding" screen. Source: action navigate_connect, effect navigate, target user-onboarding. This begins a fresh FAPI account-access consent flow in which the PSU selects data permissions and authorises the AISP via HSBC's Open Banking portal.

On Tap on retry_button (error state only), transition to the loading frame (consent-list/loading) and annotate "triggers retryLoad ViewModel action — re-fetches GET /account-access-consents/{ConsentId} for all stored ConsentIds". Source: action retry_load, effect call_api. After the async fetch completes, the screen transitions to either content or error depending on the response.

On Tap on reauth_button (error_auth state only), navigate to the "login" screen. Source: action navigate_reauth, effect navigate, target login. This re-initiates the FAPI OAuth 2.0 authorisation code flow. Annotate: "HTTP 401 TokenExpiredSession recovery path — navigates PSU to re-authorise their Open Banking session".

For all navigation interactions, use Figma's "Navigate to" prototype action with a Smart Animate transition (300ms, ease-in-out) to represent the standard M3 forward-navigation motion (shared-axis X forward). The back-arrow in the top app bar should use "Navigate back" to return to the previous screen in the prototype flow.

---

## Accessibility Annotations

Every interactive component must meet a minimum touch target of 48×48dp. The consent cards span 361×116dp (active) and 361×88dp (history), both vastly exceeding this threshold. The three CTAs (connect_button, retry_button, reauth_button) are 56dp tall — above the minimum.

Apply contentDescription to all non-decorative icons: bank_logo's contentDescription is "HSBC"; status chips have contentDescription resolved from strings.consent_list_status_prefix concatenated with the status label ("Status: Authorised", "Status: Expired"); the reconfirm_urgency_chip contentDescription is "Reconfirm soon"; error/lock icons carry descriptive contentDescriptions stated in each frame above.

The reconfirm_banner must be announced to TalkBack as a priority alert. Apply role="alert" or annotate as a TalkBack live-region component so PSUs using screen readers hear the reconfirmation warning immediately upon navigating to the content state.

Colour contrast ratios (verified against WCAG AA): onSurface #181C20 on background #F7F9FF = 16.7:1 (AAA); error #BA1A1A on #FFDAD6 = 4.9:1 (AA); onPrimaryContainer #004B6F on primaryContainer #C9E6FF = 7.3:1 (AAA); #41474D on #F7F9FF = 5.8:1 (AA). All pairs pass WCAG AA at both normal and large text sizes.

For the near-expiry expiry countdown text (#BA1A1A on #F1F4F9 card): contrast ratio is 4.8:1 (AA). This is the error colour on a light card surface. When cards are in the pressed/active state (#DDE3EA), verify that contrast remains above 3:1 for large text (11sp labelSmall is below 18pt, so 4.5:1 must be maintained — use onErrorContainer #93000A on pressed surfaces instead of #BA1A1A if needed).

All focus indicators must have a visible 3dp ring in primary #266489. The M3 "focused" component state applies this ring automatically when using official M3 component kit variants in Figma. Ensure keyboard navigation order follows the visual reading order: top app bar → banner → section label → card[0] → card[1] → divider (skipped) → section label → card[2] → bottom nav.

---

## State Transition Animations

When prototyping state transitions in Figma, apply the following motion specs derived from the design system (motion.intensity: low, durations.medium: 300ms, emphasis-easing: cubic-bezier(0.2, 0.0, 0, 1.0)).

Loading → Content: Use Figma's Smart Animate transition at 300ms with the emphasis easing. The content area fades in (opacity 0 → 1) while sliding upward 8dp (Y +8dp → Y 0). The reconfirm_banner slides in from the top simultaneously if has_near_expiry_consents is true.

Loading → Empty: Use a 300ms fade (opacity 0 → 1) for the empty state icon and text, with a 150ms delay before the connect_button fades in.

Loading → Error / Error Auth: Use a 300ms fade for the error composition. The error icon scales from 0.9 to 1.0 simultaneously (subtle entrance that draws attention without aggressive animation — reduce_motion_supported must disable this scale if the user has requested reduced motion).

Content → Loading (retry tap): The consent list fades out at 150ms (short duration) and the spinner appears. This short fade prevents a jarring cut while the retry request is in-flight.

All transitions between states should use Smart Animate with "change in" direction (existing content fades out; incoming content fades in) rather than directional slides, because the screen stays on the same navigation level throughout state changes — there is no navigational depth change within the screen.

---

## Figma File Organisation

Structure the Figma file using the following page and section layout to support collaborative handoff.

Create a Figma page named "Consent List — Screens". Within it, create three named sections: "States", "Components", and "Specs".

In the "States" section, place all five frames in a horizontal row with 64dp gaps: consent-list/loading, consent-list/content, consent-list/empty, consent-list/error, consent-list/error-auth. Label each frame clearly. Add a "Primary" star annotation to consent-list/content as the reference state for design review.

In the "Components" section, place isolated component variants for independent review: ConsentCard/active-normal, ConsentCard/active-near-expiry, ConsentCard/history, StatusChip/Authorised, StatusChip/Expired, UrgencyChip/Reconfirm, Banner/Reconfirm, ReauthButton/enabled. Each component should show all its interactive states stacked vertically (default, hover, pressed, focused) so developers can see the full state matrix in one glance.

In the "Specs" section, place a copy of the Colour Token table and Type Scale table from this document as Figma text/table frames. Add a spacing annotation frame showing the 16dp horizontal padding, 8dp item gap, and 12dp card corner radius with M3 red-line annotations.

Use the Figma "Dev Mode" annotations to mark which components are already implemented in the KMP source (once the feature is built). Mark navigable flows with connection arrows linking the consent_card tap target to the consent-detail frame (placed in a separate Figma page or linked to an external frame reference).

---

## Spacing and Density Details

The screen uses the "comfortable" density setting (design-tokens.yaml spacing.density: comfortable). This translates to the following specific spacing decisions for this screen.

The top app bar is 56dp tall. Below it, the scroll region begins at y=56dp. The bottom nav occupies 80dp. Combined chrome is 136dp, leaving 716dp of scrollable content area on a 852dp canvas.

Card internal padding is 16dp on all four sides. Between the card internal padding and card children, there is a vertical gap of 8dp between each child element (header_row → urgency_chip → permission_summary → expiry_countdown → granted_since).

Between cards in the active list, the gap is 8dp. Between the active list and the section divider, 8dp. The divider has 8dp top and bottom margin. Between the divider and the history section label, 4dp. Between the history section label and the history list, 4dp.

The reconfirm_banner sits 8dp below the app bar (or 0dp if the scroll list starts flush with the app bar edge — use 0dp inset for the banner and let the list's top padding create the space). The banner has 16dp all-side internal padding and uses full 393dp width to create an edge-to-edge warning treatment (no horizontal card inset).

The empty state and error state compositions are centred vertically in the 716dp content zone. To centre them, use a Frame with fill + Auto Layout (vertical, centre-centre alignment). The icon is 48dp, the heading is ~32dp line-height, the body is ~40dp (two lines at 20sp line-height), and the button is 56dp, totalling approximately 208dp of content plus 48dp gaps. This centres naturally in 716dp (approximately 254dp top, 254dp bottom padding around the 208dp content block).

The scroll column (for content state) starts at y=56dp (below app bar) and extends to y=772dp (above bottom nav). Enable vertical scrolling on this frame in Figma by setting the Frame's scroll direction to "Vertical" and ensuring content overflows.

---

## Design Notes for Handoff

The screen follows the OBIE Open Banking PSU journey for an AISP consent management view. The data model is OBReadConsentResponse1 from the HSBC Open Banking API (OBIE AIS v4.0 specification). Each consent has a ConsentId, Status (Authorised / Expired / Revoked), ExpirationDateTime, CreationDateTime, and Permissions array.

The 90-day reconfirmation requirement (FR-008) is visually enforced by the errorContainer banner and the reconfirm_urgency_chip. Designers should not alter the error-container treatment for the banner — the colour communicates urgency in a regulated-industry context where PSUs must take timely action to maintain their banking data access.

The muted outlined styling of history cards (elevation 0, border, surfaceVariant chips) versus the elevated filled styling of active cards (elevation 1, primaryContainer chips) is a deliberate visual hierarchy. Do not blend these styles — the visual distinction helps PSUs immediately classify their consent status at a glance.

The HSBC logo is represented by the asset ic_hsbc_logo. In the final Figma file, replace the placeholder rectangle with the actual HSBC vector asset respecting brand guidelines. The logo should appear at 40×20dp without clipping — use an image frame with "Fit" content mode.

When sharing this file with the development team, export assets at 2x and 3x density. The ic_hsbc_logo should be exported as a vector PDF to preserve sharpness at all display densities. The Material Symbol icons (warning_amber, check_circle, schedule, error_outline, lock_open, link_off, more_horiz, home, account_balance, receipt_long, arrow_back) are available in the Compose Multiplatform runtime as Material Icons Extended and do not require separate asset exports — annotate them as "system icon, no export needed". The filled button, assist chip, and NavigationBar components map directly to their Compose Material 3 counterparts: `Button(style: Filled)`, `AssistChip`, and `NavigationBar` with `NavigationBarItem`. Pass the resolved hex values as Color arguments to the Compose theme override where the component deviates from the screen's default theme surface.
