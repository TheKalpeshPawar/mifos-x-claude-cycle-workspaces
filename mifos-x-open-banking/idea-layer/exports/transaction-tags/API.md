# API Reference — Transaction Tags & Notes

| Field | Value |
|---|---|
| Feature | transaction-tags |
| Base URL | https://apisandbox.openbankproject.com |
| Auth Scheme | DirectLogin (header: `DirectLogin token=<token>`) |
| OBP Version | v3.0.0 (tag/comment/image endpoints); v1.2.1 compatible |

---

## GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags

**Tag:** Transaction-Metadata
**Purpose:** Fetch all tags previously added to a specific transaction. Called on screen entry (loading state); response drives the chips rendered in view_tags and edit_mode states.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier (e.g. `gh.29.uk`) |
| accountId | String | Account containing the transaction |
| transactionId | String | Specific transaction identifier |

### Response Fields

| Field | Type | Description |
|---|---|---|
| tags | List\<TransactionTag\> | Array of tag objects associated with the transaction |
| id | String | Unique tag identifier used for DELETE |
| value | String | Tag label text (e.g. `#groceries`) |
| date | String | ISO 8601 timestamp when tag was added |
| user | User | User object who added the tag |

### Error Codes

| Code | Meaning |
|---|---|
| 401 | USER_NOT_LOGGED_IN |
| 403 | INSUFFICIENT_AUTHORISATION |
| 404 | TRANSACTION_NOT_FOUND |

---

## POST /obp/v3.0.0/banks/{bankId}/accounts/{accountId}/transactions/{transactionId}/metadata/tags

**Tag:** Transaction-Metadata
**Purpose:** Add a new tag to a transaction. Called when the user types a tag in add_tag_input and taps "Add". The tag `id` returned is stored locally to support subsequent DELETE.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier |
| accountId | String | Account containing the transaction |
| transactionId | String | Target transaction identifier |

### Request Body

| Field | Type | Required | Example | Description |
|---|---|---|---|---|
| value | String | Yes | `#groceries` | Tag label — must begin with `#`; max 50 chars |

### Response Fields

| Field | Type | Description |
|---|---|---|
| id | String | Newly created tag identifier |
| value | String | The tag label as stored |
| date | String | ISO 8601 creation timestamp |

### Error Codes

| Code | Meaning |
|---|---|
| 400 | INVALID_TAG_VALUE — value is empty or exceeds character limit |
| 401 | USER_NOT_LOGGED_IN |

---

## DELETE /obp/v3.0.0/banks/{bankId}/accounts/{accountId}/transactions/{transactionId}/metadata/tags/{tagId}

**Tag:** Transaction-Metadata
**Purpose:** Remove a tag from a transaction. Called when the user taps an existing tag chip (remove_tag action). The `tagId` is the `id` field from the POST or GET response.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier |
| accountId | String | Account containing the transaction |
| transactionId | String | Transaction identifier |
| tagId | String | Identifier of the tag to delete |

### Response

| Field | Type | Description |
|---|---|---|
| result | String | `"Success"` on successful deletion |

### Error Codes

| Code | Meaning |
|---|---|
| 401 | USER_NOT_LOGGED_IN |
| 404 | TAG_NOT_FOUND — tagId does not exist or was already deleted |

---

## POST /obp/v3.0.0/banks/{bankId}/accounts/{accountId}/transactions/{transactionId}/metadata/comments

**Tag:** Transaction-Metadata
**Purpose:** Persist the notes text area content as a private comment on the transaction. Called as part of the save_metadata action when noteText is non-empty.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier |
| accountId | String | Account containing the transaction |
| transactionId | String | Target transaction identifier |

### Request Body

| Field | Type | Required | Example | Description |
|---|---|---|---|---|
| value | String | Yes | `Weekly shop — bought extra for bank holiday` | Free-text note content; max 2 000 chars |

### Response Fields

| Field | Type | Description |
|---|---|---|
| id | String | Newly created comment identifier |
| value | String | The stored note text |
| date | String | ISO 8601 creation timestamp |

### Error Codes

| Code | Meaning |
|---|---|
| 400 | INVALID_COMMENT_VALUE |
| 401 | USER_NOT_LOGGED_IN |

---

## POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images

**Tag:** Transaction-Metadata
**Purpose:** Attach a receipt image URL to the transaction after the image has been uploaded to cloud storage. Called when the user selects an image from gallery (pick_image_from_gallery) or captures one via camera (open_camera).

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier |
| accountId | String | Account containing the transaction |
| transactionId | String | Target transaction identifier |

### Request Body

| Field | Type | Required | Example | Description |
|---|---|---|---|---|
| label | String | Yes | `Whole Foods receipt 23-May-2026` | Human-readable description of the receipt |
| URL | String | Yes | `https://storage.example.com/receipts/abc123.jpg` | Publicly accessible URL of the uploaded image |

### Response Fields

| Field | Type | Description |
|---|---|---|
| id | String | Newly created image record identifier |
| label | String | Image description |
| URL | String | Public image URL |
| date | String | ISO 8601 creation timestamp |

### Error Codes

| Code | Meaning |
|---|---|
| 400 | INVALID_IMAGE_URL — URL is malformed or inaccessible |
| 401 | USER_NOT_LOGGED_IN |

---

## Client Save Flow

The save_metadata action executes the following API calls sequentially:

1. For each new tag in `tags` not yet persisted: POST tags
2. For each removed tag (chip tapped): DELETE tags/{tagId}
3. If `noteText` changed and is non-empty: POST comments
4. If new images in `attachedImages`: POST images (one request per image)

On all calls returning 2xx: transition to save_success state, show banner, auto-navigate to transaction-detail after 1 800 ms.
On any call returning 4xx/5xx: transition to error state with field-level error code.

---

*Generated by /idea export | 2026-05-25*
