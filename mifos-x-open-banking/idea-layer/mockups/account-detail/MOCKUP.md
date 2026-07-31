# Account detail — Visual Mockup

> Auto-generated from `screens/account-detail/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/account-detail/demo-data.yaml`

**Implemented** — `feature/account-detail`, `AccountDetailRoute(accountId)`. The app's **hub
screen**: the only gated entry point to seven sub-screens.

---

## Screen: Account detail

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · empty · error`

**Two streams merged.** Account metadata and balances are fetched in parallel and combined in the
ViewModel via `combineScreenStates` — the reference example of the two-stream shape, alongside
`statement-detail`.

**No `Unsupported` state, deliberately.** This screen is the *host* of the gated resources, not a
gated resource itself. `GET /accounts/{id}` always resolves for an account in consent. Its chips
are what get gated.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Account                             │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │  loading_spinner
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

One spinner covers **both** streams. `combineScreenStates` holds Loading until each resolves.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Account                             │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  account_header_card
│  │ CURRENT ACCOUNT                  │   │
│  │ Current account ·· 3349          │   │  titleLarge
│  │ 80-20-01 10203349                │   │  mono
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │  description card
│  │ GLOBAL MONEY ACCOUNT             │   │  OMITTED when blank
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │  open_banking_badge
│  │ 🛡  Shared via Open Banking       │   │
│  └──────────────────────────────────┘   │
│                                          │
│  BALANCES                                │  balances_header
│  ┌──────────────────────────────────┐   │
│  │ Available            £21,530.92  │   │  balances_list, mono
│  │ Current              £21,530.92  │   │
│  └──────────────────────────────────┘   │
│                                          │
│  EXPLORE                                 │  actions_header
│  (📄 Transactions) (📃 Statements) →     │  action_chips, horizontal scroll
│  (🔄 Standing orders) (📶 Direct debits) │  GATED per product
│  (⏱ Scheduled) (👥 Beneficiaries)        │
│  (🏧 ATM locator) (📄 Product) (👤 Holder)│
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

### Component hierarchy

```
account-detail/
├── TopAppBar → back_button + title
├── account_header_card: card
├── description card                    [omitted when Description is blank]
├── open_banking_badge: card
├── balances_header: section_header
├── balances_list: list                 → balances_empty_state when none
├── actions_header: section_header
└── action_chips: chip_row (horizontal, 9 chips)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Header card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Identifier | mono, `onSurfaceVariant` | `formatAccountIdentifier` |
| Balance | `headlineSmall`, mono, `semantic.money.neutral` | **unsigned** |
| Chip | tonal, `secondaryContainer` | 32dp, `radius/full` |

**Content order is deliberate:** header → *description* → balances → Explore.

**The description card renders OBIE `Description` verbatim and is omitted — not blanked — when the
field is empty.** Guarded with `isNotBlank()`, because the field is free text and a whitespace-only
value would otherwise leave a heading above an empty line. It earns its place because
`AccountTypeCode` reports `CACC` for a Global Money wallet exactly as for an ordinary current
account, so the description is frequently the only thing that says what the product is.

> The sandbox is uneven here: two test accounts return the literal filler `"Description of the
> account"`, one `BMM ACCOUNT`, one `GLOBAL MONEY ACCOUNT`. The same string is also the default of
> `AccountDetailFixtures.detail()`, so seeing it in the app is **not** evidence of a hardcoded value.

### The nine Explore chips — and which are gated

All nine always exist in `AccountDetailChip`'s declaration order; `availableChipsFor` decides
visibility per product.

| # | Chip | Icon | Target | Gated? |
|---|---|---|---|---|
| 1 | Transactions | `receipt_long` | `transactions` | ungated |
| 2 | Statements | `description` | `statements` | **credit-card ONLY** |
| 3 | Standing orders | `autorenew` | `standing-orders` | gated |
| 4 | Direct debits | `subscriptions` | `direct-debits` | gated |
| 5 | Scheduled payments | `schedule` | `scheduled-payments` | **every product EXCEPT credit card** |
| 6 | Beneficiaries | `people` | `beneficiaries` | **every product EXCEPT credit card** |
| 7 | ATM locator | `atm` | `_placeholder:atm-locator` | ungated — **placeholder** |
| 8 | Product | `description` | `product` | ungated |
| 9 | Account holder | `person` | **`account-holder`** | ungated |

**Statements is the mirror of Scheduled payments and Beneficiaries.** Statements shows *only* on a
credit card; those two show on *everything except* a credit card. Gating is **opt-in** — a chip
absent from the `gated` map is always visible.

Prediction comes from `HsbcProductCapability.supports`, corrected at runtime: the **store fetcher**
calls `recordIfUnsupported(...)` on a `U000` refusal before rethrowing — never a ViewModel. It
fails **open**: `HsbcProductType.Unknown` and unlisted endpoints stay permissive.

**This is the app's only gated entry point.** Home used to be a second, gating a Statements
quick-action, but that row is gone — so `HsbcProductCapability` has exactly one consumer again.

#### Two chips whose targets were repaired

- **`chip_atm_locator` → `_placeholder:atm-locator`.** The `atm-locator` screen was deleted in the
  2026-07-28 reverse sync; `AtmLocatorRoute` survives in `cmp-navigation` as a `PlaceholderScreen`
  destination only. The `_placeholder:` prefix marks it as intentionally unresolved so nav-target
  verification does not read it as a dead reference.
  > This chip's description trips the DC-2 forbidden-token scan on the word "placeholder" — a
  > **false positive**, recorded at confidence 55 in `CAPABILITY_GAPS.yaml`. It legitimately names
  > the source class `PlaceholderScreen("ATM locator")`.
- **`chip_party` → `account-holder`.** Was `target: party`, a screen renamed on 2026-07-28.
  `flow.yaml` already recorded the correct binding (`AccountDetailChip.Party → AccountHolderRoute`);
  `ui.yaml` did not. Retargeted 2026-07-30. The chip's **enum member is still named `Party`** in
  source — only the screen was renamed.

**Interactions** — every chip is `effect: navigate`, passing `accountId`. All nine resolve through
one host callback, `onNavigateToChip(chip, accountId)`, dispatched by `navigateFromChip()` — they
are **not** nine discrete ViewModel actions.

---

## State: empty

Balances specifically — the account resolved but returned none. `balances_empty_state` replaces the
list **inside** the content layout; the header card, description and chips all remain. There is no
whole-screen empty state, because an account in consent always has metadata to show.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Account                             │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_state
│      Couldn't load this account            │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Typed 401 / 403 / 404 / network handling. Retry refreshes **both** streams.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| accounts | account-detail | account card tap |
| account-detail | transactions · statements · standing-orders · direct-debits · scheduled-payments · beneficiaries · product · account-holder | Explore chips |
| account-detail | *(placeholder)* | ATM locator chip |

All eight real targets resolve to existing `screens/` directories. **Home no longer navigates
here** — `onNavigateToAccountDetail` was removed from `homeGraph`; account detail is reached from
the Accounts tab only.
