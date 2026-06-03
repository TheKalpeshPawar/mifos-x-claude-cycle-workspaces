---
ui_yaml_sha: sha256:agent-registration-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: agent-registration-content-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: content
state_visibility: content
viewmodel: AgentRegistrationViewModel

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# agent-registration — content state

> Generated from screens/agent-registration/ui.yaml (enriched 2026-06-02: viewmodel + states_handled + obp_create_agent binding)
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **content** state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking. This state is identical to idle — it is the default loaded view showing a ready-to-fill registration form.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #4C662B, secondary #386663, background #F9FAEF, on_surface #1A1C16, surface_variant #E1E4D5, on_surface_variant #44483D, error #BA1A1A, outline #E1E4D5, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #1A1C16. Back arrow icon left. Background #FFFFFF, zero elevation. No bottom nav.

**Component 2 — Header Block** (full width minus 40dp insets, top margin 16dp): Title "Agent Registration" Outfit Bold 32sp #4C662B. Subtitle "Register to become an authorised OBP field agent with your bank" Outfit Regular 14sp #44483D, top margin 4dp, bottom margin 24dp.

**Component 3 — Legal Name Field** (full width minus 40dp insets): Label "Legal Name" Outfit SemiBold 12sp #44483D, bottom margin 6dp. Outlined text field 56dp tall, corner radius 12dp, outline #E1E4D5, background #FFFFFF. Populated value "Amara Osei" 14sp #1A1C16. Bottom margin 4dp.

**Component 4 — Phone Number Row** (full width minus 40dp insets): Label "Mobile Phone Number" Outfit SemiBold 12sp #44483D, bottom margin 6dp. Horizontal row: static prefix box "+254" (#F9FAEF bg, 12dp radius, 1dp #E1E4D5 border, body_medium #1A1C16 SemiBold) + flex phone input "712 345 678" (same outlined style). Bottom margin 4dp.

**Component 5 — Agent Number Field** (full width minus 40dp insets): Label "Agent Number" Outfit SemiBold 12sp #44483D, bottom margin 6dp. Outlined text field; value "AGT-2026-00142" 14sp #1A1C16; corner radius 12dp, outline #E1E4D5. Bottom margin 4dp.

**Component 6 — Currency Selector** (full width minus 40dp insets): Label "Operating Currency" Outfit SemiBold 12sp #44483D, bottom margin 6dp. Combobox outlined field; value "KES — Kenyan Shilling" 14sp #1A1C16; expand_more trailing icon #44483D; corner radius 12dp, outline #E1E4D5. Bottom margin 4dp.

**Component 7 — Services Chip Group** (full width minus 40dp insets, top margin 8dp): Label "Supported Services" Outfit SemiBold 12sp #44483D, bottom margin 10dp. Wrap chip group, 8dp gap: "Cash Deposit" (selected: #4C662B bg / #FFFFFF label / 20dp radius), "Cash Withdrawal" (selected), "Account Opening" (unselected: #CDEDA3 bg / #4C662B label / #4C662B border 1dp), "Bill Payment" (unselected), "Fund Transfer" (unselected). Bottom margin 24dp.

**Component 8 — Commission Rate Field** (full width minus 40dp insets): Label "Commission Rate (%)" Outfit SemiBold 12sp #44483D, bottom margin 6dp. Outlined decimal field; value "1.5" 14sp #1A1C16; percent trailing icon #44483D; corner radius 12dp, outline #E1E4D5. Bottom margin 28dp.

**Component 9 — Register Button** (full width minus 40dp insets): Filled button 56dp tall, corner radius 14dp, background #4C662B, label "Register as Agent" Outfit SemiBold 16sp #FFFFFF centered. Elevation 2dp. Bottom margin 12dp. Bound to obp_create_agent (POST /obp/v5.1.0/banks/{bankId}/agents).

**Component 10 — Terms Notice**: "By registering, you agree to the Mifos Agent Terms and Conditions" Outfit Regular 12sp #44483D centred, horizontal padding 20dp, bottom margin 24dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #F9FAEF. The #CDEDA3 unselected chips with #4C662B selected chips and the earth-green filled submit button create a focused, accessible form composition aligned with field-officer finance workflows.

↑↑↑ MOCKUP PROMPT
