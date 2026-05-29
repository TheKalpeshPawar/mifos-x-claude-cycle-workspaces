# pfm-dashboard — loading state — section 2/2

> Composition fragment. Compose into the parent (loading.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
96. **text** (#merchant_name_spotify) — label: "Spotify", content: "Spotify"
97. **text** (#merchant_meta_spotify) — label: "1 transaction", content: "1 transaction"
98. **text** (#merchant_amount_spotify) — label: "£11.99", content: "£11.99"
99. **list_item** (#merchant_row_tfl) — label: "Transport for London"
100. **text** (#merchant_name_tfl) — label: "Transport for London", content: "Transport for London"
101. **text** (#merchant_meta_tfl) — label: "23 transactions", content: "23 transactions"
102. **text** (#merchant_amount_tfl) — label: "£78.50", content: "£78.50"
103. **button** (#view_all_transactions_button) — label: "View All Transactions"
104. **box** (#no_budget_set_banner) — label: "No budget set banner", content: "No budget set banner"
105. **text** (#no_budget_banner_title) — label: "No budget set", content: "No budget set"
106. **text** (#no_budget_banner_body) — label: "Set a monthly budget to track how much you spend against your target.", content: "Set a monthly budget to track how much you spend against your target."
107. **button** (#set_budget_cta_button) — label: "Set Budget Now"

↓↓↓ MOCKUP PROMPT

Design the **loading** state of the Pfm Dashboard screen for **Mifos X Open Banking**, a open banking KMP super-app delivering consumer retail banking and field officer agent banking. Section 2 of 2.

Palette: background #12140E, surface #12140E, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, onPrimaryContainer #CDEDA3, secondary #A0CFCB, surfaceContainer #1E201A, surfaceContainerHigh #282A24, outline #8F9285, outlineVariant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 - Text Label** (full width minus 32dp insets): dashboard archetype. "Spotify" Outfit Medium 14sp #E3E3D8.

**Component 2 - Text Label** (full width minus 32dp insets): dashboard archetype. "1 transaction" Outfit Medium 14sp #E3E3D8.

**Component 3 - Text Label** (full width minus 32dp insets): dashboard archetype. "£11.99" Outfit Medium 14sp #E3E3D8.

**Component 4 - List Item** (full width minus 32dp insets): dashboard archetype. "Transport for London" Outfit Medium 14sp #E3E3D8.

**Component 5 - Text Label** (full width minus 32dp insets): dashboard archetype. "Transport for London" Outfit Medium 14sp #E3E3D8.

**Component 6 - Text Label** (full width minus 32dp insets): dashboard archetype. "23 transactions" Outfit Medium 14sp #E3E3D8.

**Component 7 - Text Label** (full width minus 32dp insets): dashboard archetype. "£78.50" Outfit Medium 14sp #E3E3D8.

**Component 8 - Button** (full width minus 32dp insets): dashboard archetype. "View All Transactions" Outfit Medium 14sp #E3E3D8.

**Component 9 - Card** (full width minus 32dp insets): dashboard archetype. "No budget set banner" Outfit Medium 14sp #E3E3D8.

**Component 10 - Text Label** (full width minus 32dp insets): dashboard archetype. "No budget set" Outfit Medium 14sp #E3E3D8.

**Component 11 - Text Label** (full width minus 32dp insets): dashboard archetype. "Set a monthly budget to track how much you spend against your target." Outfit Medium 14sp #E3E3D8.

**Component 12 - Button** (full width minus 32dp insets): dashboard archetype. "Set Budget Now" Outfit Medium 14sp #E3E3D8.

DO NOT use em-dash anywhere in text. DO NOT make any headline more than 3 lines or any subtitle more than 25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green primary #B2D188 anchors budget indicators, chart accents, and CTA buttons, creating a balanced and premium feel calibrated to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
