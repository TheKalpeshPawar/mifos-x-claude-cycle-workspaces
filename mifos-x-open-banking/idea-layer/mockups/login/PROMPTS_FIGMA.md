# Login — Figma Design Prompts

> Generated from: `screens/login/ui.yaml` (status: approved, quality: 95)
> Canvas: 393 × 852dp · Pixel 5 · @2x density
> Design system: Open Banking — Trust Blue (Material 3, seed #266489)
> Generated: 2026-07-16T00:00:00Z

These prompts are written as natural-language design instructions for Figma AI, Figma Make, or
a human designer building the "Connect with HSBC" login screen. Each section describes one
screen state as a complete frame, top to bottom. Auto Layout specs, variant states, and
prototype wiring follow the per-state descriptions.

---

## Design System Summary

### Colour Palette (light theme, Material 3 resolved tokens)

The app uses the "Open Banking — Trust Blue" palette derived from a seed of #266489. In Figma,
create a local colour library with the following variables. All are in the `light` mode collection.

Primary surfaces and interactive elements use the Trust Blue family. Background and surface
roles use a very light off-white (#F7F9FF). Text hierarchy relies on `onSurface` (#181C20) for
primary copy and `onSurfaceVariant` (#41474D) for supporting and secondary text. Errors use the
M3 error role (#BA1A1A).

| Role | Token name | Hex |
|---|---|---|
| Primary | `color/primary` | #266489 |
| On Primary | `color/on-primary` | #FFFFFF |
| Primary Container | `color/primary-container` | #C9E6FF |
| On Primary Container | `color/on-primary-container` | #004B6F |
| Secondary | `color/secondary` | #50606E |
| On Secondary | `color/on-secondary` | #FFFFFF |
| Surface | `color/surface` | #F7F9FF |
| On Surface | `color/on-surface` | #181C20 |
| Surface Variant | `color/surface-variant` | #DDE3EA |
| On Surface Variant | `color/on-surface-variant` | #41474D |
| Surface Container Low | `color/surface-container-low` | #F1F4F9 |
| Outline | `color/outline` | #72787E |
| Outline Variant | `color/outline-variant` | #C1C7CE |
| Error | `color/error` | #BA1A1A |
| On Error | `color/on-error` | #FFFFFF |
| Error Container | `color/error-container` | #FFDAD6 |
| Background | `color/background` | #F7F9FF |
| On Background | `color/on-background` | #181C20 |

### Typography Scale (Roboto, Material 3)

All text uses Roboto. Set up the following text styles in Figma. Sizes are in sp (treat as px
in Figma at 1× scale for prototyping; multiply by 2 for @2× export slices).

| Style name | Size | Weight | Line height |
|---|---|---|---|
| `type/display-large` | 57 | 400 | 64 |
| `type/headline-small` | 24 | 400 | 32 |
| `type/title-large` | 22 | 400 | 28 |
| `type/title-medium` | 16 | 500 | 24 |
| `type/title-small` | 14 | 500 | 20 |
| `type/body-large` | 16 | 400 | 24 |
| `type/body-medium` | 14 | 400 | 20 |
| `type/body-small` | 12 | 400 | 16 |
| `type/label-large` | 14 | 500 | 20 |
| `type/label-medium` | 12 | 500 | 16 |
| `type/label-small` | 11 | 500 | 16 |

### Spacing and Shape

Use a 4dp base spacing scale: 4, 8, 12, 16, 24, 32, 48, 64. Screen horizontal padding is 16dp
on both sides. Cards use a corner radius of 12dp (M3 medium). Buttons use 12dp radius. The
minimum touch target for any interactive element is 48dp in both dimensions (WCAG 2.5.5).
Elevation uses M3 tonal surfaces: level 0 = 0dp, level 1 = 1dp shadow (maps to tonal overlay
in light theme).

---

## Semantic Token to Figma Variable Mapping

When the codebase or this document references a role name like `primary` or `on-surface-variant`,
use the corresponding Figma variable from the colour library above. The mapping is one-to-one.

| Code role | Figma variable | Resolved hex |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/on-surface` | #181C20 |
| `surfaceVariant` | `color/surface-variant` | #DDE3EA |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `outlineVariant` | `color/outline-variant` | #C1C7CE |
| `error` | `color/error` | #BA1A1A |
| `errorContainer` | `color/error-container` | #FFDAD6 |
| `onError` | `color/on-error` | #FFFFFF |
| `background` | `color/background` | #F7F9FF |

---

## Frame 1 — State: content (default, primary flow)

Create a frame named `login/content` at 393 × 852px with a background fill of #F7F9FF
(`color/background`). Set the frame to use Auto Layout in the vertical direction, with 0px
padding at the top (the top app bar sits flush), horizontal padding of 0px on the sides
(inner sections define their own 16dp padding), and item spacing of 0px between sections
(sections control their own spacing internally).

### Top App Bar

Place an M3 Small Top App Bar component at the top of the frame. Set its height to 64dp and
its background to #F7F9FF. Insert a back-arrow navigation icon (arrow_back, 24dp) on the
leading side. Set the title text to "Connect with HSBC" using the `type/title-medium` text
style (16sp, weight 500, #181C20). There are no trailing action icons on this screen. The
component should fill the full 393dp width.

### HSBC Explainer Card

Below the top app bar, add 16dp of vertical spacing and then place a Card component with 16dp
of horizontal margin on each side (resulting in a 361dp wide card). Apply the M3 Elevated Card
variant with elevation level 1. Set the corner radius to 12dp on all corners. Fill the card
with #F1F4F9 (`color/surface-container-low`).

Inside the card, use a vertical Auto Layout with 12dp item spacing and 16dp padding on all
four sides. Add the following children in order:

First, place the HSBC logo image. Use a 48dp tall image component centred horizontally. The
asset is `ic_hsbc_logo` — this is the HSBC wordmark or brand mark. Add a content description
attribute "HSBC logo" for accessibility.

Second, create a small inline row (horizontal Auto Layout, 4dp item spacing, hug-hug sizing)
for the regulated badge. Place a verified_user icon at 16dp by 16dp, filled with #266489
(`color/primary`). Next to it, add a text label using `type/label-small` (11sp, weight 500,
#266489). The label reads "Regulated UK Open Banking connection". This badge visually confirms
the FCA-authorised TPP status to the end user.

Third, add the explainer headline as a text layer using `type/title-medium` (16sp, weight 500,
#181C20) with the value "Connect with HSBC". Set the width to fill the card container (fill
container), and text wrapping to wrap.

Fourth, add the explainer body text using `type/body-small` (12sp, weight 400, #41474D). The
text reads: "You'll be redirected to HSBC to approve permissions and select accounts. Your
credentials are never shared with this app." Set width to fill container with wrap enabled.

Fifth, place a horizontal Divider component spanning the full card width. Set its colour to
#C1C7CE (`color/outline-variant`) and its thickness to 1dp. This visually separates the
PSU-facing copy from the technical security notice below.

Sixth, create another inline row (horizontal Auto Layout, 4dp item spacing) for the security
notice. Place a lock_outline icon at 16dp by 16dp, filled with #41474D
(`color/on-surface-variant`). Add body text using `type/label-small` (11sp, weight 500,
#41474D): "Secured with FAPI 1.0 Advanced, mTLS, and PS256-signed tokens." Set the text to
fill container width with wrap enabled.

### Permissions Section Header

Below the card (with 20dp of vertical spacing after the card), add a section header text layer
using `type/label-large` (14sp, weight 500, #181C20). The label reads "Permissions requested".
Apply 16dp of horizontal padding (matching screen padding) so the text aligns with the card
edges.

### Permissions List

Immediately below the header (8dp spacing), render a vertical list of 10 permission rows, each
64dp tall (min height — content may cause slight height increase). Each row follows the M3
List Item One-Line + Supporting Text pattern.

Each row consists of a leading icon (check_circle_outline, 24dp, filled with #266489), a
headline text using `type/body-medium` (14sp, 400, #181C20), and a supporting text line using
`type/body-small` (12sp, 400, #41474D). Apply 16dp horizontal padding to each row. Use a
vertical Auto Layout with 2dp item spacing between headline and supporting text.

The ten rows, in order, are:
Row 1 — "Account details" / "Account identifiers, sort code, account number, nickname"
Row 2 — "Balances" / "Current and available balances for each account"
Row 3 — "Transaction history" / "Debits and credits with merchant, amount, and date"
Row 4 — "Beneficiaries" / "Saved payees on your account"
Row 5 — "Standing orders" / "Scheduled recurring payment instructions"
Row 6 — "Direct debits" / "Active direct debit mandates and their status"
Row 7 — "Scheduled payments" / "One-off future-dated payment instructions"
Row 8 — "Statements" / "Monthly statement metadata and PDF references"
Row 9 — "Product information" / "Interest rates and product features attached to your accounts"
Row 10 — "Account holder name" / "Full legal name registered on the account"

Note that this list will extend the frame height in a real screen — the permissions_list
component is scrollable (LazyColumn) in the implementation. For the Figma static frame, show
all 10 rows inline; the prototype can clip the frame to the canvas bounds.

### Consent Validity and Expiry

After the permissions list (16dp of vertical spacing), add two text layers with 16dp horizontal
padding.

The first line uses `type/body-small` (12sp, 400, #41474D): "Your consent is valid for 90
days and covers transactions from 30 Mar 2026."

Immediately below (4dp spacing), add a second text layer using `type/label-medium` (12sp,
weight 500, #266489): "Expires 26 Sep 2026". This is the ViewModel-computed expiry date derived
from ExpirationDateTime 2026-09-26T00:00:00Z in the OBReadConsent1 payload.

### Primary Call to Action

After the expiry line (24dp of vertical spacing), add a Filled Button component. Set its width
to fill the container minus 32dp of horizontal margin (16dp each side). Set its height to 48dp
and corner radius to 12dp. The button background is #266489 (`color/primary`). The label text
reads "Continue to HSBC" in `type/label-large` (14sp, weight 500, #FFFFFF). Add a trailing
icon (open_in_new, 18dp, #FFFFFF) to signal that this action opens an external app. Add a
content description "Continue to HSBC — opens HSBC app or website".

### Secondary Call to Action

Below the primary button (8dp of vertical spacing), add a Text Button component of the same
width. Set its height to 48dp with no background. The label reads "Cancel" in
`type/label-large` (14sp, weight 500, #181C20, `color/on-surface`). No icon. Add a content
description "Cancel — return to previous screen". Centre the label horizontally.

---

## Frame 2 — State: loading

Create a frame named `login/loading` at 393 × 852px, background #F7F9FF. Use a vertical Auto
Layout. The top app bar is identical to the content frame — same title, back arrow, and
#F7F9FF background.

Directly below the top app bar, place a LinearProgressIndicator component spanning the full
393dp width. Set its height to 4dp. Set its colour to #266489 (`color/primary`). The indicator
is indeterminate — it animates continuously left to right to convey that a network request is
in progress. Do not clip this indicator to horizontal padding; it should be edge to edge.

Below the progress indicator, add 64dp of vertical space and then centre a text label using
`type/body-medium` (14sp, 400, #41474D): "Preparing your secure connection…". Centre the text
horizontally and horizontally pad it to 32dp from each edge. This message reassures the user
that the consent-create POST to HSBC's account-access-consents API is in flight and that no
action is required.

The rest of the frame is empty background. The loading state is transient — it appears
between the user tapping "Continue to HSBC" and the FAPI redirect launching.

---

## Frame 3 — State: authorising

Create a frame named `login/authorising` at 393 × 852px, background #F7F9FF. Use a vertical
Auto Layout. The top app bar is identical to the content frame.

Below the top app bar, add 96dp of vertical spacing to create a centre-of-screen focal area.
Then place a CircularProgressIndicator component centred horizontally. Set its diameter to
48dp and its colour to #266489 (`color/primary`). The indicator should be the indeterminate
spinning variant. Add a content description "Waiting for HSBC authorisation" for screen
readers.

Below the spinner (16dp spacing), add a text layer centred horizontally using `type/body-medium`
(14sp, 400, #41474D): "Waiting for HSBC authorisation…". Pad the text 32dp from each horizontal
edge.

Below that (8dp spacing), add a second text layer centred horizontally using `type/body-small`
(12sp, 400, #41474D): "Complete sign-in in the HSBC app or website, then return here." Pad
the text 32dp from each horizontal edge.

This state appears once the app has successfully POSTed the OBReadConsent1 payload, received
the ConsentId, constructed the PS256-signed FAPI /authorize URL, and launched the app-to-app
redirect to HSBC. The user is now authenticating inside HSBC's mobile app or web portal, and
this screen holds until the deep-link callback (consent-callback screen) is triggered.

---

## Frame 4 — State: error

Create a frame named `login/error` at 393 × 852px, background #F7F9FF. The top app bar is
identical to the content frame.

Below the top app bar, add 96dp of vertical spacing. Then place an error_outline Material icon
centred horizontally. Set the icon size to 48dp. Tint the icon with #BA1A1A (`color/error`).

Below the icon (16dp spacing), add a headline text layer centred horizontally using
`type/headline-small` (24sp, 400, #181C20): "Could not connect to HSBC". Pad to 24dp from
each horizontal edge.

Below the headline (8dp spacing), add a body text layer centred horizontally using
`type/body-medium` (14sp, 400, #41474D). The copy in this layer is dynamic — it is sourced
from the ViewModel and maps to one of five error messages:

For a network failure: "Unable to reach HSBC. Check your connection and try again."
For HTTP 400 (bad consent payload): "HSBC rejected the consent request. Please try again."
For HTTP 401 (authorisation): "Authorisation failed. The app may need to re-register with HSBC."
For HTTP 500 (server error): "HSBC is temporarily unavailable. Try again in a moment."
For a FAPI redirect failure: "Could not open HSBC. Ensure the HSBC Mobile Banking app is installed, or try again."

In the Figma frame, show the NetworkException variant ("Unable to reach HSBC…") as the
representative body copy. Create component variants for each of the five error body texts.

Below the body text (24dp spacing), add a Filled Button identical in dimensions and styling
to the primary CTA in the content frame (#266489, 48dp tall, 12dp radius, fill width minus
32dp). The label reads "Try again" in `type/label-large` (14sp, weight 500, #FFFFFF). No icon.
Add a content description "Try again — retry connecting to HSBC".

---

## Frame 5 — State: empty

Create a frame named `login/empty` at 393 × 852px, background #F7F9FF. The top app bar is
identical to the content frame.

Below the top app bar, add 96dp of vertical spacing. Then place a manage_search Material icon
centred horizontally. Set the icon size to 48dp. Tint the icon with #41474D
(`color/on-surface-variant`). This neutral icon conveys "nothing to show" without alarming
the user, since this state is a pre-flight guard rather than a user-triggered error.

Below the icon (16dp spacing), add a headline text layer centred horizontally using
`type/headline-small` (24sp, 400, #181C20): "No permissions configured". Pad to 24dp from
each horizontal edge.

Below the headline (8dp spacing), add a body text layer centred horizontally using
`type/body-medium` (14sp, 400, #41474D): "No Open Banking read scopes are available to
request." This state fires when the ViewModel resolves an empty requested_permissions list,
which would result in a zero-scope OBReadConsent1 that HSBC's AIS API would reject with an
HTTP 400 error.

Below the body (24dp spacing), add a Filled Button identical to the primary CTA in the
content frame. The label reads "Go back" in `type/label-large` (14sp, weight 500, #FFFFFF).
Add a content description "Go back — return to previous screen". On tap, this navigates to the
user-onboarding screen.

---

## Auto Layout Specifications

The following Auto Layout rules govern the main content areas of each frame.

For the root frame container, use vertical direction, no padding, clip content on, fixed width
393dp, hug height for prototyping, fill height for fixed-canvas export.

For the top app bar component, use horizontal direction, 16dp left and right padding, height
fixed at 64dp, fill width, align children to centre-vertical. Leading icon and title text are
spaced with 4dp item spacing. The title uses fill-width text; the leading icon uses hug sizing.

For the hsbc_explainer_card container, use vertical direction, 16dp padding all sides, 12dp
item spacing. Width: fill container with 16dp left and right outer margins. Height: hug content.
Corner radius 12dp. The card_divider inside the card uses fill-width, fixed 1dp height, and
is placed between explainer_body and security_notice.

For each permission_row, use horizontal direction, 16dp left padding, 12dp right padding,
12dp top and bottom padding, 12dp item spacing. The leading icon is fixed 24dp × 24dp. The
text column on the right uses vertical direction, 2dp item spacing, fill-remaining width. The
headline text and supporting text both use fill-width with wrap enabled.

For the primary button (continue_hsbc_button, retry_button, login_empty_back_button), use
horizontal direction, centred alignment, fixed height 48dp, fill-width minus 32dp outer margin.
Label text uses hug-width inside the button. The trailing icon (open_in_new) is fixed 18dp.

For loading and authorising states, the content area below the app bar uses a vertical
direction container with fill height and centred vertical alignment, enabling the spinner or
progress indicator to optically sit in the upper third of the visible area.

---

## Component Variants

### continue_hsbc_button variants

Create a Figma component for the primary CTA button with the following named variants. Each
variant changes only the fill colour or content opacity; layout and size remain fixed.

Default (resting): background #266489, label #FFFFFF, icon #FFFFFF, opacity 100%.
Hovered: background #266489 (primary) with a #FFFFFF (onPrimary) state-layer overlay at 8% opacity, label #FFFFFF, icon #FFFFFF.
Pressed: background #266489 (primary) with a #FFFFFF (onPrimary) state-layer overlay at 12% opacity, scale animation 0.97.
Disabled: background #C1C7CE (outlineVariant), label #72787E (outline), icon #72787E, opacity 38%.
Focused: resting fill plus a 2dp ring in #266489 with 2dp gap from button edge.

### cancel_button / TextButton variants

Default: label #181C20 (on-surface), no background fill.
Hovered: label #181C20, background #266489 at 8% opacity (hover state layer).
Pressed: background #266489 at 12% opacity.
Disabled: label #72787E at 38% opacity.
Focused: label #181C20 plus a 2dp focus ring in #266489.

### permission_row variants

Default: no background, icon check_circle_outline #266489.
Selected (for future use): background primaryContainer #C9E6FF at 12% opacity.

### ob_regulated_badge variants

Default: icon verified_user #266489, text #266489.

### error_state body text variants

Create five component variants of the body text layer labelled:
`error/network`, `error/http-400`, `error/http-401`, `error/http-500`, `error/fapi-redirect`.
Each variant swaps only the text content as documented in Frame 4 above.

---

## Prototype Interaction Flow

Wire the following prototype connections in Figma using the Prototype panel.

From `login/content`, tap on `continue_hsbc_button`: animate with Smart Animate (spring,
damping 20, stiffness 300, mass 1) to `login/loading`. This represents the user initiating
the consent-create POST. In a real device, this transitions to the `loading` state in the
ViewModel (uiState = Loading).

From `login/loading`, after a simulated 1.5s delay: animate to `login/authorising`. This
represents the completed consent POST and the FAPI redirect launching to HSBC. Use a Dissolve
transition over 300ms.

From `login/authorising`, add a note that the return path is handled by the OS deep-link
callback (consent-callback screen) and is not a direct Figma connection — the user completes
authentication in the HSBC app, which then returns via the registered redirect URI.

From `login/content`, tap on `cancel_button`: animate with Slide Left (300ms, ease-in-out)
to the `user-onboarding` frame. This navigates back without staging any consent data.

From `login/error`, tap on `retry_button`: animate identically to the `continue_hsbc_button`
transition — Smart Animate to `login/loading`.

From `login/empty`, tap on `login_empty_back_button`: animate with Slide Left (300ms,
ease-in-out) to `user-onboarding`.

From the back arrow in the top app bar on all frames: animate with Slide Left (300ms,
ease-in-out) to the `user-onboarding` frame. This mirrors the NavigateBack ViewModel action.

---

## Accessibility Notes

Every interactive component must meet WCAG 2.1 AA contrast requirements. The primary
colour #266489 on white (#FFFFFF) achieves a contrast ratio of approximately 4.6:1, meeting
AA for normal text. The error colour #BA1A1A on white achieves approximately 5.9:1. The
on-surface-variant colour #41474D on surface #F7F9FF achieves approximately 9.8:1 (AAA).

All tap targets must be at least 48 × 48dp. This is achieved by the button height (48dp),
the minimum list item height (56dp), the back arrow tap area (48dp), and the badge row
(explicitly padded to 48dp vertical reach in implementation).

Icon-only buttons (the back arrow) must carry a content description for screen readers. The
back arrow should read "Navigate back". The app bar itself should be announced to
TalkBack/VoiceOver as a navigation landmark.

The permissions list is a live region in the loading-to-content transition: once the list
populates, VoiceOver/TalkBack should announce "10 permissions loaded". In Figma, annotate
this region with an ARIA-live polite annotation on the permissions_list frame.

The loading_indicator and authorising_spinner are both annotated as aria-live assertive so
that the state change is announced immediately to users who cannot see the visual transition.
In Figma, add a tooltip annotation layer on each progress component: "Loading — screen readers
will announce this state change".

The consent_expiry_display value ("Expires 26 Sep 2026") should be announced by screen readers
in full. Annotate it with a content description: "Consent expires 26 September 2026". Avoid
abbreviations in the announced string.

The HSBC logo image carries a content description ("HSBC logo") but is not a focusable element
— mark it as decorative-role=image with a non-empty alt in Figma's accessibility panel, so it
is announced once during focus traversal and then excluded from subsequent reads.

For the ob_regulated_badge, the verified_user icon is decorative (the text label conveys the
full meaning). Mark the icon with role=none in Figma accessibility annotations. The text label
"Regulated UK Open Banking connection" is sufficient for screen reader output.

Ensure sufficient motion-reduced variants: the LinearProgressIndicator, CircularProgressIndicator,
and any shimmer loaders should honour the OS "Reduce Motion" flag. In Figma, create a
`prefers-reduced-motion` variant page or use comment annotations to indicate which components
need a static fallback (e.g., a determinate progress bar at 30% fill as a stand-in for the
indeterminate animation).
