# Consent list — API Contracts

> Generated from `screens/consent-list/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `30c96226cc2a` · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Auth | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer, `scope=accounts` | `OBReadConsentResponse1` | memory |

Read on the **client-credentials** token, not the PSU bearer. This is why
`consentDetailStore` lives in `ConsentStores.kt` apart from `BankingStores` — consent
management runs on a client-credentials token minted per fetch, and the same store backs both
this screen and `consent-detail`.

## 1 · Consent status

`GET /account-access-consents/{ConsentId}` → `200` `OBReadConsentResponse1`

```json
{
  "Data": {
    "ConsentId": "764351380",
    "Status": "AUTH",
    "CreationDateTime": "2026-07-13T11:31:27+00:00",
    "StatusUpdateDateTime": "2026-07-13T11:42:04+00:00",
    "Permissions": ["ReadAccountsBasic", "ReadAccountsDetail", "…20 items total"],
    "ExpirationDateTime": "2030-12-31T00:00:00+00:00",
    "TransactionFromDateTime": "2020-01-01T00:00:00+00:00",
    "TransactionToDateTime": "2030-12-31T00:00:00+00:00"
  },
  "Links": { "Self": "…/account-access-consents/764351380" },
  "Meta": { "TotalPages": 1 },
  "Risk": {}
}
```

### Fields the screen derives from

| Rendered | Source |
|---|---|
| status chip | `Data.Status` |
| permission count | `Data.Permissions.length` |
| expiry countdown | `Data.ExpirationDateTime` − now |
| connection date | `Data.CreationDateTime` |
| Active / History partition | `Data.Status` — `AUTH` → Active; `Expired`/`Revoked` → History |
| reconfirm urgency chip + banner | expiry countdown ≤ 14 days |

## Consent identity

The screen reads `ConsentSession.consentId()` — **the current connection only**. There is no
device-side consent history, so "History" holds a prior state of the same consent rather than
a list of past consents. A `null` consentId is not an error: it means never-connected, and
renders the Empty state with a Connect CTA.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 401 | — (empty body on AIS resources) | CC token expired or invalid | **dedicated `ErrorAuth` state** with a sign-in-again CTA — not the generic error |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | consent lacks permission, or is not `Authorised` | `Error` |
| 404 / 400 `U011` | resource not found | consent unknown — treat as revoked, show History or Empty |
| 5xx | `UK.OBIE.Unexpected.ServerError` | HSBC-side failure | `Error` + Retry |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | Retry with back-off |

401 gets its own UiState because its recovery differs in kind — re-authentication, not a retry
of the same call.

## Source binding

`core/network/api/Aisp.kt` `getConsent` · `core/data/.../banking/store/ConsentStores.kt`
`consentDetailStore` · `ConsentDetailRepository.consentStream` — all shipped and consumed.
