---
ui_yaml_sha: ed2405e9b0ab40e84eddfcb7e669dd5d6df03b6a59f4997cb41c63dd2313c905
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5ff923164909d4610bba309cd96fdc52c545131ebe04f0c0e277cb15a9976eef

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-profile
state: saving
state_visibility: saving

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-profile — saving state

> Auto-generated from screens/customer-profile/ui.yaml @ SHA 1505ecdefbe53630
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the saving state of the customer-profile screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Saving..." Outfit Medium 18sp #E3E3D8 centered with circular progress indicator 20dp #B2D188 trailing. Leading back-arrow 24dp #8F9285 (disabled, muted). Background #12140E.

**Component 2 — List Row** (full width minus 32dp insets, top margin 24dp): Section heading "Personal Information" Outfit SemiBold 14sp #B2D188. surface_container #1E201A card, 12dp radius. All fields visible but disabled (opacity 0.5): "Full Name" / "John Kamau Mwangi", "Date of Birth" / "14 March 1985 (Age: 41)", "National ID" / "KE12345678", "Tax PIN (KRA)" / "A001234567M", "Phone" / "+254 722 123 456", "Email" / "john.mwangi@gmail.com". Each 56dp, label Outfit Regular 12sp #8F9285, value Outfit Medium 15sp #E3E3D8 at 50% opacity, 1dp #44483D dividers.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading "Address" Outfit SemiBold 14sp #B2D188 (50% opacity). Rows: "123 Moi Avenue, Nairobi", "Nairobi County, Kenya", "Postcode: 00100", all Outfit Medium 15sp #E3E3D8 at 50% opacity.

**Component 4 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading "Employment" Outfit SemiBold 14sp #B2D188 (50% opacity). Rows: "Safaricom PLC", "KES 85,000", "Permanent" all at 50% opacity.

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled button 48dp tall, 12dp radius, background #354E16 (dimmed variant), circular progress 18dp #B2D188 left, label "Saving..." Outfit SemiBold 15sp #CDEDA3 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E with disabled opacity overlay. Anchored by #B2D188 on the spinner and #354E16 on the saving button, the layout stays calm and restrained, communicating progress without alarm.
↑↑↑ MOCKUP PROMPT
