---
ui_yaml_sha: sha256:standing-order-create-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: standing-order-create-content-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form_screen

feature: standing-order-create
state: content
state_visibility: content
viewmodel: CreateStandingOrderViewModel

generated_by: /idea-render-screen (LLM-local authored)
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# standing-order-create — content state

> Authored locally from screens/standing-order-create/ui.yaml (LLM-local render path; no Stitch SDK).
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md (design-tokens.yaml schema v3.0).

↓↓↓ MOCKUP PROMPT

Design the **content** state of the New-Standing-Order screen for **mifos-x-open-banking**, an Open Banking KMP super-app (consumer retail banking + field-officer agent banking on Open Bank Project API v7, Compose Multiplatform). Material 3, light theme, 390×844dp mobile baseline, Outfit font throughout. form_screen archetype — a vertically scrolling form on the #F9FAEF warm off-white background, single white form card, no bottom nav.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, secondary #386663, error #BA1A1A, background #F9FAEF, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, outline_variant #C5C8BA.

Top app bar: back arrow + title "New Standing Order". No bottom navigation (this is a focused create flow).

**Component 1 - From account** (read-only outlined field, full width): label "From account", value "Primary Checking · DE89 ·· 0130", trailing expand_more chevron. Opens the account picker. Tapping switches the source account and reloads the payee list.

**Component 2 - Pay to** (read-only outlined field, full width): label "Pay to", value "John Smith · Lloyds Bank", trailing expand_more chevron. Opens a dropdown of the source account's existing beneficiaries.

**Component 3 - Amount** (outlined text field, full width): label "Amount", value "250.00", trailing currency suffix "EUR", supporting text "Amount taken on each payment date".

**Component 4 - Repeats label** (caption text): "Repeats" in on_surface_variant.

**Component 5 - Frequency chips** (horizontal filter chip group): Daily, Weekly, Fortnightly, Monthly, Yearly. "Monthly" is the selected chip (primary_container fill). Maps to STANDING_ORDER_FREQUENCIES (DAILY/WEEKLY/BI-WEEKLY/MONTHLY/YEARLY; BI-WEEKLY shown as "Fortnightly").

**Component 6 - First payment date** (read-only outlined field, full width): label "First payment date", value "15 Jul 2026", trailing calendar_today icon, supporting text "First payment runs on this date". This is the recurrence anchor.

**Component 7 - Recurrence hint** (small text in primary green): "Repeats on the 15th of each month". Derived from frequency + chosen first-payment date.

**Component 8 - End date** (read-only outlined field, full width): label "End date (optional)", placeholder/value empty, trailing calendar_today icon, supporting text "Leave empty to pay until cancelled".

**Component 9 - Create button** (filled primary button, full width): primary #4C662B fill, on_primary white text "Create standing order", pill/12dp radius.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full scrollable form on #F9FAEF. The #4C662B accent appears on the selected frequency chip, the recurrence hint, and the submit button — trust-first density (dial 5) with measured motion (dial 3) calibrated to the taste-default aesthetic.
↑↑↑ MOCKUP PROMPT
