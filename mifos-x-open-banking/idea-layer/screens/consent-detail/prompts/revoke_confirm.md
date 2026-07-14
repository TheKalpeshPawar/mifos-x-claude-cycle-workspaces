---
ui_yaml_sha: dc51a93dfe2c575708401b94ec0aad258941119f5f0891dc9bcbab82740013cd
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: ac144c7e8a7428eb4a81acf3a99b2a3f7af0619549acedd022193a81b8e6e36f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-detail
state: revoke_confirm
state_visibility: revoke_confirm

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — revoke_confirm state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA 0dad2dc72d31f7d8
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the revoke_confirm state of the consent-detail screen for **HSBC Open Banking**, a UK AISP app presenting a destructive-action confirmation dialog before removing an HSBC account-access consent, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consent detail" #E0E3E8 on #101417; back-arrow leading disabled while dialog is open; archetype screen.

**Component 2 - Card** (full-width minus 32dp, 96dp, #1C2024 radius 12dp, beneath scrim): HSBC logo 40dp circle; Chip "Authorised" filled #004B6F label #95CDF7; "aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01" 12sp #8B9198 truncated; rendered at 0.5 opacity beneath the scrim.

**Component 3 - Card** (dialog, full-width minus 48dp, 224dp, #262A2E radius 16dp, elevation 4, centred vertically in viewport above scrim): Outfit Medium 18sp "Revoke HSBC access?" #E0E3E8 padded 24dp top and sides; Outfit Regular 14sp "This will immediately remove this consent. Account data will stop refreshing and cannot be recovered without re-authorising." #C1C7CE 8dp below headline; 24dp gap; bottom row two Buttons 8dp apart: outlined "Cancel" Outfit Medium 14sp #95CDF7 border #95CDF7 radius 24dp, filled "Revoke" Outfit Medium 14sp #00344E on #FFB4AB container radius 24dp.

**Component 4 - List** (full-width minus 32dp, beneath scrim at 0.4 opacity, non-interactive): "Data shared" label and 10 permission rows visible but dimmed, reinforcing what access will be removed.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

The dialog sits over a #000000 40% scrim; "Revoke" uses #FFB4AB container as a calm but unmistakable signal of a destructive action, while Trust Blue (#95CDF7) on the outlined "Cancel" keeps the safer choice restrained and prominent.

↑↑↑ MOCKUP PROMPT
