# Payment consent — Visual Mockup

> Auto-generated from `screens/payment-consent/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/payment-consent/demo-data.yaml`

---

## Screen: Authorising payment

**Archetype** `empty_state` · **Initial state** `validating`
**States** `validating · exchanging · checking · authorised · error`

A **headless callback screen**, not a browsable one. It exists only for the return leg of the PISP
app-to-app authorisation and is never reachable from navigation. Its five states are a custom
vocabulary — three sequential progress stages, a terminal success, and an error — rather than the
canonical `loading/content/empty/error`, because there is no "content" to browse.

> **Design-validation note.** `DESIGN_VALIDATION.yaml#F-003` flags the absence of a literal
> `loading`/`content` pair as a warning rather than a critical, on the grounds that
> `validating`/`checking` are members of the schema's permitted `any_of` set. That finding carries
> a bias disclosure: it was adjudicated by the same author who wrote the screen. If a reviewer
> requires the literal vocabulary, this becomes a second critical.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **hidden** — the only PISP screen that hides it | `ui.yaml#shell.bottom_navigation_visible: false` |
| Top app bar | **visible**, title `{strings.payment_consent.screen_title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **none** — no back arrow; leaving mid-authorisation must go through `abandon_button` | `ui.yaml#shell.top_app_bar_leading: none` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

Hiding the bottom nav is the point: the PSU is mid-authorisation on an irreversible action, and a
tab tap would strand a staged consent. The only exits are `abandon_button` and completion.

---

## States: validating · exchanging · checking

All three render the **same two components** (`authorising_indicator`, `progress_detail`) and differ
only in the detail line. `check_again_button` appears in `checking` alone.

```
┌─────────────────────────────────────────┐
│  Authorising payment                    │  top-bar, NO leading icon
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │  authorising_indicator
│                                          │
│      Checking with your bank…            │  progress_detail — per stage
│                                          │
│           Check again                    │  checking state ONLY, text
│                                          │
└─────────────────────────────────────────┘
   no bottom nav
```

| State | `progress_detail` reads | What is happening |
|---|---|---|
| `validating` | "Verifying the response from your bank…" | `PendingAuthStore.consume` (single-use); returned `state`/`nonce` matched |
| `exchanging` | "Completing authorisation…" | POST `/oauth2/token`, `private_key_jwt` client assertion |
| `checking` | "Checking with your bank…" | polling GET `/domestic-payment-consents/{ConsentId}` until `Data.Status == AUTH` |

### Component hierarchy

```
payment-consent/ (validating | exchanging | checking)
├── TopAppBar → "Authorising payment"   [no leading icon]
├── Content (centered)
│   ├── authorising_indicator: progress_indicator (circular)
│   ├── progress_detail: text
│   └── check_again_button: button (text)   [checking only]
└── (no bottom nav)
```

| Element | Token | Notes |
|---|---|---|
| Indicator | `primary` | 48dp circular |
| Detail text | `bodyMedium` on `onSurfaceVariant` | centred |
| Check-again | `labelLarge` on `primary`, text variant | low emphasis — the automatic poll is primary |

**The poll is load-bearing, not best-effort.** Submitting against a consent that is not `Authorised`
returns `400 U009`, so the screen does not hand back until `AUTH` is confirmed or the deadline
passes. That is the opposite of the AIS `consent-callback`, whose status poll is best-effort
because a successful token exchange already proves authorisation there.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `check_again_button` | `check_again` | `call_api` | manual re-poll for a PSU who finished at the bank just after the automatic window — advances without restarting the payment |

`progress_detail` exists so a slow poll does not read as a hang.

---

## State: authorised

```
┌─────────────────────────────────────────┐
│  Authorising payment                    │
├─────────────────────────────────────────┤
│                                          │
│                  ( ✓ )                   │  verified_user, 64dp
│                                          │
│         Payment authorised                │
│                                          │
│    Sending your payment now…              │
│                                          │
└─────────────────────────────────────────┘
```

| Element | Token | Notes |
|---|---|---|
| Icon | `verified_user`, `primary` | 64dp — not `check_circle`; this confirms **authorisation**, not settlement |
| Title | `headlineMedium`, centred | |
| Body | `bodyMedium` on `onSurfaceVariant` | |

**A transient state, by design.** It confirms the consent reached `Authorised` and immediately
emits `PaymentConsentEvent.Authorised(consentId, token)`; **send-money** performs the submit. This
screen never navigates to Home the way the AIS `consent-callback` does.

Two deliberate constraints a reader should not "simplify away":

1. **The payment-scoped token is NEVER written to `ConsentSession`.** Doing so would overwrite the
   AIS session token and conflate a one-payment authorisation with a data-sharing session. This is
   the single most important invariant in the feature.
2. **Success is an event, not a navigation** — so send-money retains ownership of the idempotency
   key and the staged `Initiation`. Handing back by navigating would lose both.

The copy says "Sending your payment now", not "Payment sent". Nothing has been submitted yet.

---

## State: error

```
┌─────────────────────────────────────────┐
│  Authorising payment                    │
├─────────────────────────────────────────┤
│                                          │
│                  ( ! )                   │  error_outline, error, 64dp
│                                          │
│      Authorisation didn't complete        │
│                                          │
│   Your bank's response couldn't be       │  ← error.message
│   verified.                               │
│                                          │
│  [        Try again        ]              │  restart_authorisation_button
│            Abandon payment                │  abandon_button — ALWAYS shown
│                                          │
└─────────────────────────────────────────┘
```

### Recovery by cause

| Error type | Trigger | `restart_authorisation_button` | Why |
|---|---|:---:|---|
| `CodeExpired` | 400 `invalid_grant` | **shown** | nothing submitted; a fresh consent is safe |
| `AuthorisationTimedOut` | still `AwaitingAuthorisation` past deadline | **shown** | nothing submitted |
| `NetworkError` | IOException / timeout | **shown** | nothing submitted |
| `StateMismatch` | returned `state` ≠ pending | **hidden** | a **security** failure — possible replay/injection; never silently retried |
| `NoPendingAuthorisation` | app restarted mid-flow | **hidden** | nothing to resume; the single-use pending auth is gone |
| `ConsentRejected` | PSU declined at the bank | **hidden** | the PSU said no — re-prompting would override their decision |

`abandon_button` is shown in **every** error case, including the three with no restart. There is
always an exit.

| Element | Token | Notes |
|---|---|---|
| Icon | `error` | 64dp |
| Title | `headlineMedium`, centred | |
| Message | `bodyMedium` on `onSurfaceVariant` | |
| Restart CTA | `primary`, radius `full`, filled | |
| Abandon | `labelLarge` on `primary`, text variant | same-weight escape, lower emphasis |

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `restart_authorisation_button` | `retry_authorisation` | `emit_event` | emits `RestartAuthorisation`; **send-money** stages a fresh consent and relaunches |
| `abandon_button` | `abandon_payment` | `emit_event` | emits `Abandoned`, drops the payment |

Both are `emit_event`, not `call_api` — this screen decides nothing itself; send-money owns the
payment lifecycle.

**Abandon deliberately does not revoke.** The staged consent is left unauthorised rather than
deleted: an unauthorised consent expires on its own and can never be submitted against, so a
revocation call would be ceremony. Contrast `consent-detail`, where revoking an **active AIS**
consent is a real, necessary API call.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| payment-consent | `send-money` | every outcome — `Authorised`, `RestartAuthorisation`, `Abandoned` (all events, parent handles) |
| payment-consent | `consent-list` | error recovery when `error.type == ConsentRejected` (`dependencies`) |

Both resolve to existing `screens/` directories. Entry is **not** navigational: the redirect
arrives via the already-shipped per-platform `ConsentRedirectBus`.

---

## Implementation status

**SPECIFICATION ONLY.** No `feature/payment-consent` module exists in source. It reuses two shipped
pieces — `ConsentRedirectBus` and `PendingAuthStore` — but needs `core/network/api/Pisp.kt` for the
consent-status poll and a payments-scope token path. `ConsentCreationScope.PAYMENTS` already exists
at `OAuth.kt:103`; no caller passes it yet.
