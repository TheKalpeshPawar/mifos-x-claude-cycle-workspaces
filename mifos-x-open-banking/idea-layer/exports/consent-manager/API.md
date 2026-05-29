# API Reference — Connected Apps (Consent Manager)

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | consent-manager                             |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/my/consents

**Auth:** DirectLogin
**Tag:** Consent
**Trigger:** `loadConsents()` on screen entry / `RetryLoad` event

Lists all PSD2 consents granted by the currently authenticated consumer user. The `ConsentManagerViewModel` maps each OBP `Consent` object into a `ConsentItem` domain model, deriving display fields (app name from `consumer_id`, formatted grant/expiry dates, human-readable status, scope list from JWT payload). ACCEPTED → ACTIVE; EXPIRED → EXPIRED; REVOKED / INITIATED records are filtered or surfaced separately.

### Response Fields

| Field           | Type                    | Description                                                              |
|-----------------|-------------------------|--------------------------------------------------------------------------|
| consents        | List\<Consent\>         | All PSD2 consents granted by the authenticated user                      |
| consent_id      | String                  | Unique consent identifier — used as path param in DELETE revoke call     |
| status          | String                  | `INITIATED` \| `ACCEPTED` \| `REVOKED` \| `EXPIRED`                     |
| created_at      | String                  | ISO-8601 UTC consent creation timestamp (e.g. `2026-04-01T08:00:00Z`)   |
| valid_until     | String                  | ISO-8601 UTC consent expiry timestamp (e.g. `2026-07-01T08:00:00Z`)     |
| consumer_id     | String                  | Third-party app consumer identifier                                      |
| redirects       | List\<ConsentRedirect\> | OAuth redirect URIs registered for this consent                          |
| json_web_token  | String                  | JWT encoding consent scopes, issuer, and iat                             |

### ConsentItem (domain model mapped from OBP Consent)

| Field     | Type            | Mapped from    | Notes                                                      |
|-----------|-----------------|----------------|------------------------------------------------------------|
| id        | String          | consent_id     | Used as key for revoke API call and list identity          |
| appName   | String          | consumer_id    | Display name e.g. "MoneyManager Pro"                       |
| grantedAt | String          | created_at     | Formatted "1 Mar 2026"                                     |
| expiresAt | String          | valid_until    | Formatted "1 Mar 2027"                                     |
| status    | ConsentStatus  | status         | ACTIVE (ACCEPTED), EXPIRED, REVOKED, INITIATED             |
| scopes    | List\<String\>  | jwt payload    | Human-readable scope labels e.g. "Read Accounts"           |

### Demo Data

| consent_id                      | status   | created_at           | valid_until          | consumer_id                         |
|---------------------------------|----------|----------------------|----------------------|-------------------------------------|
| consent-001-ke-safaricom-data   | ACCEPTED | 2026-04-01T08:00:00Z | 2026-07-01T08:00:00Z | consumer-safaricom-lipa-001         |
| consent-002-ke-equity-open      | ACCEPTED | 2026-04-15T10:30:00Z | 2026-10-15T10:30:00Z | consumer-equity-open-banking-002    |
| consent-003-ke-ncba-loop        | REVOKED  | 2026-03-10T12:00:00Z | 2026-06-10T12:00:00Z | consumer-ncba-loop-app-003          |
| consent-004-ke-pesalink-payments| INITIATED| 2026-05-22T09:15:00Z | 2026-06-22T09:15:00Z | consumer-pesalink-payments-004      |

> The UI demo layer maps these to the MoneyManager Pro, TaxHelper, and BudgetWise display cards. See `screens/consent-manager/demo-data.yaml` for redirect URLs and JWT values.

### Error Codes

| Code | OBP Error Key              | UI Behaviour                                                          |
|------|----------------------------|-----------------------------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN         | Navigate to login screen                                              |
| 403  | INSUFFICIENT_AUTHORISATION | Show error state with "Unable to load connected apps" message         |
| 500  | INTERNAL_SERVER_ERROR      | Show error state (cloud_off icon) + Retry button                     |

---

## DELETE /obp/v5.1.0/my/consents/{consentId}

**Auth:** DirectLogin
**Tag:** Consent
**Trigger:** `RevokeConsentConfirmed(consentId)` event — fires after user taps the "Revoke" button in the revoke_confirm dialog

Revokes the specified PSD2 consent. On success the ViewModel removes the consent from the local list, dismisses the dialog, and re-renders the list (or transitions to `empty` if no consents remain). On failure a `REVOKE_FAILED` error is surfaced as a snackbar without clearing the dialog.

### Path Parameters

| Name       | Type   | Description                                                  |
|------------|--------|--------------------------------------------------------------|
| consentId  | String | ID of the consent to revoke (from `ConsentItem.id`)          |

### Response Fields

| Field      | Type   | Description                                                   |
|------------|--------|---------------------------------------------------------------|
| consent_id | String | ID of the revoked consent (used to remove item from local list)|
| status     | String | `REVOKED` — confirms successful revocation                    |

### Demo Revoke Response

| consent_id                | status  |
|---------------------------|---------|
| consent-003-ke-ncba-loop  | REVOKED |

### Error Codes

| Code | OBP Error Key              | UI Behaviour                                                                        |
|------|----------------------------|-------------------------------------------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN         | Navigate to login; dismiss dialog                                                   |
| 404  | CONSENT_NOT_FOUND          | Snackbar: "This app was already disconnected"; dismiss dialog; refresh list         |
| 500  | INTERNAL_SERVER_ERROR      | Snackbar: "Could not revoke access. Please try again."; keep dialog open for retry  |

---

_Generated by /idea export | 2026-05-30_
