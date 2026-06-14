# API Reference — Business Insights

| Field    | Value                                             |
|----------|---------------------------------------------------|
| Feature  | business-insights                                 |
| Base URL | https://sandbox.ob.hsbc.co.uk/obie/open-banking   |

---

## GET /obie/open-banking/v4.0/aisp/accounts

**Auth:** Authorization Code (OBIE authorization-code token with account-access consent, Status AUTH)
**Tag:** AISP
**Trigger:** `LoadInsights` intent on screen entry; `SelectAccount` when the account picker is opened

Returns the list of authorised accounts (`OBReadAccount6`). Business-scope filtering happens **client-side** — `Data.Account[].AccountCategory` is compared against "Business" (and `AccountTypeCode` for refinement). OBIE v4.0 has no PFM-scope flag; all scope logic is derived from account metadata. The resulting list drives the account picker chip (`biz_account_selector`).

### Consent

Requires an authorised account-access consent (Status AUTH) carrying at minimum `ReadAccounts`, plus a scoped authorization-code token.

### Response Fields

| Field                              | Type   | Description                                                        |
|------------------------------------|--------|--------------------------------------------------------------------|
| Data.Account[].AccountId           | String | Unique account identifier — used in subsequent per-account calls   |
| Data.Account[].Currency            | String | ISO 4217 account currency (e.g. GBP)                               |
| Data.Account[].AccountCategory     | String | Scope discriminator — client filters to "Business"                  |
| Data.Account[].AccountTypeCode     | String | Refinement discriminator (e.g. CurrentAccount)                     |
| Data.Account[].Nickname            | String | Display label (e.g. "TechStart — Business Current GBP")            |

### Demo Data

| AccountId               | AccountCategory | AccountTypeCode | Nickname                          | Currency |
|-------------------------|-----------------|-----------------|-----------------------------------|----------|
| acc-techstart-gbp-biz-01 | Business       | CurrentAccount  | TechStart — Business Current GBP | GBP      |

### Error Codes

| Code | OBIE Error Name                  | UI Handling                                              |
|------|----------------------------------|----------------------------------------------------------|
| 401  | UNAUTHORIZED                     | Navigate to login; session expired                       |
| 403  | OB.Resource.InvalidConsentStatus | error state: "Could not load business insights"          |

---

## GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/balances

**Auth:** Authorization Code (OBIE authorization-code token with account-access consent, Status AUTH)
**Tag:** AISP
**Trigger:** `LoadInsights` intent after `get_accounts` resolves the in-scope account

Returns current balance context for the selected account (`OBReadBalance1`). Used to provide balance context; the primary cash-flow figures (Money In / Money Out / Net) are derived client-side from the transaction list, not from this endpoint.

### Consent

Requires an authorised account-access consent (Status AUTH) carrying `ReadBalances`, plus a scoped authorization-code token.

### Path Parameters

| Name      | Type   | Required | Demo Value               | Description              |
|-----------|--------|----------|--------------------------|--------------------------|
| AccountId | String | Yes      | acc-techstart-gbp-biz-01 | In-scope business account |

### Response Fields

| Field                               | Type   | Description                                             |
|-------------------------------------|--------|---------------------------------------------------------|
| Data.Balance[].AccountId            | String | Account the balance belongs to                          |
| Data.Balance[].Amount.Amount        | String | Balance figure (e.g. "48700.00")                        |
| Data.Balance[].Amount.Currency      | String | ISO 4217 currency (e.g. GBP)                           |
| Data.Balance[].CreditDebitIndicator | String | Credit or Debit                                         |
| Data.Balance[].Type                 | String | Balance type (e.g. InterimAvailable, ClosingBooked)     |

### Demo Data

| AccountId               | Amount.Amount | Currency | CreditDebitIndicator | Type              |
|-------------------------|---------------|----------|----------------------|-------------------|
| acc-techstart-gbp-biz-01 | 48700.00     | GBP      | Credit               | InterimAvailable  |

### Error Codes

| Code | OBIE Error Name                  | UI Handling                                              |
|------|----------------------------------|----------------------------------------------------------|
| 401  | UNAUTHORIZED                     | Navigate to login; session expired                       |
| 403  | OB.Resource.InvalidConsentStatus | error state: "Could not load business insights"          |

---

## GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/transactions

**Auth:** Authorization Code (OBIE authorization-code token with account-access consent, Status AUTH)
**Tag:** AISP
**Trigger:** `LoadInsights` and `SelectPeriod` intents — fetches the transaction window used for all client-side derivation

The primary data source for the Business Insights dashboard. All cash-flow aggregation (Money In / Money Out / Net), the 8-category expense breakdown, and the top-counterparty ranking are **derived client-side** from this list — OBIE v4.0 has no insights or analytics endpoint. `fromBookingDateTime` and `toBookingDateTime` query params (UTC ISO 8601) define the reporting window for the selected period. Period re-selection re-issues this call (or re-slices a cached window client-side within the consented range).

The **Income** category absorbs credit keywords during categorisation but is excluded from the expenses-only donut chart.

### Consent

Requires an authorised account-access consent (Status AUTH) carrying a `ReadTransactions*` permission (minimum `ReadTransactionsBasic`; `ReadTransactionsDetail` required for `TransactionInformation` and `MerchantDetails`), plus a scoped authorization-code token.

### Path Parameters

| Name      | Type   | Required | Demo Value               | Description                           |
|-----------|--------|----------|--------------------------|---------------------------------------|
| AccountId | String | Yes      | acc-techstart-gbp-biz-01 | Selected business account             |

### Query Parameters

| Name                  | Type   | Required | Example                    | Description                              |
|-----------------------|--------|----------|----------------------------|------------------------------------------|
| fromBookingDateTime   | String | No       | 2026-06-01T00:00:00Z       | Period start (UTC ISO 8601)              |
| toBookingDateTime     | String | No       | 2026-06-30T23:59:59Z       | Period end (UTC ISO 8601)                |

### Response Fields

| Field                                              | Type   | Description                                                                        |
|----------------------------------------------------|--------|------------------------------------------------------------------------------------|
| Data.Transaction[].TransactionId                   | String | Unique transaction ID                                                              |
| Data.Transaction[].Amount.Amount                   | String | Transaction amount (unsigned magnitude)                                            |
| Data.Transaction[].Amount.Currency                 | String | ISO 4217 currency                                                                  |
| Data.Transaction[].CreditDebitIndicator            | String | "Credit" (Money In) or "Debit" (Money Out)                                         |
| Data.Transaction[].BookingDateTime                 | String | Settled timestamp (UTC ISO 8601) — used for period filtering                       |
| Data.Transaction[].TransactionInformation          | String | Free-text description — primary categorisation signal                              |
| Data.Transaction[].MerchantDetails.MerchantName    | String | Merchant name (when present) — preferred counterparty display name source          |
| Data.Transaction[].CreditorAccount.Identification  | String | Creditor account reference — used for counterparty resolution                      |
| Data.Transaction[].DebtorAccount.Identification    | String | Debtor account reference — used for counterparty resolution                        |

### Demo Data — Period: June 2026

**Derived cash-flow figures (client-side):**

| Metric    | Value       |
|-----------|-------------|
| Money In  | £75000.00   |
| Money Out | -£26300.00  |
| Net       | £48700.00   |

**Expense category breakdown (expenses-only donut; Income excluded):**

| Category                  | Amount      |
|---------------------------|-------------|
| Payroll & Contractors     | -£15516.01  |
| Tax                       | -£8000.00   |
| Rent & Facilities         | -£2500.00   |
| Software & Subscriptions  | -£450.00    |
| Insurance                 | -£350.00    |

**Top counterparty:**

| Counterparty        | Payment Count | Total       |
|---------------------|---------------|-------------|
| Mifos-X-Open-Bank   | 1             | -£15000.00  |

### Client-Side Derivation Notes

- **Cash flow:** sum `Amount.Amount` where `CreditDebitIndicator = Credit` → Money In; where `Debit` → Money Out; Net = In + Out (signed sum).
- **Categorisation:** debits bucketed by matching `TransactionInformation` / `MerchantDetails.MerchantName` keywords against the 8-category taxonomy. Income absorbs credit keywords but is excluded from the donut.
- **Counterparty display:** precedence — `MerchantDetails.MerchantName` > resolved Creditor/Debtor account holder name > `TransactionInformation`. Raw login usernames (OBP `other_account.holder.name`) are never displayed.

### Error Codes

| Code | OBIE Error Name                  | UI Handling                                                             |
|------|----------------------------------|-------------------------------------------------------------------------|
| 401  | UNAUTHORIZED                     | Navigate to login; session expired                                      |
| 403  | OB.Resource.InvalidConsentStatus | error state: "Could not load business insights"                         |
| —    | Network / timeout                | error state: "Check your connection and try again." + `retry_load` CTA |

---

_Generated by /idea export | 2026-06-14_
