# Consent callback — Visual Mockup

> Auto-generated from `screens/consent-callback/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30

**Implemented** — `feature/consent-callback`. The **AIS** return leg of the OAuth round-trip.
Reached only via redirect, never from navigation.

---

## Screen: Connecting

**Archetype** `empty_state` · **Initial state** `loading`
**States** `loading · awaiting · content · access_denied · security_error · error`

A **headless callback screen**. Six states: two progress stages, a terminal success, and **three
distinct failure surfaces** — because "the PSU declined", "the redirect could not be verified" and
"something broke" need different words and different exits.

> **AIS sibling of `payment-consent`, with one load-bearing asymmetry.** Here the consent-status
> poll is **best-effort**: a successful token exchange already proves authorisation. In the PISP
> screen the poll is **mandatory**, because submitting against a consent that is not `Authorised`
> returns `400 U009`. Do not unify the two.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **hidden** | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **none** — no back arrow | `ui.yaml#shell` |
| FAB | **absent** | `ui.yaml#shell` |

No back arrow and no tabs: the PSU is mid-authorisation and there is nothing to go back *to* — the
previous screen was the bank's website in a browser.

---

## States: loading · awaiting

```
┌─────────────────────────────────────────┐
│  Connecting                             │
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │
│                                          │
│      Verifying your connection…           │  per stage
│                                          │
└─────────────────────────────────────────┘
   no bottom nav
```

| State | Copy | What runs |
|---|---|---|
| `loading` | "Verifying your connection…" | `PendingAuthStore.consume` (single-use); `state`/`nonce` checked |
| `awaiting` | "Finishing up…" | code → PSU token exchange, then the best-effort status poll |

**Order matters and is not obvious.** `ConsentCallbackViewModel` records the consent
(`saveConsentMeta`) **BEFORE** persisting the tokens. Persisting the tokens flips
`ConsentSession.isActive()`, and the root navigator immediately routes to Home — tearing this
screen down. Recording afterwards would be cancelled mid-write.

---

## State: content — authorised

```
┌─────────────────────────────────────────┐
│                  ( ✓ )                   │  check_circle
│         You're connected                  │
│    Taking you to your accounts…           │
└─────────────────────────────────────────┘
```

Transient. Tokens are persisted, `isActive()` flips, and the **root navigator** routes to Home.
This screen never navigates itself.

---

## State: access_denied

```
┌─────────────────────────────────────────┐
│  Connecting                             │
├─────────────────────────────────────────┤
│                  ( ⓘ )                   │  info_outline — NOT error
│      You didn't share your accounts       │
│                                          │
│   You chose not to share your HSBC        │
│   account data. You can start again at    │
│   any time.                               │
│                                          │
│  [        Start over        ]             │
└─────────────────────────────────────────┘
```

**The PSU declined at the bank. That is a valid choice, not a failure.**

- Glyph is `info_outline` in `onSurfaceVariant` — **never** `error_outline` in `error`.
- Copy is neutral: "You chose not to share…". No "failed", no "denied", no apology.
- The CTA is "Start over", not "Try again" — retrying implies the app thinks they made a mistake.

Getting the register wrong here reads as the app arguing with a customer who exercised a right the
whole regulation exists to protect.

---

## State: security_error

```
┌─────────────────────────────────────────┐
│  Connecting                             │
├─────────────────────────────────────────┤
│                  ( ⚠ )                    │  warning
│      Security check failed                │
│                                          │
│   The authorisation response could not    │
│   be verified. Please start the           │
│   connection process again from login.    │
│                                          │
│  [        Start again        ]            │
└─────────────────────────────────────────┘
```

**A separate state from generic `error`, and it must stay separate.** The returned `state` or
`nonce` did not match the pending authorisation — a possible replay or injection. The response is
**discarded**, never retried against, and the PSU restarts from login so a fresh `state`/`nonce`
pair is minted.

Distinct from `access_denied`: nothing about the PSU's intent is known here. Distinct from `error`:
it is not transient, and no amount of retrying the same response will help.

---

## State: error

```
┌─────────────────────────────────────────┐
│                  ( ! )                   │  error_outline, error
│      Couldn't complete the connection      │
│   Check your connection and try again.    │
│  [          Try again          ]          │
└─────────────────────────────────────────┘
```

Transport failures and expired codes — the genuinely transient class. The only one of the three
failure states that offers a true retry.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| *(redirect)* | consent-callback | `ConsentRedirectBus.publish` → `RootNavScreen` collects → `consentCallbackDestination` |
| consent-callback | **home** | success — via the root navigator, not this screen |
| consent-callback | `login` | Start over / Start again |

**Entry is not navigational.** HSBC's redirect re-enters per platform — Android
`MainActivity.onCreate`/`onNewIntent`, desktop loopback, iOS bridge — and `RootNavScreen` collects
`ConsentRedirectBus.redirects` (replay = 1).

---

## The three failure states, side by side

| State | Glyph | Colour | Cause | CTA |
|---|---|---|---|---|
| `access_denied` | `info_outline` | `onSurfaceVariant` | PSU declined | Start over |
| `security_error` | `warning` | `onSurfaceVariant` | `state`/`nonce` mismatch | Start again |
| `error` | `error_outline` | `error` | transport / expired code | Try again |

Only the last is red. Collapsing these into one error surface would tell a customer who made a
deliberate choice that something went wrong.
