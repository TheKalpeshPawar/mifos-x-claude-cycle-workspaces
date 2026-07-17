# Beneficiaries — Figma Design Prompts

> Generated from `screens/beneficiaries/ui.yaml` · AccountId: 40051512345678
> Canvas: 393×852dp (Pixel 5 reference device) · Material 3 light theme · Roboto font family
> Design system: Open Banking — Trust Blue (seed #266489) · `design-tokens.yaml`

---

## Canvas Specification

All frames in this file are 393dp wide by 852dp tall, representing the Pixel 5 reference viewport
at 1× logical density. Use dp units throughout; do not use px. Set the Figma frame background to
#F7F9FF (M3 surface / background). Apply `clip content: true`. Use 8dp as the base spacing unit;
all layout values are multiples of 4.

The content area between the top app bar (64dp) and bottom navigation bar (80dp) is 708dp tall.
Horizontal screen padding is 16dp on each side, yielding a 361dp usable content column.

---

## Design System Summary

This screen uses the **Open Banking — Trust Blue** Material 3 design system, derived from seed
primary colour #266489. The primary colour expresses trust and institutional credibility,
appropriate for a regulated UK Open Banking AISP product.

The palette follows M3 tonal-surface conventions. Backgrounds and card surfaces use #F7F9FF
(surface), while elevated surfaces step to #F1F4F9 (surfaceContainerLow). Primary interactive
elements — the circular progress indicator, the filled CTA button, the active bottom-nav tab, and
the search bar active indicator — all use #266489. Destructive / error states use #BA1A1A (error).
Supporting text and icons use #41474D (onSurfaceVariant).

The typography stack is exclusively **Roboto** sans-serif. Roboto Mono is reserved for numeric
account identifiers and IBAN strings to guarantee digit alignment and scan-readability. All touch
targets must be at least 48×48dp, satisfying both WCAG AA and the M3 interaction model. Motion is
low-intensity: standard M3 transitions at 300ms using `cubic-bezier(0.2, 0.0, 0, 1.0)`.

---

## Semantic Token → Figma Variable Mapping

Map each semantic token to a Figma variable in the `color/` group under the `light` mode. Every
colour reference in this document is the resolved light-mode hex; the dark-mode counterparts live
in the same variable path under `dark` mode.

| Semantic token       | Figma variable path              | Light hex  |
|----------------------|----------------------------------|------------|
| `primary`            | `color/primary`                  | #266489    |
| `onPrimary`          | `color/onPrimary`                | #FFFFFF    |
| `primaryContainer`   | `color/primaryContainer`         | #C9E6FF    |
| `onPrimaryContainer` | `color/onPrimaryContainer`       | #004B6F    |
| `secondary`          | `color/secondary`                | #50606E    |
| `onSecondary`        | `color/onSecondary`              | #FFFFFF    |
| `secondaryContainer` | `color/secondaryContainer`       | #D3E5F5    |
| `onSecondaryContainer`| `color/onSecondaryContainer`    | #384956    |
| `background`         | `color/background`               | #F7F9FF    |
| `surface`            | `color/surface`                  | #F7F9FF    |
| `onSurface`          | `color/onSurface`                | #181C20    |
| `surfaceVariant`     | `color/surfaceVariant`           | #DDE3EA    |
| `onSurfaceVariant`   | `color/onSurfaceVariant`         | #41474D    |
| `surfaceContainerLow`| `color/surfaceContainerLow`      | #F1F4F9    |
| `outline`            | `color/outline`                  | #72787E    |
| `outlineVariant`     | `color/outlineVariant`           | #C1C7CE    |
| `error`              | `color/error`                    | #BA1A1A    |
| `onError`            | `color/onError`                  | #FFFFFF    |
| `errorContainer`     | `color/errorContainer`           | #FFDAD6    |
| `onErrorContainer`   | `color/onErrorContainer`         | #93000A    |

---

## Typography Scale — Figma Text Styles

Create the following text styles in Figma under a `type/` group. All use font family "Roboto".
For account identifiers and IBAN strings, a `type/mono/` group with "Roboto Mono" is required.

| Style name            | Font      | Size | Line h | Weight | Usage in this screen                      |
|-----------------------|-----------|------|--------|--------|-------------------------------------------|
| `type/titleLarge`     | Roboto    | 22sp | 28sp   | 400    | Top app bar title "Beneficiaries"         |
| `type/headlineSmall`  | Roboto    | 24sp | 32sp   | 400    | Empty state title, error state title      |
| `type/bodyLarge`      | Roboto    | 16sp | 24sp   | 400    | List item headline (creditor name)        |
| `type/bodyMedium`     | Roboto    | 14sp | 20sp   | 400    | Supporting text, empty/error body copy    |
| `type/labelLarge`     | Roboto    | 14sp | 20sp   | 500    | Button labels (Try again / View consents) |
| `type/labelMedium`    | Roboto    | 12sp | 16sp   | 500    | Avatar initials                           |
| `type/labelSmall`     | Roboto    | 11sp | 16sp   | 500    | Trailing reference label in list item     |
| `type/bodyLarge`      | Roboto    | 16sp | 24sp   | 400    | Search placeholder text                   |
| `type/mono/bodyMedium`| Roboto Mono | 14sp | 20sp | 400  | IBAN identifier "DE89370400440532013000"  |

---

## Shape & Spacing Reference

Corner radii follow M3 shape tokens. Key values for this screen:

- **Full pill / circular buttons**: `ShapeKeyTokens.CornerFull` → 9999dp (effectively 50% of height)
- **Search bar**: 28dp radius (M3 SearchBar default — full pill at 48dp height)
- **Avatar**: 9999dp radius (circular)
- **Card / modal surfaces**: not used in this screen; this screen is a plain list

Screen-level padding: 16dp horizontal. List content padding top: 8dp. Gap between search bar and
first list item: 8dp. List item height (two-line): 72dp. Divider between items: 1dp #DDE3EA.

---

## Frame 1 — Loading State

Create a 393×852dp frame named **"Beneficiaries / 1-Loading"**. Fill with #F7F9FF.

### Top App Bar

Place a Material 3 Small Top App Bar component anchored to the top of the frame. Set it to
393dp wide and 64dp tall with a fill of #F7F9FF and no shadow or elevation tint. Inside the
leading slot (left side, 16dp from screen edge), place an `arrow_back` icon (24dp square, tinted
#266489) centred within a 48×48dp touch-target rectangle. Set this icon button's accessibility
label to "Back to account detail". In the title slot, set the text to "Beneficiaries" using
`type/titleLarge` (#181C20). Leave the trailing action slot empty.

### Circular Progress Indicator

In the body area (between the app bar and bottom nav), centre a circular progress indicator
element — this is the M3 `CircularProgressIndicator` (indeterminate variant). Make it 48dp in
diameter with a stroke width of 4dp. Tint it with `color/primary` (#266489). Position it at the
geometric centre of the body area: vertically at y = 64 + (708 / 2) = 418dp from the frame top,
horizontally at 393 / 2 = 196.5dp from the left. This element has a Figma layer accessibility
label of "Loading beneficiaries". Add a prototype trigger: `After Delay 1500ms → navigate to
Frame 2 (Content)` for demo purposes.

### Bottom Navigation Bar

Place a Navigation Bar component 80dp tall at the bottom of the frame (y = 772dp), spanning the
full 393dp width. Fill with #F7F9FF. Add four navigation items:

1. **Home** — icon `home`, label "Home", unselected tint #41474D
2. **Accounts** — icon `account_balance`, label "Accounts", selected tint #266489 (contextual
   parent of beneficiaries drill-down)
3. **Transactions** — icon `receipt_long`, label "Transactions", unselected tint #41474D
4. **More** — icon `more_horiz`, label "More", unselected tint #41474D

The selected tab indicator uses `color/primary` (#266489) as the pill fill and icon tint.
Unselected tabs use `color/onSurfaceVariant` (#41474D).

**Auto Layout for loading frame**: The frame itself uses a vertical auto-layout with three direct
children — top_app_bar (64dp fixed height, hug width), body_area (fill height remaining space, fill
width), bottom_nav (80dp fixed height, fill width). The body_area centres its single child
(progress_indicator) using `align-items: center` and `justify-content: center`.

---

## Frame 2 — Content State (Full List)

Create a 393×852dp frame named **"Beneficiaries / 2-Content"**. Fill with #F7F9FF.

Copy the top app bar and bottom navigation bar from Frame 1 exactly.

### Body Content Column

Between the app bar and bottom nav, create a vertical auto-layout container 393dp wide and 708dp
tall, with horizontal padding of 16dp on each side and top padding of 8dp. Set overflow to
`clip`. Name this container `body_scroll`.

### Search Bar

Inside `body_scroll`, place a search bar component 361dp wide (fill parent minus 32dp padding) and
48dp tall. Use `color/surfaceContainerLow` (#F1F4F9) as the fill. Apply a 1dp stroke using
`color/outline` (#72787E). Set corner radius to 28dp (full pill at this height). Place a `search`
icon (24dp, #72787E) as the leading element with 16dp left padding. Set the placeholder text
"Search by name or reference" in `type/bodyLarge` (#72787E). When a query is typed, show a `close`
icon (24dp, #72787E) on the trailing side to clear the input. The active-focus indicator colour is
`color/primary` (#266489). Below the search bar, add 8dp vertical spacing before the first list
item.

### Beneficiary List Items

Create five list items in sequence, each using the M3 `ListItem` two-line variant at 72dp height
and full width (361dp). Separate each adjacent pair with a horizontal divider 1dp tall, filled
with `color/outlineVariant` (#DDE3EA), no horizontal inset.

**List item anatomy** — apply identically to all five rows, substituting real data:

- **Leading slot**: a circular avatar 40dp × 40dp, corner radius 9999dp. Fill with
  `color/primaryContainer` (#C9E6FF). Inside, centre a two-character initials string using
  `type/labelMedium` (#004B6F / `color/onPrimaryContainer`). Mark the avatar `aria-hidden: true`
  in Figma (the headline text carries the accessible name).
- **Headline slot**: creditor name in `type/bodyLarge` (#181C20). Single line, maxLines 1.
- **Supporting text slot**: scheme short label + " · " + account identifier in `type/bodyMedium`
  (#41474D). For IBAN identifiers, use `type/mono/bodyMedium` for the identifier portion only.
- **Trailing slot**: payment reference code in `type/labelSmall` (#50606E), right-aligned.

The five rows with real data from `demo-data.yaml`:

**Row 1 — BEN-001**
Initials `JL` · Headline "Jameson Lettings" · Supporting "Sort Code · 40-12-09 65872310" ·
Trailing "RENT-FLAT12"

**Row 2 — BEN-002**
Initials `JS` · Headline "John Sharma" · Supporting "Sort Code · 23-05-80 11223344" ·
Trailing "FAMILY"

**Row 3 — BEN-003**
Initials `EE` · Headline "EDF Energy" · Supporting "Sort Code · 60-00-01 99887766" ·
Trailing "ELEC-8841"

**Row 4 — BEN-004**
Initials `HL` · Headline "Hargreaves Lansdown" · Supporting "Sort Code · 11-22-33 44556677" ·
Trailing "ISA-TOPUP"

**Row 5 — BEN-005**
Initials `PR` · Headline "Priya Rajan — N26 GmbH" ·
Supporting: scheme label "IBAN" in `type/bodyMedium` (#41474D), then " · ", then identifier
"DE89370400440532013000" in `type/mono/bodyMedium` (#41474D) — the Roboto Mono font ensures
digit alignment for the 22-character IBAN string. Trailing "TRAVEL-EUR".

**Auto Layout for body_scroll**: direction vertical, padding h 16dp top 8dp bottom 16dp,
gap 0 (items butt together — dividers handle visual separation). Width: fill (393dp). Height:
hug (list fits within 708dp available since 5 × 72dp + 4 × 1dp + 48dp search + 8dp gap = 428dp
total, well within 708dp).

---

## Frame 3 — Content State (Search Active, 1 Result)

Duplicate Frame 2 and rename it **"Beneficiaries / 3-Content-Search-Active"**.

In the search bar, replace the placeholder with the active query text "ener" in `type/bodyLarge`
(#181C20 — active text colour). Show the trailing `close` icon (24dp, #41474D). Apply a 2dp
bottom border tinted #266489 (primary) below the search bar to indicate active focus.

Remove list rows BEN-001, BEN-002, BEN-004, and BEN-005. Keep only **BEN-003 (EDF Energy)** —
its `CreditorAccount.Name` contains "ener" (ignoreCase match). Remove the four dividers that no
longer have an adjacent pair. The body below the single result is empty #F7F9FF. This demonstrates
the client-side filter — no spinner, no network call.

Add an annotation note: "filter_beneficiaries('ener') — client-side only, no API call. IgnoreCase
match on CreditorAccount.Name and Reference fields."

---

## Frame 4 — Content State (Search, No Results)

Duplicate Frame 2 and rename it **"Beneficiaries / 4-Content-Search-Empty"**.

Replace the search bar placeholder with the active query "zzzmatch". Remove all five list rows.
In the body area below the search bar, centre a vertical column (padding h 32dp) containing:

1. The `search_off` Material icon at 48dp × 48dp, tinted #41474D. Set its Figma accessibility
   description to "No search results".
2. Below, add 16dp vertical spacing.
3. The title "No results found" in `type/headlineSmall` (#181C20), text-align centre.
4. Below, add 8dp vertical spacing.
5. The body "Try a different name or reference." in `type/bodyMedium` (#41474D), text-align centre.

This empty state is the `search_no_results` component, rendered within the Content UI state
whenever `beneficiaries_filtered.isEmpty()` is true.

**Auto Layout**: column, direction vertical, align-items centre, gap 0 (use Spacer children for
gaps), padding horizontal 32dp. Height: hug. Position vertically centred within the body_scroll
container below the search bar.

---

## Frame 5 — Empty State (No Beneficiaries)

Create a 393×852dp frame named **"Beneficiaries / 5-Empty"**. Fill with #F7F9FF.

Copy the top app bar (with back arrow, "Beneficiaries" title) and bottom navigation bar from
Frame 1.

In the body area (708dp, between app bar and bottom nav), create a single vertical auto-layout
column centred both horizontally and vertically — use `align-self: center` and `align-content:
center` with `fillMaxSize` semantics. Apply 32dp horizontal padding.

This column contains the `empty_beneficiaries` component with:

1. The `people_outline` Material icon at 48dp × 48dp, tinted #41474D (`color/onSurfaceVariant`).
   Accessibility description: "No saved beneficiaries".
2. 16dp vertical spacer.
3. Title text "No beneficiaries set up" in `type/headlineSmall` (#181C20), text-align centre.
4. 8dp vertical spacer.
5. Body text "No payees have been saved for this account. Set up payees in your bank app to see
   them here." in `type/bodyMedium` (#41474D), text-align centre, max width 329dp (361dp minus
   32dp extra horizontal padding), wrap enabled.

There are no action buttons in this state — it is read-only information. The PSU must manage
payees within their bank app (outside this AISP).

**Auto Layout**: direction vertical, align-items centre, justify-content centre, gap 0, padding
h 32dp. The outer frame uses fill-width auto-layout to hold top bar + body + bottom nav.

---

## Frame 6 — Error State (Retryable: 401 / 429 / Network / 500)

Create a 393×852dp frame named **"Beneficiaries / 6-Error-Retryable"**. Fill with #F7F9FF.

Copy the top app bar and bottom navigation bar from Frame 1.

In the body area, create a centred vertical column (padding h 32dp) containing:

1. The `error_outline` Material icon at 48dp × 48dp, tinted #BA1A1A (`color/error`).
   Accessibility description: "Error loading beneficiaries".
2. 24dp vertical spacer.
3. Title "Unable to load beneficiaries" in `type/headlineSmall` (#181C20), text-align centre.
4. 8dp vertical spacer.
5. Body text demonstrating the HTTP 401 TokenExpired message: "Your session has expired.
   Please sign in again to continue." in `type/bodyMedium` (#41474D), text-align centre.
   In production this text is dynamic — `{error.message}` from the ViewModel.
6. 24dp vertical spacer.
7. The `retry_button` — a filled M3 Button component 265dp wide (match_parent − 64dp) and 48dp
   tall, corner radius 9999dp (full pill). Fill: `color/primary` (#266489). Label text "Try again"
   in `type/labelLarge` (#FFFFFF). Minimum touch target: 48dp height already satisfied.
   Prototype interaction: `On tap → navigate to Frame 1 (Loading) with transition Dissolve 300ms`.
   This simulates `retryLoad()` re-triggering the beneficiaries fetch.
   Visibility condition annotation: "Shown only when `error.type ∈ {TokenExpired, RateLimited,
   NetworkError, ServerError}`."

**Component variants to prepare**:
- retry_button / default: bg #266489 text #FFFFFF
- retry_button / pressed: bg #004B6F text #FFFFFF (overlay 12% onPrimary)
- retry_button / focused: bg #266489 with 3dp #266489 focus ring outline
- retry_button / disabled: bg #DDE3EA text #72787E (this button is never disabled in this error
  context, but prepare the variant for completeness)

**Auto Layout for error body column**: direction vertical, align-items centre, justify-content
centre, gap 0, padding h 32dp.

---

## Frame 7 — Error State (ConsentRevoked: HTTP 403)

Duplicate Frame 6 and rename it **"Beneficiaries / 7-Error-ConsentRevoked"**.

Replace the body copy with: "Your account access consent has been revoked. Re-authorise to restore
beneficiaries access." This represents the HTTP 403 ConsentRevoked message from the AIS endpoint.

Replace the `retry_button` with the `view_consents_button` — a tonal M3 Button, same dimensions
(265dp × 48dp, radius 9999dp). Fill: `color/secondaryContainer` (#D3E5F5). Label text "View
consents" in `type/labelLarge` (`color/onSecondaryContainer` #384956). Do not show `retry_button`
in this sub-variant — they are mutually exclusive based on `error.type`.

Visibility annotation on `view_consents_button`: "Shown only when `error.type == ConsentRevoked`."
Prototype interaction: `On tap → navigate to consent-list screen`. This emits
`NavigateTo(Screen.ConsentList)` from the ViewModel, allowing the PSU to review and re-authorise
the ReadBeneficiariesDetail permission scope.

**Component variants to prepare for view_consents_button**:
- default: bg #D3E5F5 text #384956
- pressed: bg #B7C9D9 text #384956 (overlay 12% on surface)
- focused: bg #D3E5F5 with 3dp #266489 focus ring
- disabled: not applicable in this context (button always enabled when shown)

---

## Auto Layout Specifications — Frame Structure

Every frame in this file shares the same outer auto-layout structure:

**Frame root**: direction vertical, align-items stretch, justify-content space-between,
gap 0, padding 0, clip content true. Width: 393dp fixed. Height: 852dp fixed.

**top_app_bar**: direction horizontal, align-items centre, padding left 4dp right 16dp
(leading icon needs 4dp left for optical balance), gap 0. Width: fill (393dp). Height: 64dp fixed.

**body_scroll / body_area**: direction vertical, align-items stretch or centre (centre for
empty/error states), justify-content start (content) or centre (empty/error). Width: fill.
Height: fill (takes remaining space between app bar and bottom nav). Padding: h 16dp, top 8dp.
Overflow: scroll (content) or clip (empty/error).

**search_bar**: direction horizontal, align-items centre, padding h 16dp. Width: fill. Height:
48dp fixed. Corner radius: 28dp.

**beneficiary_row**: direction horizontal, align-items centre, padding h 16dp, top 8dp, bottom
8dp, gap 16dp. Width: fill. Height: 72dp fixed. Use Fixed height to guarantee consistent row
cadence regardless of text length (rely on maxLines 1 and ellipsis for overflow).

**avatar**: width 40dp fixed, height 40dp fixed, corner radius 9999dp, align-items centre,
justify-content centre. Fill: `color/primaryContainer`.

**error_body_column / empty_body_column**: direction vertical, align-items centre, justify-content
centre, gap 0, padding h 32dp. Width: fill. Height: fill (occupies full body_area).

**cta_button (retry / view_consents)**: direction horizontal, align-items centre, justify-content
centre. Width: fixed 265dp. Height: 48dp fixed. Corner radius: 9999dp. Padding h: 24dp.

**bottom_nav**: direction horizontal, align-items stretch, justify-content space-around, padding 0.
Width: fill (393dp). Height: 80dp fixed.

---

## Component Variants

### Avatar

Create a component named `Avatar/Initials` with the following properties:

- **Size**: Small (40dp) — the only size used in this screen
- **Colour seed**: property `string` — determines background hue in production (runtime-computed);
  for Figma use a single visual variant with `color/primaryContainer` fill and
  `color/onPrimaryContainer` text
- **Initials**: text property `string` (2 chars max), `type/labelMedium` (#004B6F)
- **Corner radius**: 9999dp (circular)

Variants to expose: `size=[small|medium|large]`, `style=[initials|icon]`.

### ListItem Two-Line (Beneficiary Row)

Create a component named `ListItem/TwoLine/Beneficiary` with these auto-layout properties:
- Direction horizontal, align-items centre, padding h 16dp, gap 16dp, height 72dp, width fill.
- Slots: `leading` (Avatar/Initials, 40dp), `content_column` (vertical, weight 1, gap 2dp),
  `trailing` (labelSmall text, right-aligned).
- `content_column` children: `headline` (bodyLarge, #181C20) and `supporting` (bodyMedium, #41474D).
- No on_click handler — this row is display-only (AIS read-only data). Do not add hover/press
  states to indicate interactivity.

### Search Bar

Create a component named `SearchBar/Beneficiary`:
- Width fill, height 48dp, corner radius 28dp, fill #F1F4F9, stroke 1dp #72787E.
- Slots: `leading_icon` (search, 24dp, #72787E), `text` (bodyLarge, #72787E placeholder /
  #181C20 active), `trailing_icon` (close, 24dp, #41474D, visible only when query non-empty).
- Variants: `state=[empty|active|focused]`.
  - empty: placeholder visible, no trailing icon, stroke #72787E
  - active: query text visible, trailing close icon shown, stroke #266489 (2dp)
  - focused: same as active; add inner shadow 0 0 0 3dp #266489 for keyboard focus ring

### Filled Button (retry_button)

Create a component named `Button/Filled/Primary`:
- Width fixed 265dp, height 48dp, corner radius 9999dp.
- Fill `color/primary` (#266489). Label `type/labelLarge` (#FFFFFF).
- Variants: `state=[default|hovered|pressed|focused|disabled]`.
  - default: bg #266489
  - hovered: bg #266489 + 8% white overlay
  - pressed: bg #004B6F
  - focused: bg #266489 + 3dp focus ring #266489
  - disabled: bg #DDE3EA, text #72787E

### Tonal Button (view_consents_button)

Create a component named `Button/Tonal/Secondary`:
- Width fixed 265dp, height 48dp, corner radius 9999dp.
- Fill `color/secondaryContainer` (#D3E5F5). Label `type/labelLarge` (`color/onSecondaryContainer`
  #384956).
- Variants: `state=[default|hovered|pressed|focused]`.
  - default: bg #D3E5F5
  - hovered: bg #D3E5F5 + 8% onSurface overlay
  - pressed: bg #B7C9D9
  - focused: bg #D3E5F5 + 3dp focus ring #266489

---

## Prototype Interaction Flow

Wire the following Figma prototype connections to create a functional walkthrough:

1. **Frame 1 (Loading) → Frame 2 (Content)**: After delay 1.5s, Smart Animate dissolve 300ms.
   Simulates the OBReadBeneficiary5 API response arriving and populating the list.

2. **Frame 2 (Content) back_button → account-detail screen**: On tap, Navigate to the
   account-detail Figma frame. Slide-out transition (horizontal, 300ms ease).

3. **Frame 2 (Content) search bar tap → Frame 3 (Search Active)**: On tap, Navigate to
   Frame 3. No transition (instant focus state change).

4. **Frame 3 (Search Active) search bar clear icon → Frame 2 (Content)**: On tap, Navigate to
   Frame 2. Instant.

5. **Frame 4 (Search Empty) clear icon → Frame 2 (Content)**: On tap, Navigate to Frame 2.

6. **Frame 6 (Error Retryable) retry_button → Frame 1 (Loading)**: On tap, Navigate to Frame 1.
   Fade 300ms. Simulates `retryLoad()` re-triggering the API fetch.

7. **Frame 7 (Error ConsentRevoked) view_consents_button → consent-list screen**: On tap,
   Navigate to the consent-list Figma frame. Push-right transition 300ms.

8. **All frames back_button → account-detail screen**: On tap, Navigate to account-detail.
   Pop-left slide transition 300ms. This back_button is always visible per `ui.yaml` — it appears
   in the top app bar across all four UI states.

---

## Accessibility Annotations

Add a Figma accessibility annotation layer (use the A11y Annotation Kit plugin or equivalent) on
each frame:

**Touch targets**: Annotate every interactive element with its minimum touch target. The
`back_button` icon is 24dp but its touch target must be 48×48dp — use a transparent overlay
rectangle to document this. The `retry_button` and `view_consents_button` at 48dp height already
satisfy the minimum. The `beneficiary_search` at 48dp satisfies the minimum.

**Screen reader reading order**: On Frame 2 (Content), annotate the reading order as:
1. Top app bar: "Beneficiaries" (landmark), 2. back_button (interactive), 3. search bar
(interactive, role textfield), 4. beneficiary_row BEN-001 (accessibility_label from template:
"Jameson Lettings, Sort Code account, 40-12-09 65872310"), 5–8. remaining rows in order.

The `beneficiary_avatar` images are `aria_hidden: true` — the avatar conveys no information
not already in the headline and supporting text. Do not annotate them as interactive.

**Contrast**: All text combinations in this screen meet WCAG AA:
- #181C20 on #F7F9FF: ratio 19.6:1 (passes AA and AAA)
- #41474D on #F7F9FF: ratio 11.1:1 (passes AA and AAA)
- #50606E on #F7F9FF: ratio 7.0:1 (passes AA)
- #004B6F on #C9E6FF: ratio 5.6:1 (passes AA, avatar context)
- #FFFFFF on #266489: ratio 4.6:1 (passes AA for large text; labelLarge 14sp w500 qualifies)
- #384956 on #D3E5F5: ratio 5.5:1 (passes AA)

**Motion**: All prototype transitions use 300ms. Annotate that `prefers-reduced-motion` should
collapse all transitions to instant. The circular progress indicator (indeterminate) should render
as a static arc when reduced motion is active.

**Colour independence**: The error state uses the `error_outline` icon in addition to the red
#BA1A1A colour. The empty state uses `people_outline`. Both states communicate meaning through
icon + text, not colour alone. The scheme label (Sort Code / IBAN / Paym) in the supporting text
slot also distinguishes scheme type without relying on colour alone.

---

## Design Handoff Notes

**Scheme label mapping**: The `CreditorAccount.SchemeName` OBIE field maps to display labels as
follows — `UK.OBIE.SortCodeAccountNumber` → "Sort Code"; `UK.OBIE.IBAN` → "IBAN";
`UK.OBIE.Paym` → "Paym"; `UK.OBIE.PAN` → "Card"; default → "Account". This is a ViewModel-layer
transform; the Figma design uses the resolved labels directly.

**Avatar colour determinism**: In production the avatar background hue is computed from
`BeneficiaryId` using a seed-based colour derivation (maps the string hash into one of the M3
tonal surface variants). For Figma, use the single `primaryContainer` (#C9E6FF) / `onPrimaryContainer`
(#004B6F) pair throughout all five rows. Note that all five avatars in the demo data will look
identical in the static mockup; the runtime will differentiate them by hue.

**IBAN formatting**: The IBAN `DE89370400440532013000` is 22 characters. Render it in Roboto Mono
at 14sp. Do not insert spaces in the Figma representation; the runtime may choose to insert
group-of-4 spaces (`DE89 3704 0044 0532 0130 00`) for readability — document this as an open
decision for the engineering team.

**No FAB**: The `fab_visible: false` override in `ui.yaml` means no FAB should appear in any
Figma frame for this screen. Adding a payee is not a feature of this AISP view (AISP is read-only
by regulation; payee management is done in the bank's own app).

**Error message copy**: The body text in error frames is dynamic. The values shown in Frames 6
and 7 are representative demo strings. Engineering will supply the final localised strings via the
`strings.error.beneficiaries.*` resource keys. Annotate both body text layers as "dynamic:
{error.message}" in the Figma file using the annotation layer.
