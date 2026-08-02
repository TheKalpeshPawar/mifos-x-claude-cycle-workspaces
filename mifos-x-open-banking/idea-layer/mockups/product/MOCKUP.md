# Product — Visual Mockup

> Auto-generated from `screens/product/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/product/demo-data.yaml`

**Implemented** — `feature/product`, `ProductRoute(accountId)`. Reached from the account-detail
Explore list.

---

## Screen: Product

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · empty · error`

**The only screen in the app not backed by a stream.** `ProductRepository.getProduct(accountId)` is
a bare `suspend` returning `NetworkResult<ProductTerms?, NetworkError>` — no Store5, no
`AppStoreRegistry` qualifier, no `registerForLogout`. The ViewModel maps the raw `NetworkResult`
onto the four states by hand.

`data-flow.yaml` declares `cache_strategy: none` deliberately: the bank can revise product terms,
and a cached copy would misstate the charges a customer is actually subject to. **Do not copy this
screen as a template** unless the data genuinely must not be cached.

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
│  ←  Product                             │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │  progress_indicator, circular
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Product                             │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  product_header_card
│  │ PERSONAL CURRENT ACCOUNT         │   │  product_type_label, labelSmall
│  │ HSBC Advance Account             │   │  product_name, titleLarge
│  │ PCA-ADV-001                      │   │  product_id, bodySmall mono
│  └──────────────────────────────────┘   │
│                                          │
│  FEES & CHARGES                          │  section_header
│  ┌──────────────────────────────────┐   │
│  │ Monthly maximum charge   £80.00  │   │  monthly_max_charge_row
│  └──────────────────────────────────┘   │
│                                          │
│  CREDIT INTEREST                         │  section_header
│  ┌──────────────────────────────────┐   │
│  │ Tier 1  £0 – £1,000       0.15%  │   │  tier_band_list
│  │ Tier 2  £1,000 – £5,000   0.75%  │   │
│  │ Tier 3  Over £5,000       1.10%  │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
product/
├── TopAppBar → back + "Product"
├── product_header_card: card
│   ├── product_type_label (labelSmall, secondary)
│   ├── product_name       (titleLarge)
│   └── product_id         (bodySmall, mono, on-surface-variant)
├── fees_header: section_header
│   └── monthly_max_charge_row: list_item
├── credit_interest_header: section_header
└── credit_interest_list: list
    └── tier_band_list: list (per band — range + rate)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Header card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Type label | `labelSmall` on `secondary`, uppercase | e.g. "PERSONAL CURRENT ACCOUNT" |
| Product name | `titleLarge` on `onSurface` | |
| Product id | `bodySmall`, mono, `onSurfaceVariant` | |
| Charges / rates | `bodyLarge`, mono, `semantic.money.neutral` | **unsigned** |
| Section header | `labelMedium` on `onSurfaceVariant`, uppercase | |

> **`%` renders literally if you write `%%`.** Compose Multiplatform's resource formatter does
> **not** collapse Android's `%%` escape, so `"%1$s%% AER"` displays `0.15%% AER`. Write a single
> `%`. No assertion catches this — tags and counts pass — so check a screenshot golden after
> touching any templated rate string. This screen is the app's densest user of `%`.

**Tier bands are flattened before they reach the UI.** `ProductTerms` (`core/model`) turns the
nested OBIE `PCA`/`BCA` band groups into plain lists, so the feature never sees an OBIE shape.
One `ProductBlock` DTO serves both `PCA` and `BCA` because the fields read are identically shaped.

**Interactions** — none. Rows are informational; there is no product detail beyond this screen.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Product                             │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  description glyph
│      No product details                   │
│   The bank doesn't publish terms for      │
│   this account.                           │
├─────────────────────────────────────────┤
```

**Two different outcomes both mean Empty, and neither is an error:**

| Outcome | Why empty |
|---|---|
| `Success(null)` | the mapper found neither a `PCA` nor a `BCA` block — the **normal** answer for GlobalMoney, Savings and CreditCard |
| **HTTP 404** | the bank publishes no product resource for this account |

Neither is a failure a customer can act on, so neither gets the error icon or a Retry. 401, 403 and
transport failures keep the error state.

> **Stale test:** `tests.yaml` TC-PROD-006 still asserts 404 → error. It contradicts this screen
> and the resolved `data-flow.yaml`; the three-way contradiction between `data-flow`, `api.yaml`
> and `tests.yaml` was resolved to **empty** on 2026-07-30, but the test row was not updated.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Product                             │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│    Couldn't load product details           │
│   Check your connection and try again.    │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Reserved for 401, 403 and transport failures. A 404 is **not** here — see Empty above.

Because there is no stream, Retry re-invokes the one-shot `getProduct(accountId)` directly rather
than calling `stream.refresh()`. The feature's test fake returns a `NetworkResult` with no
buffered refresh trigger, unlike every stream-backed feature's fake.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | product | Explore option (`AccountDetailChip.Product`), carrying `accountId` |
| product | account-detail | back |

**Ungated** — a product either exists or the empty state explains it. `AccountDetailChip.Product`
already existed; its `navigateFromChip` branch was repointed off the dead `ProductsRoute`
placeholder, so no new chip member was added and the suites asserting all nine chips in
declaration order stayed green.
