# API Reference — Transaction Detail

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | transaction-detail                     |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/transaction

**Auth:** DirectLogin
**Tag:** Transactions
**Trigger:** `loadTransactionDetail(transactionId)` on ScreenOpened / RetryLoad event

### Path Parameters

| Name          | Type   | Value          | Description                                |
|---------------|--------|----------------|--------------------------------------------|
| bankId        | String | gh.29.uk       | OBP bank identifier                        |
| accountId     | String | (from session) | Account owning this transaction            |
| transactionId | String | (from nav args)| Unique transaction identifier              |

### Response Fields

| Field                              | Type                   | Description                                   |
|------------------------------------|------------------------|-----------------------------------------------|
| id                                 | String                 | Transaction identifier                        |
| this_account                       | Object                 | Source account reference                      |
| this_account.id                    | String                 | Account ID                                    |
| this_account.account_routings      | List\<AccountRouting\> | IBAN / sort code routings                     |
| other_account                      | Object                 | Counterparty / beneficiary reference          |
| other_account.id                   | String                 | Counterparty ID                               |
| other_account.holder.name          | String                 | Beneficiary display name (e.g. "Tesco PLC")   |
| other_account.holder.is_alias      | Boolean                | true if counterparty name is an alias         |
| other_account.account_routings     | List\<AccountRouting\> | Beneficiary IBAN / routing                    |
| other_account.metadata.image_url   | String?                | Merchant logo URL (if available)              |
| details.type                       | String                 | Transaction type (e.g. "SEPA Credit Transfer")|
| details.description                | String                 | Merchant / reference description              |
| details.posted                     | String                 | ISO-8601 posted timestamp                     |
| details.completed                  | String                 | ISO-8601 completed timestamp                  |
| details.new_balance.currency       | String                 | Account balance currency after transaction    |
| details.new_balance.amount         | String                 | Account balance after transaction             |
| details.value.currency             | String                 | Transaction currency (e.g. "GBP")             |
| details.value.amount               | String                 | Signed amount (e.g. "-42.50")                 |
| metadata.narrative                 | String?                | User-set narrative / note                     |
| metadata.comments                  | List\<Comment\>        | User comments on the transaction              |
| metadata.tags                      | List\<Tag\>            | User-applied tags                             |

### Sample Response

```json
{
  "id": "txn_20260525_001",
  "this_account": {
    "id": "acc-primary-0130",
    "account_routings": [
      { "scheme": "IBAN", "address": "GB29 NWBK 6016 1331 9268 19" }
    ]
  },
  "other_account": {
    "id": "counterparty_tesco_001",
    "holder": { "name": "Tesco PLC", "is_alias": false },
    "account_routings": [
      { "scheme": "IBAN", "address": "DE89 3704 0044 0532 0130 00" }
    ],
    "metadata": { "image_url": "https://cdn.obp.io/logos/tesco.png" }
  },
  "details": {
    "type": "SEPA Credit Transfer",
    "description": "SEPA-2026051500123",
    "posted": "2026-05-25T14:32:00Z",
    "completed": "2026-05-25T14:32:00Z",
    "new_balance": { "currency": "GBP", "amount": "4207.50" },
    "value": { "currency": "GBP", "amount": "-42.50" }
  },
  "metadata": {
    "narrative": null,
    "comments": [],
    "tags": []
  }
}
```

### Error Codes

| Code | Message                                      | UI Behaviour                                    |
|------|----------------------------------------------|-------------------------------------------------|
| 401  | Unauthorized — DirectLogin token expired     | Redirect to login screen                        |
| 404  | Transaction not found                        | Show error state: "Transaction not found"       |
| 500  | OBP server error                             | Show error state with retry action              |

---

_Generated by /idea export | 2026-05-29_
