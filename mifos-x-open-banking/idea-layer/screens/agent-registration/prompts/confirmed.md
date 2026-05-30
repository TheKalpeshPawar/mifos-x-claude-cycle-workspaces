---
ui_yaml_sha: a468125e1106b883f7fa067dc586fd6b137420230253c4e395c0ea724594b5e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: e032f112a8d332682e8f768babf736e1facbe43aee6929146ac627c906f0bc49

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: confirmed
state_visibility: confirmed

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# agent-registration — confirmed state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA e27e494ce8c400c9
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the confirmed state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Confirmed Status Banner** (full width minus 32dp insets, top margin 32dp, background #354E16, 12dp corner radius, 20dp padding): Card with Row layout. Leading verified-agent icon 32dp #CDEDA3. Right column: title "Agent Confirmed" Outfit SemiBold 18sp #CDEDA3, body "You are registered as an active Mifos field agent. You can now onboard customers and process transactions." Outfit Regular 14sp #A0CFCB, top margin 4dp. form archetype.

**Component 3 — Agent Details Card** (full width minus 32dp insets, top margin 16dp, background #1E201A, 12dp corner radius, 16dp padding): Read-only rows for "Legal Name", "Agent Number", "Operating Currency", "Supported Services" (chips: Cash Deposit, Cash Withdrawal, Account Opening, Bill Payment, Fund Transfer), "Commission Rate (%)". Each row 48dp, label 12sp #8F9285, value 14sp #E3E3D8, divider #44483D between rows.

**Component 4 — Button** (full width minus 32dp insets, top margin 24dp, bottom margin 32dp): Filled pill Button 48dp tall, corner radius 999, background #B2D188, label "Go to Dashboard" Outfit SemiBold 16sp #1F3701 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Layout on #12140E. The deep green #354E16 confirmation banner radiates financial approval and institutional trust; the #B2D188 dashboard button invites the newly confirmed agent forward with calm confidence.

↑↑↑ MOCKUP PROMPT
