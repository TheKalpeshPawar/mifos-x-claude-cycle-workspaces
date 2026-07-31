# Licences — Feature Specification

> Generated from `screens/licences/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `6456461723c5`
> Endpoints: **0** · DTOs: 0 · Components: 1 · Test scenarios: 3

## Export gate exception

Fails gates **E1** (state_model has ≥1 ViewModel) and **E3** (api[] has ≥1 entry). Step 1.5
says SKIP with "run `/idea enrich` first" — but enrichment cannot add a ViewModel that does not
exist in source. `LicencesScreen.kt` is a stateless composable reading a bundled asset. The
gate would never clear, so this exports with the exception recorded.
Recorded in `PIPELINE_STATE#capabilities.idea-feature-export.metrics.e1_e3_exceptions`.

## 1. Overview

Open-source licence readout — a pushed, **arg-less** destination reached from the Settings
About section. Renders the MPL licence text bundled in `feature/settings`' Compose resources.

| Attribute | Value |
|---|---|
| Feature ID | `licences` · Cluster settings-and-legal |
| Priority | should · Status **implemented** · quality 90 |
| Archetype | detail_screen · Route `LicencesRoute` (arg-less) |
| Source module | `feature/settings` — **no module of its own** |

**Source-originated.** It ships in source but had no idea-layer representation until the
2026-07-28 reverse sync added it — the opposite direction from every other screen. It is one of
two screens without their own module (the other is `user-onboarding` inside `feature/login`).

## 2. Screen inventory

A single component: `licences_screen` (stack). There is nothing else — no header card, no
sections, no actions beyond back navigation.

## 3. State model

**None.** No ViewModel, no state fields, no actions, no DI. Back is a nav-host callback.

`states: [content]` — the only single-state screen in the corpus.

## 4. How the text is loaded

```kotlin
produceState(initialValue = "") {
    value = Res.readBytes("files/mpl_licence.txt").decodeToString()
}
```

Rendered monospace. The asset lives at `composeResources/files/mpl_licence.txt`.

**AboutLibraries was tried for a dependency list and removed.** This screen shows the app's own
MPL-2.0 licence, not a third-party dependency inventory — a deliberate narrowing, not an
unfinished feature.

TC-LICENCES-003 pins the consequence of `produceState`: the body is **empty before the resource
read resolves**. There is no `Loading` state, so a slow read shows a blank screen rather than a
spinner. Acceptable for a bundled asset that resolves in microseconds; worth knowing if the
asset ever grows.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `settings` | About section → Licences row | `licences` |
| back | top app bar | `settings` |

Arg-less — nothing is passed in either direction.

## 6. API dependencies

**None.** See `API.md`.

## 7. Design tokens

Monospace body text (`typography.font_family.mono`) on `surface`. No card, no elevation — a
legal text dump wants legibility, not chrome.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-LICENCES-001 | renders the bundled MPL text | `feature/settings/src/androidUnitTest/.../LicencesScreenRobolectricTest.kt` |
| TC-LICENCES-002 | back → settings | ↑ |
| TC-LICENCES-003 | **body is empty before the resource read resolves** | ↑ |

## 9. Notes

`docs.yaml` declares **no `acceptance_refs`** and no `flow_ref`. Both are defensible for a
source-originated legal screen with no requirement behind it, but it means the feature is
invisible to any FR-coverage audit.
