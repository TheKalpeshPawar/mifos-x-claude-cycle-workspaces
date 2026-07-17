# Consent Detail — Figma Design Prompts

> Auto-generated from `screens/consent-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-17T00:00:00Z

---

## Canvas Specification

Create a Figma page named **"Consent Detail"**. All frames use a 393×852dp (1×) canvas representing Pixel 5 in Material 3 light theme. Set `Clip Content` on every frame. Background fill for the page: #F7F9FF (surface). Roboto is the sole typeface across all text layers.

The persistent shell across all frames:
- **Top app bar** (small M3 variant): 393×56dp, fill #F7F9FF, positioned at y=0. Leading element is a back-arrow icon button (24dp icon, 48×48dp touch target, #181C20 tint). Title text layer: "Connection Detail", Style=TitleLarge (Roboto 22sp/28 400w), fill #181C20. Elevation shadow: level-0 (no shadow on top bar; content scrolls beneath).
- **Bottom navigation bar**: 393×80dp, fill #F7F9FF, positioned at y=772dp (i.e. 852−80). Four tabs left-to-right: Home (home icon), Accounts (account_balance icon), Transactions (receipt_long icon), More (more_horiz icon). Each tab is 98dp wide. Icon size 24dp. Label Style=LabelMedium (Roboto 12sp 500w). "More" tab is selected across all consent-detail frames — selected tint #266489, label #266489; active indicator: 64×32dp rounded rectangle fill #C9E6FF, radius 16dp, centered behind icon. Inactive tab tint #41474D.
- **FAB**: not present on any frame.
- **Scrollable content area**: 393×716dp, y=56dp, clip content. Horizontal padding 16dp (use Auto Layout horizontal padding, not individual spacers).

---

## Design System Summary

### Resolved Colour Palette (light mode)

| Role | Hex | Usage |
|---|---|---|
| `primary` | #266489 | Active tab indicator, primary chip tint, progress indicator, filled button bg, check_circle_outline icon |
| `onPrimary` | #FFFFFF | Text on filled primary buttons |
| `primaryContainer` | #C9E6FF | Status chip bg (Authorised), selected tab indicator |
| `onPrimaryContainer` | #004B6F | Status chip text/icon, filled-tonal button text (reconfirm) — secondary role |
| `secondary` | #50606E | (date/list icon fallback) |
| `secondaryContainer` | #D3E5F5 | `reconfirm_button` FilledTonal background |
| `onSecondaryContainer` | #384956 | `reconfirm_button` label text |
| `error` | #BA1A1A | `revoke_button` border+text (outlined), `dialog_confirm_button` filled bg, error_state icon tint |
| `onError` | #FFFFFF | `dialog_confirm_button` label text |
| `errorContainer` | #FFDAD6 | Error chip/badge background (not primary use here) |
| `onErrorContainer` | #93000A | Error container text |
| `surface` / `background` | #F7F9FF | Page bg, top app bar, bottom nav bg, content area |
| `onSurface` | #181C20 | Primary text (headlines, titles, list headlines) |
| `surfaceVariant` | #DDE3EA | Skeleton shimmer fill, dividers alternative |
| `onSurfaceVariant` | #41474D | Secondary text (supporting text, section labels, unselected icons, body-level labels) |
| `surfaceContainerLow` | #F1F4F9 | `status_header_card` ElevatedCard background |
| `surfaceContainer` | #EBEEF3 | `revoke_confirm_dialog` background |
| `outline` | #72787E | Divider, subtle outlines |
| `outlineVariant` | #C1C7CE | List item 0.5dp dividers |
| `scrim` | #000000 | Dialog backdrop (at 32% opacity) |
| `tertiaryContainer` | #EADDFF | Expiry warning banner bg (conditional variant only — M3 proxy for custom warning-container role) |
| `onTertiaryContainer` | #4C4162 | Expiry warning icon + text (conditional variant only) |

### Typography (Roboto M3 default)

| Role | Size/Line | Weight | Usage in this screen |
|---|---|---|---|
| TitleLarge | 22sp / 28 | 400 | Top app bar title |
| HeadlineMedium | 28sp / 36 | 400 | Empty/error state titles |
| BodyLarge | 16sp / 24 | 400 | List item headline text |
| BodyMedium | 14sp / 20 | 400 | Supporting text, dialog body, revoking label |
| BodySmall | 12sp / 16 | 400 | Expiry warning banner text |
| LabelLarge | 14sp / 20 | 500 | Button labels, section headers |
| LabelSmall | 11sp / 16 | 500 | ConsentId micro-label |

### Spacing Scale

Base unit: 4dp. Screen horizontal padding: 16dp. Common gaps: 8dp, 12dp, 16dp, 24dp. Corner radii: extra_small 4dp, small 8dp, medium 12dp, large 16dp, extra_large 28dp (dialog), full 9999dp (buttons/chips).

---

## Frame 1 — Loading State

Create a frame named **"consent-detail/loading"** at 393×852dp.

The content area (y=56dp to y=772dp) should show a single circular progress indicator centered both horizontally and vertically within the 716dp tall content zone. Use a 48×48dp circular spinner component. Set the track color to #C9E6FF and the active indicator color to #266489. In Figma, represent this as a ring shape (48dp outer, 40dp inner) with a 240° arc in #266489 on a full ring in #C9E6FF. Label the layer `load_progress`. Add a text annotation beside it in the spec panel: "Animating: 1 200ms linear spin, continuous." The spinner should include a contentDescription annotation "Loading consent details" for accessibility handoff.

Apply the top app bar and bottom nav shell as described in the Canvas Specification. No scrim, no overlay.

Auto Layout for the content layer: Vertical direction, fill width 393dp, height 716dp, alignment Center (both axes).

---

## Frame 2 — Content State (Primary)

Create a frame named **"consent-detail/content"** at 393×852dp. This is a scrollable content screen; set `Overflow: Scroll (vertical)` on the content layer. The virtual scroll height will exceed 852dp — this is expected. Clip content should be on.

### Status Header Card

Begin the scrollable content with 16dp top padding. Insert an Elevated Card component named `status_header_card`: width 361dp (fill minus 16dp each side), height 80dp, background #F1F4F9 (surfaceContainerLow), corner radius 16dp on all four corners, drop shadow elevation 2 (3dp blur, y=1dp, color #000000 at 12% opacity). Internal padding: 16dp all sides.

Inside the card, place a horizontal Auto Layout row named `bank_identity_row` filling the card width. Set horizontal arrangement to SpaceBetween, vertical alignment to CenterVertically. On the left, create a rectangle placeholder 48×24dp for the HSBC logo (fill #C9E6FF as a placeholder; replace with `ic_hsbc_logo` vector asset on handoff). Layer name: `bank_logo`. Apply contentDescription annotation: "HSBC logo".

On the right, create an AssistChip named `status_chip`: background fill #C9E6FF, height 32dp, horizontal padding 12dp, gap 8dp between icon and label. The leading icon is `check_circle` 18dp fill #004B6F. The label text reads "Authorised", Style=LabelLarge (14sp 500w), fill #004B6F. Corner radius 100dp (pill shape). This chip changes color based on Data.Status: for AwaitingAuthorisation use `tertiaryContainer` bg #EADDFF / `onTertiaryContainer` icon+text #4C4162; for Rejected/Revoked use `errorContainer` bg #FFDAD6 / `onErrorContainer` text #93000A.

Below the bank_identity_row, place the ConsentId label named `consent_id_label`: text "ID: aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01", Style=LabelSmall (11sp 500w), fill #41474D, marginTop 8dp.

### Expiry Warning Banner (hidden in this primary frame)

Insert a component placeholder named `expiry_warning_banner` with visibility set to Hidden (Figma: layer hidden). It occupies 361dp×56dp with background #EADDFF, radius 12dp, and internal padding 12dp. See Frame 7 for the visible variant. Do not show it in this primary frame.

### Access Period Section

After the status header card, add a 16dp vertical gap. Then insert a text label named `dates_header`: text "ACCESS PERIOD", Style=LabelLarge (14sp 500w), fill #41474D. Padding: top 16dp, bottom 8dp, left 0 (16dp already applied by parent).

Below the header, insert a Column Auto Layout named `dates_list`, fill width 393dp. Add a 0.5dp separator fill #C1C7CE between each row. Create four ListItem rows, each 393×72dp, with horizontal padding 16dp and vertical padding 12dp:

The first row (`created_date_row`): leading icon `event` 24dp fill #41474D (48×48dp touch-safe container), headline "Connected on" LabelLarge 14sp 500w #181C20, supporting text "2026-06-28T18:25:00Z" BodyMedium 14sp #41474D. The supporting text should use Roboto Mono for the ISO-8601 timestamp to aid readability.

The second row (`expiry_date_row`): leading icon `event_busy` 24dp fill #41474D, headline "Expires on", supporting "2026-09-26T00:00:00Z" in Roboto Mono.

The third row (`transaction_from_row`): leading icon `history` 24dp fill #41474D, headline "Transaction history from", supporting "2026-03-30T00:00:00Z" in Roboto Mono.

The fourth row (`transaction_to_row`): leading icon `event_available` 24dp fill #41474D, headline "Transaction history to", supporting "2026-06-28T23:59:59Z" in Roboto Mono.

### Reconfirm Button

After the dates list, add 16dp vertical gap. Insert a Filled Tonal Button named `reconfirm_button`: width fill 361dp (within 16dp horizontal padding), height 40dp, background #D3E5F5 (secondaryContainer), corner radius 100dp. Leading icon `refresh` 18dp fill #384956 (onSecondaryContainer). Label text "Reconfirm access", Style=LabelLarge (14sp 500w), fill #384956. Internal layout: horizontal Auto Layout, verticalAlignment Center, gap 8dp between icon and label, horizontal padding 24dp. Min touch target 48dp tall — expand the invisible tap area by 4dp top and bottom via a transparent bounding layer.

Hover state layer: apply a #384956 fill at 8% opacity over the button background. Pressed state: #384956 at 12%. Disabled: background #181C20 at 12% (#EBEEF3 effective), text #181C20 at 38% opacity.

### Data Shared Section

Add 24dp vertical gap. Insert section header `permissions_header`: text "DATA SHARED", Style=LabelLarge (14sp 500w), fill #41474D, padding top 16dp bottom 8dp.

Below, create a Column Auto Layout named `permissions_list`, fill width 393dp. Add 10 ListItem rows, each named `permission_row[0]` through `permission_row[9]`, each 393×72dp with 16dp horizontal and 12dp vertical padding. Use 0.5dp #C1C7CE separator between rows.

Each permission row has: leading icon `check_circle_outline` 24dp fill #266489 (primary) in a 48×48dp touch-safe container. Headline text (LabelLarge 14sp 500w #181C20) and supporting text (BodyMedium 14sp #41474D) are in a Column Auto Layout, gap 2dp. The ten rows in order:

Row 0: "Account details" / "Account identifiers, sort code, account number, nickname"
Row 1: "Balances" / "Current and available balances for each account"
Row 2: "Transaction history" / "Debits and credits with merchant, amount, and date"
Row 3: "Beneficiaries" / "Saved payees on your account"
Row 4: "Standing orders" / "Scheduled recurring payment instructions"
Row 5: "Direct debits" / "Active direct debit mandates and their status"
Row 6: "Scheduled payments" / "One-off future-dated payment instructions"
Row 7: "Statements" / "Monthly statement metadata and PDF references"
Row 8: "Product information" / "Interest rates and product features attached to your accounts"
Row 9: "Account holder name" / "Full legal name registered on the account"

### Revoke Button

After the permissions list, add 24dp vertical gap. Insert an Outlined Button named `revoke_button`: width fill 361dp, height 40dp, border 1dp stroke #BA1A1A (error), corner radius 100dp, no background fill (transparent). Leading icon `link_off` 18dp fill #BA1A1A. Label text "Revoke access", Style=LabelLarge (14sp 500w), fill #BA1A1A. Horizontal Auto Layout, gap 8dp, horizontal padding 24dp.

Hover state: apply #BA1A1A fill at 8% over the transparent button area. Pressed: #BA1A1A at 12%. Focused: #BA1A1A at 10% with 3dp #BA1A1A focus ring.

End the scrollable content with 24dp bottom padding.

---

## Frame 3 — Revoke Confirm State

Create a frame named **"consent-detail/revoke_confirm"** at 393×852dp.

Start with the same scrolled consent content as Frame 2 (status_header_card, expiry_warning_banner hidden, dates section, permissions section — without the reconfirm or revoke buttons which are state_binding:[content] only). Freeze the content at a mid-scroll position to represent it being behind the dialog. Apply a rectangle overlay named `scrim` at full screen 393×852dp, fill #000000 at 32% opacity, placed above the content layers and below the dialog.

Insert an Alert Dialog component named `revoke_confirm_dialog`, centered horizontally and vertically in the 716dp content zone (x=57dp, y=316dp approximately). Dimensions: 280×auto (~220dp). Background #EBEEF3 (surfaceContainer), corner radius 28dp (extra_large) on all corners. Internal padding: 24dp all sides. Elevation: 6dp shadow (#000000 at 20% blur).

Title layer: text "Revoke HSBC access?", Style=HeadlineSmall (24sp 32 400w), fill #181C20, marginBottom 16dp.

Body layer: text "Removing this connection will stop Mifos from reading your HSBC account data. You can reconnect at any time.", Style=BodyMedium (14sp 20 400w), fill #41474D.

Actions row: horizontal Auto Layout, arrangement=End, gap 8dp, marginTop 24dp. Two buttons:

`dialog_cancel_button`: Text Button, no background, label "Cancel" LabelLarge 14sp 500w fill #266489, height 40dp, corner radius 100dp, horizontal padding 12dp. Hover state: #266489 at 8%.

`dialog_confirm_button`: Filled Button, background #BA1A1A (error), label "Revoke" LabelLarge 14sp 500w fill #FFFFFF (onError), height 40dp, corner radius 100dp, horizontal padding 24dp. Hover: apply #FFFFFF at 8% over the #BA1A1A fill. Pressed: #FFFFFF at 12%. This is the destructive action — give it a subtle pulse animation note in the handoff spec: "Shake feedback on confirm tap (4dp horizontal oscillation, 300ms)."

Apply top app bar and bottom nav as normal.

---

## Frame 4 — Revoking State

Create a frame named **"consent-detail/revoking"** at 393×852dp.

The content area shows only the in-progress revocation UI — no consent data visible (clean slate). Center a vertical Column Auto Layout in the 716dp content zone, alignment CenterHorizontally.

Create a circular progress spinner named `revoke_progress` (48×48dp, #266489 active arc, #C9E6FF track, animating). Below it, add 16dp gap, then a text label "Revoking access…" BodyMedium (14sp 20 400w) fill #41474D, textAlign Center. Wrap both in a Column, gap 16dp.

In the top app bar, set the back arrow icon to 38% opacity (#181C20 at 38%) to indicate it is disabled during the DELETE operation — annotate with: "Back navigation disabled while API call is in-flight to prevent double-submission."

Apply bottom nav normally.

---

## Frame 5 — Error State

Create a frame named **"consent-detail/error"** at 393×852dp.

The content area is vertically and horizontally centered. Create a Column Auto Layout named `error_state`, centerHorizontally, gap 8dp, horizontal padding 32dp.

First layer: Icon `error_outline` 48×48dp, tint #BA1A1A. Set contentDescription to empty (the title provides context). In Figma, use an icon vector with stroke weight appropriate for 48dp (2dp stroke or Material outlined set).

Second layer: title text "Something went wrong", Style=HeadlineMedium (28sp 36 400w), fill #181C20, textAlign Center.

Third layer: body text "We couldn't load your connection details. Please check your network connection and try again.", Style=BodyLarge (16sp 24 400w), fill #41474D, textAlign Center. Note: in production, this body text is dynamic — derived from the `ConsentDetailErrorCode` enum. Annotate the layer: "Content driven by error.message — varies by error code (ConsentNotFound, NetworkError, TokenExpired, RevokeServerError, etc.)."

Fourth layer (`retry_button`): Filled Button, background #266489 (primary), label "Try again" LabelLarge 14sp 500w fill #FFFFFF, height 40dp, corner radius 100dp, width 280dp, marginTop 24dp. Hover: #FFFFFF at 8% over #266489. Pressed: #FFFFFF at 12%.

Apply top app bar and bottom nav normally.

---

## Frame 6 — Empty State

Create a frame named **"consent-detail/empty"** at 393×852dp.

Identical layout to Frame 5 but with neutral (not error) visual treatment. Center a Column Auto Layout named `empty_state`, centerHorizontally, gap 8dp, horizontal padding 32dp.

First layer: Icon `link_off` 48×48dp, tint #41474D (onSurfaceVariant). Represents a broken or absent connection.

Second layer: title text "No connection found", Style=HeadlineMedium (28sp 36 400w), fill #181C20, textAlign Center.

Third layer: body text "The selected connection returned no data. It may have already been removed. Return to your connections list.", Style=BodyLarge (16sp 24 400w), fill #41474D, textAlign Center.

Fourth layer (`empty_go_back_button`): Filled Button, background #266489, label "Go back" LabelLarge 14sp 500w fill #FFFFFF, height 40dp, corner radius 100dp, width 280dp, marginTop 24dp. Same hover/pressed state layers as Frame 5's retry button.

Apply top app bar and bottom nav normally.

---

## Frame 7 — Conditional Variant: Expiry Warning Visible

Create a frame named **"consent-detail/content/expiry_warning"** at 393×852dp.

This variant is identical to Frame 2 (content state) with one addition: after the `status_header_card` and before the `dates_header`, make the `expiry_warning_banner` layer **visible**.

The expiry warning banner is a Card: width 361dp, height 56dp, background fill #EADDFF (tertiaryContainer — the M3 custom "warning-container" role mapped to the nearest warm-neutral palette entry), corner radius 12dp (medium), internal horizontal padding 12dp, vertical padding 12dp. The card has no elevation (level-0).

Inside the card, a horizontal Row Auto Layout (gap 12dp, verticalAlignment CenterVertically):
- Icon `access_time` 24dp, tint #4C4162 (onTertiaryContainer). Set contentDescription to "" (decorative; the text is the accessible label).
- Text "Expires in 3 days. Reconfirm your connection before 2026-09-26.", Style=BodySmall (12sp 16 400w), fill #4C4162, maxLines 2.

Add a design annotation on this frame: "Shown only when `expiryWarningDays != null` (ExpirationDateTime ≤ 7 days from today). Primary demo data (2026-09-26) does not trigger this — use hypothetical date 2026-09-29 to preview. The warning-container / on-warning-container semantic roles are not defined in design-tokens.yaml; proxy via tertiaryContainer #EADDFF / onTertiaryContainer #4C4162."

---

## Auto Layout Specifications

### Content Column (frames 2, 7)

Direction: Vertical. Width: 393dp fill. Height: hug (scrollable, ~1340dp virtual). Internal padding: top 16dp, left 16dp, right 16dp, bottom 24dp. Item spacing: 0 (spacing is embedded within sections via dedicated gap layers or section-header padding).

### Status Header Card internals

Direction: Vertical. Width: fill (361dp). Height: hug. Padding: 16dp. Item spacing: 8dp. `bank_identity_row`: Horizontal, SpaceBetween, fill width, CenterVertically.

### Dialog internals

Direction: Vertical. Width: 280dp fixed. Height: hug. Padding: 24dp. Item spacing: actions row has marginTop 24dp from body. Actions row: Horizontal, End alignment, gap 8dp.

### Permission row internals

Direction: Horizontal. Width: fill (393dp). Height: 72dp fixed. Padding: horizontal 16dp, vertical 12dp. Leading icon: 48×48dp touch container (24dp icon centered). Text Column: Vertical, gap 2dp, hug width (fill remaining), centerVertically. Between rows: 0.5dp separator rectangle, fill #C1C7CE.

### Buttons

All buttons: Horizontal Auto Layout, CenterVertically, horizontal padding 24dp (text-only) or 16dp+gap 8dp (with icon), height 40dp fixed, corner radius 100dp. Width: fill 361dp for primary CTAs (reconfirm_button, revoke_button); 280dp fixed for centered empty/error state buttons; hug for dialog buttons.

---

## Component Variants

### FilledTonal Button — reconfirm_button

Create a 4-variant component set in Figma with property `State`:

- **Default**: bg #D3E5F5 (secondaryContainer), text+icon #384956 (onSecondaryContainer)
- **Hover**: bg #D3E5F5 + #384956 at 8% state-layer overlay blended on top
- **Pressed**: bg #D3E5F5 + #384956 at 12% state-layer overlay
- **Focused**: bg #D3E5F5 + #384956 at 10% state-layer overlay + 3dp focus ring stroke #384956
- **Disabled**: bg #181C20 at 12% (effective: ~#E5E8ED), text #181C20 at 38% opacity

### Outlined Button (Error) — revoke_button

- **Default**: bg transparent, stroke 1dp #BA1A1A, text+icon #BA1A1A
- **Hover**: bg #BA1A1A at 8% (state layer fill), stroke unchanged, text unchanged
- **Pressed**: bg #BA1A1A at 12%, stroke unchanged
- **Focused**: bg #BA1A1A at 10%, stroke #BA1A1A 3dp outer focus ring
- **Disabled**: stroke #181C20 at 12%, text #181C20 at 38% opacity

### AssistChip — status_chip (Authorised)

- **Default**: bg #C9E6FF, text+icon #004B6F, stroke none (filled assist chip)
- **Hover**: bg #C9E6FF + #004B6F at 8% overlay
- **Pressed**: bg #C9E6FF + #004B6F at 12% overlay

### FilledButton (Error) — dialog_confirm_button

- **Default**: bg #BA1A1A, text #FFFFFF
- **Hover**: bg #BA1A1A + #FFFFFF at 8% state-layer overlay
- **Pressed**: bg #BA1A1A + #FFFFFF at 12% overlay
- **Focused**: bg #BA1A1A + #FFFFFF at 10% + 3dp focus ring #BA1A1A

---

## Semantic Token → Figma Variable Mapping

Define a Figma Variables collection named **"Open Banking / Light"** (mode: Light). The following bindings connect M3 role names to the Figma variable names and resolved hex values:

| Semantic token | Figma variable | Resolved hex (light) |
|---|---|---|
| `primary` | `color/primary` | #266489 |
| `onPrimary` | `color/on-primary` | #FFFFFF |
| `primaryContainer` | `color/primary-container` | #C9E6FF |
| `onPrimaryContainer` | `color/on-primary-container` | #004B6F |
| `secondary` | `color/secondary` | #50606E |
| `secondaryContainer` | `color/secondary-container` | #D3E5F5 |
| `onSecondaryContainer` | `color/on-secondary-container` | #384956 |
| `tertiary` | `color/tertiary` | #64597B |
| `tertiaryContainer` | `color/tertiary-container` | #EADDFF |
| `onTertiaryContainer` | `color/on-tertiary-container` | #4C4162 |
| `error` | `color/error` | #BA1A1A |
| `onError` | `color/on-error` | #FFFFFF |
| `errorContainer` | `color/error-container` | #FFDAD6 |
| `onErrorContainer` | `color/on-error-container` | #93000A |
| `surface` | `color/surface` | #F7F9FF |
| `onSurface` | `color/on-surface` | #181C20 |
| `surfaceVariant` | `color/surface-variant` | #DDE3EA |
| `onSurfaceVariant` | `color/on-surface-variant` | #41474D |
| `surfaceContainerLow` | `color/surface-container-low` | #F1F4F9 |
| `surfaceContainer` | `color/surface-container` | #EBEEF3 |
| `outline` | `color/outline` | #72787E |
| `outlineVariant` | `color/outline-variant` | #C1C7CE |
| `scrim` | `color/scrim` | #000000 |

Apply all text, fill, and stroke layers to their variable bindings so the design scales automatically across Light/Dark mode switching.

---

## Prototype Interaction Flow

In Figma Prototype mode, connect frames as follows:

On **Frame 2 (content)**: the `revoke_button` triggers a "Navigate to" interaction → Frame 3 (revoke_confirm). Transition: "Slide up" 300ms ease-in-out (M3 modal enter). On `reconfirm_button`: "Navigate to" → Frame 2 (placeholder; actual nav is external to Figma login screen, so loop back or annotate as "Opens Login screen externally"). On tab "More" (bottom nav, any frame): annotate as "Navigates to Settings".

On **Frame 3 (revoke_confirm)**: `dialog_cancel_button` triggers "Navigate to" → Frame 2 (content), transition "Dissolve" 150ms ease-out. `dialog_confirm_button` triggers "Navigate to" → Frame 4 (revoking), transition "Dissolve" 150ms.

On **Frame 4 (revoking)**: after animation timer (represent as 2 000ms delay), auto-transition "Navigate to" consent-list frame (external; annotate as "Navigates to Consent List screen after DELETE 204/404").

On **Frame 5 (error)**: `retry_button` triggers "Navigate to" → Frame 1 (loading), transition "Dissolve" 150ms to represent retry in-flight.

On **Frame 6 (empty)**: `empty_go_back_button` triggers "Navigate to" → consent-list external (annotate).

Use **Smart Animate** as the fallback transition for any unlisted interactions. All transitions respect M3 `emphasizedDecelerate` easing (cubic-bezier 0.05, 0.7, 0.1, 1.0) for entry and `emphasizedAccelerate` (cubic-bezier 0.3, 0.0, 0.8, 0.15) for exit, at 300ms medium duration.

---

## Accessibility Handoff Notes

All interactive surfaces (buttons, dialog actions, back arrow) require a minimum touch target of 48×48dp. Where the visual element is smaller (e.g., 40dp button height), expand with an invisible bounding box layer named `{component}_touch_target`.

Content descriptions for Figma annotation (required for the Compose implementation):
- `bank_logo`: "HSBC logo"
- `status_chip`: "Status: Authorised" (state-dependent)
- `expiry_warning_icon`: "" (decorative, text carries the message)
- `load_progress`: "Loading consent details"
- `revoke_progress`: "Revoking connection, please wait"
- `error_state` icon: "" (decorative)
- `empty_state` icon: "" (decorative)

Contrast compliance (WCAG AA minimum, per design-system accessibility target):
- Primary text #181C20 on #F7F9FF: 15.8:1 (AAA)
- Secondary text #41474D on #F7F9FF: 7.0:1 (AAA)
- Error #BA1A1A on #FFFFFF: 5.1:1 (AA)
- onPrimaryContainer #004B6F on #C9E6FF chip: 4.8:1 (AA)
- FilledTonal button #384956 on #D3E5F5: 5.6:1 (AA)
- Revoke label #BA1A1A on #F7F9FF: 5.1:1 (AA)
- Dialog confirm #FFFFFF on #BA1A1A: 5.1:1 (AA)
- Primary progress #266489 on #F7F9FF: 4.6:1 (AA)

All section labels, list headlines, and dialog text exceed 4.5:1. The permission list icons (#266489 at 24dp) exceed the 3:1 ratio required for non-text elements at that size.

Reduce-motion support: the circular progress spinners and shimmer animations should be suppressed (replaced with static states) when `reduce_motion` is enabled. Annotate each animated layer with "reduce_motion: static" in the Figma comment.
