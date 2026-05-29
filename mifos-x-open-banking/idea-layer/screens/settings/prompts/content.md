---
ui_yaml_sha: c717833dff1dd0af44ee8aba62225240b2ae37761f8b10eea54bf8cb7c37482a
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: bd2098e7a4ed1e15d5ff3ef124063b0200ce8b8f28a291a792b5ae9c5f7dcb57

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

> Auto-generated from screens/settings/ui.yaml @ SHA 53070507da802b6e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **content** state of the Settings screen for **mifos-x-open-banking**, a Open Banking KMP super-app - consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web Material 3 balanced dark theme, 393×852dp (Pixel 5), Outfit font throughout.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, tertiary_container #1F4E4B, on_tertiary_container #BCEBE7, error #FFB4AB, on_error #690005.

**Component 1 - Stack** (full width minus 32dp insets): rendered per design system component spec. settings archetype.

**Component 2 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 3 - Card** (full width minus 32dp insets): rendered per design system component spec.

**Component 4 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 5 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 6 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 7 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 8 - Input** (full width minus 32dp insets): rendered per design system component spec.

**Component 9 - Divider** (full width minus 32dp insets): rendered per design system component spec.

**Component 10 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 11 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 12 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 13 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 14 - Input** (full width minus 32dp insets): rendered per design system component spec.

**Component 15 - Card** (full width minus 32dp insets): rendered per design system component spec.

**Component 16 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 17 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 18 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 19 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 20 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 21 - Input** (full width minus 32dp insets): rendered per design system component spec.

**Component 22 - Divider** (full width minus 32dp insets): rendered per design system component spec.

**Component 23 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 24 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 25 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 26 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 27 - Input** (full width minus 32dp insets): rendered per design system component spec.

**Component 28 - Card** (full width minus 32dp insets): rendered per design system component spec.

**Component 29 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 30 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 31 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 32 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 33 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 34 - Input** (full width minus 32dp insets): rendered per design system component spec.

**Component 35 - Divider** (full width minus 32dp insets): rendered per design system component spec.

**Component 36 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 37 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 38 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 39 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 40 - Icon** (full width minus 32dp insets): rendered per design system component spec.

**Component 41 - Card** (full width minus 32dp insets): rendered per design system component spec.

**Component 42 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 43 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 44 - Link** (full width minus 32dp insets): rendered per design system component spec.

**Component 45 - Icon** (full width minus 32dp insets): rendered per design system component spec.

**Component 46 - Divider** (full width minus 32dp insets): rendered per design system component spec.

**Component 47 - Stack** (full width minus 32dp insets): rendered per design system component spec.

**Component 48 - Text** (full width minus 32dp insets): rendered per design system component spec.

**Component 49 - Text** (full width minus 32dp insets): rendered per design system component spec.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #B2D188. The #B2D188 accent creates a balanced and premium feel calibrated to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
