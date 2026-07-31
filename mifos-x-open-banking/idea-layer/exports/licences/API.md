# Licences — API Contracts

> Generated from `screens/licences/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 0 · DTOs: 0

## No API surface

**This feature makes no network calls and touches no repository.** It reads one bundled asset
from Compose resources and renders it.

This file exists deliberately rather than being omitted, so a reader can tell **"this feature
has no API"** apart from **"this feature has not been exported yet"**.

| | |
|---|---|
| Endpoints | 0 |
| DTOs | 0 |
| Auth requirement | none |
| Network permission needed | none |
| Persistence | none |
| Cache strategy | n/a |

## The one read it performs

```kotlin
Res.readBytes("files/mpl_licence.txt").decodeToString()
```

A **bundled Compose resource**, not a file-system or network read. It ships inside the
`feature/settings` artifact and is available offline, on every platform, with no permission.

Wrapped in `produceState`, so the composition renders once with an empty body and again when
the read resolves — which is what TC-LICENCES-003 asserts.

## Why there is no dependency inventory

AboutLibraries was trialled to generate a third-party dependency list and **removed**. This
screen shows the application's own MPL-2.0 licence only.

That is a scope decision, not an unfinished feature: a full dependency inventory would need a
build-time generator, a data model and a list UI — none of which exist, and none of which the
project committed to.

## Gates E1 + E3

This feature fails both. Two others share the shape:

| Feature | Gates failed | Why |
|---|---|---|
| `licences` | E1 + E3 | bundled text asset; no ViewModel |
| `user-onboarding` | E1 + E3 | static IntroScreen; no ViewModel, no I/O |
| `settings` | E3 only | client-only — reads `UserDataRepository` |

In all three the gate is unclearable by enrichment, because the missing thing is absent from
**source**, not from the specification. They export with the exception recorded rather than
being skipped silently — a skipped feature looks identical to an unexported one in the matrix,
which is exactly the ambiguity these files exist to remove.
