# API Reference — Transaction Tags & Notes

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | transaction-tags                       |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** Screen entry — fetch existing tags for the transaction

### Path Parameters

| Name          | Type   | Value          |
|---------------|--------|----------------|
| bankId        | String | gh.29.uk       |
| accountId     | String | (from session) |
| transactionId | String | (from nav args)|

### Response Fields

| Field      | Type                   | Description                       |
|------------|------------------------|-----------------------------------|
| tags       | List\<TransactionTag\> | All tags on this transaction      |
| id         | String                 | Tag identifier                    |
| value      | String                 | Tag value (e.g. "#groceries")     |
| date       | String                 | ISO-8601 creation timestamp       |
| user       | User                   | Author of the tag                 |

### Error Codes

| Code | Message                    |
|------|----------------------------|
| 401  | USER_NOT_LOGGED_IN         |
| 403  | INSUFFICIENT_AUTHORISATION |
| 404  | TRANSACTION_NOT_FOUND      |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `add_tag` action — user types tag in add_tag_input and taps "Add" button

### Request Body Fields

| Field | Type   | Required | Example       |
|-------|--------|----------|---------------|
| value | String | Yes      | "#groceries"  |

### Response Fields

| Field | Type   | Description                     |
|-------|--------|---------------------------------|
| id    | String | Newly created tag identifier    |
| value | String | Tag value as submitted          |
| date  | String | ISO-8601 creation timestamp     |

### Error Codes

| Code | Message             |
|------|---------------------|
| 400  | INVALID_TAG_VALUE   |
| 401  | USER_NOT_LOGGED_IN  |

---

## DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `remove_tag` action — user taps an existing tag chip

### Path Parameters

| Name          | Type   | Description         |
|---------------|--------|---------------------|
| tagId         | String | Tag to be removed   |

### Response Fields

| Field  | Type   | Example    |
|--------|--------|------------|
| result | String | "Success"  |

### Error Codes

| Code | Message            |
|------|--------------------|
| 401  | USER_NOT_LOGGED_IN |
| 404  | TAG_NOT_FOUND      |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `save_metadata` action — user taps "Save" with notes text populated

### Request Body Fields

| Field | Type   | Required | Example                                       |
|-------|--------|----------|-----------------------------------------------|
| value | String | Yes      | "Weekly shop — bought extra for bank holiday" |

### Response Fields

| Field | Type   | Description                        |
|-------|--------|------------------------------------|
| id    | String | Newly created comment identifier   |
| value | String | Comment text as submitted          |
| date  | String | ISO-8601 creation timestamp        |

### Error Codes

| Code | Message               |
|------|-----------------------|
| 400  | INVALID_COMMENT_VALUE |
| 401  | USER_NOT_LOGGED_IN    |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `save_metadata` action — user has attached a receipt image via gallery or camera

### Request Body Fields

| Field | Type   | Required | Example                               |
|-------|--------|----------|---------------------------------------|
| label | String | Yes      | "Whole Foods receipt 23-May-2026"     |
| URL   | String | Yes      | Hosted URL of the receipt image       |

### Response Fields

| Field | Type   | Description                       |
|-------|--------|-----------------------------------|
| id    | String | Newly created image identifier    |
| label | String | Image label                       |
| URL   | String | Stored image URL                  |
| date  | String | ISO-8601 creation timestamp       |

### Error Codes

| Code | Message             |
|------|---------------------|
| 400  | INVALID_IMAGE_URL   |
| 401  | USER_NOT_LOGGED_IN  |

---

_Generated by /idea export | 2026-05-29_
