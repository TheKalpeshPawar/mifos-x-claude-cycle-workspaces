# Account holder — API Contracts

> Generated from `screens/account-holder/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `4f37f6731908` · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `party` | GET | `/accounts/{AccountId}/party` | ReadParty | `OBReadParty2` | memory (store5) |

## 1 · Account party

`GET /accounts/{AccountId}/party` → `200` `OBReadParty2`

```json
{
  "Data": { "Party": {
    "PartyId": "55786146", "PartyNumber": "7458", "PartyType": "Sole",
    "Name": "Mr Bantu", "FullLegalName": "Mr Bantu Sinfield",
    "LegalStructure": "UK.OBIE.Individual", "AccountRole": "UK.OBIE.Principal",
    "EmailAddress": "bantu@digitalapicraft.com",
    "Phone": "+91-9445672233", "Mobile": "+91-9445672233",
    "Relationships": { "Account": { "Related": "…/accounts/1123456841", "Id": "1123456841" } }
  } },
  "Links": { "Self": "…/accounts/1123456841/party" },
  "Meta": { "TotalPages": 1 }
}
```

`Data.Party` is an **object, not an array** — that is what distinguishes `OBReadParty2` (this
endpoint) from `OBReadParty3` (`/parties`, plural).

**Every name, address, phone, email and mobile field is PII.**

### Account-scoped, not PSU-scoped

HSBC UK Personal exposes **no** PSU-level `/party` — only `/accounts/{AccountId}/party`. For
personal accounts the PSU *is* the account holder, so account-scoped party is the app user's
own identity.

This is why the entry point matters: the account-detail chip carries a real `accountId`,
whereas the deleted Settings → Profile row passed an empty `selectedAccountId`, producing a
malformed `GET /accounts//party` that HSBC rejected with a generic 403.

### Mapping

`Data.Party` → flat `PartyProfile` (`core/model`) with `displayName`, `roleLabel`, `initials`,
`email`, `mobile`, `addressLine`. The feature never sees an OBIE shape.

The OBIE `Address[]` is **never returned by the HSBC sandbox**, so `addressLine` is empty in
practice and that row hides.

## Naming correction 2026-07-30

`response_dto` read **`PartyResponse`** — the source-side class name
(`core/network/model/ais/party/PartyResponse.kt`). Every other dto ref in the idea-layer — 23
of 24 — uses the OBIE wire name, which is what `dtos/` registers. Retargeted to
`OBReadParty2`, whose `source_binding` preserves the link back to `PartyResponse.kt`.

`OBReadParty2` and `OBReadParty3` also carried stale `used_by` entries for `party` (renamed to
`account-holder` on 2026-07-28) and `profile` (deleted). Both corrected in the same pass.

## Cache

`BankingStores.partyStore(aisp): Store<String, PartyProfile>` — `createMemoryStore`, keyed on
`AccountId`. **No validator, no `markFresh()`, no Room.**

Memory rather than Room because party identity is consent-scoped: a cached copy could outlive
the consent that permitted the read. Every consent-scoped store in the app is memory-only for
the same reason; only `accountsStore` and `transactionsStore` are Room-persisted.

The stream is per-ViewModel, bound to `viewModelScope`, and dies with it. `ProfileRepository`
deliberately exposes **no `refresh()`** — recovery is `RetryLoad` on the stream the ViewModel
already holds.

`partyStore` is also the one memory store with **no capability registry** — there is no
`AccountEndpoint.Party` — so a `U000` here surfaces as an ordinary error rather than hiding a
chip. The chip is ungated: every account has a holder.

## Error matrix

| HTTP | ErrorCode | Kind | Retry? | UI action |
|---|---|---|:--:|---|
| 401 | `UK.OBIE.Header.Invalid` | `TokenExpired` | ✅ | Retry after refresh |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | `ConsentMissingParty` | ✗ | ReadParty absent from the consent — re-authorise |
| 404 | `U011` | `ProfileNotFound` | ✗ | unknown account id |
| 5xx / network | — | `LoadFailed` | ✅ | Retry |
| — | — | blank `displayName` | — | **Empty**, not an error — a successful fetch with no usable identity |

## Source binding

`core/network/api/Aisp.kt` `getParty` · `core/data/.../banking/store/BankingStores.kt`
`partyStore` · `ProfileRepository` (stateless; kept under its old `core/data` name after the
feature rename) — all shipped and consumed.

`Aisp.getParties` (plural, `OBReadParty3`) also ships but has **no store, repository or feature
consuming it**.
