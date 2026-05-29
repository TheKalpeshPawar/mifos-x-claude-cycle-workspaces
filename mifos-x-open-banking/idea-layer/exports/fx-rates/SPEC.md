# SPEC — Exchange Rates

| Field         | Value               |
|---------------|---------------------|
| Feature       | fx-rates            |
| Flavor        | consumer            |
| Status        | approved            |
| Quality Score | 97                  |
| ViewModel     | FxRatesViewModel    |

---

## Overview

The Exchange Rates screen is a consumer-facing dashboard that provides live foreign-exchange rate information and an interactive currency converter. On screen entry the loading state renders the page title and shimmer skeletons for the converter card and all rate rows. Once data loads, the content state reveals a white converter card (elevation 4, 16dp radius) containing: an amount input field ("I want to send", default 1,000), a source currency selector (GBP), a circular swap button (swap_vert icon, #CDEDA3 background), a destination currency selector (EUR), a large converted-amount display ("= 1,167.20 EUR", display_medium, #4C662B), and a rate label ("Rate: 1 GBP = 1.1672 EUR"). Below the converter sits a filled CTA button ("Send this amount") that navigates to send-money. A "Popular Pairs" section lists six rate rows (GBP/EUR, GBP/USD, GBP/JPY, EUR/USD, USD/INR, EUR/GBP), each showing the pair label, current rate, and a coloured delta indicator (green arrow_upward / red arrow_downward / grey remove). Tapping any row pre-populates the converter with that pair. Rates are sourced from OBP FX and Currencies endpoints; a "Rates updated: 14 May 2026, 15:42 UTC" timestamp is shown below the page title. Each component carries per-state definitions (loading: skeleton, error: banner, empty: box) added during 2026-05-27 enrichment.

---

## Screens

| ID             | Name            | Route     | Layout | Scroll   |
|----------------|-----------------|-----------|--------|----------|
| fx_rates_main  | Exchange Rates  | /fx-rates | Column | Vertical |

**Initial state:** loading

**Shell:** Screen-level title (no top app bar). Accessed via Home → Services tile; no dedicated bottom-nav tab active.

---

## Components

| ID                        | Type    | Description                                                                                               |
|---------------------------|---------|-----------------------------------------------------------------------------------------------------------|
| fx_rates_title            | text    | "Exchange Rates" — Outfit/headline_large, #4C662B, 24dp top padding, 16dp horizontal; heading level 1; always visible |
| last_updated_text         | text    | "Rates updated: 14 May 2026, 15:42 UTC" — Outfit/body_small, #44483D, 16dp h-pad, 4dp top, 12dp bottom; API-driven from obp_get_fx_rate.effective_date |
| converter_card            | box     | #FFFFFF fill, 16dp radius, elevation 4, 20dp padding, 16dp h-margin, 16dp bottom margin; region role "Currency converter" |
| send_amount_input         | input   | "I want to send" label; value "1,000"; Outfit/title_large 700w, #4C662B; #F9FAEF bg, 8dp radius; decimal keyboard; triggers update_amount action |
| from_currency_select      | input   | "From" label; "GBP" value; select variant; arrow_drop_down trailing; #F9FAEF bg, 8dp radius; populates from obp_currencies; triggers select_from_currency |
| swap_currencies_icon      | icon    | swap_vert, 32dp, #4C662B on #CDEDA3 circle (16dp radius, 8dp padding); align_self center, 4dp v-margin; triggers swap_currencies |
| to_currency_select        | input   | "To" label; "EUR" value; select variant; arrow_drop_down trailing; #F9FAEF bg, 8dp radius; populates from obp_currencies; triggers select_to_currency |
| converted_result_display  | text    | "= 1,167.20 EUR" — Outfit/display_medium 700w, #4C662B, centred, 8dp v-padding; bound to obp_get_fx_rate.conversion_value |
| rate_info_text            | text    | "Rate: 1 GBP = 1.1672 EUR" — Outfit/body_small, #44483D, centred, 16dp bottom; bound to obp_get_fx_rate.conversion_value |
| send_money_cta            | button  | "Send this amount" — filled, #4C662B bg, #FFFFFF text, Outfit/label_large, 12dp radius, 14dp v-padding, full-width; navigates to send-money |
| section_divider           | divider | #E1E4D5, 16dp h-margin, 8dp v-margin                                                                     |
| popular_pairs_header      | text    | "Popular Pairs" — Outfit/title_medium 600w, #1A1C16, 16dp h-padding, 8dp top/bottom; heading level 2     |
| rate_row_gbp_eur          | box     | GBP/EUR row — #FFFFFF, 8dp radius, 16dp h-pad, 14dp v-pad, 16dp h-margin, 2dp bottom; row layout space-between; tappable select_pair |
| pair_label_gbp_eur        | text    | "GBP / EUR" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_gbp_eur        | text    | "1.1672" — Outfit/body_large 600w, #1A1C16                                                               |
| rate_change_gbp_eur       | text    | "+0.2%" — Outfit/body_small 500w, #4C662B, arrow_upward leading icon                                    |
| rate_row_gbp_usd          | box     | GBP/USD row — same layout; tappable select_pair                                                           |
| pair_label_gbp_usd        | text    | "GBP / USD" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_gbp_usd        | text    | "1.2834" — Outfit/body_large 600w, #1A1C16                                                               |
| rate_change_gbp_usd       | text    | "-0.1%" — Outfit/body_small 500w, #BA1A1A, arrow_downward leading icon                                  |
| rate_row_gbp_jpy          | box     | GBP/JPY row — same layout; tappable select_pair                                                           |
| pair_label_gbp_jpy        | text    | "GBP / JPY" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_gbp_jpy        | text    | "193.45" — Outfit/body_large 600w, #1A1C16                                                               |
| rate_change_gbp_jpy       | text    | "+0.4%" — Outfit/body_small 500w, #4C662B, arrow_upward leading icon                                    |
| rate_row_eur_usd          | box     | EUR/USD row — same layout; tappable select_pair                                                           |
| pair_label_eur_usd        | text    | "EUR / USD" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_eur_usd        | text    | "1.0993" — Outfit/body_large 600w, #1A1C16                                                               |
| rate_change_eur_usd       | text    | "-0.3%" — Outfit/body_small 500w, #BA1A1A, arrow_downward leading icon                                  |
| rate_row_usd_inr          | box     | USD/INR row — same layout; tappable select_pair                                                           |
| pair_label_usd_inr        | text    | "USD / INR" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_usd_inr        | text    | "83.22" — Outfit/body_large 600w, #1A1C16                                                                |
| rate_change_usd_inr       | text    | "0.0%" — Outfit/body_small 500w, #44483D, remove leading icon (flat/neutral)                             |
| rate_row_eur_gbp          | box     | EUR/GBP row — #FFFFFF, 8dp radius, 16dp h-margin, 16dp bottom margin (last row); tappable select_pair    |
| pair_label_eur_gbp        | text    | "EUR / GBP" — Outfit/body_large 500w, #1A1C16                                                            |
| rate_value_eur_gbp        | text    | "0.8568" — Outfit/body_large 600w, #1A1C16                                                               |
| rate_change_eur_gbp       | text    | "-0.2%" — Outfit/body_small 500w, #BA1A1A, arrow_downward leading icon                                  |

---

## States

| ID      | Trigger                                  | Description                                                                                                         |
|---------|------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoadEvent            | fx_rates_title always visible; skeleton shimmer (short4 = 200ms, reduced-motion: static) for last_updated_text, converter_card, all inputs, converted_result_display, rate_info_text, send_money_cta, popular_pairs_header, and all 6 rate rows |
| content | API returns rate data successfully       | Full screen: title + timestamp + converter card (live rate) + send CTA + divider + "Popular Pairs" header + 6 rate rows, each with live pair/rate/change data |
| error   | Network or OBP API failure               | fx_rates_title visible; converter card and all rate rows hidden; component-level banners surface per-component error messages (e.g. "Could not load exchange rate. Please try again." with retry); screen-level message: "Unable to load exchange rates. Check your connection and try again." |
| empty   | No rate data available for selected pair | fx_rates_title visible; converter card and rate rows hidden; empty icon: currency_exchange; message: "No exchange rates available for the selected currencies. Try a different currency pair."; action: "Reset to GBP / EUR" (reset_currency_pair) |

---

## State Model

**ViewModel:** `FxRatesViewModel`

| Name             | Type            | Default      |
|------------------|-----------------|--------------|
| fromCurrency     | String          | "GBP"        |
| toCurrency       | String          | "EUR"        |
| sendAmount       | Double          | 1000.0       |
| convertedAmount  | Double          | 1167.20      |
| exchangeRate     | Double          | 1.1672       |
| rateList         | List\<FxRate\>  | emptyList()  |
| lastUpdated      | String          | ""           |
| isLoading        | Boolean         | true         |
| networkError     | String?         | null         |
| rateUnavailable  | String?         | null         |

**Events:** `AmountChangedEvent`, `FromCurrencySelectedEvent`, `ToCurrencySelectedEvent`, `SwapCurrenciesEvent`, `PairSelectedEvent`, `SendMoneyEvent`, `RetryLoadEvent`

**Actions:** `update_amount`, `select_from_currency`, `select_to_currency`, `swap_currencies`, `select_pair`, `navigate`, `retry_load`

**DI Dependencies:** `FxRatesRepository`, `NavigationService`

**Errors:**
- `networkError`: "Unable to load exchange rates. Check your connection and try again."
- `rateUnavailable`: "No exchange rates available for the selected currencies. Try a different currency pair."

---

## Navigation

| From     | To         | Trigger            | Type |
|----------|------------|--------------------|------|
| fx-rates | send-money | send_money_cta tap | push |

---

## API Endpoints

| Endpoint                                                                      | Auth        | Tag | Purpose                                              |
|-------------------------------------------------------------------------------|-------------|-----|------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/currencies                                     | DirectLogin | FX  | Populate from/to currency dropdown selectors         |
| GET /obp/v5.1.0/banks/{bankId}/fx/{fromCurrencyCode}/{toCurrencyCode}         | DirectLogin | FX  | Fetch live exchange rate for converter + popular pairs|

---

## Design Tokens

| Token                             | Value           | Usage                                                                                |
|-----------------------------------|-----------------|--------------------------------------------------------------------------------------|
| colors.light.primary              | #4C662B         | Screen title, converted result display, rate info, swap icon, positive delta text, send CTA fill |
| colors.light.primary_container    | #CDEDA3         | Swap icon circular background                                                        |
| colors.light.error                | #BA1A1A         | Negative delta indicators (-0.1%, -0.3%, -0.2%)                                     |
| colors.light.surface              | #FFFFFF         | Converter card fill, all rate row fills                                              |
| colors.light.background           | #F9FAEF         | Screen base; amount input and currency selector backgrounds                          |
| colors.light.on_surface           | #1A1C16         | Pair labels, rate values, "Popular Pairs" header                                     |
| colors.light.on_surface_variant   | #44483D         | Timestamp text, rate label (body_small), neutral delta (0.0%)                       |
| colors.light.surface_variant      | #E1E4D5         | Section divider colour                                                               |
| typography.scale.headline_lg      | Outfit 32sp/400 | "Exchange Rates" screen title                                                        |
| typography.scale.display_md       | Outfit 45sp/400 | Converted amount result "= 1,167.20 EUR" (700w override from ui.yaml)               |
| typography.scale.title_lg         | Outfit 22sp/400 | send_amount_input label (title_large alias)                                          |
| typography.scale.title_md         | Outfit 16sp/500 | "Popular Pairs" section header (600w override)                                       |
| typography.scale.body_lg          | Outfit 16sp/400 | Pair labels (500w) and rate values (600w)                                            |
| typography.scale.body_sm          | Outfit 12sp/400 | Timestamp, rate label, delta change percentages                                      |
| typography.scale.label_lg         | Outfit 14sp/500 | "Send this amount" CTA button label                                                  |
| radius.sm                         | 8dp             | Amount input, currency selectors, rate row cards                                     |
| radius.md                         | 12dp            | "Send this amount" CTA button                                                        |
| radius.lg                         | 16dp            | Converter card, swap icon circular container                                         |
| elevation.level2                  | 3dp             | Converter card (source specifies 4dp; closest M3 level is level2=3dp)               |
| motion.duration.short4            | 200ms           | Loading skeleton shimmer; reduced_motion_fallback: static_placeholder                |
| iconography.set                   | Material Symbols Outlined | swap_vert, arrow_drop_down, arrow_upward, arrow_downward, remove, currency_exchange, calculate, info_outline, money_off, schedule |

---

_Generated by /idea export | 2026-05-30_
