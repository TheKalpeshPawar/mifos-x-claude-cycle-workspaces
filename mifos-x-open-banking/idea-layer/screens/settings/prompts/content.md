---
ui_yaml_sha: 7077f6e070d0a7f1125c62a5ea1cc4d67d31364ecad1feced39956a7353733f4
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 8fd9b20890bfa63b6cd0f3edeaeedcac7de4acf22ff321e23efc6e90f64723b0

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: settings
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — content state

> Auto-generated from screens/settings/ui.yaml @ SHA 57cc58437ce99bc3
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the settings screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Settings" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Card** (full width minus 32dp insets, top margin 24dp, 12dp corner radius, background #1E201A): Section header "Appearance" Outfit Medium 12sp #8F9285 uppercase with 16dp padding. settings archetype. Two List Rows separated by 1dp divider #44483D. Row 1: leading moon icon 20dp #B2D188, title "Dark Mode" Outfit Medium 14sp #E3E3D8, subtitle "Switch to a darker color scheme" Outfit Regular 12sp #8F9285, trailing toggle switch ON state track #354E16 thumb #B2D188. Row 2: leading globe icon 20dp #A0CFCB, title "Language" Outfit Medium 14sp #E3E3D8, subtitle "Choose your preferred display language" Outfit Regular 12sp #8F9285, trailing "English" Outfit Regular 13sp #C5C8BA + chevron 16dp #44483D.

**Component 3 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header "Notifications" Outfit Medium 12sp #8F9285 uppercase. Three List Rows with 1dp dividers #44483D. Row 1: bell icon 20dp #B2D188, "Push Notifications" title, "Receive alerts and updates from Mifos X" subtitle 12sp #8F9285, trailing toggle ON #354E16 #B2D188. Row 2: alert-circle icon 20dp #B2D188, "Transaction Alerts" title, "Notify me for every debit and credit activity" subtitle, trailing toggle ON. Row 3: megaphone icon 20dp #A0CFCB, "Marketing Updates" title, "Product news and promotions" subtitle, trailing toggle OFF track #44483D thumb #8F9285.

**Component 4 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header "Security" Outfit Medium 12sp #8F9285 uppercase. Three List Rows. Row 1: fingerprint icon 20dp #B2D188, "Biometric Login" title, "Use fingerprint or face ID to sign in faster" subtitle, toggle ON. Row 2: shield icon 20dp #A0CFCB, "Data and Consent" title, "Manage your data sharing consents" subtitle, trailing chevron 16dp #44483D. Row 3: lock icon 20dp #A0CFCB, "Change Password" title, "Update your account login password" subtitle, trailing chevron 16dp #44483D.

**Component 5 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A, bottom margin 32dp): Section header "About" Outfit Medium 12sp #8F9285 uppercase. Four List Rows. Row 1: info icon 20dp #A0CFCB, "About Mifos X Open Banking" Outfit Medium 14sp #E3E3D8, trailing chevron. Row 2: file-text icon 20dp #A0CFCB, "Terms of Service" Outfit Medium 14sp #E3E3D8, trailing chevron. Row 3: eye icon 20dp #A0CFCB, "Privacy Policy" Outfit Medium 14sp #E3E3D8, trailing chevron. Row 4: code icon 20dp #A0CFCB, "Open-source Licences" Outfit Medium 14sp #E3E3D8, trailing chevron. Below cards: "App Version" label Outfit Regular 13sp #8F9285 left-aligned, "v1.0.0" right-aligned same style #44483D, both on plain #12140E background.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E with four grouped card sections. The earthy green #B2D188 on active toggle thumbs and biometric icon provides a clear visual signal of enabled features, keeping the layout minimal and restrained for this regulated open banking platform.
↑↑↑ MOCKUP PROMPT
