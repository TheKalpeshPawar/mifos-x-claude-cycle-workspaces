# mifos-x-open-banking — Product Idea

> Source of truth. Update before running `/idea sync` to propagate changes.
> Last updated: 2026-05-22 (post-template sync — empty-slate scaffold)

## Status: Empty Slate

The current source tree contains three template features (crypto, currency-rates, emi-calculator) inherited from `kmp-project-template`. These are **scheduled for removal** — they do not reflect the product intent of this project. Only `home`, `profile`, and `settings` will be retained as scaffolding for the actual app.

> Real feature scope is **not yet defined**. Run `/idea add` to declare features once vision is finalized.

## Elevator Pitch (placeholder)

**Mifos X Open Banking** is a Kotlin Multiplatform open-banking application from the Mifos Initiative — runs on Android, iOS, Desktop, and Web from a single codebase using Stream-First architecture (BaseViewModel + ScreenDataStream + Store5).

Specific feature roster, problem statement, and target users will be filled in once product direction is set.

## Target Users (placeholder)

To be defined. Likely audiences when scope is set:
- Mifos community / banking-cooperative end users
- Developers learning KMP for fintech

---

## Personas

> To be defined once feature scope is set.

---

## Brand

| Token | Value |
|---|---|
| **App name** | Mifos X Open Banking |
| **Primary color** | `#1800B1` (Mifos deep purple) |
| **Accent** | `#575899` |
| **Secondary** | `#5C0068` |
| **Tertiary** | `#7E5260` |
| **Design system** | Material Design 3 (light + dark) |
| **Background (light)** | `#FCF8FF` |
| **Background (dark)** | `#13131B` |
| **Typography** | Inter (body) · Space Grotesk (display) |

---

## At a glance

| | |
|---|---|
| **Domain** | open banking / fintech (scope TBD) |
| **Platforms** | Android · iOS · Desktop · Web (Wasm + JS) |
| **Tech stack** | Kotlin 2.1.20 · Compose Multiplatform 1.8.2 · Koin 4.1.0 · Ktor/Ktorfit · Room KMP · Store5 |
| **Architecture** | Stream-First (BaseViewModel + ScreenDataStream + Store5) |
| **Backend** | TBD (currently Firebase Crashlytics + Performance for observability only) |
| **License** | MPL-2.0 |
| **Repo** | [openMF/mifos-x-open-banking](https://github.com/openMF/mifos-x-open-banking) |

---

## Active Scaffolding

These three feature modules are retained as scaffolding for the eventual product:

| Module | Role |
|---|---|
| **home** | Entry point / hub — will route to real features once defined |
| **profile** | User profile shell — will integrate with real auth/user data |
| **settings** | App preferences — theme, language, notifications |

---

## Pending Removal (template residue)

These modules will be removed from source — they came from `kmp-project-template` and are not part of this project's scope:

- `feature/crypto` — template demo for Store5 + external HTTP
- `feature/currency-rates` — template demo for streaming repository
- `feature/emi-calculator` — template demo for pure-derived state

> Until removed, they remain in `PROJECT_CONFIG.yaml#modules.feature` to reflect actual source state. The idea-layer intentionally does **not** describe them as product features.
