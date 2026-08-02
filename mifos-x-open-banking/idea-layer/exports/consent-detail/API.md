# Consent detail — API Contracts

> Generated from `screens/consent-detail/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `b6bb85d0ec32` · Endpoints: 2 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|---|
| 1 | `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer, `scope=accounts` | `OBReadConsentResponse1` |
| 2 | `consent-revoke` | DELETE | `/account-access-consents/{ConsentId}` | CC bearer, `scope=accounts` | — (`204 No Content`) |

Both on the **client-credentials** token, not the PSU bearer — consent management is isolated
that way throughout (`ConsentStores.kt`).

## 1 · Consent status

`GET /account-access-consents/{ConsentId}` → `200` `OBReadConsentResponse1`

Same envelope as `consent-list`; this screen renders more of it.

| Rendered | Source |
|---|---|
| status badge (colour-coded) | `Data.Status` |
| permission rows (human-readable labels) | `Data.Permissions[]` |
| created | `Data.CreationDateTime` |
| expires | `Data.ExpirationDateTime` |
| transactions from / to | `Data.TransactionFromDateTime` / `…ToDateTime` |
| expiry warning banner | `ExpirationDateTime` − now ≤ 7 days |
| 90-day reconfirm prompt | `CreationDateTime` + 90 days |

The four date fields are shown in full rather than summarised — this is the trust-critical
surface for "what am I sharing, and until when".

## 2 · Revoke consent

`DELETE /account-access-consents/{ConsentId}` → `204 No Content`

```http
DELETE /obie/open-banking/v4.0/aisp/account-access-consents/764351380
Content-Type: application/json
Authorization: Bearer <CC access token>
x-fapi-financial-id: <OB financial-id>
Accept: application/json
```

No request body. No response body.

### This call is step 1 of 3

`AppLogout.logOut()` wraps it:

1. **this DELETE**, best-effort inside `runCatching`
2. `consentSession.forgetAll()` — removes PSU tokens; **the actual logout**
3. `userDataRepository.clearUserData()` + `storeCacheManager.clearAll()`

Step 1 failing does not stop steps 2 and 3. An expired, already-revoked, 404 or network-failed
consent must still sign the PSU out locally — otherwise a bank-side inconsistency would trap
them in a session they asked to end.

## Error matrix

| HTTP | Endpoint | ErrorCode | Meaning | UI action |
|---|---|---|---|---|
| 404 | GET | `U011` | consent unknown | `ConsentNotFoundError` — no retry |
| 403 | GET | `UK.OBIE.Resource.ConsentMismatch` | revoked or not `Authorised` | `ConsentRevokedError` |
| 401 | either | — | CC token expired | `TokenExpiredError` — re-authenticate |
| 5xx | DELETE | `UK.OBIE.Unexpected.ServerError` | HSBC-side failure | `RevokeServerError` — Retry |
| **404** | **DELETE** | — | consent already gone bank-side | **not an error** — treated as already-revoked; local state cleaned and logout proceeds |
| 429 | either | `UK.OBIE.Rules.TooManyRequests` | rate limited | Retry with back-off |

The 404-on-DELETE row is the one worth pinning (TC-CDETAIL-008). Treating it as a failure
would leave a PSU unable to sign out because the bank had already dropped the consent they
were trying to revoke.

## Source binding

`core/network/api/Aisp.kt` `getConsent` / `deleteConsent` ·
`core/data/.../banking/ConsentRevokeRepository.kt` ·
`core/data/.../user/AppLogout.kt` + `impl/AppLogoutImpl.kt` (Koin `single`) — all shipped and
consumed. `AppLogout` is the single sign-out path in the app.
