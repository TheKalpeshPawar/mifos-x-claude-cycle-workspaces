# API Reference — Card Detail

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | card-detail                            |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v5.1.0/banks/{bankId}/cards/{cardId}

**Auth:** DirectLogin
**Tag:** Cards
**Trigger:** `CardDetailViewModel.loadCard()` on screen entry / `RetryLoad` event

Fetches the full card record for a specific card. The ViewModel maps the response to `CardDetailUiState`, populating the masked PAN display (`bank_card_number`), cardholder name (`name_on_card`), expiry date (`expires`, formatted MM/YY), network logo (`card_network`), and active status (`enabled`). The `on_hot_list` flag maps to `isFrozen` — when `true` the card visual shows the frozen overlay and the freeze button switches to "Unfreeze Card". `cancelled: true` triggers the empty state.

### Path Parameters

| Name   | Type   | Example                  | Description                                         |
|--------|--------|--------------------------|-----------------------------------------------------|
| bankId | String | kcb-ke                   | OBP bank identifier                                 |
| cardId | String | card-kcb-visa-mwangi-001 | Card unique identifier (from the cards list screen) |

### Response Fields

| Field            | Type             | Description                                                              |
|------------------|------------------|--------------------------------------------------------------------------|
| id               | String           | Unique card identifier                                                   |
| bank_id          | String           | Bank that issued the card (e.g. "kcb-ke")                               |
| bank_card_number | String           | Masked or full PAN (e.g. "4111 **** **** 3421")                         |
| name_on_card     | String           | Cardholder name as embossed (e.g. "JOHN K MWANGI")                      |
| card_type        | String           | e.g. "DEBIT", "CREDIT"                                                  |
| card_description | String           | Human-readable card product name (e.g. "KCB Visa Classic Debit Card")   |
| card_network     | String           | Payment network (e.g. "VISA", "MASTERCARD")                             |
| allows           | List\<String\>   | Permitted operations: "credit", "debit", "cash_withdrawal", "online_payment", "contactless" |
| enabled          | Boolean          | `true` = card is active; maps to `isActive` in ViewModel                |
| cancelled        | Boolean          | `true` = permanently cancelled; triggers empty state                    |
| on_hot_list      | Boolean          | `true` = card is frozen/hot-listed; maps to `isFrozen` in ViewModel     |
| technology       | String           | e.g. "CHIP_AND_PIN", "CHIP_AND_SIGNATURE"                               |
| expires          | String           | Expiry date ISO-8601 (e.g. "2028-05-31"); ViewModel formats as "MM/YY"  |
| replacement      | CardReplacement  | Replacement request status object (nullable)                             |

### Demo Data

| Field            | Value                                                              |
|------------------|--------------------------------------------------------------------|
| id               | card-kcb-visa-mwangi-001                                           |
| bank_id          | kcb-ke                                                             |
| bank_card_number | 4111 **** **** 3421                                                |
| name_on_card     | JOHN K MWANGI                                                      |
| card_type        | DEBIT                                                              |
| card_description | KCB Visa Classic Debit Card                                        |
| card_network     | VISA                                                               |
| allows           | credit, debit, cash_withdrawal, online_payment, contactless        |
| enabled          | true                                                               |
| cancelled        | false                                                              |
| on_hot_list      | false                                                              |
| technology       | CHIP_AND_PIN                                                       |
| expires          | 2028-05-31 (rendered as "05/28" on card visual)                   |

### Error Codes

| Code | OBP Message                | UI Handling                                         |
|------|----------------------------|-----------------------------------------------------|
| 400  | INVALID_CARD_ID            | Show error state with retry button                  |
| 401  | USER_NOT_LOGGED_IN         | Navigate to login screen                            |
| 403  | INSUFFICIENT_AUTHORISATION | Show error state ("Please try again or contact support") |
| 404  | CARD_NOT_FOUND             | Show empty state ("Card may have been cancelled or removed") |

---

_Generated by /idea export | 2026-05-30_
