# Payment consent — API Contracts

> Generated from `screens/payment-consent/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `64c86ff15dcb` · Endpoints: 3 · DTOs: 2

PISP resources on `/obie/open-banking/v4.0/pisp`; OAuth on `/obie/open-banking/v1.1`.

## Endpoint summary

| # | ID | Method | Path | Auth | JWS | Idem |
|---|---|---|---|---|:--:|:--:|
| 1 | `payment-authorize-redirect` | GET | `/v1.1/oauth2/authorize` | none — browser redirect | — | — |
| 2 | `payment-token-exchange` | POST | `/v1.1/oauth2/token` | `private_key_jwt` in form body | — | — |
| 3 | `payment-consent-status` | GET | `/domestic-payment-consents/{ConsentId}` | CC token, scope=payments | — | — |

All three are reads or auth calls — none needs a detached JWS. Only the two `send-money`
writes do.

## 1 · Authorisation redirect

`GET /v1.1/oauth2/authorize?response_type=…&client_id=…&state=…&nonce=…&scope=payments&redirect_uri=…&request=<signed JWT>`

Not a call the client makes directly — `send-money` emits `LaunchAuthorisation` and the Screen
opens it. Identical in shape to the AIS authorize call except **`scope=payments`** and the
intent id is the domestic-payment `ConsentId`.

`302` to the bank login; after SCA the browser returns to the registered callback with
`code`, `id_token` and `state`. The return leg arrives through the already-shipped
per-platform `ConsentRedirectBus`.

## 2 · Token exchange

`POST /v1.1/oauth2/token` · `Content-Type: application/x-www-form-urlencoded` · **no
`Authorization` header** — the client authenticates with `private_key_jwt` in the form body.

```
grant_type=authorization_code
code=<authorisation code from the redirect>
redirect_uri=<registered callback>
client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
client_assertion=<PS256-signed JWT>
```

→ `200` `OAuthTokenResponse` — `access_token`, `token_type`, `refresh_token`, `expires_in`,
`scope` (`payments`), `id_token`.

**The resulting token is scoped to this one payment and MUST NOT be persisted into
`ConsentSession`**, which holds the AIS data-sharing session.

Errors follow RFC 6749 (`{error, error_description}`), **not** the OB envelope:

| HTTP | error | Meaning | UI action |
|---|---|---|---|
| 400 | `invalid_grant` | code expired (30–60s TTL) or already used | Restart authorisation |
| 400 | `invalid_request` | client assertion malformed / bad signature | non-recoverable + support ref |
| 401 | `invalid_client` | wrong `kid`, expired `exp`, reused `jti`, or `iss` ≠ `sub` | non-recoverable + support ref |

## 3 · Consent status

`GET /domestic-payment-consents/{ConsentId}` → `200` `OBWriteDomesticConsentResponse5`

```json
{
  "Data": {
    "ConsentId": "812774903",
    "Status": "AUTH",
    "CreationDateTime": "2026-07-30T10:42:33+00:00",
    "StatusUpdateDateTime": "2026-07-30T10:43:51+00:00",
    "Initiation": { "…echoed; send-money resends this verbatim…" }
  },
  "Links": { "Self": "…/domestic-payment-consents/812774903" },
  "Meta": { "TotalPages": 1 }
}
```

**This poll is load-bearing, not best-effort.** Submitting against a consent that is not
`Authorised` returns `400 U009`, so the return to `send-money` is gated on it — unlike the AIS
`consent-callback`, whose poll only supplies the expiry.

Polled on the **client-credentials payments token**, matching how the shipped
`ConsentStores.kt` reads the AIS consent on a client-credentials token rather than the PSU
bearer. That also means tracking survives expiry of the single-payment PSU token.

| Poll parameter | Value |
|---|---|
| interval | 1500 ms |
| deadline | 45000 ms |
| terminal success | `AUTH` |
| terminal failure | `RJCT` |
| on deadline | `AuthorisationTimedOut` → offer Restart |

Status vocabulary: `AWAU` AwaitingAuthorisation → `AUTH` Authorised | `RJCT` Rejected.

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 400 | `U011` | ConsentId unknown or already consumed | Abandon → `send-money` |
| 401 | `UK.OBIE.Header.Invalid` | payments CC token expired | re-mint and re-poll |

## Reuse map

| Reusable — do not rebuild | |
|---|---|
| `core/data/.../callback/PendingAuthStore.kt` | state/nonce/consentId stash, single-use `consume()` |
| `ConsentRedirectBus` (cmp-navigation) | Android `onCreate`/`onNewIntent`, desktop loopback, iOS bridge |
| `core/network/api/OAuth.kt` `exchangeAuthorizationCode` | call shape; needs a payments-scope variant |
| `core/network/BuildClientAssertion.kt` | `private_key_jwt` assertion — unchanged |

| Must not reuse | |
|---|---|
| `ConsentSession.saveConsentMeta` / token persistence | would overwrite the AIS session token and flip `isActive()` semantics |

**Missing:** payments-scope client-credentials token path (`OAuth.kt` mints `accounts` only) ·
`Pisp.kt` client for the consent-status read.
