---
ui_yaml_sha: sha256:standing-order-create-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: standing-order-create-submitting-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form_screen

feature: standing-order-create
state: submitting
state_visibility: submitting
viewmodel: CreateStandingOrderViewModel

generated_by: /idea-render-screen (LLM-local authored)
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# standing-order-create — submitting state

> Authored locally from screens/standing-order-create/ui.yaml (LLM-local render path; no Stitch SDK).
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md (design-tokens.yaml schema v3.0).

↓↓↓ MOCKUP PROMPT

Design the **submitting** state of the New-Standing-Order screen for **mifos-x-open-banking** (Open Banking KMP super-app, Material 3, light theme, 390×844dp, Outfit font). form_screen archetype. This is `form.submitting` — the OBP POST is in flight. The form stays visible and filled but the submit button is disabled and shows a busy label.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, secondary #386663, background #F9FAEF, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, outline_variant #C5C8BA.

Top app bar: back arrow + title "New Standing Order". No bottom navigation.

**Component 1 - From account** (read-only outlined field): "Primary Checking · DE89 ·· 0130", expand_more chevron. Visually dimmed/non-interactive while submitting.

**Component 2 - Pay to** (read-only outlined field): "John Smith · Lloyds Bank", expand_more chevron. Dimmed while submitting.

**Component 3 - Amount** (outlined text field): "250.00", suffix "EUR", supporting text "Amount taken on each payment date". Dimmed while submitting.

**Component 4 - Repeats label** (caption): "Repeats".

**Component 5 - Frequency chips** (filter chip group): Daily, Weekly, Fortnightly, Monthly, Yearly — "Monthly" selected. Dimmed while submitting.

**Component 6 - First payment date** (read-only field): "15 Jul 2026", calendar_today icon, supporting text "First payment runs on this date". Dimmed.

**Component 7 - Recurrence hint** (small primary text): "Repeats on the 15th of each month".

**Component 8 - End date** (read-only field, optional): "End date (optional)", empty, calendar_today icon, supporting "Leave empty to pay until cancelled". Dimmed.

**Component 9 - Create button** (filled primary button, full width, DISABLED): reduced-opacity primary fill, a small inline circular spinner before the label, text "Creating…". Not pressable.

DO NOT use em-dash anywhere in text. DO NOT show an error message in this state. DO NOT make the button look pressable.

The only motion is the inline button spinner — measured motion (dial 3). The dimmed form communicates the request is committing without hiding the entered values.
↑↑↑ MOCKUP PROMPT
