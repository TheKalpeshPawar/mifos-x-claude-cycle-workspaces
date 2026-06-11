# SPEC — PFM Settings

| Field         | Value               |
|---------------|---------------------|
| Feature       | pfm-settings        |
| Flavor        | consumer            |
| Status        | approved            |
| Quality Score | 95                  |
| ViewModel     | PfmSettingsViewModel|

---

## Overview

The PFM Settings screen lets the Consumer persona choose the **base currency** used by the unified personal-finance dashboard. Spending across all of the user's personal accounts is converted into this currency (via OBP `/fx` rates) so the dashboard can total multi-currency activity. The screen renders a labelled radio list whose options are the distinct currencies across the user's personal accounts (EUR, GBP in the demo); the current selection is read from the `pfm_base_currency` personal-data-field (append-only store — newest row wins on read) and seeded from the default account's currency when never set. Selecting an option persists immediately by appending a new personal-data-field row and confirms with a snackbar. Reached from the pfm-dashboard "tune" top-bar action. Back returns to the dashboard.

---

## Screens

| ID           | Name         | Route          | Layout | Scroll   |
|--------------|--------------|----------------|--------|----------|
| pfm-settings | PFM Settings | /pfm-settings  | Column | Vertical |

**Shell:** Top app bar — title "PFM Settings", navigation icon `arrow_back` (navigate_back action). No bottom navigation bar.

| Bar Item   | Icon       | Action        |
|------------|------------|---------------|
| Back arrow | arrow_back | navigate_back |

---

## Components

| ID                    | Type      | Description                                                                                            |
|-----------------------|-----------|--------------------------------------------------------------------------------------------------------|
| settings_section_label| text      | "BASE CURRENCY" — Outfit/label_medium, #5C6057, uppercase; padding_horizontal 20dp, padding_top 8dp; a11y heading level 2 |
| settings_section_help | text      | "Spending across all personal accounts is converted into this currency." — Outfit/body_small, #5C6057  |
| currency_option_eur   | list_item | "EUR"; leading radio_button (selected); padding_horizontal 20dp; on tap → select_base_currency; a11y role radio |
| currency_option_gbp   | list_item | "GBP"; leading radio_button (unselected); padding_horizontal 20dp; on tap → select_base_currency; a11y role radio |

> The radio options are data-driven — one row per distinct currency across the user's personal accounts. EUR/GBP shown as the demo set.

---

## States

| ID        | Trigger                                       | Description                                                                          |
|-----------|-----------------------------------------------|--------------------------------------------------------------------------------------|
| loading   | Screen entry — reading persisted base currency| Section label/help hidden; 3 skeleton rows (height 48)                                |
| populated | Personal-data-field + account currencies loaded| Section label + help + radio options visible; snackbar "Base currency set to GBP." on save |
| error     | Read of personal-data-fields failed           | "Could not load settings" + retry_load                                               |

---

## State Model

**ViewModel:** `PfmSettingsViewModel`
**Screen State Type:** `PfmSettingsUiState`

| Field           | Type                | Default        |
|-----------------|---------------------|----------------|
| availableCurrencies | List<String>    | emptyList()    |
| selectedCurrency| String              | ""             |
| uiState         | PfmSettingsUiState  | Loading        |

**Screen State Members:** `Loading`, `Populated`, `Error`

**Events:** `OnCurrencySelected`, `OnRetry`, `NavigateBack`

**Actions:**

| Action                       | Trigger            | Description                                                                    |
|------------------------------|--------------------|--------------------------------------------------------------------------------|
| `loadBaseCurrency()`         | ScreenOpened       | Reads `pfm_base_currency` (newest row); derives options from personal accounts; seeds from default account currency when unset |
| `selectBaseCurrency(code)`   | OnCurrencySelected | Persists the choice (POST appends a new field row); updates selection; shows snackbar |
| `retry()`                    | OnRetry            | Re-reads personal-data-fields on error                                          |

**DI Dependencies:** `UserDataRepository` (personal-data-fields), `AccountsRepository`, `FxRepository`

**Errors:**

| ID            | Message                                        |
|---------------|------------------------------------------------|
| load_failed   | "Could not load settings"                      |
| save_failed   | "Couldn't save your base currency. Try again." |
| not_logged_in | "Your session expired. Please sign in again."  |

---

## Navigation

| ID       | From         | To            | Trigger                | Type |
|----------|--------------|---------------|------------------------|------|
| nav_back | pfm-settings | pfm-dashboard | top app bar back arrow | pop  |

Reached from pfm-dashboard's "tune" top-bar action (PfmSettingsRoute). The currency radios are in-screen state actions (`select_base_currency`) — they do not navigate.

---

## API Endpoints

| Endpoint                                            | Method | Auth        | Tag  | Purpose                                                       |
|-----------------------------------------------------|--------|-------------|------|--------------------------------------------------------------|
| GET /obp/v6.0.0/my/personal-data-fields             | GET    | DirectLogin | User | Read persisted base currency (`pfm_base_currency`, newest row)|
| POST /obp/v6.0.0/my/personal-data-fields            | POST   | DirectLogin | User | Persist chosen base currency (appends a new row)             |
| GET /obp/v5.1.0/banks/{bank_id}/fx/{from}/{to}      | GET    | DirectLogin | FX   | Live conversion rate used to re-denominate dashboard spending |

---

## Design Tokens

| Token                           | Value   | Usage                                              |
|---------------------------------|---------|----------------------------------------------------|
| colors.light.on_surface_variant | #5C6057 | settings_section_label; settings_section_help      |
| colors.light.primary            | #4C662B | selected radio button                              |
| typography.label_medium         | Outfit  | settings_section_label                             |
| typography.body_small           | Outfit  | settings_section_help                              |
| spacing (20dp)                  | 20dp    | horizontal padding on label/help/options           |
| spacing.sm (8dp)                | 8dp     | label top padding / help bottom padding            |

---

_Generated by /idea export | 2026-06-11_
