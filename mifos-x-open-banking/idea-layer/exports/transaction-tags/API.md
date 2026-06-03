# API Reference — Transaction Tags & Notes

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | transaction-tags                       |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** Screen entry (`MetadataLoaded`) and `RetryLoad` event — fetches all tags previously attached to this transaction. Bound to `tags_chips_row` component via `endpoint_id: obp_transaction_tags_get`.

### Path Parameters

| Name          | Type   | Value          | Description                                     |
|---------------|--------|----------------|-------------------------------------------------|
| bankId        | String | gh.29.uk       | Bank identifier from active session context     |
| accountId     | String | acc-wanjiru-001| Account identifier from transaction context     |
| transactionId | String | txn-wfm-230526 | Transaction ID from navigation argument         |

### Response Fields

| Field | Type                   | Description                                   |
|-------|------------------------|-----------------------------------------------|
| tags  | `List<TransactionTag>` | Existing tags on this transaction              |
| id    | String                 | Tag identifier (used for DELETE)               |
| value | String                 | Tag text (e.g. `"#groceries"`)                 |
| date  | String                 | ISO-8601 date tag was added                    |
| user  | User                   | User who created the tag                       |

### Error Codes

| Code | OBP Message                | UI Mapping                                        |
|------|----------------------------|---------------------------------------------------|
| 401  | `USER_NOT_LOGGED_IN`       | Error state — `cloud_off` icon + retry button     |
| 403  | `INSUFFICIENT_AUTHORISATION` | Error state                                     |
| 404  | `TRANSACTION_NOT_FOUND`    | Error state — "Unable to load metadata"           |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `TagAdded(value: String)` event — fired when user taps "Add" button with a non-empty, non-duplicate tag in the `add_tag_input`.

### Request Body

| Field | Type   | Required | Example        | Notes                             |
|-------|--------|----------|----------------|-----------------------------------|
| value | String | Yes      | `"#groceries"` | Must start with `#`; no spaces    |

### Response Fields

| Field | Type   | Description                           |
|-------|--------|---------------------------------------|
| id    | String | OBP-assigned tag identifier           |
| value | String | Echo of submitted tag value           |
| date  | String | ISO-8601 timestamp when tag was added |

### Error Codes

| Code | OBP Message          | UI Mapping                                    |
|------|----------------------|-----------------------------------------------|
| 400  | `INVALID_TAG_VALUE`  | Inline error: "Could not add tag."            |
| 401  | `USER_NOT_LOGGED_IN` | Global error state                            |

---

## DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `TagRemoved(value: String)` event — fired when user taps an existing tag chip (remove gesture).

### Path Parameters

| Name   | Type   | Description                                     |
|--------|--------|-------------------------------------------------|
| tagId  | String | Tag identifier from `obp_transaction_tags_get` response |

### Response Fields

| Field  | Type   | Description       |
|--------|--------|-------------------|
| result | String | `"Success"`       |

### Error Codes

| Code | OBP Message          | UI Mapping                       |
|------|----------------------|----------------------------------|
| 401  | `USER_NOT_LOGGED_IN` | Global error state               |
| 404  | `TAG_NOT_FOUND`      | Silently remove chip from UI     |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `SaveClicked` event — saves the private transaction note. Bound to `notes_text_area` via `endpoint_id: obp_transaction_comment_add`, `binds: noteText`.

### Request Body

| Field | Type   | Required | Example                                             |
|-------|--------|----------|-----------------------------------------------------|
| value | String | Yes      | `"Weekly shop — bought extra for bank holiday"`    |

### Response Fields

| Field | Type   | Description                                   |
|-------|--------|-----------------------------------------------|
| id    | String | Comment identifier                            |
| value | String | Saved note text                               |
| date  | String | ISO-8601 timestamp                            |

### Error Codes

| Code | OBP Message              | UI Mapping                             |
|------|--------------------------|----------------------------------------|
| 400  | `INVALID_COMMENT_VALUE`  | Error: "Could not save note."          |
| 401  | `USER_NOT_LOGGED_IN`     | Global error state                     |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images

**Auth:** DirectLogin
**Tag:** Transaction-Metadata
**Trigger:** `ImagePicked(uri)` or `CameraCaptured(uri)` event — attaches receipt image. Bound to `receipt_attachment_area` via `endpoint_id: obp_transaction_image_add`, `binds: attachedImages`.

### Request Body

| Field | Type   | Required | Example                                  | Notes                              |
|-------|--------|----------|------------------------------------------|------------------------------------|
| label | String | Yes      | `"Whole Foods receipt 23-May-2026"`      | Human-readable label for the image |
| URL   | String | Yes      | `"https://storage.mifos.io/rcpt/..."`   | Pre-uploaded image URL             |

### Response Fields

| Field | Type   | Description          |
|-------|--------|----------------------|
| id    | String | Image identifier     |
| label | String | Echo of image label  |
| URL   | String | Echo of image URL    |
| date  | String | ISO-8601 timestamp   |

### Error Codes

| Code | OBP Message           | UI Mapping                              |
|------|-----------------------|-----------------------------------------|
| 400  | `INVALID_IMAGE_URL`   | Error: "Could not attach image."        |
| 401  | `USER_NOT_LOGGED_IN`  | Global error state                      |

---

## Demo Data

**Transaction context (Amina Wanjiru, Whole Foods Market):**

| Field         | Value                     |
|---------------|---------------------------|
| bankId        | `"gh.29.uk"`              |
| accountId     | `"acc-wanjiru-001"`       |
| transactionId | `"txn-wfm-230526"`        |

**GET tags — demo response:**

```json
{
  "tags": [
    {"id": "tag-001", "value": "#groceries", "date": "2026-05-23T14:32:00Z"},
    {"id": "tag-002", "value": "#work-expense", "date": "2026-05-23T14:33:00Z"}
  ]
}
```

---

_Generated by /idea export | 2026-06-02_
