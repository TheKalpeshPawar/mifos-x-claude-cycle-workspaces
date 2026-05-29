# API Reference — Transaction Tags & Notes

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | transaction-tags                       |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** Screen entry (`MetadataLoaded`) and `RetryLoad` event — fetches all tags previously attached to this transaction.

### Path Parameters

| Name          | Type   | Value                              | Description                     |
|---------------|--------|------------------------------------|---------------------------------|
| bankId        | String | gh.29.uk                           | Bank identifier                 |
| accountId     | String | (from session / nav args)          | Account owning the transaction  |
| transactionId | String | (from nav args)                    | Transaction being annotated     |

### Response Fields

| Field      | Type                   | Description                                         |
|------------|------------------------|-----------------------------------------------------|
| tags       | List\<TransactionTag\> | All tags currently attached to this transaction     |
| id         | String                 | Tag identifier                                      |
| value      | String                 | Tag value (e.g. "#groceries")                       |
| date       | String                 | ISO-8601 creation timestamp                         |
| user       | User                   | User object — id + username of tag author           |

### Demo Data (Kenyan persona — amina.wanjiru)

| id         | value        | date                        | user.username       |
|------------|--------------|-----------------------------|---------------------|
| tag-ke-001 | #groceries   | 2026-05-22T12:01:00+03:00   | amina.wanjiru       |
| tag-ke-002 | #transport   | 2026-05-22T12:02:00+03:00   | amina.wanjiru       |
| tag-ke-003 | #utilities   | 2026-05-24T18:00:00+03:00   | amina.wanjiru       |

### Error Codes

| Code | Message                    | UI Handling                         |
|------|----------------------------|-------------------------------------|
| 401  | USER_NOT_LOGGED_IN         | Navigate to login                   |
| 403  | INSUFFICIENT_AUTHORISATION | Show error state; no retry          |
| 404  | TRANSACTION_NOT_FOUND      | Show error state with retry         |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `add_tag` action — user types a tag in `add_tag_input` and taps "Add"; fires `TagAdded(value)` event on success.

### Path Parameters

| Name          | Type   | Value                     | Description                    |
|---------------|--------|---------------------------|--------------------------------|
| bankId        | String | gh.29.uk                  | Bank identifier                |
| accountId     | String | (from session / nav args) | Account owning the transaction |
| transactionId | String | (from nav args)           | Transaction being annotated    |

### Request Body Fields

| Field | Type   | Required | Example      | Validation                          |
|-------|--------|----------|--------------|-------------------------------------|
| value | String | Yes      | "#groceries" | Non-empty; TAG_DUPLICATE guard in VM |

### Response Fields

| Field | Type   | Description                           |
|-------|--------|---------------------------------------|
| id    | String | Newly created tag identifier          |
| value | String | Tag value exactly as submitted        |
| date  | String | ISO-8601 creation timestamp           |

### Demo Data

| id         | value  | date                      |
|------------|--------|---------------------------|
| tag-ke-004 | #rent  | 2026-05-23T15:00:00+03:00 |

### Error Codes

| Code | Message           | UI Handling                             |
|------|-------------------|-----------------------------------------|
| 400  | INVALID_TAG_VALUE | Show inline TAG_SAVE_FAILED error toast |
| 401  | USER_NOT_LOGGED_IN| Navigate to login                       |

---

## DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `remove_tag` action — user taps an existing tag chip; fires `TagRemoved(value)` event on success.

### Path Parameters

| Name          | Type   | Value                     | Description                      |
|---------------|--------|---------------------------|----------------------------------|
| bankId        | String | gh.29.uk                  | Bank identifier                  |
| accountId     | String | (from session / nav args) | Account owning the transaction   |
| transactionId | String | (from nav args)           | Transaction being annotated      |
| tagId         | String | e.g. tag-ke-001           | Identifier of the tag to remove  |

### Response Fields

| Field  | Type   | Example   | Description               |
|--------|--------|-----------|---------------------------|
| result | String | "Success" | Confirmation of deletion  |

### Demo Data

| result  |
|---------|
| Success |

### Error Codes

| Code | Message            | UI Handling                          |
|------|--------------------|--------------------------------------|
| 401  | USER_NOT_LOGGED_IN | Navigate to login                    |
| 404  | TAG_NOT_FOUND      | Silently remove chip; show toast     |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `save_metadata` action — fired when user taps "Save" and `noteText` is non-empty; bound to `notes_text_area` via `obp_transaction_comment_add`.

### Path Parameters

| Name          | Type   | Value                     | Description                    |
|---------------|--------|---------------------------|--------------------------------|
| bankId        | String | gh.29.uk                  | Bank identifier                |
| accountId     | String | (from session / nav args) | Account owning the transaction |
| transactionId | String | (from nav args)           | Transaction being annotated    |

### Request Body Fields

| Field | Type   | Required | Example                                         |
|-------|--------|----------|-------------------------------------------------|
| value | String | Yes      | "Paid via Equity mobile — confirmed by SMS KES 3,420" |

### Response Fields

| Field | Type   | Description                         |
|-------|--------|-------------------------------------|
| id    | String | Newly created comment identifier    |
| value | String | Comment text exactly as submitted   |
| date  | String | ISO-8601 creation timestamp         |

### Demo Data

| id         | value                                               | date                      |
|------------|-----------------------------------------------------|---------------------------|
| cmt-ke-002 | Paid via Equity mobile — confirmed by SMS KES 3,420 | 2026-05-22T12:10:00+03:00 |

### Error Codes

| Code | Message               | UI Handling                              |
|------|-----------------------|------------------------------------------|
| 400  | INVALID_COMMENT_VALUE | Show inline NOTE_SAVE_FAILED error toast |
| 401  | USER_NOT_LOGGED_IN    | Navigate to login                        |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `save_metadata` action — fired when user has attached a receipt image via `pick_image_from_gallery` or `open_camera`; bound to `receipt_attachment_area` via `obp_transaction_image_add`.

### Path Parameters

| Name          | Type   | Value                     | Description                    |
|---------------|--------|---------------------------|--------------------------------|
| bankId        | String | gh.29.uk                  | Bank identifier                |
| accountId     | String | (from session / nav args) | Account owning the transaction |
| transactionId | String | (from nav args)           | Transaction being annotated    |

### Request Body Fields

| Field | Type   | Required | Example                            | Description                          |
|-------|--------|----------|------------------------------------|--------------------------------------|
| label | String | Yes      | "Carrefour receipt 22-May-2026"    | Human-readable label for the image   |
| URL   | String | Yes      | (hosted CDN URL of captured image) | Publicly reachable receipt image URL |

### Response Fields

| Field | Type   | Description                        |
|-------|--------|------------------------------------|
| id    | String | Newly created image record ID      |
| label | String | Image label as submitted           |
| URL   | String | Stored receipt image URL           |
| date  | String | ISO-8601 creation timestamp        |

### Demo Data

| id         | label                         | URL                                                                         | date                      |
|------------|-------------------------------|-----------------------------------------------------------------------------|---------------------------|
| img-ke-001 | Carrefour receipt 22-May-2026 | https://receipts.equitybank.co.ke/2026/05/22/txn-ke-20260522-44001.jpg     | 2026-05-22T12:15:00+03:00 |

### Error Codes

| Code | Message             | UI Handling                               |
|------|---------------------|-------------------------------------------|
| 400  | INVALID_IMAGE_URL   | Show inline IMAGE_SAVE_FAILED error toast |
| 401  | USER_NOT_LOGGED_IN  | Navigate to login                         |

---

_Generated by /idea export | 2026-05-30_
