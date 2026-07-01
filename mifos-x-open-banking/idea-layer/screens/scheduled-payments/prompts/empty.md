---
ui_yaml_sha: b176ea2d469f885b24e961885ac2755e38a0e1865e6d2f063caf8d6eec8ce214
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 0f61869dde2546dae0fa15d44bc56aeb455e5ab6026ce50725d6dcb4332d1f7a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: scheduled-payments
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# scheduled-payments — empty state

> Auto-generated from screens/scheduled-payments/ui.yaml @ SHA 683c7e08e742bb24
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the scheduled-payments screen for **HSBC Open Banking**, a UK AISP reference app confirming no future-dated one-off payments exist in the OBReadScheduledPayment3 feed, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left, 48dp touch; title Outfit medium 22sp "Scheduled Payments" #E0E3E8.

**Component 2 - Empty State** (361dp wide, vertically centered in remaining height, centered, generous vertical breathing room): schedule-clock icon 64dp #95CDF7 centered; Outfit medium 20sp "No scheduled payments" #E0E3E8 below icon, 16dp gap; Outfit regular 14sp "No future-dated one-off payments are set up on this HSBC account at this time." #C1C7CE centered, 2-line max; no CTA button. This is the empty_state archetype.

**Component 3 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Payments", "More"; "Payments" filled icon #95CDF7; inactive #C1C7CE.

Do not render a payment setup or initiation CTA; AISP has no write access and cannot create payments on behalf of the user. Do not add an illustrative scene or promotional graphic beyond the single schedule icon; low-variance minimalist-ui. Do not use amber, green, or warm tones in the empty illustration; cool trust-blue palette throughout. Do not frame the empty state as an error or warning; the message tone is calm and informational.

Honest absence of data. No urgency, no alarm. Read-only AISP transparency. Tone: calm, #95CDF7 minimal.

↑↑↑ MOCKUP PROMPT
