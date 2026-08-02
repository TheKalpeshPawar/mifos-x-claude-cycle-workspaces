# Settings — Visual Mockup

> Auto-generated from `screens/settings/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31

**Implemented** — `feature/settings`, the **More** bottom-nav tab. The project's only
**client-only** feature: no store, no `core/data` banking layer, no `:core:network` dependency.

---

## Screen: Settings

**Archetype** `settings` · **States** `content · empty · error`

**Three states, and no `loading`.** The ViewModel injects `UserDataRepository` and reads DataStore,
which does not fail and does not take long enough to warrant a spinner. `Empty` and `Error` are
**synthetic, test-only** states with no production trigger — they exist so the surface is
exhaustive, not because either has been observed.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — More tab active (tab 4 of 4) | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.settings.title}` | `ui.yaml#shell` |
| Top app bar leading | **null** — tab root, no back arrow | `ui.yaml#shell.top_app_bar_leading: null` |
| FAB | **absent** | `ui.yaml#shell` |

Settings **became** the More tab: `MoreTab` previously pointed at a `PlaceholderScreen`, and
`SettingsRoute` replaced it. It stays a **flat route**, not a `navigation<Graph>`, so
`shouldShowNavigation` (which tests `startDestinationRoute`) keeps the bottom bar visible.

---

## State: content

```
┌─────────────────────────────────────────┐
│  Settings                               │  no back arrow — tab root
├─────────────────────────────────────────┤
│  APPEARANCE                              │  section_header
│  ┌──────────────────────────────────┐   │
│  │ Theme                    System ▾│   │  theme_row — select
│  └──────────────────────────────────┘   │
│                                          │
│  ACCOUNT                                 │  section_header
│  ┌──────────────────────────────────┐   │
│  │ 🛡  Manage consents            ›  │   │  consents_row — chevron
│  │    Review and revoke access      │   │
│  └──────────────────────────────────┘   │
│                                          │
│  ABOUT & LEGAL                           │  section_header
│  ┌──────────────────────────────────┐   │
│  │ 🛈  Privacy policy             ↗  │   │  privacy_row — EXTERNAL glyph
│  ├──────────────────────────────────┤   │
│  │ ⓘ  Open-source licences        ›  │   │  licences_row — chevron
│  ├──────────────────────────────────┤   │
│  │    App version                    │   │  app_version_row — NO affordance
│  │    1.0.0 (142)                    │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

### Component hierarchy

```
settings/
├── TopAppBar → "Settings"   [no leading icon]
├── appearance_header: section_header
│   └── theme_row: select (FOLLOW_SYSTEM | LIGHT | DARK)
├── account_header: section_header
│   └── consents_row: list_item (leading policy, trailing chevron)
├── about_header: section_header
│   ├── privacy_row: list_item (leading privacy_tip, trailing external_link)
│   ├── licences_row: list_item (leading info, trailing chevron)
│   └── app_version_row: list_item (no icon, no trailing, no click)
└── BottomNav (More active)
```

| Element | Token | Notes |
|---|---|---|
| Section header | `labelMedium` on `onSurfaceVariant`, uppercase | |
| Row min height | `accessibility.min_touch_target_dp` | 48dp |
| Row title | `bodyLarge` on `onSurface` | |
| Row subtitle | `bodyMedium` on `onSurfaceVariant` | |
| Leading icon | `onSurfaceVariant`, 24dp | |
| Trailing | `onSurfaceVariant`, 24dp | chevron **or** external-link |

**The trailing glyph tells the truth about where a tap goes.** `chevron` means it opens in-app;
`external_link` means it leaves for the browser. `privacy_row` carries the external glyph and the
`opens_externally` a11y label because `LocalUriHandler.openUri` hands off to the platform —
a customer should know before tapping that they are leaving a banking app.

**`app_version_row` is deliberately inert** — no icon, no trailing affordance, no click handler.
It is a build-identity readout. Giving it a chevron would promise a screen that does not exist.

> **Known gap:** `app_version_row` has no `accessibility_label`. One of two interactive-or-listed
> components in the project missing one (the other is `transactions/tx_category_tag`). Recorded,
> not fixed here.

### Theme — the only persisted preference

| Interaction | Action | Effect | Notes |
|---|---|---|---|
| Tap row | `ToggleThemeMenu` | `transform_state` | flips `isThemeMenuExpanded` — **local UI state, nothing persisted** |
| Dismiss | `DismissThemeMenu` | `transform_state` | collapses without changing selection |
| Pick option | `SelectTheme(config)` | **`persist_db`** | writes `user_preferences.darkThemeConfig` via `UserDataRepository` |

Only `SelectTheme` persists. It writes through `androidx.datastore`, the stream re-emits, and the
**whole app retints** — this feature is the first production caller of `setDarkThemeConfig`; the
read path to the applied theme was already wired end-to-end.

### Other interactions

| Component | Action | Target | Effect |
|---|---|---|---|
| `consents_row` | `navigate_consent_list` | `consent-list` | `navigate` — the only outbound in-app nav in the account group |
| `privacy_row` | `open_privacy_url` | `https://mifos.org/privacy-policy/` | `share_external` |
| `licences_row` | `navigate_licences` | `licences` | `navigate` — sibling destination in the same module |

Nav rows are **nav-host callbacks**, not `SettingsAction` members.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  Settings                               │
├─────────────────────────────────────────┤
│         Nothing to show yet               │
│   Your preferences aren't available.      │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

**Synthetic.** `SettingsUiState.Empty` has **no production trigger** — DataStore always resolves a
preference set, falling back to defaults. It exists so the state surface is exhaustive and so
`FakeUserDataRepository` can drive it in tests. Design it plainly; a customer will not see it.

No illustration glyph, unlike every other empty state in the app — there is nothing meaningful to
depict, and a wallet or folder icon would imply missing data rather than an impossible state.

---

## State: error

```
┌─────────────────────────────────────────┐
│  Settings                               │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│      Couldn't load settings               │
│   Something went wrong reading your       │
│   preferences.                            │
│  [          Try again          ]          │  retry_button
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

Both `SettingsErrorKind` values render here and **both are retriable**, so the CTA is
unconditional. Also synthetic — a DataStore read has no production failure path; the state is
reachable only through the test fake, which was designed with a failure hook from the start
precisely because production offers none.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| settings | `consent-list` | `consents_row` |
| settings | `licences` | `licences_row` |
| settings | *external browser* | `privacy_row` → `https://mifos.org/privacy-policy/` |

Both in-app targets resolve to existing `screens/` directories. Settings is a **tab**, so it has no
inbound nav reference — it is reached from the bottom bar.

---

## Removed in the 2026-07-28 reverse sync

The idea-layer previously listed five features this screen does **not** have. Recorded so they are
not reintroduced:

| Removed | Status in source |
|---|---|
| Biometric lock | does not ship |
| Session timeout | does not ship |
| Notifications | does not ship |
| Profile row | deleted — passed an empty `selectedAccountId`, producing a malformed `GET /accounts//party` → 403. Identity now lives on `account-holder`, reached from an account-detail chip |
| Clear Local Data | does not ship |
