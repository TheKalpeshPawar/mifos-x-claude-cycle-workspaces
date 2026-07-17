# Consent Callback — Figma Design Prompts

> Generated from `screens/consent-callback/ui.yaml` and `design-tokens.yaml`
> Canvas: 393×852dp (Pixel 5) · No top app bar · No bottom nav · No FAB · Full-screen modal
> Design system: Open Banking — Trust Blue · seed #266489 · Material 3 · Roboto

---

## Design System Summary

### Colour Palette (M3 Light — resolved hex)

**Primary (Trust Blue)**

The primary colour, #266489, conveys financial trust and open-banking authority. Use it for all interactive
elements — filled button backgrounds, progress spinners, outlined button strokes and labels, and the success
check icon. Do not use it for error states; reserve it for actions and confirmations.

- Primary: #266489
- On Primary: #FFFFFF (labels on filled primary surfaces)
- Primary Container: #C9E6FF (pale blue highlight; selected chips)
- On Primary Container: #004B6F (dark navy; text on pale-blue containers)

**Secondary (Slate)**

- Secondary: #50606E
- On Secondary: #FFFFFF
- Secondary Container: #D3E5F5
- On Secondary Container: #384956

**Surface and Background**

All screens in this application share the same surface colour, which reads as a warm off-white with a
slight blue cast — matching the Trust Blue brand without overwhelming it.

- Surface / Background: #F7F9FF (surfaceBright — use this as the fill for every screen frame)
- On Surface: #181C20 (near-black — headings, titles, primary text)
- On Surface Variant: #41474D (dark grey — body copy, secondary text, neutral icons)
- Surface Variant: #DDE3EA (light grey-blue — dividers, skeleton shimmers)
- Surface Container: #EBEEF3
- Surface Container High: #E5E8ED

**Error**

- Error: #BA1A1A (accessible red; meets WCAG AA 5.1:1 on #F7F9FF for UI components)
- On Error: #FFFFFF
- Error Container: #FFDAD6 (pale rose for error panel backgrounds)
- On Error Container: #93000A

**Outline**

- Outline: #72787E (mid-grey; borders for outlined buttons and input fields)
- Outline Variant: #C1C7CE (lighter stroke for card borders and dividers)

---

### Typography (Roboto — M3 Default)

Set up a shared Text Styles library in Figma with the following styles:

| Figma Style Name | Font | Size | Weight | Line Height | Use |
|---|---|---|---|---|---|
| Headline/Small | Roboto | 24 | Regular (400) | 32 | Screen headings in empty/error states |
| Title/Medium | Roboto | 16 | Medium (500) | 24 | Loading headline |
| Body/Large | Roboto | 16 | Regular (400) | 24 | Long-form body text |
| Body/Medium | Roboto | 14 | Regular (400) | 20 | Supporting body copy, state messages |
| Body/Small | Roboto | 12 | Regular (400) | 16 | Loading sub-copy, captions |
| Label/Large | Roboto | 14 | Medium (500) | 20 | Button labels |

---

### Semantic Token → Figma Variable Mapping

Create a Figma Variable Collection named **Open Banking — Trust Blue**. Group variables as shown below.
Bind all component instances to these variables rather than hardcoded hex values to support future
dark-mode and high-contrast theme switching.

**Colour variables (Light mode values listed)**

| Semantic Token | Figma Variable Path | Light Value |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/onPrimary` | #FFFFFF |
| `primaryContainer` | `color/primaryContainer` | #C9E6FF |
| `onPrimaryContainer` | `color/onPrimaryContainer` | #004B6F |
| `secondary` | `color/secondary` | #50606E |
| `onSecondary` | `color/onSecondary` | #FFFFFF |
| `error` | `color/error` | #BA1A1A |
| `onError` | `color/onError` | #FFFFFF |
| `errorContainer` | `color/errorContainer` | #FFDAD6 |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/onSurface` | #181C20 |
| `onSurfaceVariant` | `color/onSurfaceVariant` | #41474D |
| `surfaceVariant` | `color/surfaceVariant` | #DDE3EA |
| `outline` | `color/outline` | #72787E |
| `outlineVariant` | `color/outlineVariant` | #C1C7CE |

**Typography variables**

| Token | Figma Variable Path | Value |
|---|---|---|
| `headlineSmall` | `typography/headline-small` | Roboto 24/32 Regular |
| `titleMedium` | `typography/title-medium` | Roboto 16/24 Medium |
| `bodyMedium` | `typography/body-medium` | Roboto 14/20 Regular |
| `bodySmall` | `typography/body-small` | Roboto 12/16 Regular |
| `labelLarge` | `typography/label-large` | Roboto 14/20 Medium |

**Spacing variables**

| Token | Figma Variable Path | Value |
|---|---|---|
| `spacing.sm` | `spacing/sm` | 8 |
| `spacing.lg` | `spacing/lg` | 24 |
| `spacing.xl` | `spacing/xl` | 48 |
| `spacing.screen-padding` | `spacing/screen-padding` | 16 |

---

## Per-State Design Prompts

### Frame: loading

Create a mobile frame at 393 by 852 points. Name the frame **Callback / Loading**. Set the fill to
`color/surface` (#F7F9FF). Ensure no top app bar, navigation bar, or FAB placeholder is present inside
this frame — the screen intentionally occupies the full display area without any shell chrome.

Inside the frame, create an Auto Layout frame named `loading_layout`. Set the layout direction to
Vertical. Set both primary-axis and cross-axis alignment to Center. Apply 48 points of padding on all
four sides (top, right, bottom, left) — this represents `spacing.xl`. Set the frame to Fill Container on
both axes so it fully occupies the parent 393×852 frame. Set Item Spacing to 0 — spacing between
elements is handled by explicit Spacer frames rather than Auto Layout gaps.

Place a **Circular Progress Indicator** inside `loading_layout`. Create this as a circle of 48×48 points.
Apply a 4-point stroke in `color/primary` (#266489). Use the Arc tool to simulate an indeterminate spinner
by trimming the path to 270 degrees (start 0°, end 270°). Name the layer `loading_spinner`. Annotate with
a content description note: "Verifying HSBC authorisation". In a production Figma file you would link this
to a pre-built CircularProgressIndicator component from your M3 component library; here, the arc
representation communicates the intent accurately enough for handoff.

Add a Spacer frame of 48 height by Fill width. Name it `spacer_xl`. This represents `spacing.xl` between
the spinner and the headline.

Add a Text layer named `loading_headline`. Set the text to "Verifying your authorisation…". Apply the
`typography/title-medium` text style (Roboto 16/24 Medium). Bind the text fill to `color/onSurface`
(#181C20). Set text alignment to Center. Set the width to Fill so it spans the 297-point content area
(393 minus 48 padding on each side). Ensure the font renders without ligature substitution on the ellipsis
character — use the Unicode horizontal ellipsis (U+2026) rather than three separate dots.

Add a Spacer frame of 8 height by Fill width. Name it `spacer_sm`. This represents `spacing.sm`.

Add a Text layer named `loading_body`. Set the text to "Securely exchanging credentials with HSBC. This
takes a few seconds." Apply `typography/body-small` (Roboto 12/16 Regular). Fill: `color/onSurfaceVariant`
(#41474D). Text alignment: Center. Constrain the max width to 280 points and center it within the 297-point
column. Use Auto Layout text wrapping (Hug width, Fixed width 280) so the copy wraps gracefully across two
lines without becoming a single long string.

**Auto Layout summary for loading_layout**

Direction: Vertical. Primary-axis alignment: Center. Cross-axis alignment: Center. Padding: 48 top / 48
right / 48 bottom / 48 left. Item spacing: 0 (explicit spacers). Width: Fill Container. Height: Fill
Container.

This frame contains no interactive elements. It is a display-only state. No prototype interactions are
attached directly to this frame — transitions into and out of it are driven programmatically by the
ViewModel.

---

### Frame: content

Duplicate the `loading_layout` frame. Rename the duplicate container to `success_layout` and name the
outer frame **Callback / Content**. Remove `loading_spinner`, `spacer_xl`, `loading_headline`, `spacer_sm`,
and `loading_body` from the duplicate. The container padding and Auto Layout settings (Vertical,
Center/Center, 48dp all sides, Fill both axes) remain unchanged.

Place a **Success Icon** component inside `success_layout`. Use the Material Symbols `check_circle` glyph
in Filled style (Weight 400, Grade 0, Optical Size 48). Size the icon at 64×64 points — larger than the
48dp used for error/awaiting icons to reinforce the positive, resolved outcome. Set the icon fill to
`color/primary` (#266489). Name the layer `success_icon`. Annotate: contentDescription "HSBC authorisation
successful". The filled check_circle renders as a solid blue circle with a white checkmark inside, which
is visually distinct from all the 48dp error-family icons on other states.

Add a Spacer of 24 height by Fill width, named `spacer_lg`. This represents `spacing.lg` — a slightly
smaller gap than the loading state's xl gap, keeping the success layout slightly more compact.

Add a Text layer named `success_headline`. Text: "Connected to HSBC". Style: `typography/headline-small`
(Roboto 24/32 Regular). Fill: `color/onSurface` (#181C20). Alignment: Center. Width: Fill.

Add a Spacer of 8 height by Fill width, named `spacer_sm`.

Add a Text layer named `success_body`. Text: "Your account data is ready. Taking you to your accounts
now." Style: `typography/body-medium` (Roboto 14/20 Regular). Fill: `color/onSurfaceVariant` (#41474D).
Max width: 280 points. Alignment: Center.

**Auto Layout summary for success_layout**

Direction: Vertical. Primary-axis alignment: Center. Cross-axis alignment: Center. Padding: 48 all sides.
Item spacing: 0. Width: Fill Container. Height: Fill Container.

**Prototype interaction**: On the `success_layout` frame, add an After Delay interaction set to 1500
milliseconds, navigating to the **Accounts** destination frame. Use the M3 Forward Shared Axis transition
— Slide Right direction, duration 450ms, easing cubic-bezier(0.2, 0.0, 0, 1.0) (M3 Emphasised Decelerate).
This matches the `Long 450ms` motion token used in the Kotlin implementation. When reduced motion is active
(honour the system `prefers-reduced-motion` flag), navigate immediately without the slide animation.

---

### Frame: empty

This frame represents the AwaitingAuthorisation scenario: the PSU has authorised at the HSBC portal, the
app has successfully exchanged the auth code for a PSU bearer token, but the GET
/account-access-consents/{ConsentId} poll returned `Status: AwaitingAuthorisation` — HSBC has not yet
updated the consent record. The PSU is presented with a manual re-poll option.

Create a frame at 393×852 named **Callback / Empty** with background `color/surface` (#F7F9FF). No shell
chrome. Create an Auto Layout container named `awaiting_state` with Vertical direction, Center/Center
alignment, 48 points of padding on all sides, Fill Container on both axes, Item Spacing 0.

Place a 48×48 icon using the Material Symbols `hourglass_empty` glyph (Filled, Weight 400). Set the fill
to `color/onSurfaceVariant` (#41474D). This colour choice is deliberate: the PSU is waiting, not
experiencing a failure. Using the error red (#BA1A1A) here would alarm the user unnecessarily. The neutral
grey-blue icon communicates "patience required" rather than "something went wrong". Name the layer
`awaiting_icon`.

Add a Spacer of 16 height by Fill width.

Add a Text layer named `awaiting_title`. Text: "Waiting for HSBC to confirm". Style:
`typography/headline-small` (Roboto 24/32 Regular). Fill: `color/onSurface` (#181C20). Alignment: Center.
Width: Fill.

Add a Spacer of 8 height by Fill width.

Add a Text layer named `awaiting_body`. Text: "HSBC has not yet updated the consent status. Please wait a
moment or try again." Style: `typography/body-medium` (Roboto 14/20 Regular). Fill:
`color/onSurfaceVariant` (#41474D). Max width: 280 points. Alignment: Center. The copy is factual and
empathetic — it explains the situation without technical jargon (no mention of APIs or status codes).

Add a Spacer of 24 height by Fill width.

Create a **Filled Button** component named `poll_again_button`. Set the width to Fill Container, which
resolves to 297 points within the 48dp padding on each side. Set the height to 48 points — the M3 minimum
touch target and the standard ButtonDefaults height. Set corner radius to 12dp (M3 `ShapeKeyTokens.Corner
Large`). Set the background fill to `color/primary` (#266489). Add a Text child layer with text "Check
again", style `typography/label-large` (Roboto 14/20 Medium), fill `color/onPrimary` (#FFFFFF). Align the
label to the centre of the button both horizontally and vertically. Add 24dp horizontal padding inside the
button between the label and the button edges (M3 filled button content padding).

**Auto Layout summary for awaiting_state**

Direction: Vertical. Primary-axis alignment: Center. Cross-axis alignment: Center. Padding: 48 all sides.
Item spacing: 0. Width: Fill Container. Height: Fill Container.

**Prototype interaction on poll_again_button**: On Tap → Navigate to the `loading` frame. Use a Push Right
slide transition at 150ms Short easing (cubic-bezier(0.2, 0.0, 0, 1.0) decelerate). This represents the
ViewModel calling `pollConsentStatus()`, which transitions back to the Loading state while the new API
request is in flight.

---

### Frame: error

This frame represents a hard-stop failure: the HSBC /oauth2/token endpoint returned HTTP 400 or 401
(invalid or expired auth code, or private_key_jwt client authentication failure), the consent poll returned
`Status: Rejected` or `Status: Revoked`, or a network error prevented the exchange from completing. The PSU
must restart the consent flow.

Create a frame at 393×852 named **Callback / Error** with background `color/surface` (#F7F9FF). No shell
chrome. Container `error_state`: Vertical Auto Layout, Center/Center, 48dp padding, Fill Container.

Place a 48×48 icon using Material Symbols `cancel` (Filled, Weight 400). Fill: `color/error` (#BA1A1A).
Name: `error_icon`. The `cancel` glyph (circle with X) communicates a definitive stop. Use the error red
to immediately signal that something requires user action. Do not use the `error_outline` or `report` glyphs
here — `cancel` is the clearest signal of a completed-but-failed outcome.

Add a Spacer of 16 height by Fill width.

Add a Text layer named `error_title`. Text: "Authorisation was declined". Style:
`typography/headline-small` (Roboto 24/32 Regular). Fill: `color/onSurface` (#181C20). Alignment: Center.

Add a Spacer of 8 height by Fill width.

Add a Text layer named `error_body`. Text: "HSBC reported that the consent was not approved. Please try
connecting again or contact HSBC if you believe this is an error." Style: `typography/body-medium`
(Roboto 14/20 Regular). Fill: `color/onSurfaceVariant` (#41474D). Max width: 280 points. Alignment:
Center. The copy includes the contact-HSBC clause for rejection cases where the PSU did not actively decline
but believes the rejection was an error.

Add a Spacer of 24 height by Fill width.

Create a **Filled Button** named `retry_button`. Width: Fill Container (297dp). Height: 48dp. Corner
radius: 12dp. Background: `color/primary` (#266489). Label: "Try again". Label style:
`typography/label-large`, fill `color/onPrimary` (#FFFFFF).

**Auto Layout summary for error_state**: same as awaiting_state above (Vertical, Center, 48dp, Fill).

**Prototype interaction on retry_button**: On Tap → Navigate to the `login` screen destination. Transition:
Push Left slide (navigating backwards), 300ms M3 Medium easing (cubic-bezier(0.2, 0.0, 0, 1.0)). This
represents `navigate_retry()`: LocalStorage.clearOAuthState(), LocalStorage.clearConsentId(), then
Navigator.navigate(Route.Login).

---

### Frame: access_denied

This frame is shown when the HSBC redirect URI carries `error=access_denied`. The PSU actively chose not
to grant the app access to their HSBC account data at the bank's authorisation portal. Crucially, no token
exchange was attempted — this is not a technical failure, it is an intentional user decision. The design
tone must reflect this distinction: informative and non-alarming, with a lower-urgency CTA.

Create a frame at 393×852 named **Callback / Access Denied** with background `color/surface` (#F7F9FF).
No shell chrome. Container `access_denied_state`: Vertical Auto Layout, Center/Center, 48dp padding, Fill.

Place a 48×48 icon using Material Symbols `block` (Filled, Weight 400). Fill: `color/error` (#BA1A1A).
Name: `access_denied_icon`. The `block` glyph communicates that access was refused, but the error red is
the only element in this frame that signals a problem — the copy and CTA style deliberately step back from
the high-urgency tone of the `error` state.

Add a Spacer of 16 height.

Add a Text layer named `denied_title`. Text: "Access not shared". Style: `typography/headline-small`
(Roboto 24/32 Regular). Fill: `color/onSurface` (#181C20). Alignment: Center. The headline avoids the
word "denied" or "refused" — "not shared" is empathetic and positions the outcome as a neutral decision
rather than a rejection. This follows Open Banking UX best practices for consent flows.

Add a Spacer of 8 height.

Add a Text layer named `denied_body`. Text: "You chose not to share your HSBC account data. You can start
again at any time." Style: `typography/body-medium` (Roboto 14/20 Regular). Fill:
`color/onSurfaceVariant` (#41474D). Max width: 280 points. Alignment: Center. "You chose" reinforces that
the decision was the PSU's own — the app is not blaming the bank or itself.

Add a Spacer of 24 height.

Create an **Outlined Button** named `denied_cta_button`. Width: Fill Container (297dp). Height: 48dp.
Corner radius: 12dp. Background: transparent. Stroke: 1dp `color/primary` (#266489). Label: "Start over".
Label style: `typography/label-large` (Roboto 14/20 Medium). Label fill: `color/primary` (#266489). The
outlined button variant is intentional: it signals a lower-urgency, voluntary action. The PSU is not forced
to restart — they can close the app instead. Contrast this with the filled buttons on the `error` and
`security_error` states, which imply a required action.

**Auto Layout summary for access_denied_state**: same as error_state (Vertical, Center, 48dp, Fill).

**Prototype interaction on denied_cta_button**: On Tap → Navigate to the `login` screen. Transition: Push
Left, 300ms Medium easing. Represents `navigate_retry()`: clears OAuth state + ConsentId, then navigates.

**Design rationale note**: The three error-family states (`error`, `access_denied`, `security_error`) all
share the same layout structure but differ in icon choice, copy tone, and CTA button variant. This
three-level hierarchy — filled button (error, security) / outlined button (access_denied) — communicates
urgency accurately: security violations and technical failures require immediate action, while a voluntary
declination is a recoverable situation the PSU can return to on their own terms.

---

### Frame: security_error

This frame is shown when a FAPI-1.0-Advanced security check fails. Specifically, when the `state`
parameter in the HSBC redirect does not match the `oauth_state` value stored locally before the
redirect, or when the hybrid-flow `id_token` nonce does not match the stored nonce. This gate is a
defence against CSRF attacks and token replay. No token exchange is attempted. All local authentication
state — including any partially stored tokens — must be revoked before the user re-authenticates.

Create a frame at 393×852 named **Callback / Security Error** with background `color/surface` (#F7F9FF).
No shell chrome. Container `security_error_state`: Vertical Auto Layout, Center/Center, 48dp padding, Fill.

Place a 48×48 icon using Material Symbols `security` (Filled, Weight 400). Fill: `color/error` (#BA1A1A).
Name: `security_icon`. The `security` glyph (a shield) is the correct choice for this state rather than
`cancel` or `block` — it communicates that a security check was triggered, which is more specific and
informative. A PSU who sees a shield icon understands something about their connection's integrity is being
protected, even if they do not understand the underlying FAPI mechanism. Use the error red to signal that
action is required, consistent with the other error-family states.

Add a Spacer of 16 height.

Add a Text layer named `security_error_title`. Text: "Security check failed". Style:
`typography/headline-small` (Roboto 24/32 Regular). Fill: `color/onSurface` (#181C20). Alignment: Center.
The headline uses plain language. It does not mention CSRF, nonce mismatch, or state parameters — these
technical terms would confuse the PSU without helping them resolve the situation.

Add a Spacer of 8 height.

Add a Text layer named `security_error_body`. Text: "The authorisation response could not be verified.
Please start the connection process again." Style: `typography/body-medium` (Roboto 14/20 Regular). Fill:
`color/onSurfaceVariant` (#41474D). Max width: 280 points. Alignment: Center. The body copy is deliberately
brief. Over-explaining a security failure could give a malicious actor information about the detection
mechanism. The PSU receives exactly enough information to know they need to restart.

Add a Spacer of 24 height.

Create a **Filled Button** named `security_retry_button`. Width: Fill Container (297dp). Height: 48dp.
Corner radius: 12dp. Background: `color/primary` (#266489). Label: "Start again". Label style:
`typography/label-large`, fill `color/onPrimary` (#FFFFFF). Use a filled button here — higher urgency
than the access_denied outlined button — because a security violation requires the PSU to definitively
restart the flow, not optionally consider restarting. The CTA label "Start again" is subtly different from
the error state's "Try again": it implies a clean slate rather than a retry, which matches the underlying
behaviour (TokenStore.revokeAll() + LocalStorage.clearAll()).

**Auto Layout summary for security_error_state**: same as error_state (Vertical, Center, 48dp, Fill).

**Prototype interaction on security_retry_button**: On Tap → Navigate to the `login` screen. Transition:
Push Left, 300ms Medium easing. Represents `navigate_login()`: LocalStorage.clearAll(),
TokenStore.revokeAll(), then Navigator.navigate(Route.Login). This is a stronger teardown than
`navigate_retry()` — appropriate for a potential security incident.

---

## Component Variants

### Button / Filled

Create a Figma Main Component named **Button / Filled**. Define the following property variants:

**Default state**: Background `color/primary` (#266489). Label `color/onPrimary` (#FFFFFF). Corner radius
12dp. Height 48dp. Horizontal content padding 24dp. Vertical content padding 0 (label centred by Auto
Layout). Use `typography/label-large` for the label (Roboto 14/20 Medium). Apply an elevation of 1dp
(shadow: 0 1dp 2dp rgba(0,0,0,0.3), 0 1dp 3dp rgba(0,0,0,0.15)).

**Hovered state**: Add an 8% `color/onPrimary` (#FFFFFF) state-layer overlay on top of the `color/primary` (#266489) container. In Figma, implement this as a white rectangle fill at 8% opacity placed above the primary-filled background — do not introduce a new hex value. Elevation lifts to Level 1 (2dp shadow). Use this variant to represent keyboard focus on desktop and pointer hover on web.

**Pressed state**: Add a 12% `color/onPrimary` overlay (ripple centre). Scale the button to 0.98 using
a Smart Animate transition of 150ms (M3 Short duration). The overlay spreads from the tap point outward.
Reset to Default state after 150ms.

**Focused state**: Identical to Default but with a 3dp focus ring drawn 2dp outside the button edge,
colour `color/primary` (#266489). The ring has a gap of 2dp from the button outline. Use this for
keyboard and switch-access navigation indicators in accessibility testing.

**Disabled state**: Background: `color/onSurface` (#181C20) at 12% opacity over `color/surface` (#F7F9FF) — implement in Figma as a `color/onSurface` fill layer at 12% alpha; do not use a new hex value. Label: `color/onSurface` (#181C20) at 38% opacity — implement as the same token at 38% alpha; do not use a new hex value. Remove elevation shadow. The button should not receive pointer events.

**Component property**: Add a Boolean property `icon-leading` (default: false). When true, add a 18dp icon
slot to the left of the label with 8dp spacing between icon and text, and increase the left content
padding to 16dp.

### Button / Outlined

Create a Main Component **Button / Outlined**. Apply to `denied_cta_button` only.

**Default**: Background transparent. Stroke 1dp `color/outline` (#72787E) — note M3 spec uses outline, not
primary, for the default stroke; however in this application the stroke colour is overridden to
`color/primary` (#266489) to maintain brand consistency and distinguish the outlined button from a disabled
filled button. Label `color/primary` (#266489). Corner radius 12dp. Height 48dp. Horizontal content
padding 24dp. Label style `typography/label-large`.

**Hovered**: Add an 8% `color/primary` (#266489) fill overlay to the background. Stroke stays 1dp.

**Pressed**: 12% `color/primary` overlay (ripple). Stroke stays 1dp. Scale 0.98.

**Focused**: 3dp outer focus ring in `color/primary` offset 2dp from button border. Stroke stays 1dp.

**Disabled**: Stroke `color/onSurface` at 12%. Label `color/onSurface` at 38%. Background transparent.

### CircularProgressIndicator

Create a Main Component **Progress / Circular** for `loading_spinner`.

**Indeterminate (animated)**: Draw a 48×48 Frame containing a circle with a 4dp stroke in
`color/primary` (#266489). Use a Vector arc trimmed from 10° to 280° (270° sweep). Add a Smart Animate
rotation loop: 0° → 360° over 1200ms, linear easing, infinite repeat. Name this the Indeterminate variant.

**Reduced motion**: Static arc, same dimensions and colour, trimmed to exactly 75% (0° to 270°). No
animation. Apply this variant automatically when the prototype or production app detects
`prefers-reduced-motion`.

### Icon / State-Indicator

Create a component set **Icon / State-Indicator** wrapping the five icons used by this screen:

- `success`: check_circle Filled 64dp, fill `color/primary` (#266489)
- `awaiting`: hourglass_empty Filled 48dp, fill `color/onSurfaceVariant` (#41474D)
- `error`: cancel Filled 48dp, fill `color/error` (#BA1A1A)
- `access-denied`: block Filled 48dp, fill `color/error` (#BA1A1A)
- `security`: security Filled 48dp, fill `color/error` (#BA1A1A)

The `success` icon is intentionally larger (64dp vs 48dp) to weight the positive completion state more
strongly in the visual hierarchy.

---

## Prototype Interaction Flow

Wire the following connections in Figma's Prototype panel. All six frames should be connected to form a
complete user journey that covers every valid ViewModel state transition.

**Entry point**: Mark the `loading` frame as the Starting Frame for the Callback flow.

**1. loading → content (success)**
Trigger: After Delay 2000ms (simulates typical token-exchange + consent-poll round-trip time).
Navigate To: `Callback / Content`.
Animation: Dissolve, 300ms, M3 Standard easing cubic-bezier(0.2, 0.0, 0, 1.0).

**2. content → accounts (auto-navigate)**
Trigger: After Delay 1500ms.
Navigate To: Accounts screen frame.
Animation: Slide Left (Forward Shared Axis), 450ms, cubic-bezier(0.2, 0.0, 0, 1.0).
Note: Add a prototype comment: "Reduce-motion: no slide, instant navigate".

**3. loading → empty (AwaitingAuthorisation)**
Add a second interaction to the loading frame via the Overflow menu.
Trigger: On Click on a hotspot labelled "Status: Awaiting" (place invisibly in bottom-right corner for
prototype testing convenience). Navigate To: `Callback / Empty`. Animation: Dissolve 300ms.

**4. loading → error**
Trigger: On Click on a hotspot labelled "Status: Rejected / HTTP 4xx". Navigate To: `Callback / Error`.
Animation: Dissolve 300ms.

**5. loading → access_denied (immediate, no delay)**
Trigger: On Click on a hotspot labelled "error=access_denied redirect". Navigate To:
`Callback / Access Denied`. Animation: Dissolve 150ms.

**6. loading → security_error (immediate, no delay)**
Trigger: On Click on a hotspot labelled "State mismatch". Navigate To: `Callback / Security Error`.
Animation: Dissolve 150ms.

**7. poll_again_button → loading (re-poll)**
Trigger: On Tap.
Navigate To: `Callback / Loading`.
Animation: Push Right, 150ms, Short easing.
Note: represents `pollConsentStatus()` re-entering the loading state.

**8. retry_button → login**
Trigger: On Tap.
Navigate To: Login screen frame.
Animation: Push Left (backward direction), 300ms, M3 Medium easing.
Note: represents `navigate_retry()`.

**9. denied_cta_button → login**
Trigger: On Tap.
Navigate To: Login screen frame.
Animation: Push Left, 300ms, same as above.
Note: represents `navigate_retry()` — same side-effects as error state.

**10. security_retry_button → login**
Trigger: On Tap.
Navigate To: Login screen frame.
Animation: Push Left, 300ms.
Note: represents `navigate_login()` — stronger teardown (revokeAll + clearAll).

---

## Accessibility Annotations

Apply accessibility annotation overlays to each frame before sharing with the development team. Use the
Figma Accessibility Annotation Kit (or equivalent) to document the following.

### loading frame

The `loading_layout` container should be marked as a Semantic Group with the accessibility label
"Authorisation in progress". The `loading_spinner` element carries a standalone content description:
"Verifying HSBC authorisation". The screen reader should announce this on frame entry. The two text layers
(`loading_headline` and `loading_body`) are read in document order — no separate accessibility labels
required. There are no interactive elements on this frame, so touch target size compliance does not apply.

### content frame

The `success_icon` should carry the content description "HSBC authorisation successful". Mark
`success_layout` as a Semantic Group with label "Authorisation complete". No interactive elements. The
frame self-dismisses after 1.5 seconds — annotate this with a note: "Live region — announce once on
render, then auto-navigate. Do not re-announce on subsequent focus events."

### empty frame

Mark `awaiting_state` as a Semantic Group with label "Waiting for HSBC to confirm authorisation". The
`poll_again_button` carries accessibilityLabel: "Check consent status again". Annotate the button with a
touch target marker at 48×48dp — it meets the minimum. The semantic announcement should read: "Check
again, button". Ensure the headline "Waiting for HSBC to confirm" is read before the body text, which
should be read before the button, following document order.

Contrast ratios on #F7F9FF surface:

- #181C20 (headline): 16.5:1 — WCAG AAA
- #41474D (body): 7.0:1 — WCAG AA+
- #266489 (button bg): 4.5:1 for large text — WCAG AA; the button label #FFFFFF on #266489 is 4.5:1 — AA

### error frame

Mark `error_state` as a Semantic Group with label "Authorisation was declined by HSBC". The `retry_button`
carries accessibilityLabel: "Return to login to try connecting again". Announce as: "Try again, button".
Ensure TalkBack / VoiceOver reads the error message components (title, then body) in order before reaching
the button. Add a Live Region annotation to the container so the error is announced when the state renders
even if the user was on a different screen element.

### access_denied frame

Mark `access_denied_state` as a Semantic Group with label "Access to HSBC account data was not shared".
The `denied_cta_button` carries accessibilityLabel: "Start the account connection process again". Announced
as: "Start over, button". Note: This is an Outlined button — ensure the button role is still correctly
announced as "button" regardless of visual style.

### security_error frame

Mark `security_error_state` as a Semantic Group with label "Security verification failed". Set the Live
Region to Assertive so that TalkBack immediately interrupts any ongoing announcement and reads this error
— a security event requires immediate attention. The `security_retry_button` carries accessibilityLabel:
"Start the connection process again from login". Announced as: "Start again, button".

### Global accessibility rules

Every button on this screen — `poll_again_button`, `retry_button`, `denied_cta_button`,
`security_retry_button` — meets the 48×48dp minimum touch target size (WCAG 2.5.5 Target Size, and M3
component defaults). No button falls below this. Annotate each with a touch target bounding box in the
accessibility overlay layer.

All text colours on the #F7F9FF surface achieve WCAG AA contrast ratios as follows: #181C20 reaches
16.5:1 (AAA), #41474D reaches 7.0:1 (AA+), #266489 reaches 4.5:1 (AA for large text, UI components),
#BA1A1A reaches 5.1:1 (AA for UI components). No text falls below the AA threshold.

Annotate each screen with a Reduce Motion note: "When system prefers-reduced-motion is active, replace
`loading_spinner` animated arc with a static 75%-trim arc. Suppress the 1500ms slide animation on
`content → accounts` — navigate immediately. Other state transitions use dissolve (150ms) which are
acceptable under reduced-motion."

The screen provides no back navigation affordance (no top app bar, no navigation rail, no back button).
Annotate this with an implementation note: "Android predictive back / iOS swipe-back gesture should be
disabled on this route or wired to the same login destination to prevent the PSU navigating back to a
partial OAuth callback URL state."
