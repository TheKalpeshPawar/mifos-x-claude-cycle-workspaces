---
ui_yaml_sha: 2f2a6c96ff6e2c74c96d19567b252075cd0b6d28aa6c9b12c9aa6a48cb3ac2e2
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f3163ad47722ab358ffa9735a77abfea996d8a5ecf093728b9f1a88c68143640

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: accounts
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — error state

> Auto-generated from screens/accounts/ui.yaml @ SHA f91475d3720f6886
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Accounts screen for **HSBC Open Banking**, a UK account-information AISP app showing consent-gated account balances.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceVariant #41474D, outline #8B9198, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, secondary #B7C9D9, inversePrimary #266489.

**Component 1 - Top App Bar** (64dp tall, full width): Title "My Accounts" Outfit Medium 18sp #E0E3E8 centered. Leading shield icon 24dp #95CDF7. Trailing refresh icon 24dp #8B9198. Background #101417, zero elevation. This is the error_state archetype for the Accounts screen after a failed AISP data fetch.

**Component 2 - Error Illustration** (centered, top margin 64dp): 160dp x 160dp disconnected-data-link icon rendered in neutral steel tones #41474D / #8B9198 on transparent #101417 background. Outline style, 4dp stroke, conveys "data unavailable" without harsh red alarm styling.

**Component 3 - Error Code Chip** (centered, top margin 24dp): Chip 32dp tall, 8dp corner radius, background #93000A, label "Error 401 - Session expired" Outfit Regular 12sp #FFDAD6 centered.

**Component 4 - Error Title** (centered, top margin 12dp, horizontal padding 32dp): "Couldn't load your accounts" Outfit SemiBold 22sp #E0E3E8, centered, max 2 lines.

**Component 5 - Error Subtext** (centered, top margin 8dp, horizontal padding 40dp): "Your bank session may have expired. Check your connection or sign in again to restore access." Outfit Regular 14sp #C1C7CE, line-height 20sp, centered, max 25 words.

**Component 6 - Retry Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 9999dp, background #95CDF7, leading refresh icon 20dp #00344E, label "Retry" Outfit SemiBold 16sp #00344E centered.

**Component 7 - Go Back Link** (centered, top margin 16dp): Text Button "Return to dashboard" Outfit Medium 13sp #8B9198, no background, no leading icon. 48dp minimum tap target.

**Component 8 - Bottom Navigation Bar** (56dp tall, full width, pinned bottom, background #1C2024): Active "Accounts" icon and label #95CDF7 Outfit Medium 11sp. Inactive "Transactions" and "Consent" icon and label #8B9198 Outfit Regular 11sp.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Centered layout on #101417 with generous vertical breathing room. The steel-blue #95CDF7 retry button holds the primary action without alarm-red tone, keeping this error_state calm and non-punitive for a regulated UK Open Banking context where trust is the paramount design value.

↑↑↑ MOCKUP PROMPT
