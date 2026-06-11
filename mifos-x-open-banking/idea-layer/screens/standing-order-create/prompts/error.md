---
ui_yaml_sha: sha256:standing-order-create-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: standing-order-create-error-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form_screen

feature: standing-order-create
state: error
state_visibility: error
viewmodel: CreateStandingOrderViewModel

generated_by: /idea-render-screen (LLM-local authored)
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# standing-order-create — error state

> Authored locally from screens/standing-order-create/ui.yaml (LLM-local render path; no Stitch SDK).
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md (design-tokens.yaml schema v3.0).

↓↓↓ MOCKUP PROMPT

Design the **error** state of the New-Standing-Order screen for **mifos-x-open-banking** (Open Banking KMP super-app, Material 3, light theme, 390×844dp, Outfit font). form_screen archetype. This is `form.error` non-null — a validation failure or a failed POST. The form stays fully editable; an inline error message appears above the button.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, secondary #386663, error #BA1A1A, error_container #FFDAD6, background #F9FAEF, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, outline_variant #C5C8BA.

Top app bar: back arrow + title "New Standing Order". No bottom navigation.

**Component 1 - From account** (read-only outlined field): "Primary Checking · DE89 ·· 0130", expand_more chevron.

**Component 2 - Pay to** (read-only outlined field): "John Smith · Lloyds Bank", expand_more chevron.

**Component 3 - Amount** (outlined text field): "250.00", suffix "EUR", supporting text "Amount taken on each payment date".

**Component 4 - Repeats label** (caption): "Repeats".

**Component 5 - Frequency chips** (filter chip group): Daily, Weekly, Fortnightly, Monthly, Yearly — "Monthly" selected.

**Component 6 - First payment date** (read-only field, ERROR): label "First payment date", value "10 Jun 2026", calendar_today icon. Border and supporting text in error #BA1A1A because the chosen date is not strictly after today.

**Component 7 - Recurrence hint** (small primary text): "Repeats on the 10th of each month".

**Component 8 - End date** (read-only field, optional): "End date (optional)", empty, calendar_today icon, supporting "Leave empty to pay until cancelled".

**Component 9 - Inline error text** (error #BA1A1A, small): "Start date must be after today". role=alert. Sits directly above the button.

**Component 10 - Create button** (filled primary button, full width, ENABLED): primary #4C662B fill, white text "Create standing order". The form is still submittable after the user corrects the date.

DO NOT use em-dash anywhere in text. DO NOT mix the error #BA1A1A and pending #E8A317 colors. DO NOT hide the entered values — the user fixes one field, not the whole form.

The error red appears only on the offending date field and the inline message — everything else keeps the calm taste-default surface. Measured motion (dial 3).
↑↑↑ MOCKUP PROMPT
