# Statements — Visual Mockup

> Auto-generated from `screens/statements/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/statements/demo-data.yaml`

**Implemented** — `feature/statements`, account-scoped pushed screen. **The first feature with a
non-`Nothing` event type**, and the origin of the project's platform file-delivery seam.

---

## Screen: Statements

**Archetype** `index_list` · **Initial state** `loading` · **States** `loading · content · empty · error`

**Credit-card only.** `HsbcProductCapability.supports(Statements, …)` is true *only* for
`CreditCard` — the exact mirror of `scheduled-payments` and `beneficiaries`, which appear on every
product **except** a credit card.

**Four states, not five.** Unlike the three gated list features, this one's store does **not** call
`recordIfUnsupported`, so there is no `unsupported` surface — the chip is simply hidden on
non-credit products.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Statements                          │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Statements                          │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ 1 Jun – 30 Jun 2026          ⭳   │   │  period + download icon
│  │ Statement 0042 · PDF              │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ 1 May – 31 May 2026          ⭳   │   │
│  │ Statement 0041 · PDF              │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ 1 Apr – 30 Apr 2026          ⭳   │   │
│  │ Statement 0040 · PDF              │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
statements/
├── TopAppBar → back + "Statements"
├── statements_list: list (vertical, items ← statements)
│   └── statement_card: card
│       ├── periodLabel      (titleMedium)
│       ├── statementId · format (bodySmall, on-surface-variant)
│       └── download_button: icon_button (download)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | tappable → `statement-detail` |
| Period | `titleMedium` on `onSurface` | e.g. "1 Jun – 30 Jun 2026" |
| Meta | `bodySmall` on `onSurfaceVariant` | statement id + format |
| Download icon | `primary`, 24dp | 48dp touch target |

**Two distinct tap targets per row.** The card opens `statement-detail`; the download icon fetches
the PDF without navigating. Keep them visually separate — a single tap target that sometimes
downloads and sometimes navigates would be unpredictable.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `statement_card` | navigate | `navigate` | → `statement-detail(accountId, statementId)` |
| `download_button` | `DownloadStatement` | `call_api` | one-shot `StatementFileRepository.downloadStatementFile(...)` → bytes → `StatementFileHandler` |

### The download seam — reuse this shape

The list itself is an ordinary memory-cached `ScreenDataStream` the ViewModel owns. The **download
is not part of it**: it is a one-shot `suspend` returning `NetworkResult<ByteArray, …>`, whose
bytes are handed to an injected **`StatementFileHandler`** — a delivery-seam *interface the feature
declares but does not implement*, keeping the ViewModel testable against a fake.

The platform binding is an **app-layer `expect`/`actual`** in `cmp-navigation`:
`StatementFileHandlerProvider.kt` (`expect`) + `.nonJs.kt` (FileKit `openFileSaver` +
`PlatformFile.write`) + `.js.kt` (no-op), via the `nonJsCommonMain`/`jsCommonMain` split, bound as
`single<StatementFileHandler>` in cmp-navigation's `KoinModules`.

**Reuse this whole shape** for any feature producing a file the platform must save or share.
`statement-detail` already does, injecting the same repository and handler for its Download PDF
without owning a second platform binding.

### Events — the first non-`Nothing` event type in the app

`BaseViewModel<StatementsState, StatementsEvent, StatementsAction>` with **two** events, both
download-failure snackbars.

**A successful download raises no event** — the platform's own save/share sheet is the feedback.
Adding a "Downloaded" snackbar on top would double-report an outcome the OS already confirmed.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Statements                          │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  description glyph
│         No statements yet                 │
│   Statements appear here once your first  │
│   billing period closes.                  │
├─────────────────────────────────────────┤
```

Consent-scoped statement metadata returned none. No CTA — nothing the customer can do but wait.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Statements                          │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│      Couldn't load statements              │
│   Check your connection and try again.    │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

**List failures only.** A failed *download* does not replace the screen — it raises a
`StatementsEvent` snackbar over the intact list, because the list is still valid and the PSU may
want to try a different statement.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | statements | Explore option (credit card only), carrying `accountId` |
| statements | `statement-detail` | statement card tap |
| statements | account-detail | back |

---

## Screenshot testing

`feature/statements` is the **first *feature* to apply the Roborazzi plugin** (only `cmp-android`
did before). `StatementsScreenScreenshotTest` renders each state through
`createComposeRule().onRoot().captureRoboImage(...)` — not the standalone `captureRoboImage { }`
overload, which silently skipped alternate captures. Goldens are committed under
`src/androidUnitTest/screenshots/`.

Worth knowing when changing this mockup: the states here have **pixel goldens**, so a visual change
fails `verifyRoborazziDebug` rather than passing silently.
