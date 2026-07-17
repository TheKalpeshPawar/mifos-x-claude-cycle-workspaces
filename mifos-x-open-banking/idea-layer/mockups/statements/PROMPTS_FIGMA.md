# Statements — Figma Design Prompts

> Generated from: `screens/statements/ui.yaml` + `design-tokens.yaml` + `demo-data.yaml`
> Canvas: 393×852dp (Pixel 5 viewport) — use 1× as base frame, export @2× and @3×
> Design system: Open Banking — Trust Blue · Material Design 3 · Roboto · seed #266489
> Generated: 2026-07-16T00:00:00Z

---

## 1. Design System Summary

### Resolved Colour Palette (M3 Light — use as Figma variables)

Create a Figma variable collection named `color/light` and register each role below as a variable. Use these exact hex values — do not alter them. The palette derives from Material Theme Builder with seed colour #266489 (Trust Blue).

| Semantic Token | Figma Variable | Hex |
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
| onBackground | color/onBackground | #181C20 |
| surface | color/surface | #F7F9FF |
| onSurface | color/onSurface | #181C20 |
| surfaceVariant | color/surfaceVariant | #DDE3EA |
| onSurfaceVariant | color/onSurfaceVariant | #41474D |
| outline | color/outline | #72787E |
| outlineVariant | color/outlineVariant | #C1C7CE |

### Roboto Type Scale (M3 — use as Figma text styles)

Create a text style library with the following entries. Font: Roboto (ensure Google Fonts Roboto is installed in Figma).

| Style name | Size | Line height | Weight | Usage in this screen |
|---|---|---|---|---|
| titleLarge | 22sp | 28sp | 400 | Top app bar title |
| titleMedium | 16sp | 24sp | 500 | Error/empty state title |
| bodyLarge | 16sp | 24sp | 400 | Statement row headline (period label) |
| bodyMedium | 14sp | 20sp | 400 | Supporting text, body copy |
| bodySmall | 12sp | 16sp | 400 | Date range trailing text |
| labelMedium | 12sp | 16sp | 500 | Bottom nav labels |

### Spacing and Shape System

The base spacing unit is 4dp. Common values used in this screen: 8dp, 12dp, 16dp, 20dp, 24dp, 32dp, 48dp. Corner radius tokens: none=0, extra_small=4dp, small=8dp, medium=12dp, large=16dp, full=9999dp. Minimum touch target for any interactive element is 48dp. All dp values translate 1:1 to Figma points at 1× density.

---

## 2. Frame Setup

### Canvas and Base Frame

Create a new Figma frame named "Statements" with dimensions 393×852 points. Set the fill to `color/background` (#F7F9FF). Enable the Auto Layout with vertical direction, no padding, and item spacing 0. All child frames will stack vertically and must respect the safe-area padding. The frame represents the full Pixel 5 screen at 1× density.

Pin the top app bar to the top of the frame and the bottom navigation bar to the bottom. The scrollable content area occupies the space between them — approximately 708dp tall at rest.

Create four variants of this base frame, one per state: Loading, Content, Empty, and Error. Organise them left-to-right in the canvas with 48dp gap between frames, under a section named "Statements — All States".

---

## 3. Shared Chrome Components

### Top App Bar

Create a component named `TopAppBar/Small/Statements`. Set dimensions to 393×64 points, fill `color/surface` (#F7F9FF), with no elevation shadow (elevation level0 — the small top app bar has no shadow when content is at rest scroll position).

Inside, use an Auto Layout row with vertical alignment centre, horizontal padding left 4dp right 16dp, height 64dp. Place the following children from left to right:

First, place a Navigation Icon button. This is an icon button component with a touch target of 48×48dp. Centre the `arrow_back` Material Symbol icon at 24×24dp, filled with `color/primary` (#266489). Label it "Navigate back" in the accessibility layer — this arrow takes the user back to the account-detail screen. Add an on-click prototype interaction: "On Tap → Navigate to account-detail frame."

Second, place a Text element with the text "Statements", style `titleLarge` (Roboto 22/28 Regular, colour `color/onSurface` #181C20). Give it weight 1 in the layout so it expands to fill available space. Left-align the text.

The trailing area has no actions for this screen — leave it empty or add a spacer of 16dp width.

### Bottom Navigation Bar

Create a component named `BottomNav/OpenBanking`. Set dimensions to 393×80 points, fill `color/surface` (#F7F9FF). Add a 1dp top border using `color/outlineVariant` (#C1C7CE) to separate it from content.

Inside, use an Auto Layout row, evenly space four tab items. Each tab item is a column Auto Layout (verticalAlignment centre, horizontalAlignment centre, width fill/25%), containing: a Material Symbol icon at 24×24dp, followed by a Text label at labelMedium style (Roboto 12/16 Medium).

The four tabs are:
- Tab 1: icon `home`, label "Home"
- Tab 2: icon `account_balance`, label "Accounts"
- Tab 3: icon `receipt_long`, label "Transactions"
- Tab 4: icon `more_horiz`, label "More"

For this screen (Statements is a sub-screen, not a bottom-nav destination), all four tabs are in the unselected state: icon tint `color/onSurfaceVariant` (#41474D), label colour `color/onSurfaceVariant` (#41474D). No indicator pill is shown. The minimum touch target per tab is 48dp height.

Create a boolean variant property `selected` on the tab item component (true/false) so you can later toggle selected state if the design is reused in a bottom-nav root screen context.

---

## 4. State: Loading

### Frame Description

The Loading frame shows the skeleton shimmer state while the app fetches account statements from the HSBC Open Banking AIS endpoint. The top app bar and bottom nav are fully rendered and visible. The content area contains three shimmer placeholder rows.

### Shimmer Skeleton Rows

Inside the content area (the space between top app bar and bottom nav, approximately 393×708dp), place a Column Auto Layout with: direction vertical, top padding 16dp, horizontal padding 16dp, gap between items 12dp, background transparent (inherits frame background #F7F9FF).

Create a component named `Skeleton/ListRow` with dimensions 361×72 points (match_parent minus 32dp horizontal padding). Set the fill to `color/surfaceVariant` (#DDE3EA) and corner radius 8dp. This represents a single shimmer placeholder row.

Apply a shimmer animation overlay to each skeleton row. In Figma, represent this as a gradient fill overlaid on the row: a linear gradient flowing left-to-right from `color/surfaceVariant` (#DDE3EA) at 0%, transitioning through `color/surfaceContainerLow` (#F1F4F9) at 50%, and back to #DDE3EA at 100%. This gradient simulates the shimmer sweep. In the prototype, use Smart Animate to loop this state. Note for engineers: the real animation is a continuous 1.5-second left-to-right shimmer loop with each row offset by +0.2s (row 1: 0s, row 2: 0.2s, row 3: 0.4s). Add the accessibility annotation "reduce-motion: static fill, no animation" on the skeleton frame.

Place three instances of `Skeleton/ListRow` in the column. Label them skeleton_row_1, skeleton_row_2, skeleton_row_3.

Below the three skeleton rows, the rest of the content area is left empty at background colour #F7F9FF.

---

## 5. State: Content

### Frame Description

The Content frame shows six statement rows, sorted from most recent (May 2026) to oldest (December 2025), separated by hairline dividers. Each row is a list item with period label, closing balance, formatted date range, and a download icon button. The content area is a scrollable lazy column.

### Statement Row Component

Create a component named `StatementRow` with dimensions 393×72 points minimum height (height should grow to wrap content if the period label wraps, but in practice all period labels fit on one line). Set the fill to `color/surface` (#F7F9FF). Add a ripple/pressed state: when pressed, overlay a fill using `color/onSurface` (#181C20) at 8% opacity (M3 press state).

Inside the row, use an Auto Layout row with: direction horizontal, vertical alignment centre, horizontal padding left 16dp right 8dp (right padding reduced to 8dp to bring the icon button closer to edge), vertical padding top 12dp bottom 12dp, gap 8dp between the text column and the trailing group.

The text column occupies the remaining horizontal space (weight 1). Use a vertical Auto Layout column with gap 4dp. Place two Text elements:

The first text element is the period label headline. Apply the `bodyLarge` style (Roboto 16/24 Regular, colour `color/onSurface` #181C20). The text is the ViewModel-derived period string such as "May 2026" — generated from OBStatement2.StartDateTime via kotlinx-datetime.

The second text element is the closing balance supporting text. Apply the `bodyMedium` style (Roboto 14/20 Regular, colour `color/onSurfaceVariant` #41474D). The text is formatted as "Closing balance: £2,847.63". The amount is drawn from OBStatement2.StatementAmount where Type=ClosingBalance, formatted to GBP with two decimal places.

The trailing group uses a vertical Auto Layout column with horizontal alignment end, gap 4dp. It contains two elements:

The first trailing element is the date range. Apply `bodySmall` style (Roboto 12/16 Regular, colour `color/onSurfaceVariant` #41474D). The text reads "1 May 2026 – 31 May 2026", formatted from OBStatement2.StartDateTime and EndDateTime.

The second trailing element is the Download Statement Button. Create a component named `IconButton/Download` with a touch target of 48×48dp (use an invisible hit area frame). Centre a 24×24dp `file_download` Material Symbol icon within the touch target, tinted `color/primary` (#266489). This button has two variants: **idle** (shows file_download icon) and **in-progress** (shows a CircularProgressIndicator spinner at 24dp, stroke width 2dp, tint #266489). Add a boolean variant property `isDownloading: true/false` to toggle between these states. In the prototype, mark this button with an on-click interaction: "On Tap → trigger download flow." The accessibility label in idle state is "Download [period] statement" and in in-progress state is "Downloading [period] statement."

Add a prototype interaction on the full `StatementRow` component: "On Tap → Navigate to statement-detail frame." Note that the download button sits within the row but should prevent the row's tap from triggering when the download button is tapped — annotate this with a comment: "stopPropagation: download button tap does not fire parent row navigation."

Create six instances of `StatementRow` in the content column, populated with the following real data:

Row 1: period "May 2026", supporting "Closing balance: £2,847.63", trailing date "1 May 2026 – 31 May 2026"
Row 2: period "April 2026", supporting "Closing balance: £2,610.40", trailing date "1 Apr 2026 – 30 Apr 2026"
Row 3: period "March 2026", supporting "Closing balance: £2,314.92", trailing date "1 Mar 2026 – 31 Mar 2026"
Row 4: period "February 2026", supporting "Closing balance: £1,988.57", trailing date "1 Feb 2026 – 28 Feb 2026"
Row 5: period "January 2026", supporting "Closing balance: £1,754.10", trailing date "1 Jan 2026 – 31 Jan 2026"
Row 6: period "December 2025", supporting "Closing balance: £1,502.88", trailing date "1 Dec 2025 – 31 Dec 2025"

### Divider Between Rows

Between each pair of consecutive statement rows, place a `Divider` component: a horizontal line, 393dp wide, 1dp tall, fill `color/outlineVariant` (#C1C7CE). No corner radius. No top/bottom padding. There are five dividers total (between rows 1–2, 2–3, 3–4, 4–5, 5–6). There is no divider after the final row.

### Content Area Auto Layout

Wrap the six rows and five dividers inside a vertical Auto Layout frame named `statements_list`. Set this frame to: width fill (393dp), height hug, no padding (padding is inside each row), gap 0 between children. This simulates the LazyColumn. Clip content if the total height exceeds the available content area — engineers will scroll this at runtime.

### Download In-Progress Variant

Create an additional content sub-variant frame showing the download in-progress state for Row 1 (May 2026). In this variant, the `download_statement_button` for the May 2026 row shows a CircularProgressIndicator spinner instead of the file_download icon. All other rows remain unchanged. Label this frame "Content — Downloading May 2026" and place it to the right of the main Content frame.

---

## 6. State: Empty

### Frame Description

The Empty frame is shown when the HSBC AIS endpoint returns an empty `Data.Statement` array — meaning the account has no statement history yet (a newly opened account, or no statements in the accessible consent period). The content area is vertically and horizontally centred.

### Empty State Component

Create a component named `EmptyState/Statements`. Place it in the content area (393×708dp) using an Auto Layout column with: vertical and horizontal alignment centre, padding 32dp on all sides, gap 8dp between children except after the icon where the gap is 16dp.

Place the following elements top-to-bottom:

First, a `description` Material Symbol icon at 48×48dp, tinted `color/onSurfaceVariant` (#41474D). Set the `contentDescription` accessibility property to "No statements". This is a document/file icon that communicates the data type of this screen.

Second, a spacer of 16dp height.

Third, a Text element with the text "No statements yet", applying `titleMedium` style (Roboto 16/24 Medium, colour `color/onSurface` #181C20), centre-aligned.

Fourth, a spacer of 8dp height.

Fifth, a multi-line Text element with the text "Statements will appear here once your account generates periodic statements. They are produced monthly by HSBC." Apply `bodyMedium` style (Roboto 14/20 Regular, colour `color/onSurfaceVariant` #41474D), centre-aligned, with horizontal padding 32dp so the line length is comfortable. Limit to approximately 280dp maximum line width at this font size.

There is no call-to-action button on the empty state — the user cannot take any action to create statements; they are generated by the bank.

---

## 7. State: Error

### Frame Description

The Error frame is shown when the AIS call fails. The most common failure in the HSBC Open Banking sandbox is HTTP 401 (access token expired). The content area shows a centred error icon, error title, the localised error message from the ViewModel, and a "Try again" filled button.

### Error State Component

Create a component named `EmptyState/Error/Statements`. Place it in the content area using the same centred column layout as the empty state: Auto Layout column, vertical and horizontal alignment centre, padding 32dp all sides.

Place the following elements:

First, an `error_outline` Material Symbol icon at 48×48dp, tinted `color/error` (#BA1A1A). Set `contentDescription` to "Error loading statements."

Second, a spacer of 16dp height.

Third, a Text element with the text "Unable to load statements", applying `titleMedium` style (Roboto 16/24 Medium, colour `color/onSurface` #181C20), centre-aligned.

Fourth, a spacer of 8dp height.

Fifth, a Text element showing the error body message. For the demo scenario (HTTP 401), this reads: "Session expired. Please re-authenticate." Apply `bodyMedium` style (Roboto 14/20 Regular, colour `color/onSurfaceVariant` #41474D), centre-aligned. In the design, annotate this text node with a note: "Dynamic — resolved from ViewModel error map. 401: 'Session expired. Please re-authenticate.' / 403: 'Consent does not include ReadStatements.' / 429: 'Too many requests. Please wait and retry.' / network: localised device message." This documents the four error variants without needing four separate frames.

Sixth, a spacer of 24dp height.

Seventh, the Retry Button. Create a `Button/Filled` component instance with the label text "Try again" (Roboto labelLarge 14/20 Medium, colour #FFFFFF). Fill the button background with `color/primary` (#266489). Set corner radius to 20dp (the `ui.yaml` declares cornerRadius 20dp and horizontalPadding 24dp). The button height is 48dp minimum. Add horizontal padding inside the button of 24dp left and right so the button wraps the label with comfortable breathing room. The minimum touch target is 48dp. Set `contentDescription` to "Retry loading statements."

In the Figma prototype, add a tap interaction on the retry button: "On Tap → Navigate to Loading frame" (representing the in-flight state that follows a retry tap).

### Error State Variants

Create two component variants of the error state to cover the main cases a designer needs to handoff:

Variant 1 (shown in the main Error frame): HTTP 401 — "Session expired. Please re-authenticate." — retry button visible.

Variant 2 (supplementary, smaller annotation frame): HTTP 403 — "Consent does not include ReadStatements." — retry button visible (the user can navigate to consent management to fix this, though the retry itself will also re-trigger auth).

---

## 8. Component Variants and Interactive States

### StatementRow Variants

The `StatementRow` component should have three interactive states, implemented as Figma variants on a single component set:

**Default (rest):** Background #F7F9FF, no overlay. Download icon visible in primary blue.

**Pressed:** Overlay the row with `color/onSurface` (#181C20) at 8% opacity, applied as a fill on a full-size overlay frame within the component. This matches the M3 press state ripple approximation for static Figma. The download button area is excluded from this press ripple if the user presses the icon button — annotate this edge case.

**Downloading (in-progress):** The `isDownloading` variant property set to true on the download icon button. The file_download icon is replaced by a CircularProgressIndicator at 24dp diameter, 2dp stroke, tint #266489. The row body itself remains in the rest state (no press overlay).

### Download IconButton Variants

The `IconButton/Download` component should have two variants:

**Idle:** A 48×48dp transparent touch target with a `file_download` icon (24dp, tint #266489) centred inside. Hover state: add `color/primary` (#266489) at 8% opacity as a circular fill (radius 9999dp) on the 40dp inner area.

**In-progress:** Replace the icon with a circular progress spinner frame. Represent this in Figma as a 24dp circle with a 2dp stroke arc covering 270° (three-quarters of the circle), tinted #266489. Annotate: "Engineers implement as M3 CircularProgressIndicator with modifier size 24dp."

### Retry Button Variants

The `Button/Filled/Retry` component should have: default (bg #266489, label #FFFFFF), pressed (bg darkened by 8% overlay, label #FFFFFF), and disabled (bg #DDE3EA, label #41474D, not used in this screen but document for consistency).

---

## 9. Auto Layout Specifications

### Top App Bar (TopAppBar/Small/Statements)
Direction: horizontal. Padding: top 20dp, bottom 20dp, left 4dp, right 16dp. Item spacing: 0 (icon button + title span). Alignment: centre vertical. Sizing: fixed width 393dp, fixed height 64dp.

### Statement Row (StatementRow)
Direction: horizontal. Padding: top 12dp, bottom 12dp, left 16dp, right 8dp. Item spacing: 8dp. Alignment: centre vertical. Sizing: fill width (393dp), hug height (min 72dp).

Inner text column: direction vertical, gap 4dp, alignment leading, sizing fill width (weight 1).

Inner trailing column: direction vertical, gap 4dp, alignment trailing, sizing hug.

### Skeleton Column (loading state)
Direction: vertical. Padding: top 16dp, horizontal 16dp. Item spacing: 12dp. Sizing: fill width, hug height.

### Empty / Error State Column
Direction: vertical. Padding: 32dp all sides. Item spacing: 8dp (except 16dp after icon). Alignment: centre horizontal and vertical. Sizing: fill width and height.

### Bottom Navigation Bar
Direction: horizontal. Padding: 0. Item spacing: 0. Sizing: fixed 393×80dp. Each tab: direction vertical, item spacing 4dp, alignment centre horizontal and vertical, sizing fill (25% each).

---

## 10. Prototype Interaction Flow

Document the following interaction flows in the Figma prototype panel:

**Row tap (Content state):** On Tap on any `StatementRow` (excluding the download button touch area) → Navigate to the `statement-detail` screen frame. Apply "Smart Animate" with "Ease Out" easing, 300ms duration. This models the M3 navigation transition.

**Download button tap (idle):** On Tap on `IconButton/Download` (idle variant) → Switch component variant to in-progress. After a simulated delay (2000ms in prototype), switch back to idle. In the real implementation, this is driven by `downloadState[statementId]` in the ViewModel. Annotate on the prototype frame: "Engineers: component reacts to `downloadState[statementId] == InProgress`; download success opens platform share sheet / saves to Downloads folder."

**Retry button tap (error state):** On Tap on retry button → Navigate to Loading frame → After 1500ms delay → Navigate to Content frame. This simulates a successful retry. Annotate: "In the real app, retry triggers `retryLoad(accountId)` which delegates to `statementsLoad(accountId)`. Result determines which state follows Loading."

**Back navigation:** On Tap on arrow_back in the top app bar → Navigate back (or explicitly navigate to `account-detail` frame). Apply "Move In from Left" or Smart Animate reverse direction.

---

## 11. Semantic Token to Figma Variable Mapping Table

Use this table to wire all Figma colour styles and variables to their semantic counterparts. Apply variables — not raw hex values — to all components so that a light/dark mode switch can be implemented later by swapping the variable collection.

| Semantic usage in this screen | Figma variable to apply |
|---|---|
| Screen background | color/background → #F7F9FF |
| Top app bar background | color/surface → #F7F9FF |
| Top app bar back icon | color/primary → #266489 |
| Top app bar title text | color/onSurface → #181C20 |
| Statement row background | color/surface → #F7F9FF |
| Statement row period label | color/onSurface → #181C20 |
| Statement row supporting text | color/onSurfaceVariant → #41474D |
| Statement row date trailing | color/onSurfaceVariant → #41474D |
| Download icon (idle) | color/primary → #266489 |
| Download spinner | color/primary → #266489 |
| Row press ripple overlay | color/onSurface → #181C20 at 8% |
| Row divider | color/outlineVariant → #C1C7CE |
| Skeleton shimmer fill | color/surfaceVariant → #DDE3EA |
| Empty state icon | color/onSurfaceVariant → #41474D |
| Empty state title | color/onSurface → #181C20 |
| Empty state body | color/onSurfaceVariant → #41474D |
| Error icon | color/error → #BA1A1A |
| Error title | color/onSurface → #181C20 |
| Error body | color/onSurfaceVariant → #41474D |
| Retry button fill | color/primary → #266489 |
| Retry button label | color/onPrimary → #FFFFFF |
| Bottom nav background | color/surface → #F7F9FF |
| Bottom nav icon/label (unselected) | color/onSurfaceVariant → #41474D |
| Bottom nav icon/label (selected) | color/primary → #266489 |
| Bottom nav top border | color/outlineVariant → #C1C7CE |

---

## 12. Accessibility Annotations

Add an "Accessibility" annotation layer group on each frame. Use the Figma Accessibility Annotation Kit (or a custom annotation component) to mark the following:

On the `TopAppBar`: annotate arrow_back with role=button, label="Back", min-touch=48dp. Ensure colour contrast of #266489 on #F7F9FF passes WCAG AA (contrast ratio 4.89:1, passes AA for large text / icons; passes AA for normal text if ≥18px).

On each `StatementRow`: annotate the row as role=button, label="[period] statement, closing balance [amount], [start]–[end]. Double-tap to open detail." Annotate `download_statement_button` separately as role=button, label="Download [period] statement", min-touch=48dp.

On `empty_statements`: annotate icon as decorative=false, label="No statements". Mark the title and body as a live region so screen readers announce the state change.

On `error_state`: annotate icon as decorative=false, label="Error loading statements". Mark the title, body, and button as a live region. Annotate `retry_button` as role=button, label="Retry loading statements", min-touch=48dp.

On `BottomNav`: each tab annotates as role=tab, selected=false (for this sub-screen context). Tab labels are always visible (not tooltip-only).

Minimum contrast requirements: All body text (#41474D on #F7F9FF) achieves 4.89:1 — passes WCAG AA. Primary text (#181C20 on #F7F9FF) achieves 14.6:1 — passes WCAG AAA. Error icon (#BA1A1A on #F7F9FF) achieves 4.72:1 — passes WCAG AA for graphical elements.

---

## 13. Design Handoff Notes for Engineers

The `StatementsViewModel` exposes a `StatementsState` with two fields: `uiState: StatementsUiState` (sealed class with Loading / Content / Empty / Error members) and `downloadState: Map<String, DownloadState>` where keys are StatementIds and values are InProgress or Idle.

The statement row's download button switches between idle and in-progress states by observing `downloadState[item.StatementId]`. The button stops event propagation so that tapping the download icon does not simultaneously trigger the row navigation to statement-detail.

The content list is a `LazyColumn` consuming `items(statements)` where statements is a `List<StatementRowUiModel>` sorted descending by StartDateTime. Each `StatementRowUiModel` carries: `StatementId`, `StatementReference`, `periodLabel` (e.g. "May 2026"), `closingBalanceFormatted` (e.g. "£2,847.63"), `startDateFormatted` (e.g. "1 May 2026"), `endDateFormatted` (e.g. "31 May 2026"). All formatting is done by the ViewModel using `kotlinx-datetime` — the UI layer receives pre-formatted strings.

The retry button's on-click calls `retryLoad(accountId)` which delegates to `statementsLoad(accountId)`, resetting `uiState` to Loading before re-issuing the API call.

For the download flow: `downloadStatement(statementId, accountId)` calls `GET /accounts/{accountId}/statements/{statementId}/file` with `Accept: application/pdf, text/csv`. On success, bytes are dispatched to the platform file handler (Android ShareSheet / iOS share extension). On HTTP 501, a toast is shown: "Statement download not available for this account type." On network error, a toast shows a generic error message. All toasts use the snackbar host declared in `app-shell.yaml`.

---

## 14. Figma File Structure Recommendation

Organise the Figma file as follows to align with the project's layer model:

Create a top-level page named "Statements Screen". Within it, create three sections:

Section 1: "All States" — place the four main frames (Loading, Content, Content-Downloading, Empty, Error) left-to-right with 48dp spacing. Add a frame label above each using the Figma section header text.

Section 2: "Components" — place all reusable component sets: `StatementRow` (3 variants), `IconButton/Download` (2 variants), `Skeleton/ListRow`, `EmptyState/Statements`, `EmptyState/Error/Statements`, `Button/Filled/Retry`, `TopAppBar/Small/Statements`, `BottomNav/OpenBanking`. These should be published to the team library so they can be consumed by other screens in the Open Banking project.

Section 3: "Interaction Annotations" — copy the Content frame and annotate each interactive element with an arrow and label: navigate_statement_detail (row tap), download_statement (download button tap), navigate_back (arrow_back tap), retry_load (retry button tap — visible on Error frame only).

Add a cover frame at the top of the file with the project name "mifos-x-open-banking", screen name "Statements", design system "Open Banking — Trust Blue M3", and the generated date "2026-07-16".
