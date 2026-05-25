# Direct Debits — API Reference

| Field | Value |
|---|---|
| Feature | direct-debits |
| Base URL | https://apisandbox.openbankproject.com |
| Auth | DirectLogin (header: `DirectLogin token=<token>`) |

---

## List Direct Debit Mandates

**GET** `/obp/v3.0.0/banks/{bank_id}/accounts/{account_id}/direct-debits`

Retrieves all direct debit mandates (active and cancelled) for the specified account. This is the primary read endpoint populating the direct-debits list screen.

**Auth:** DirectLogin

**Path Parameters:**

| Param | Type | Description |
|---|---|---|
| bank_id | String | OBP bank identifier (e.g., `gb.mifos`) |
| account_id | String | Account to retrieve mandates for |

**Query Parameters:** None

**Request Body:** None

**Response Fields:**

| Field | Type | Description |
|---|---|---|
| direct_debits | Array\<DirectDebit\> | List of all mandates for the account |

**DirectDebit Object:**

| Field | Type | Description |
|---|---|---|
| direct_debit_id | String | Unique mandate identifier (used for cancellation) |
| bank_id | String | OBP bank identifier |
| account_id | String | Debited account identifier |
| counterparty_id | String | Payee counterparty reference |
| merchant_name | String | Display name of the collecting merchant |
| amount_value | String | Per-collection amount (decimal string) |
| amount_currency | String | ISO 4217 currency code (e.g., "GBP") |
| frequency | String | Collection frequency (e.g., "MONTHLY") |
| start_date | String | ISO 8601 mandate start date |
| end_date | String | ISO 8601 mandate end date; null if indefinite |
| next_collection_date | String | ISO 8601 date of next scheduled collection |
| active | Boolean | true if mandate is currently active |
| mandate_reference | String | Bank-assigned mandate reference (e.g., "DD-NF-20240301") |

**Sample Response:**

```json
{
  "direct_debits": [
    {
      "direct_debit_id": "dd-netflix-uuid-001",
      "bank_id": "gb.mifos",
      "account_id": "acc-primary-0130",
      "counterparty_id": "netflix-counterparty-uuid",
      "merchant_name": "Netflix",
      "amount_value": "15.99",
      "amount_currency": "GBP",
      "frequency": "MONTHLY",
      "start_date": "2024-03-01",
      "end_date": null,
      "next_collection_date": "2026-06-03",
      "active": true,
      "mandate_reference": "DD-NF-20240301"
    },
    {
      "direct_debit_id": "dd-spotify-uuid-002",
      "bank_id": "gb.mifos",
      "account_id": "acc-primary-0130",
      "counterparty_id": "spotify-counterparty-uuid",
      "merchant_name": "Spotify",
      "amount_value": "10.99",
      "amount_currency": "GBP",
      "frequency": "MONTHLY",
      "start_date": "2023-11-15",
      "end_date": null,
      "next_collection_date": "2026-06-12",
      "active": true,
      "mandate_reference": "DD-SP-20231115"
    },
    {
      "direct_debit_id": "dd-gym-uuid-003",
      "bank_id": "gb.mifos",
      "account_id": "acc-primary-0130",
      "counterparty_id": "puregym-counterparty-uuid",
      "merchant_name": "PureGym",
      "amount_value": "29.99",
      "amount_currency": "GBP",
      "frequency": "MONTHLY",
      "start_date": "2022-06-01",
      "end_date": "2026-04-30",
      "next_collection_date": null,
      "active": false,
      "mandate_reference": "DD-GYM-20220601"
    }
  ]
}
```

**Error Codes:**

| Code | Message | UI Behaviour |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 403 | INSUFFICIENT_AUTHORISATION | Show LOAD_FAILED error state |
| 404 | BANK_ACCOUNT_NOT_FOUND | Show LOAD_FAILED error state |

---

## Cancel Direct Debit Mandate

**DELETE** `/obp/v3.0.0/banks/{bank_id}/accounts/{account_id}/direct-debits/{direct_debit_id}`

Cancels an existing direct debit mandate. This is a destructive, irreversible operation — the mandate will stop collecting future payments after cancellation. The UI guards this with a `cancel_confirm` dialog (RULE-PROTO-CONTENT-001: no accidental destructive actions).

**Auth:** DirectLogin

**Path Parameters:**

| Param | Type | Description |
|---|---|---|
| bank_id | String | OBP bank identifier |
| account_id | String | Account the mandate belongs to |
| direct_debit_id | String | Unique mandate identifier from the list response |

**Request Body:** None

**Response (HTTP 200):**

```json
{
  "direct_debit_id": "dd-netflix-uuid-001",
  "active": false,
  "cancelled_at": "2026-05-25T14:32:00Z"
}
```

**Error Codes:**

| Code | Message | UI Behaviour |
|---|---|---|
| 400 | INVALID_DIRECT_DEBIT_ID | Show CANCEL_FAILED error toast |
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 403 | INSUFFICIENT_AUTHORISATION | Show CANCEL_FAILED error toast |
| 404 | DIRECT_DEBIT_NOT_FOUND | Show CANCEL_FAILED error toast |
| 409 | MANDATE_ALREADY_CANCELLED | Reload mandate list (treat as success) |

---

## Create Direct Debit Mandate

**POST** `/obp/v4.0.0/banks/{bank_id}/accounts/{account_id}/owner/direct-debit`

Creates a new direct debit mandate authorising a payee to collect from the account. Triggered by the "Set Up Direct Debit" FAB flow.

**Auth:** DirectLogin

**Path Parameters:**

| Param | Type | Description |
|---|---|---|
| bank_id | String | OBP bank identifier |
| account_id | String | Account to be debited |

**Request Fields:**

| Field | Type | Required | Description |
|---|---|---|---|
| start_date | String | Yes | ISO 8601 mandate start date (YYYY-MM-DD) |
| end_date | String | No | ISO 8601 mandate end date; omit for indefinite |
| to | DirectDebitCounterparty | Yes | Payee counterparty details |
| amount_value | String | Yes | Per-collection amount (decimal string) |
| amount_currency | String | Yes | ISO 4217 currency code |

**Request Body:**

```json
{
  "start_date": "2026-06-01",
  "end_date": null,
  "to": {
    "counterparty_id": "netflix-counterparty-uuid"
  },
  "amount_value": "15.99",
  "amount_currency": "GBP"
}
```

**Response Fields:**

| Field | Type | Description |
|---|---|---|
| direct_debit_id | String | Newly created mandate identifier |
| bank_id | String | Bank identifier |
| account_id | String | Debited account identifier |
| counterparty_id | String | Payee counterparty reference |
| amount_value | String | Authorised collection amount |
| amount_currency | String | Currency code |
| start_date | String | Mandate effective from |
| end_date | String | Mandate expires on (null if indefinite) |
| active | Boolean | true on creation |

**Error Codes:**

| Code | Message | UI Behaviour |
|---|---|---|
| 400 | INVALID_BANK_ID | Show CREATE_FAILED error toast |
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 403 | INSUFFICIENT_AUTHORISATION | Show CREATE_FAILED error toast |
| 404 | BANK_ACCOUNT_NOT_FOUND | Show CREATE_FAILED error toast |

---

## Mandate Data Shown in UI (Populated State)

| Merchant | Amount | Frequency | Next Collection | Status | Mandate Ref |
|---|---|---|---|---|---|
| Netflix | £15.99 | Monthly | 3 Jun 2026 | Active | DD-NF-20240301 |
| Spotify | £10.99 | Monthly | 12 Jun 2026 | Active | DD-SP-20231115 |
| PureGym | £29.99 | Monthly | — | Cancelled | DD-GYM-20220601 |

---

## Implementation Notes

**Active count:** Derive `activeCount` client-side from `directDebits.count { it.active }`. The UI chip reads this value from `DirectDebitsViewModel.activeCount`.

**Cancelled mandate display:** Include `active: false` mandates in the list response — the UI renders them in a muted style for audit traceability. Do not filter them server-side.

**Cancellation flow (ViewModel):**
1. `CancelDirectDebitClicked` → set `selectedMandate`, `showCancelDialog = true`
2. `CancelConfirmed` → call `DELETE` endpoint with `selectedMandate.directDebitId`
3. On HTTP 200 or 409 → reload mandate list (`GET`), clear `selectedMandate`, set `showCancelDialog = false`
4. On other error → show `CANCEL_FAILED` toast, keep dialog open

**Next collection date:** If `next_collection_date` is null (for cancelled/expired mandates), omit the "Next: …" row entirely in the card — the PureGym cancelled card does not show a next date.

**Mandate reference:** Surface the `mandate_reference` on every card in `label_small` muted style. Required for user support and audit. Injected into the cancel confirm dialog body for user confirmation.

**Navigation back:** `navigate_back` targets the `accounts` screen (not home), supporting the "payments" section sub-navigation pattern.

---

*Generated by /idea export | 2026-05-25*
