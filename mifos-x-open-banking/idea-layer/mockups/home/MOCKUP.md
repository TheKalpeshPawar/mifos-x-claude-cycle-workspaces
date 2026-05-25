# MOCKUP — Home Dashboard

| Field   | Value    |
|---------|----------|
| Feature | home     |
| Flavor  | consumer |

---

## Screen Layout

The Home Dashboard is a vertically scrollable column on surface background (#FCF8FF). It is anchored by a bottom navigation bar (5 tabs) that persists across all scroll positions. The scroll content hierarchy from top to bottom:

1. Greeting text + date (padding-top 24 dp, horizontal 20 dp)
2. Primary account hero card (horizontal margin 20 dp)
3. Total balance chip (horizontal margin 20 dp, margin-top 12 dp)
4. Recent Transactions section header (horizontal 20 dp, top 20 dp, bottom 12 dp)
5. Three transaction rows (horizontal margin 20 dp, gap 8 dp)
6. Services section title (horizontal 20 dp, top 20 dp, bottom 12 dp)
7. Services grid — 3 tiles in a horizontal row (horizontal 20 dp)
8. Bottom spacer (24 dp) above the bottom nav bar

---

## Components

### Greeting Block

**greeting_text**
- Content: "Good morning, Alex"
- Style: headline_medium typography, color #1800B1, padding-top 24 dp, padding-horizontal 20 dp
- Data-driven: personalized via `HomeScreenState.greetingName` ("Alex")
- Accessibility: role=heading level=1

**greeting_date**
- Content: "Monday, 25 May 2026"
- Style: body_medium typography, color #666666, padding-horizontal 20 dp, padding-bottom 16 dp

---

### Primary Account Hero Card

**primary_account_card**
- Container: background #1800B1 (Mifos deep purple), border-radius 20 dp, padding 24 dp, horizontal margin 20 dp, elevation 4 dp
- Accessibility: role=region, label="Primary Checking account card"

Contents from top to bottom:

**account_card_label**
- Content: "Primary Checking"
- Style: label_large typography, color #FFFFFFB3 (70% white opacity)

**account_card_balance**
- Content: "£4,250.00"
- Style: display_small typography, color #FFFFFF, padding-top 8 dp, padding-bottom 4 dp
- Accessibility: label="Account balance: four thousand two hundred fifty pounds"

**account_card_iban**
- Content: "•••• •••• •••• 0130"
- Style: body_medium typography, color #FFFFFFB3, padding-bottom 20 dp
- Accessibility: label="Account number ending 0130"

**quick_actions_row** — Horizontal row of three equal-flex buttons:

| Button               | ID                   | Style                                                 | Target       |
|----------------------|----------------------|-------------------------------------------------------|--------------|
| "Send Money"         | btn_send_money       | Filled white (#FFFFFF), text #1800B1, border-radius 12| send-money   |
| "Beneficiaries"      | btn_add_beneficiary  | Outlined white border, text #FFFFFF, border-radius 12 | beneficiaries|
| "View Cards"         | btn_view_cards       | Outlined white border, text #FFFFFF, border-radius 12 | cards        |

All three: label_medium typography, padding-horizontal 12 dp, padding-vertical 8 dp, flex=1.

---

### Total Balance Chip

**total_balance_chip**
- Container: background #E8E4FF (soft lavender), border-radius 12 dp, padding-horizontal 16 dp, padding-vertical 10 dp, margin-horizontal 20 dp, margin-top 12 dp
- Row contents: account_balance_wallet icon (16 dp, #1800B1) + "Total across 3 accounts: £12,480.50" text (label_medium, #1800B1)
- Accessibility: label="Total across 3 accounts: twelve thousand four hundred eighty pounds fifty pence"

---

### Recent Transactions Section

**recent_transactions_header**
- Horizontal row: "Recent Transactions" heading (left) + "View All" link (right)
- Heading: title_large typography, color #1A1A1A, role=heading level=2
- Link: "View All", label_medium, color #1800B1; navigates to transactions

**transaction_row_1 — Tesco Supermarket**
- Card: background #FFFFFF, border-radius 12 dp, padding 16 dp, margin-horizontal 20 dp, margin-bottom 8 dp, elevation 1 dp
- Left icon container: 44×44 dp circle, background #E8F5E9, contains shopping_cart icon (22 dp, #4CAF50)
- Center column: "Tesco Supermarket" (body_large, #1A1A1A) + "23 May 2026 · Groceries" (body_small, #666666)
- Right column: "-£42.50" (body_large, #FF5252, weight 600) + "DEBIT" badge (label_small, #FF5252, background #FFEBEE, border-radius 4 dp)

**transaction_row_2 — Salary Payment**
- Card: same card style as row_1
- Left icon container: 44×44 dp circle, background #E8F5E9, contains payments icon (22 dp, #4CAF50)
- Center column: "Salary Payment" (body_large, #1A1A1A) + "22 May 2026 · Income" (body_small, #666666)
- Right column: "+£3,200.00" (body_large, #4CAF50, weight 600) + "CREDIT" badge (label_small, #4CAF50, background #E8F5E9, border-radius 4 dp)

**transaction_row_3 — EDF Energy**
- Card: same card style as row_1
- Left icon container: 44×44 dp circle, background #FFF3E0, contains bolt icon (22 dp, #FF9800)
- Center column: "EDF Energy" (body_large, #1A1A1A) + "20 May 2026 · Utilities" (body_small, #666666)
- Right column: "-£94.20" (body_large, #FF5252, weight 600) + "DEBIT" badge (label_small, #FF5252, background #FFEBEE)

---

### Services Grid

**services_section_title**
- Content: "Services"
- Style: title_large typography, color #1A1A1A, padding-horizontal 20 dp, padding-top 20 dp, padding-bottom 12 dp

**services_grid** — Horizontal row, spacing 12 dp, padding-horizontal 20 dp, padding-bottom 20 dp:

| Tile                  | ID                      | Background | Icon (size/color)             | Label (color)               |
|-----------------------|-------------------------|------------|-------------------------------|-----------------------------|
| Standing Orders       | service_standing_orders | #F5F0FF    | repeat, 24 dp, #1800B1        | "Standing Orders" (#1800B1) |
| ATM & Branches        | service_atm_locator     | #E0F7F7    | location_on, 24 dp, #008B8B   | "ATM & Branches" (#008B8B)  |
| FX Rates              | service_fx_rates        | #FFF3E0    | currency_exchange, 24 dp, #E65100 | "FX Rates" (#E65100)    |

All tiles: border-radius 16 dp, padding 16 dp, flex=1; icon above label with padding-top 8 dp; label_medium typography.

---

### Bottom Navigation Bar

5 tabs, always visible, positioned at screen bottom:
- **Home** (home icon, active=true) — #1800B1 indicator
- **Accounts** (account_balance icon) — target: accounts
- **Pay** (send icon) — target: send-money
- **Cards** (credit_card icon) — target: cards
- **More** (more_horiz icon) — target: more

---

## Interaction Patterns

| Element                 | Gesture | Outcome                                                         |
|-------------------------|---------|-----------------------------------------------------------------|
| btn_send_money          | Tap     | Navigate to `send-money` screen                                 |
| btn_add_beneficiary     | Tap     | Navigate to `beneficiaries` screen                              |
| btn_view_cards          | Tap     | Navigate to `cards` screen                                      |
| view_all_link           | Tap     | Navigate to `transactions` screen                               |
| service_standing_orders | Tap     | Navigate to `standing-orders` screen                            |
| service_atm_locator     | Tap     | Navigate to `atm-locator` screen                                |
| service_fx_rates        | Tap     | Navigate to `fx-rates` screen                                   |
| nav bottom bar tabs     | Tap     | Tab switch to respective screen                                 |
| Error card Retry button | Tap     | Fires `RetryLoad` event → `loadDashboardData()`                 |
| Empty card "Set Up Account" | Tap | Navigate to `accounts` screen                                  |

**Loading state:**
- Greeting text and date remain visible.
- Account card region is replaced by a grey skeleton box (#E0E0E0, height 180 dp, border-radius 20, margin-horizontal 20 dp).
- Two transaction placeholder boxes shown below (height 72 dp each, border-radius 12, grey #E0E0E0, margin-top 8 dp).
- Skeleton boxes do not animate — static grey fills for the initial load pass.

**Error state:**
- Greeting block visible.
- Error card appears: icon `error_outline` + title "Could not load your account" + message "We were unable to fetch your account data. Check your connection and try again." + "Retry" button.

**Empty state:**
- Greeting block visible.
- Empty card appears: illustration `account_empty` + title "No accounts yet" + message "Your accounts will appear here once your profile is set up." + "Set Up Account" button.

---

## Content Data

| Component              | Content Value                              |
|------------------------|--------------------------------------------|
| greeting_text          | "Good morning, Alex"                       |
| greeting_date          | "Monday, 25 May 2026"                      |
| account_card_label     | "Primary Checking"                         |
| account_card_balance   | "£4,250.00"                               |
| account_card_iban      | "•••• •••• •••• 0130"                      |
| total_balance_text     | "Total across 3 accounts: £12,480.50"     |
| txn1_merchant          | "Tesco Supermarket"                        |
| txn1_date              | "23 May 2026 · Groceries"                  |
| txn1_amount            | "-£42.50"                                  |
| txn2_merchant          | "Salary Payment"                           |
| txn2_date              | "22 May 2026 · Income"                     |
| txn2_amount            | "+£3,200.00"                              |
| txn3_merchant          | "EDF Energy"                               |
| txn3_date              | "20 May 2026 · Utilities"                  |
| txn3_amount            | "-£94.20"                                  |
| service_standing_orders| "Standing Orders"                          |
| service_atm_label      | "ATM & Branches"                           |
| service_fx_label       | "FX Rates"                                 |

---

## Design Notes

**Color usage:**
- The deep purple hero card (#1800B1) is the visual anchor of the screen — it carries the most important data (balance) and the primary user actions (quick action buttons). The reverse-color text (#FFFFFF full and #FFFFFFB3 for supporting text) preserves hierarchy inside the card.
- Transaction amounts use a semantic red/green system: #FF5252 for debits, #4CAF50 for credits. The colored amount is supported by a small badge (#FFEBEE/#DEBIT or #E8F5E9/CREDIT) — the two-signal system (color + badge) ensures debit/credit distinction is accessible beyond color alone.
- Service tile backgrounds (purple #F5F0FF, teal #E0F7F7, amber #FFF3E0) use brand-aligned tints that create category identity without requiring text labels of different colors.
- Total balance chip #E8E4FF is a transparent tint of primary — it reads as "part of the account card universe" without competing with the hero card.

**Typography:**
- display_small (account balance in hero card) is the typographic climax of the screen — the largest text, in pure white on deep purple, establishes immediate visual priority.
- headline_medium (greeting) anchors the screen's personal register; the purple color reinforces the user's session identity.
- title_large for section headers ("Recent Transactions", "Services") uses a neutral dark #1A1A1A to avoid competing with the purple greeting and hero card.
- label_small for DEBIT/CREDIT badges provides dense information at minimal size without visual noise.

**Spacing:**
- Consistent 20 dp horizontal margins create a unified canvas width for all major elements.
- 8 dp gap between transaction cards provides clear item separation without excessive whitespace.
- 12 dp tile gap in services grid creates a tight-but-breathable 3-column layout.
- 24 dp bottom spacer ensures last-scrolled content is not clipped by the bottom nav bar.

**Accessibility:**
- Greeting is role=heading level=1 — establishes the page title for screen readers.
- Section headers (Recent Transactions, Services) are role=heading level=2 — proper document outline.
- Account card is role=region with a descriptive label — allows VoiceOver/TalkBack users to navigate to the account block directly.
- Transaction rows are role=listitem with full aria labels reading the merchant, amount, and date (e.g. "Tesco Supermarket, debit forty-two pounds fifty, 23 May 2026").
- DEBIT/CREDIT badge supplements color coding — the badge text ensures color-blind users get an explicit categorical signal.
- All navigation buttons carry explicit `hint` attributes describing the destination (e.g. "Opens the send money screen").

---

_Generated by /idea export | 2026-05-25_
