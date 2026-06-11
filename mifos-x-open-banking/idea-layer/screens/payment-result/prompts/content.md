---
feature: payment-result
state: content
archetype: confirmation
flavor: consumer
project_id: mifos-x-open-banking
design_system_id: mifos-x-m3-earthgreen
aesthetic_family: taste-default
dials: { variance: 4, motion: 3, density: 5 }
brand:
  accent_color: "#4C662B"
  typography: "Outfit"
  theme: auto
  radius_system: soft
source: /idea-render-screen (LLM-local; no Stitch SDK)
note: "Per-state canonical MOCKUP PROMPT block for the stateless payment-success screen. Authored from ui.yaml because no /idea-export-stitch run has produced one yet."
---

# payment-result — content

Terminal success screen reached after a payment books (immediate settlement or
post-SCA completion). STATELESS — rendered entirely from nav args; no app shell
(no top bar, no bottom nav), full-bleed hero anchored to the top edge.

↓↓↓ MOCKUP PROMPT

Render a mobile payment-success confirmation screen (390px baseline, mobile-only).
Material Design 3, earth-green banking brand. Font: Outfit. Light + dark themes.

Palette (light): primary #4C662B, on-primary #FFFFFF, primary-container #CDEDA3,
background #F9FAEF, surface #FFFFFF, on-surface #1A1C16, on-surface-variant #44483D,
outline-variant #C5C8BA, success-tint #B6F2C0. Dark theme mirrors the project tokens.

Layout, top to bottom, no top bar and no bottom nav:

1. HERO — a full-width green gradient card bonded to the very top of the screen,
   rounded only at the bottom (28px), generous top padding (~72px), centered. It
   contains, stacked and centered:
   - A 92px white circle holding a single earth-green (#4C662B) Material "check_circle"
     / check glyph (the success mark).
   - Headline "Payment sent" in white, Outfit display-small, weight 700.
   - Sub-line "€250.00 to Liam Walker" in soft off-white (#F5FFE6), body-large.
     The counterparty is a real account-holder name (Liam Walker), NEVER a login
     username.
   - A small pill badge, semi-transparent white fill, white text, with a leading
     mint dot (#B6F2C0): "● COMPLETED".

2. DETAILS CARD — a white rounded card (16px) with light elevation, margin ~16px,
   sitting just below the hero. Rows are label (left, muted) / value (right, bold),
   separated by thin dividers (#E1E4D5):
   - Transaction ID  →  99888bf1-69aa…   (shortened — first 13 chars + ellipsis)
   - From            →  Primary Checking
   - Charge          →  €0.00
   - Posted          →  Just now

3. ACTIONS — at the bottom, full-width:
   - Primary filled button (#4C662B, white text, 52px, 12px radius): "View transaction"
     → navigates to transaction-detail.
   - Text button below it: "Done" → navigates back home.

Tone: calm, reassuring, trustworthy financial confirmation. The green hero is the
emotional anchor; the details card is quiet and factual. Measured motion only.

↑↑↑ MOCKUP PROMPT
