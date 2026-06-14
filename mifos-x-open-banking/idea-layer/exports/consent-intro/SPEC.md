# SPEC — Connect Your HSBC Account (Consent Intro)

| Field         | Value                       |
|---------------|-----------------------------|
| Feature       | consent-intro               |
| Flavor        | consumer                    |
| Status        | enriched                    |
| Quality Score | 95                          |
| ViewModel     | ConsentIntroViewModel       |

---

## Overview

The Connect Your HSBC Account screen is the entry point of the OBIE account-access-consent journey. It is a fully static onboarding screen — no network call is made here. The screen renders immediately with a large `account_balance` icon, a headline, a supporting subtitle, and three information cards designed to build trust before the PSU commits to sharing any data.

The first card, "You stay in control", presents four explicit trust pillars: (1) authentication happens at HSBC's own secure pages, not in this app; (2) the PSU selects exactly which accounts and data clusters to share on the next screen; (3) access is read-only until the PSU explicitly authorises a payment at HSBC; and (4) access can be revoked at any time from Settings. The second card, "What we'll read", summarises the read-only data the app will access — account names, numbers and balances; transaction history and statements; standing orders, direct debits and payees. The third card is a `#CDEDA3`-filled highlight card with an `open_in_browser` icon explaining that the PSU will be redirected to HSBC's secure sign-in to approve the connection, and that this app never sees their HSBC password.

Below the cards a `body_small` reassurance line confirms the PSU can review what they are sharing before anything is connected. The primary CTA "Connect your HSBC account" (filled `#4C662B`) advances to the `consent-request` screen. Beneath it, a horizontal row holds "Terms of Service" and "Privacy Policy" inline links (`#386663`), and a muted "Powered by Open Banking" footer closes the screen. The shell has no Top App Bar and no bottom navigation — this is an immersive onboarding entry.

---

## Screens

| ID            | Name                        | Route            | Layout | Scroll   |
|---------------|-----------------------------|------------------|--------|----------|
| consent-intro | Connect Your HSBC Account   | /consent-intro   | Column | Vertical |

**Shell:** No Top App Bar. No bottom navigation bar. Full-screen onboarding layout.

| Action                | Label                      | Trigger                              |
|-----------------------|----------------------------|--------------------------------------|
| connect_click         | Connect your HSBC account  | navigate to consent-request          |
| terms_click           | Terms of Service           | navigate to terms-of-service         |
| privacy_click         | Privacy Policy             | navigate to privacy-policy           |

---

## Components

| ID                         | Type   | Description                                                                                                              |
|----------------------------|--------|--------------------------------------------------------------------------------------------------------------------------|
| intro_root                 | stack  | Column, `#F9FAEF` bg, `spacing.lg` padding — root container for all children                                            |
| intro_hero_icon            | icon   | `account_balance` — 72dp, `#4C662B`, centered, `spacing.md` bottom padding; a11y role=image                             |
| intro_title                | text   | "Connect your HSBC account" — Outfit/headline_medium, `#1A1C16`, bold (700), centered, `spacing.xs` bottom padding       |
| intro_subtitle             | text   | "Link your HSBC account securely through Open Banking…" — Outfit/body_medium, `#44483D`, centered, `spacing.lg` bottom padding |
| intro_trust_card           | card   | Outlined, `#FFFFFF` bg, `#C5C8BA` border, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin; a11y group "How Open Banking protects you" |
| intro_trust_heading        | text   | "You stay in control" — Outfit/title_medium, `#1A1C16`, bold (700), heading level 2, `spacing.sm` bottom padding         |
| intro_trust_point_one      | text   | "You approve access at HSBC — not here. Sign-in and approval happen on HSBC's own secure pages." — Outfit/body_medium, `#386663` |
| intro_trust_point_two      | text   | "You choose exactly what to share. Pick which accounts and details to connect on the next screen." — Outfit/body_medium, `#386663` |
| intro_trust_point_three    | text   | "Read-only unless you authorise a payment. We can view your data; money only moves when you approve a payment at HSBC." — Outfit/body_medium, `#386663` |
| intro_trust_point_four     | text   | "Revoke access any time in Settings — disconnecting takes effect immediately." — Outfit/body_medium, `#386663`            |
| intro_access_card          | card   | Outlined, `#FFFFFF` bg, `#C5C8BA` border, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin; a11y group "What this app will read" |
| intro_access_heading       | text   | "What we'll read" — Outfit/title_medium, `#1A1C16`, bold (700), heading level 2, `spacing.sm` bottom padding             |
| intro_access_list          | list   | Bulleted, Outfit/body_medium, `#44483D` — 3 items: account names/numbers/balances; transaction history and statements; standing orders, direct debits and payees |
| intro_redirect_card        | card   | Filled, `#CDEDA3` bg, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin; a11y group "You'll be taken to HSBC to sign in" |
| intro_redirect_icon        | icon   | `open_in_browser` — 24dp, `#4C662B`; a11y "Secure redirect to HSBC sign-in"                                             |
| intro_redirect_text        | text   | "Next, you'll be taken to HSBC's own secure sign-in…" — Outfit/body_small, `#1A1C16`, `spacing.sm` start padding         |
| intro_security_note        | text   | "You can review exactly what you're sharing on the next screen before anything is connected." — Outfit/body_small, `#44483D`, centered, `spacing.md` bottom padding |
| intro_connect_button       | button | "Connect your HSBC account" — filled, `#4C662B` bg, `#FFFFFF` text, Outfit/label_large, 8dp radius, `spacing.md` padding, full width; navigates to consent-request |
| intro_legal_links          | stack  | Horizontal row, centered, `spacing.md` gap, `spacing.md` top padding — holds Terms + Privacy links                       |
| intro_terms_link           | link   | "Terms of Service" — Outfit/body_medium, `#386663`, inline, 44dp min height; navigates to terms-of-service               |
| intro_privacy_link         | link   | "Privacy Policy" — Outfit/body_medium, `#386663`, inline, 44dp min height; navigates to privacy-policy                  |
| intro_footer               | text   | "Powered by Open Banking" — Outfit/body_small, `#44483D`, centered, `spacing.md` top / `spacing.xl` bottom padding       |

---

## States

| ID      | Trigger                          | Description                                                                                              |
|---------|----------------------------------|----------------------------------------------------------------------------------------------------------|
| content | Screen entry (static)            | All components visible — hero icon, title, subtitle, three cards, security note, CTA, legal links, footer |

---

## State Model

**ViewModel:** `ConsentIntroViewModel`
**Screen State Type:** `ConsentIntroUiState`
**Pattern:** MVI

| Name               | Type    | Default | Note                                                                                             |
|--------------------|---------|---------|--------------------------------------------------------------------------------------------------|
| hasExistingConsent | Boolean | false   | True when a prior AUTH-status consent exists; CTA may relabel to "Manage your connection" for returning PSUs |

**Events:**
- `ConsentIntroEvent.NavigateToConsentRequest`
- `ConsentIntroEvent.NavigateToTermsOfService`
- `ConsentIntroEvent.NavigateToPrivacyPolicy`

**Actions:**
- `ConsentIntroAction.ConnectClicked`
- `ConsentIntroAction.TermsClicked`
- `ConsentIntroAction.PrivacyClicked`

**DI Dependencies:** `ConsentRepository` (read-only — detects existing AUTH consent)

---

## Navigation

| From          | Action        | To                | Type    | Description                                                        |
|---------------|---------------|-------------------|---------|--------------------------------------------------------------------|
| consent-intro | connect_click | consent-request   | push    | "Connect your HSBC account" CTA — advance to data-cluster review   |
| consent-intro | terms_click   | terms-of-service  | push    | "Terms of Service" inline link                                     |
| consent-intro | privacy_click | privacy-policy    | push    | "Privacy Policy" inline link — Open Banking safeguards explainer   |

---

## API Endpoints

_(none — this screen makes no network calls. The account-access-consent POST happens on the next screen, consent-request.)_

---

## Design Tokens

| Token                           | Value             | Usage                                                                              |
|---------------------------------|-------------------|------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B           | Hero icon; "Connect" button fill; redirect card icon                               |
| colors.light.primary_container  | #CDEDA3           | Redirect card background (filled highlight card)                                   |
| colors.light.background         | #F9FAEF           | Screen base (`intro_root` background)                                              |
| colors.light.surface            | #FFFFFF           | Trust card and access card fill                                                    |
| colors.light.on_surface         | #1A1C16           | Hero title; trust card heading; access card heading; redirect card body text       |
| colors.light.on_surface_variant | #44483D           | Subtitle; security note; footer; bulleted list items                               |
| colors.light.outline            | #C5C8BA           | Trust card and access card border                                                  |
| colors.light.secondary          | #386663           | Trust pillars text; Terms link; Privacy link                                       |
| colors.light.on_primary         | #FFFFFF            | "Connect your HSBC account" button label                                          |
| typography.headline_medium      | Outfit 28sp / 400 | "Connect your HSBC account" screen title                                           |
| typography.title_medium         | Outfit 16sp / 500 | "You stay in control" and "What we'll read" card headings                          |
| typography.body_medium          | Outfit 14sp / 400 | Subtitle; trust pillars; access list; legal links                                  |
| typography.body_small           | Outfit 12sp / 400 | Redirect card body text; security note; footer                                     |
| typography.label_large          | Outfit 14sp / 500 | "Connect your HSBC account" button label                                           |
| radius.md                       | 12dp              | Trust card, access card, and redirect card corners                                 |
| radius.sm                       | 8dp               | "Connect your HSBC account" button                                                 |

---

_Generated by /idea export | 2026-06-15_
