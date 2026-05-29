---
ui_yaml_sha: 3fd23727025f84161f07e7aec5d0eac94651cf54a8c6617a21f7b92e54ebab5a
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 6b793b5b0a3a9f4a25713e6789c1caab17807421b18ce54509216e96b56f5953

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: notifications
state: populated
state_visibility: populated

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# notifications — populated state

> Auto-generated from screens/notifications/ui.yaml @ SHA 507a54465bcd7622
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the populated state of the notifications screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Notifications" Outfit Medium 18sp #E3E3D8 left-aligned 16dp. Trailing text Button "Mark all read" Outfit Medium 14sp #B2D188. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Section Label Today** (full width minus 32dp insets, top margin 16dp): "Today" Outfit SemiBold 12sp #8F9285, uppercase letter-spacing 0.5.

**Component 3 — List Row** (full width minus 32dp insets, 72dp tall, top margin 4dp): Surface #1E201A, 12dp radius. Leading 40dp circle #354E16 with incoming-payment icon 20dp #B2D188. Title "Payment received" Outfit Medium 14sp #E3E3D8. Body "Payment of £50.00 received from James Wilson" Outfit Regular 13sp #C5C8BA, max 2 lines. Timestamp "10 min ago" Outfit Regular 11sp #8F9285 trailing. 8dp filled circle #B2D188 unread indicator trailing-top.

**Component 4 — List Row** (full width minus 32dp insets, 72dp tall, top margin 4dp): Surface #1E201A, 12dp radius. Leading 40dp circle #1F4E4B with identity-check icon 20dp #A0CFCB. Title "KYC verification approved" Outfit Medium 14sp #E3E3D8. Body "Your identity has been verified. You now have full access to all account features." Outfit Regular 13sp #C5C8BA. Timestamp "1 hr ago" trailing. 8dp unread dot #B2D188 trailing-top.

**Component 5 — Section Label Earlier** (full width minus 32dp insets, top margin 20dp): "Earlier" Outfit SemiBold 12sp #8F9285, uppercase.

**Component 6 — List Row** (full width minus 32dp insets, 72dp tall, top margin 4dp): Surface #1E201A, 12dp radius. Leading 40dp circle #44483D with direct-debit icon 20dp #C5C8BA. Title "Direct debit mandate created" Outfit Medium 14sp #E3E3D8. Body "Netflix £15.99/month from your Current Account." Outfit Regular 13sp #C5C8BA. Timestamp "3 hr ago" trailing. No unread dot (read).

**Component 7 — List Row** (full width minus 32dp insets, 72dp tall, top margin 4dp): Surface #1E201A, 12dp radius. Leading 40dp circle #354E16 with salary icon 20dp #B2D188. Title "Salary credited" Outfit Medium 14sp #E3E3D8. Body "£3,200.00 from Acme Ltd credited to your Current Account." Outfit Regular 13sp #C5C8BA. Timestamp "Yesterday" trailing.

**Component 8 — Bottom Nav** (64dp tall, full width, anchored bottom): 4 tabs Home, Payments, Notifications (selected indicator #354E16 pill, icon + label #B2D188), Profile. Background #1E201A, 1dp top divider #44483D. Inactive icons #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The sage-green #B2D188 unread indicator dots and selected nav state create a consistent, calm accent thread through the notification list, keeping financial awareness balanced and refined at a glance.

↑↑↑ MOCKUP PROMPT
