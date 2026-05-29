# SPEC — Exchange Rates

| Field         | Value             |
|---------------|-------------------|
| Feature       | fx-rates          |
| Flavor        | consumer          |
| Status        | approved          |
| Quality Score | 97                |
| ViewModel     | FxRatesViewModel  |

---

## Overview

The Exchange Rates screen provides Consumer users with a live currency converter and a popular currency pairs reference list. Users enter an amount, select source and target currencies (defaulting to GBP → EUR), and see the converted result in real time. A "Send this amount" CTA links directly to the Send Money screen, enabling frictionless FX-to-payment flow. Below the converter, a scrollable "Popular Pairs" section shows 6 pre-fetched rate rows (GBP/EUR, GBP/USD, GBP/JPY, EUR/USD, USD/INR, EUR/GBP) — each with pair label, exchange rate, and a colour-coded change indicator (+green, −red, =grey). Rates are fetched from OBP FX endpoints. A timestamp shows when rates were last refreshed.

---

## Screens

| ID            | Name           | Route      | Layout | Scroll   |
|---------------|----------------|------------|--------|----------|
| fx_rates_main | Exchange Rates | /fx-rates  | Column | Vertical |

**Shell:** No top app bar (screen-level title used instead). No bottom navigation bar (accessed via services tile from Home).

---

## Components

| ID                       | Type    | Description                                                                                               |
|--------------------------|---------|-----------------------------------------------------------------------------------------------------------|
| fx_rates_title           | text    | "Exchange Rates" — Outfit/headline_large, #4C662B, 24dp top padding                                      |
| last_updated_text        | text    | "Rates updated: 14 May 2026, 15:42 UTC" — Outfit/body_small, #44483D; API-driven from effective_date     |
| converter_card           | box     | #FFFFFF fill, 16dp radius, 4dp elevation, 20dp padding — contains converter widgets                      |
| send_amount_input        | input   | "I want to send" — number input, "1,000" default, Outfit/title_large 700 weight #4C662B, #F9FAEF fill    |
| from_currency_select     | input   | "From" dropdown — default "GBP 🇬🇧", arrow_drop_down trailing icon, #F9FAEF fill                        |
| swap_currencies_icon     | icon    | swap_vert, 32dp, #4C662B, #CDEDA3 circular container 16dp radius — taps to swap from/to                  |
| to_currency_select       | input   | "To" dropdown — default "EUR 🇪🇺", arrow_drop_down trailing icon, #F9FAEF fill                         |
| converted_result_display | text    | "= 1,167.20 EUR" — Outfit/display_medium, 700 weight, #4C662B, centered; recalculated on amount/currency change |
| rate_info_text           | text    | "Rate: 1 GBP = 1.1672 EUR" — Outfit/body_small, #44483D, centered                                       |
| send_money_cta           | button  | "Send this amount" — filled, #4C662B fill, white text, Outfit/label_large, 12dp radius, full width       |
| section_divider          | divider | #E1E4D5, 16dp horizontal margin, 8dp vertical margin                                                     |
| popular_pairs_header     | text    | "Popular Pairs" — Outfit/title_medium, #1A1C16, 600 weight                                               |
| rate_row_gbp_eur         | box     | GBP/EUR row — #FFFFFF fill, 8dp radius; shows "GBP / EUR · 1.1672 · +0.2%" (green)                     |
| pair_label_gbp_eur       | text    | "GBP / EUR" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_gbp_eur       | text    | "1.1672" — Outfit/body_large, 600 weight, #1A1C16                                                        |
| rate_change_gbp_eur      | text    | "+0.2%" — Outfit/body_small, #4C662B, arrow_upward leading icon                                          |
| rate_row_gbp_usd         | box     | GBP/USD row — "GBP / USD · 1.2834 · −0.1%" (red)                                                        |
| pair_label_gbp_usd       | text    | "GBP / USD" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_gbp_usd       | text    | "1.2834" — Outfit/body_large, 600 weight, #1A1C16                                                        |
| rate_change_gbp_usd      | text    | "−0.1%" — Outfit/body_small, #BA1A1A, arrow_downward leading icon                                        |
| rate_row_gbp_jpy         | box     | GBP/JPY row — "GBP / JPY · 193.45 · +0.4%" (green)                                                     |
| pair_label_gbp_jpy       | text    | "GBP / JPY" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_gbp_jpy       | text    | "193.45" — Outfit/body_large, 600 weight, #1A1C16                                                        |
| rate_change_gbp_jpy      | text    | "+0.4%" — Outfit/body_small, #4C662B, arrow_upward leading icon                                          |
| rate_row_eur_usd         | box     | EUR/USD row — "EUR / USD · 1.0993 · −0.3%" (red)                                                        |
| pair_label_eur_usd       | text    | "EUR / USD" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_eur_usd       | text    | "1.0993" — Outfit/body_large, 600 weight, #1A1C16                                                        |
| rate_change_eur_usd      | text    | "−0.3%" — Outfit/body_small, #BA1A1A, arrow_downward leading icon                                        |
| rate_row_usd_inr         | box     | USD/INR row — "USD / INR · 83.22 · 0.0%" (neutral grey)                                                 |
| pair_label_usd_inr       | text    | "USD / INR" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_usd_inr       | text    | "83.22" — Outfit/body_large, 600 weight, #1A1C16                                                         |
| rate_change_usd_inr      | text    | "0.0%" — Outfit/body_small, #44483D, remove leading icon (neutral)                                       |
| rate_row_eur_gbp         | box     | EUR/GBP row — "EUR / GBP · 0.8568 · −0.2%" (red)                                                        |
| pair_label_eur_gbp       | text    | "EUR / GBP" — Outfit/body_large, 500 weight, #1A1C16                                                     |
| rate_value_eur_gbp       | text    | "0.8568" — Outfit/body_large, 600 weight, #1A1C16                                                        |
| rate_change_eur_gbp      | text    | "−0.2%" — Outfit/body_small, #BA1A1A, arrow_downward leading icon                                        |

---

## States

| ID      | Trigger                               | Description                                                                              |
|---------|---------------------------------------|------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoadEvent         | Title visible; converter card + all rate rows show skeleton shimmer                     |
| content | API returns rates successfully        | Converter card + 6 rate rows + timestamp all populated with live data                   |
| error   | Network or FX API failure             | Title visible; converter card + rate rows hidden; error message with retry              |
| empty   | No rates available for selected pair  | Title visible; converter hidden + rate rows hidden; empty state with "Reset to GBP/EUR" action |

---

## State Model

**ViewModel:** `FxRatesViewModel`

| Name              | Type            | Default    |
|-------------------|-----------------|------------|
| fromCurrency      | String          | "GBP"      |
| toCurrency        | String          | "EUR"      |
| sendAmount        | Double          | 1000.0     |
| convertedAmount   | Double          | 1167.20    |
| exchangeRate      | Double          | 1.1672     |
| rateList          | List\<FxRate\>  | emptyList()|
| lastUpdated       | String          | ""         |
| isLoading         | Boolean         | true       |
| networkError      | String?         | null       |
| rateUnavailable   | String?         | null       |

**Events:** `AmountChangedEvent`, `FromCurrencySelectedEvent`, `ToCurrencySelectedEvent`, `SwapCurrenciesEvent`, `PairSelectedEvent`, `SendMoneyEvent`, `RetryLoadEvent`

**Actions:** `update_amount`, `select_from_currency`, `select_to_currency`, `swap_currencies`, `select_pair`, `navigate`, `retry_load`

**DI Dependencies:** `FxRatesRepository`, `NavigationService`

---

## Navigation

| From     | To         | Trigger            | Type |
|----------|------------|--------------------|------|
| fx-rates | send-money | send_money_cta tap | push |

---

## API Endpoints

| Endpoint                                                          | Auth        | Tag | Purpose                                    |
|-------------------------------------------------------------------|-------------|-----|--------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/currencies                        | DirectLogin | FX  | Populate from/to currency dropdown options |
| GET /obp/v5.1.0/banks/{bankId}/fx/{fromCurrencyCode}/{toCurrencyCode} | DirectLogin | FX  | Fetch live exchange rate for a currency pair |

---

## Design Tokens

| Token                              | Value     | Usage                                                               |
|------------------------------------|-----------|---------------------------------------------------------------------|
| colors.light.primary               | #4C662B   | Screen title, converter inputs, result display, send CTA, positive change text, swap icon |
| colors.light.primary_container     | #CDEDA3   | Swap icon circular container                                        |
| colors.light.background            | #F9FAEF   | Currency select input fill, amount input fill                       |
| colors.light.surface               | #FFFFFF   | Converter card fill, rate row fills                                 |
| colors.light.on_surface            | #1A1C16   | Pair labels, rate values, popular pairs header                      |
| colors.light.on_surface_variant    | #44483D   | Last updated timestamp, rate_info_text, neutral change (0.0%)      |
| colors.light.error                 | #BA1A1A   | Negative rate change text (−0.1%, −0.3%, −0.2%)                   |
| colors.light.surface_variant       | #E1E4D5   | Section divider color                                               |
| typography.headline_large          | Outfit 32sp | Screen title                                                      |
| typography.display_medium          | Outfit 45sp/700 | Converted result display                                      |
| typography.title_large             | Outfit 22sp | Converter amount input                                            |
| typography.title_medium            | Outfit 16sp/500 | "Popular Pairs" header                                        |
| typography.body_large              | Outfit 16sp/400/500 | Rate pair labels and rate values                          |
| typography.body_small              | Outfit 12sp/400 | Last updated timestamp, rate info text, change percentages    |
| typography.label_large             | Outfit 14sp/500 | "Send this amount" button                                     |
| radius.md                          | 12dp      | Send money CTA                                                      |
| radius.sm                          | 8dp       | Rate rows, currency select inputs                                   |
| radius.lg                          | 16dp      | Converter card, swap icon container                                 |
| elevation.level2                   | 3dp       | Converter card (specified as 4dp in source)                        |

---

_Generated by /idea export | 2026-05-29_
