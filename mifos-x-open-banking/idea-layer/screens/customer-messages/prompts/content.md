---
ui_yaml_sha: 1983cf22e27c82c37217e6ab750b592b1c3060b8a44f50772fe8f978542b961c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: deb1516e44affa1a33c450ce5b4526efdfe8874974784a1995aea2109e9d4aa4

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-messages
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-messages — content state

> Auto-generated from screens/customer-messages/ui.yaml @ SHA c2f35234fef331d8
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the customer messages screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Messages" Outfit Medium 18sp #E3E3D8 left, "5 unread" badge 20dp tall filled #E8A317 Outfit Medium 11sp #000000 right. Background #12140E.

**Component 2 — Text Field** (lookup bar, full width minus 32dp insets, 48dp tall, 24dp corner radius, top margin 8dp, background #1E201A, leading find icon 20dp #8F9285, placeholder "Find messages" Outfit Regular 14sp #8F9285, outline 1dp #44483D).

**Component 3 — List Row** (thread 1, full width, 72dp tall, background #12140E): Avatar circle 40dp initials "JM" Outfit Bold 16sp #1F3701 background #B2D188 left 16dp. Content: "John Mwangi" Outfit SemiBold 14sp #E3E3D8 left, "2 min ago" Outfit Regular 12sp #8F9285 right. Below: "Please send me the account statement for..." Outfit Regular 13sp #C5C8BA left, unread dot 8dp filled #B2D188 right. Divider 1dp #44483D bottom.

**Component 4 — List Row** (thread 2, same style, 72dp tall): Avatar "SO" initials background #1F4E4B. "Sarah Odhiambo", "1 hr ago". "Thank you for approving my application!" Outfit Regular 13sp #8F9285.

**Component 5 — List Row** (thread 3, same style, 72dp tall): Avatar "PK" initials background #354E16. "Peter Kamau", "Yesterday". "When can I expect my card to arrive?" Outfit Regular 13sp #8F9285.

**Component 6 — FAB** (bottom right 56dp circle, background #B2D188, compose icon 24dp #1F3701, label "New Message" Outfit Medium 13sp #1F3701).

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The warm amber #E8A317 unread badge signals actionable items urgently, while the sage-green #B2D188 on read avatars and FAB ties the interface back to the app's trustworthy financial identity.

↑↑↑ MOCKUP PROMPT
