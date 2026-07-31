# Consent callback — API Contracts

> Generated from `screens/consent-callback/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `a5072ad77719` · Endpoints: 2 · DTOs: 2

OAuth on `/obie/open-banking/v1.1`; AIS resources on `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|---|
| 1 | `fapi-token-exchange` | POST | `/v1.1/oauth2/token` | `private_key_jwt` in form body | `OAuthTokenResponse` |
| 2 | `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer | `OBReadConsentResponse1` |

## 1 · Token exchange

`POST /v1.1/oauth2/token` · `Content-Type: application/x-www-form-urlencoded` ·
**no `Authorization` header**

```
grant_type=authorization_code
code=<auth code from the redirect fragment>
redirect_uri=<registered callback>
client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
client_assertion=<PS256-signed JWT>
```

→ `200` `OAuthTokenResponse`:

```json
{
  "access_token": "…",
  "token_type": "Bearer",
  "refresh_token": "…",
  "expires_in": 3599,
  "scope": "openid accounts",
  "id_token": "<PS256 JWT — carries nonce + openbanking_intent_id>"
}
```

The `id_token` is not decoration: its `nonce` claim is validated against the value stashed in
`PendingAuthStore`, and `openbanking_intent_id` echoes the `ConsentId`. Both are checked
before the tokens are persisted.

**Tokens land in secure `Settings` via `SettingsConsentSession`, not the DataStore
`UserData`.** That is why `clearUserData()` alone cannot sign a user out — `forgetAll()` is
the actual logout.

## 2 · Consent status

`GET /account-access-consents/{ConsentId}` → `200` `OBReadConsentResponse1`

```json
{
  "Data": {
    "ConsentId": "764351380",
    "Status": "AUTH",
    "CreationDateTime": "2026-07-13T11:31:27+00:00",
    "StatusUpdateDateTime": "2026-07-13T11:42:04+00:00",
    "Permissions": ["ReadAccountsBasic", "ReadAccountsDetail", "…20 items"],
    "ExpirationDateTime": "2030-12-31T00:00:00+00:00",
    "TransactionFromDateTime": "2020-01-01T00:00:00+00:00",
    "TransactionToDateTime": "2030-12-31T00:00:00+00:00"
  },
  "Links": { "Self": "…/account-access-consents/764351380" },
  "Meta": { "TotalPages": 1 },
  "Risk": {}
}
```

Read on the **client-credentials** token, not the PSU bearer — matching how the shipped
`ConsentStores.kt` isolates consent management.

**Best-effort here.** A successful token exchange already proves authorisation, so this poll
only supplies the expiry. (In `payment-consent` the equivalent poll is load-bearing, because
submitting against a non-`Authorised` payment consent returns `400 U009`.)

Status vocabulary: `AWAU` AwaitingAuthorisation → `AUTH` Authorised.

## Redirect error handling

The redirect itself can carry an OAuth error instead of a code. These are handled **before**
any token exchange:

| Redirect param | UiState | Why no exchange |
|---|---|---|
| `error=access_denied` | `AccessDenied` | the PSU declined at the portal — there is no code to exchange |
| `state` mismatch | `SecurityError` | possible CSRF or crossed authorisation |
| `id_token` nonce mismatch | `SecurityError` | detected after exchange (the nonce lives in the id_token) |

## Error matrix

| HTTP | Shape | error / code | UI action |
|---|---|---|---|
| 400 | RFC 6749 | `invalid_grant` — code expired (~30–60s TTL) or already used | `Error` → back to `login` |
| 400 | RFC 6749 | `invalid_request` — JWT signature invalid | `Error` + support ref |
| 401 | RFC 6749 | `invalid_client` — wrong `kid`, expired `exp`, reused `jti`, `iss` ≠ `sub` | `Error` + support ref |
| 401 | empty body | AIS resource — missing/invalid/expired bearer | re-authenticate |
| 403 | OB envelope | consent lacks the permission, or is not `Authorised` | `Error` |
| 429 | OB envelope | rate limited | back off per `x-ratelimit-*` |

Three error shapes across this one flow: HTML (mTLS edge), RFC 6749 JSON (token endpoint),
OB envelope (resource/consent). The client must handle all three.

## Source binding

`core/network/api/OAuth.kt` `exchangeAuthorizationCode` · `core/network/api/Aisp.kt`
`getConsent` · `core/data/.../callback/PendingAuthStore.kt` ·
`core/data/.../callback/ConsentSession.kt` (`SettingsConsentSession`) — all shipped and
consumed.
