# Account holder — Feature Specification

> Generated from `screens/account-holder/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `4f37f6731908`
> Endpoints: 1 · DTOs: 1 · Components: 7 · Test scenarios: 7

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Account holder / PSU identity, gated by the `ReadParty` permission. Renders the flat
`PartyProfile` domain model — `displayName`, `roleLabel`, `initials`, `email`, `mobile` and a
single pre-flattened `addressLine` — streamed from `ProfileRepository`.

| Attribute | Value |
|---|---|
| Feature ID | `account-holder` |
| Cluster | account-extras |
| Priority | could (FR-007) |
| Status | approved · quality 96 |
| Archetype | detail_screen |
| Source module | `feature/account-holder` — **implemented** |
| Route | `AccountHolderRoute(accountId: String)` |

**Identity only.** Renamed from `feature/profile` on 2026-07-28 and gutted: the consent
status/expiry banner, the granted-permissions list and sign-out were all removed. Consent
management and sign-out live in Settings → Consents. Event type is therefore `Nothing` and
`Content` carries just the `PartyProfile`.

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| `loading_indicator` + `loading_caption` | progress_indicator, text | loading |
| `identity_card` | card | content |
| `identity_section_header` + `identity_section` | section_header, stack | content |
| `empty_state_view` · `error_state` | empty_state, error_state | empty, error |

The `Party` DTO's OBIE `Address` is never returned by the HSBC sandbox, so that row hides in
practice.

## 3. State model — `AccountHolderViewModel`

**State fields:** `accountId: String` (nav arg) · `uiState: AccountHolderUiState`
**State defaults:** `uiState = Loading`

`AccountHolderUiState`: `Loading` · `Content` · `Empty` · `Error`

**Error kinds:** `TokenExpired` · `ConsentMissingParty` · `ProfileNotFound` · `LoadFailed`
**Actions:** `RetryLoad`
**Events:** none (`E = Nothing`) — the screen owns no navigation
**DI:** `SavedStateHandle` · `ProfileRepository`

Empty is reached via `emptyIfContent` on a **blank `displayName`** — a successful fetch that
carries no usable identity is a real answer, not missing data.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Explore option "Account holder" (`AccountDetailChip.Party`) | `account-holder` (accountId) |
| top-app-bar leading | back | `account-detail` |

### Why the entry point moved

The chip's `navigateFromChip` branch was repointed from a dead `PlaceholderScreen`
(`PartyRoute`, now deleted) to `AccountHolderRoute(accountId)`. Because the chip carries
account-detail's own nav arg, **`accountId` is always valid**.

The old Settings → Profile entry passed an empty `userData.selectedAccountId` — unset until the
PSU tapped an account on Home — producing a malformed `GET /accounts//party` that HSBC rejected
with a generic 403. That entry, its `onNavigateToProfile` plumbing and the settings
`selectedAccountId` were all removed.

HSBC UK Personal exposes no PSU-level `/party`, only `/accounts/{AccountId}/party`, and for
personal accounts the PSU **is** the account holder — so account-scoped party is the app user's
own identity.

The chip is **ungated**: every account has a holder.

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `party` | GET | `/accounts/{AccountId}/party` | ReadParty | `OBReadParty2` |

Full contract in `API.md`.

### Cache

`store5` — `BankingStores.partyStore(aisp): Store<String, PartyProfile>`, keyed on `AccountId`,
**memory only**. The stream is per-ViewModel, bound to `viewModelScope`, and dies with it;
`ProfileRepository` deliberately exposes no `refresh()`.

Memory rather than Room because party identity is consent-scoped data whose cached copy could
outlive the consent that permitted it.

### Error matrix

| Kind | Trigger | Retry? |
|---|---|:--:|
| `TokenExpired` | 401 | ✅ |
| `ConsentMissingParty` | 403 — ReadParty absent from the consent | ✗ |
| `ProfileNotFound` | unknown account id | ✗ |
| `LoadFailed` | network / 5xx | ✅ |

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `card` on `surfaceContainer`, `section_header`, `list_item` rows
for email/mobile/address. Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-ACCOUNT-HOLDER-001 | identity renders | `feature/account-holder/src/commonTest/.../AccountHolderViewModelTest.kt` |
| TC-ACCOUNT-HOLDER-002 | loading while the stream has not emitted | ↑ |
| TC-ACCOUNT-HOLDER-003 | retriable error shows Retry; `RetryLoad` re-fetches | ↑ |
| TC-ACCOUNT-HOLDER-004 | back → account-detail | ↑ |
| TC-ACCOUNT-HOLDER-005 | **blank displayName → Empty** | ↑ |
| TC-ACCOUNT-HOLDER-006 | missing ReadParty consent renders on the error surface | `AccountHolderScreenUiTest.kt` (commonTest) |
| TC-ACCOUNT-HOLDER-007 | unknown account id → non-retriable not-found | `AccountHolderScreenRobolectricTest.kt` |

This feature carries a `commonTest` `*ScreenUiTest`, which needs the
`compose.uiTest` + `desktop.uiTestJUnit4` deps **plus** the `*UnitTest` exclusion filter —
without it the suite NPEs in the Android unit-test task where there is no Robolectric runner.

## 8. Notes

`docs.yaml` declares no `flow_ref` despite `flows/settings-and-profile.yaml` existing — and
that flow's name is itself a residue of the deleted `profile` screen.
