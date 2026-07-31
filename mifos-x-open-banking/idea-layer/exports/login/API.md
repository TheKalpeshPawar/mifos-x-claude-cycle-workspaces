# Login — API Contracts

> Generated from `screens/login/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `e38de56e4e0b` · Endpoints: 1 · DTOs: 2

AIS resources on `/obie/open-banking/v4.0/aisp`; OAuth on `/obie/open-banking/v1.1`.

## Endpoint summary

| # | ID | Method | Path | Auth | Request DTO | Response DTO |
|---|---|---|---|---|---|---|
| 1 | `consent-create` | POST | `/account-access-consents` | CC bearer (client_credentials, `scope=accounts`) | `OBReadConsent1` | `OBReadConsentResponse1` |

AIS reads need **no** detached JWS — only PISP writes do. This endpoint is a write in HTTP
terms but an AIS consent-staging call, and HSBC does not require `x-jws-signature` on it.

## 1 · Create account-access consent

`POST /account-access-consents` → `201` `OBReadConsentResponse1`

Request `OBReadConsent1`:

```json
{
  "Data": {
    "Permissions": [
      "ReadAccountsBasic", "ReadAccountsDetail", "ReadBalances",
      "ReadBeneficiariesBasic", "ReadBeneficiariesDetail", "ReadDirectDebits",
      "ReadPAN", "ReadParty", "ReadProducts",
      "ReadStatementsBasic", "ReadStatementsDetail",
      "ReadScheduledPaymentsBasic", "ReadScheduledPaymentsDetail",
      "ReadStandingOrdersBasic", "ReadStandingOrdersDetail",
      "ReadTransactionsBasic", "ReadTransactionsCredits",
      "ReadTransactionsDebits", "ReadTransactionsDetail"
    ],
    "ExpirationDateTime": "2030-12-31T10:40:00+02:00",
    "TransactionFromDateTime": "2010-01-01T10:40:00+02:00",
    "TransactionToDateTime": "2030-12-31T10:40:00+02:00"
  },
  "Risk": {}
}
```

Response carries `Data.ConsentId`, `Data.Status` (`AWAU` on creation), `Permissions[]` echoed,
and the three date bounds. The `ConsentId` becomes the `openbanking_intent_id` claim in the
signed request object for the authorize leg.

`Risk: {}` — empty for AIS. (Contrast `send-money`, where `Risk.PaymentContextCode` is
load-bearing.)

## 2 · Authorisation redirect (not a client call)

`GET /v1.1/oauth2/authorize?response_type=code id_token&client_id=…&state=…&nonce=…&scope=openid accounts&redirect_uri=…&request=<PS256 JWT>`

Built by this feature and handed to `BrowserLauncher` — the app never issues it as an HTTP
request. **No auth headers**; the signed request object travels in the `request` query
parameter, with `state` and `nonce` as query params.

`302` to the bank login. After SCA the browser returns to the callback with
`#code=…&id_token=…&state=…` in the **fragment**. `consent-callback` owns that return leg.

## Error matrix

| HTTP | Shape | Meaning | UI action |
|---|---|---|---|
| 400 | `{error, error_description}` | `invalid_scope` — client not registered for a requested scope | Error state; not PSU-recoverable |
| 400 | `{error, error_description}` | `invalid_request` — malformed/tampered client assertion | Error state + support ref |
| 401 | `{error, error_description}` | `invalid_client` — wrong `kid`, expired `exp`, reused `jti`, `iss` ≠ `sub` | Error state + support ref |
| 400 | OB envelope | schema/validation failure on the consent body | Error state |
| 429 | OB envelope | rate limited | Retry with back-off |
| — | — | transport / mTLS failure returns **HTML, not JSON** | Error state; client must send the client cert on every `secure.*` host |

The token endpoint returns RFC 6749 shapes; resource and consent calls return the OB envelope
`{Code, Id, Message, Errors[]}`. A missing client certificate is rejected at the edge as an
HTML page before any app logic — three distinct error shapes the client must handle.

## Auth model

`private_key_jwt` client authentication — the token endpoint has **no** `Authorization`
header; the client authenticates via `client_assertion_type` + `client_assertion` form fields.
`BuildClientAssertion.signPs256` produces the PS256-signed JWT.

## Source binding

`core/network/api/Aisp.kt` `createConsent` · `core/network/api/OAuth.kt`
`clientCredentialsToken` · `core/network/BuildClientAssertion.kt` — all shipped and consumed.
