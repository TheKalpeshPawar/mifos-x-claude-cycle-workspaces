---
ui_yaml_sha: sha256:standing-order-create-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: standing-order-create-loading-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form_screen

feature: standing-order-create
state: loading
state_visibility: loading
viewmodel: CreateStandingOrderViewModel

generated_by: /idea-render-screen (LLM-local authored)
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# standing-order-create — loading state

> Authored locally from screens/standing-order-create/ui.yaml (LLM-local render path; no Stitch SDK).
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md (design-tokens.yaml schema v3.0).

↓↓↓ MOCKUP PROMPT

Design the **loading** state of the New-Standing-Order screen for **mifos-x-open-banking** (Open Banking KMP super-app, Material 3, light theme, 390×844dp, Outfit font). form_screen archetype. This is `form.loadingPayees` — the source account and its beneficiaries are resolving before the form can render.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, background #F9FAEF, surface #FFFFFF, on_surface_variant #44483D, outline_variant #C5C8BA, surface_variant #E1E4D5.

Top app bar: back arrow + title "New Standing Order". No bottom navigation.

**Component 1 - Loading indicator** (centered, full width): a centered M3 circular progress indicator in primary #4C662B on the #F9FAEF background, vertically centered in the content area, with a quiet caption below it reading "Loading accounts and payees". Generous vertical padding (spacing.xl / 32dp). Use a static placeholder if reduced motion is preferred.

DO NOT use em-dash anywhere in text. DO NOT break the page theme. DO NOT add form fields — this state shows only the loading indicator.

Quiet, centered loading surface on #F9FAEF — measured motion (dial 3), no busy skeletons. The single primary-green spinner reassures without distraction.
↑↑↑ MOCKUP PROMPT
