# User onboarding — API Contracts

> Generated from `screens/user-onboarding/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `6aca2474d208` · Endpoints: 0 · DTOs: 0

## No API surface

**This feature makes no network calls.** `api.yaml` declares zero endpoints, and source
confirms it: `onboarding/IntroScreen.kt` is a stateless composable with `viewmodel: null`, and
TC-ONB-003 asserts the screen performs no I/O.

This file exists deliberately rather than being omitted, so a reader can tell **"this feature
has no API"** apart from **"this feature has not been exported yet"**. An absent `API.md`
carries no information; this one does.

| | |
|---|---|
| Endpoints | 0 |
| DTOs | 0 |
| Auth requirement | none |
| Network permission needed | none |
| Cache strategy | n/a |

## Gate E3

Export gate **E3** requires `api[] has ≥1 entry with a response section`. This feature fails
it by design. See `SPEC.md#export-gate-exception` — the exception is recorded in
`PIPELINE_STATE#capabilities.idea-feature-export.metrics.e1_e3_exceptions` rather than the
feature being skipped.

Two other features share this shape:

| Feature | Gates failed | Why |
|---|---|---|
| `user-onboarding` | E1 + E3 | static IntroScreen, no ViewModel, no I/O |
| `licences` | E1 + E3 | reads a bundled `composeResources` text asset; no ViewModel |
| `settings` | E3 only | client-only — reads `UserDataRepository`, no external API |

## What happens next in the journey

The PSU taps Continue and lands on `login`, which is where the first network call of the whole
app happens (`POST /account-access-consents`). See `exports/login/API.md`.
