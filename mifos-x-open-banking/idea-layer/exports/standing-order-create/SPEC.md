# SPEC — New Standing Order

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | standing-order-create          |
| Flavor        | consumer                       |
| Status        | approved                       |
| Quality Score | 90                             |
| ViewModel     | CreateStandingOrderViewModel   |
| Archetype     | form_screen                    |
| Tags          | FR-019, standing-orders, payments, form, create |

---

## Overview

The New Standing Order screen authors a recurring payment instruction. Reached from the standing-orders list FAB (only after `CreateGate.Ready` — the source account has at least one beneficiary), it captures: a source account, an existing payee (beneficiary), an amount, a frequency (Daily / Weekly / Fortnightly / Monthly / Yearly), a first-payment date (the recurrence anchor, with a human "Repeats every …" hint), and an optional end date. On submit it POSTs an OBIE domestic-standing-order-consent (`POST /pisp/domestic-standing-order-consents`) which returns a `ConsentId` with Status `AwaitingAuthorisation` (AWAU), then hands off to payment-authorize-handoff for consent → bank authorise → callback → submit (`POST /pisp/domestic-standing-orders`). SCA happens at the bank, not in-app.

This is the create half of the standing-orders lifecycle (distinct from standing-order-edit). Validation: account + payee present, amount parses > 0, start date strictly after today, end date (when set) after start. The screen is mobile-only (390px baseline) with a "New Standing Order" top app bar (back arrow) and no bottom navigation bar.

---

## Screens

| ID                    | Name              | Route                  | Layout | Scroll   |
|-----------------------|-------------------|------------------------|--------|----------|
| standing-order-create | New Standing Order| /standing-orders/create| Column | Vertical |

**Shell:** Top app bar — title "New Standing Order", navigation_icon `arrow_back`, navigation_action navigate_back, no actions. No bottom navigation bar.

---

## Components

| ID                       | Type        | Description                                                                                            |
|--------------------------|-------------|-------------------------------------------------------------------------------------------------------|
| soc_root                 | stack       | Column container, `#F9FAEF` background, 16dp horizontal padding, vertical scroll                       |
| soc_source_account_field | input       | Outlined read-only "From account", trailing `expand_more`; opens the account picker sheet              |
| soc_account_picker_sheet | bottom_sheet| Account picker, white, 24dp top radius — lists every account the user can pay from; reloads payees     |
| soc_payee_field          | input       | Outlined read-only "Pay to", trailing `expand_more`; opens the payee dropdown ("Select payee" until chosen)|
| soc_payee_menu           | menu        | Dropdown of the source account's beneficiaries (counterpartyId → name)                                 |
| soc_no_payees_hint       | text        | "Add a beneficiary first — standing orders pay an existing payee." — replaces the payee field when none |
| soc_amount_field         | text_field  | Outlined "Amount", currency-code suffix, supporting "Amount taken on each payment date"; required, > 0 |
| soc_frequency_label      | text        | "Repeats" — Outfit/label_large, `#44483D`                                                              |
| soc_frequency_chips      | chip_group  | Filter chips over DAILY/WEEKLY/BI-WEEKLY (shown "Fortnightly")/MONTHLY/YEARLY; default MONTHLY          |
| soc_start_date_field     | input       | Outlined read-only "First payment date", trailing `calendar_today`, supporting "First payment runs on this date"; required, strictly after today |
| soc_start_date_picker    | date_picker | M3 dialog — selectable dates strictly after today                                                      |
| soc_recurrence_hint      | text        | "Repeats every Monday" — Outfit/body_small, `#4C662B`; derived from frequency + chosen date            |
| soc_end_date_field       | input       | Outlined read-only "End date (optional)", trailing `calendar_today`, supporting "Leave empty to pay until cancelled"; clearable |
| soc_end_date_picker      | date_picker | M3 dialog — selectable dates strictly after the start date                                             |
| soc_error_text           | text        | Inline error (form.error) — "Start date must be after today" — Outfit/body_small, `#BA1A1A`            |
| soc_submit_button        | button      | "Create standing order" — filled `#4C662B`, white text, 12dp radius, full-width; "Creating…" while submitting |
| soc_loading              | skeleton    | Centered CircularProgressIndicator while the account + beneficiaries load                              |

---

## States

| ID         | Trigger                                  | Description                                                                                       |
|------------|------------------------------------------|--------------------------------------------------------------------------------------------------|
| loading    | `form.loadingPayees` — account + payees resolving | Centered progress; only soc_loading visible                                              |
| content    | Default editable form                    | source account, payee, amount, Repeats label + chips, first-payment date + recurrence hint, end date, submit. soc_no_payees_hint replaces soc_payee_field when the account has no beneficiaries; recurrence hint + error text appear conditionally |
| submitting | `form.submitting` — consent POST in flight| Same layout; submit button disabled with label "Creating…"                                       |
| error      | `form.error` non-null                    | Inline soc_error_text above the button (and a toast); the form stays editable                     |
| created    | `form.created` true after AWAU consent POST| No standalone success surface — navigates to payment-authorize-handoff carrying the ConsentId    |

---

## State Model

**ViewModel:** `CreateStandingOrderViewModel`

**Constructor:** `initialAccountId` (account chosen on the list FAB; blank falls back to checking-first), `todayProvider: () -> LocalDate` (injectable for tests).

**Form flow:** `StateFlow<CreateStandingOrderForm>` (default `CreateStandingOrderForm()`).

| Form field        | Type               | Default       | Notes                                                          |
|-------------------|--------------------|---------------|----------------------------------------------------------------|
| accounts          | List\<Account\>    | emptyList()   | Source-account options                                         |
| selectedAccountId | String             | ""            |                                                                |
| sourceAccountName | String             | ""            |                                                                |
| loadingPayees     | Boolean            | true          | Drives the loading state                                       |
| payees            | List\<Counterparty\>| emptyList()  | Beneficiaries of the source account                            |
| selectedPayeeId   | String             | ""            |                                                                |
| amount            | String             | ""            | Maps to RecurringPaymentAmount.Amount                          |
| currency          | String             | "GBP"         | Source account currency → RecurringPaymentAmount.Currency      |
| frequency         | String             | "MONTHLY"     | One of STANDING_ORDER_FREQUENCIES                              |
| startDate         | LocalDate?         | null          | First-payment recurrence anchor                               |
| endDate           | LocalDate?         | null          | Optional                                                       |
| submitting        | Boolean            | false         |                                                                |
| error             | String?            | null          |                                                                |
| consentId         | String             | ""            | `Data.ConsentId` from the consent POST → payment-authorize-handoff|
| created           | Boolean            | false         | true after a successful consent POST (AWAU)                    |

**Constant:** `STANDING_ORDER_FREQUENCIES = [DAILY, WEEKLY, BI-WEEKLY, MONTHLY, YEARLY]`

**Validation:** account present; payee present; amount parses > 0; startDate present and strictly after today; endDate (when set) after startDate.

**Methods:** `onPayeeSelected`, `onSourceAccountSelected`, `onAmountChanged`, `onFrequencySelected`, `onStartDateSelected`, `onEndDateSelected`, `onSubmit`

**DI Dependencies:** `StandingOrdersRepository`, `AccountsRepository`, `PaymentsRepository`, `ProfileRepository`, `CustomersRepository`

---

## Navigation

| From                  | To                       | Trigger                          | Type     |
|-----------------------|--------------------------|----------------------------------|----------|
| standing-orders       | standing-order-create    | create FAB (CreateGate.Ready)    | navigate |
| standing-order-create | payment-authorize-handoff| onSubmit success (AWAU consent)  | navigate |
| standing-order-create | standing-orders          | top-bar back (cancel)            | pop      |

> On the post-authorise return path, a "Standing order created" toast fires and the flow lands back on standing-orders with the new order in the local cache.

---

## API Endpoints

| Endpoint                                                              | Method | Auth               | Tag                          | Purpose                                        |
|----------------------------------------------------------------------|--------|--------------------|------------------------------|------------------------------------------------|
| /obie/open-banking/v4.0/pisp/domestic-standing-order-consents        | POST   | Client Credentials | pisp-domestic-standing-order | Stage the recurring instruction → ConsentId (AWAU) — **this screen's submit** |
| /obie/open-banking/v4.0/pisp/domestic-standing-orders                | POST   | Authorization Code | pisp-domestic-standing-order | Submit the authorised order — run by payment-authorize-handoff after callback, NOT this screen |

> Client (TPP) contract against the HSBC OBIE sandbox (`backend.owned=false`). This screen owns only the consent-create step; the submit step belongs to payment-authorize-handoff. The created order may also be persisted to the local Room JSON cache so it shows in the derived list immediately.

---

## Design Tokens

| Token                           | Value           | Usage                                                          |
|---------------------------------|-----------------|---------------------------------------------------------------|
| colors.light.primary            | #4C662B         | soc_submit_button fill, soc_recurrence_hint text              |
| colors.light.on_primary         | #FFFFFF         | soc_submit_button label                                       |
| colors.light.background         | #F9FAEF         | soc_root background, soc_loading background                   |
| colors.light.on_surface         | #1A1C16         | field values                                                  |
| colors.light.on_surface_variant | #44483D         | soc_frequency_label, soc_no_payees_hint                       |
| colors.light.error              | #BA1A1A         | soc_error_text text                                           |
| typography.label_large          | Outfit 14sp/500 | soc_frequency_label                                           |
| typography.body_medium          | Outfit 14sp/400 | soc_no_payees_hint                                            |
| typography.body_small           | Outfit 12sp/400 | soc_recurrence_hint, soc_error_text                          |
| radius.md                       | 12dp            | inputs, chips, soc_submit_button corner radius               |
| spacing.sm                      | 8dp             | chip spacing, error top margin                               |
| spacing.xl                      | 32dp            | soc_loading padding                                          |

---

_Generated by /idea export | 2026-06-15_
