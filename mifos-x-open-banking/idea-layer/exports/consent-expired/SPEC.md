# SPEC — Reconnect Your Account (Consent Expired)

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | consent-expired              |
| Flavor        | consumer                     |
| Status        | enriched                     |
| Quality Score | 100                          |
| ViewModel     | ConsentExpiredViewModel      |

---

## Overview

The Reconnect Your Account screen is the terminal renewal gate in the OBIE account-access-consent journey. It is shown when a previously-authorised consent has lapsed — either because its ExpirationDateTime passed (Status EXPD) or because the PSU revoked it at HSBC (Status RJCT or CANC). The screen is reachable from two callsites: cold-start splash, when the stored ConsentId resolves to a non-AUTH status; and from the consent-manager screen on explicit revoke.

On mount, when a `consentId` route argument is present, `ConsentExpiredViewModel` calls `GET /obie/open-banking/v4.0/aisp/account-access-consents/{ConsentId}` to confirm the current OBIE status before deciding which copy to render. While this check is in flight the screen shows the `loading` state — a green `#CDEDA3` status-check banner containing a 20dp circular spinner (#4C662B) and the caption "Checking your connection status…". Once the status resolves to EXPD or RJCT/CANC the screen transitions to `content`, revealing a muted reference line ("consent expired (EXPD) · 12 Mar 2026") drawn from the real `Status` and `ExpirationDateTime` fields returned by the OBIE endpoint. If the check itself fails — network error, 400, 401, or 404 — the screen falls to the `error` state: the reference line is hidden and the generic renewal copy is shown instead, so the PSU can still reconnect without knowing the technical reason.

The screen carries a full-bleed `#F9FAEF` background with no Top App Bar and no bottom navigation bar — it is a modal-style full-screen interstitial. A 72dp `schedule` icon (teal `#386663`) anchors the composition at top-centre, followed by the headline "Time to reconnect" (Outfit/headline_medium, `#1A1C16`, bold) and a centred body paragraph explaining that HSBC periodically requires re-approval to keep data secure. A white `#FFFFFF` card (16dp radius) beneath the body lists two reassurance points — that preferences are preserved and that data reloads automatically once re-consent is complete. Two buttons close the screen: a full-width filled "Reconnect" CTA (`#4C662B`, navigates to consent-request to start a fresh account-access-consent) and a secondary text-variant "Not now" link (`#386663`, navigates back to consent-intro).

---

## Screens

| ID               | Name                    | Route                  | Layout | Scroll   |
|------------------|-------------------------|------------------------|--------|----------|
| consent-expired  | Reconnect Your Account  | ConsentExpiredRoute    | Column | Vertical |

**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background. Route params: `consentId: String?` (stored ConsentId; null falls back to generic copy), `reason: String?` (optional EXPD | REVOKED hint).

---

## Components

| ID                       | Type              | Description                                                                                                                    |
|--------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------|
| expired_root             | stack (column)    | Root container — `#F9FAEF` background, spacing.lg padding, centre-aligned                                                     |
| expired_hero_icon        | icon              | `schedule` icon — 72dp, `#386663`, centre-aligned, spacing.md bottom padding; a11y role=image, label "Your account connection has expired" |
| expired_title            | text              | "Time to reconnect" — Outfit/headline_medium, `#1A1C16`, bold, centre, spacing.xs bottom padding; a11y heading level 1       |
| expired_subtitle         | text              | "Your permission to access your HSBC account data has expired…" — Outfit/body_medium, `#44483D`, centre, spacing.lg bottom   |
| expired_info_card        | card (filled)     | `#FFFFFF` fill, 16dp radius, spacing.lg padding, spacing.md bottom margin, match_parent width; a11y group "What reconnecting means" |
| expired_info_heading     | text              | "When you reconnect:" — Outfit/title_small, `#1A1C16`, bold, spacing.sm bottom; a11y heading level 2                         |
| expired_info_point_one   | text              | "You'll approve access again at HSBC — your saved preferences stay put" — Outfit/body_medium, `#44483D`, spacing.xs bottom   |
| expired_info_point_two   | text              | "Your accounts and transaction history reload automatically once it's done" — Outfit/body_medium, `#44483D`                   |
| expired_status_note      | text              | API-driven reference line — "consent expired (EXPD) · 12 Mar 2026"; Outfit/body_small, `#44483D`, centre; visible in content state only; loading shimmer in loading state |
| expired_check_banner     | card (filled)     | `#CDEDA3` fill, 8dp radius, spacing.md padding, spacing.md bottom margin; status check in-flight banner; visible in loading state only; a11y role=status |
| expired_check_spinner    | loading_indicator | Circular indeterminate — 20dp, `#4C662B`; inside check banner                                                                 |
| expired_check_message    | text              | "Checking your connection status…" — Outfit/body_small, `#1A1C16`, spacing.sm start padding; inside check banner              |
| expired_reconnect_button | button (filled)   | "Reconnect" — `#4C662B` fill, `#FFFFFF` text, Outfit/label_large, 8dp radius, spacing.md padding, match_parent; navigates to consent-request; spinner overlay while loading |
| expired_dismiss_button   | button (text)     | "Not now" — `#386663` text, Outfit/label_large, spacing.md padding, match_parent; navigates to consent-intro                  |

---

## States

| ID      | Trigger                                                           | Description                                                                                                                        |
|---------|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry — status check in flight                             | Icon + title + subtitle + info card visible; green `#CDEDA3` check-banner with spinner + "Checking your connection status…"; Reconnect button shows spinner overlay; reference line hidden |
| content | `StatusChecked(status: EXPD or RJCT/CANC)`                       | Check banner hidden; reference line resolves to "consent expired (EXPD) · 12 Mar 2026" (or RJCT/CANC variant); both CTAs active   |
| error   | `StatusCheckFailed` — network / 400 / 401 / 404                  | Reference line hidden; generic renewal copy shown (no technical detail); both CTAs still active; Reconnect navigates to consent-request |

---

## State Model

**ViewModel:** `ConsentExpiredViewModel`
**Screen State Type:** `ConsentExpiredUiState`
**Pattern:** MVI

| Name          | Type              | Default                  |
|---------------|-------------------|--------------------------|
| consentStatus | ConsentStatus     | ConsentStatus.EXPD       |
| isChecking    | Boolean           | true                     |
| checkFailed   | Boolean           | false                    |
| consentId     | String?           | null                     |

**Events:**
- `ConsentExpiredEvent.NavigateToConsentRequest`
- `ConsentExpiredEvent.NavigateToConsentIntro`

**Actions:**
- `ConsentExpiredAction.Internal.StatusChecked(status: ConsentStatus)`
- `ConsentExpiredAction.Internal.StatusCheckFailed`
- `ConsentExpiredAction.ReconnectClicked`
- `ConsentExpiredAction.DismissClicked`

**DI Dependencies:** `ConsentRepository`

**Errors:**
- `StatusCheckFailed` (HTTP 400): "We couldn't check your connection. You can still reconnect."
- `ConsentNotFound` (HTTP 404): "Your previous connection is no longer available. Please reconnect."
- `SessionEnded` (HTTP 401): "Your session has ended. Please reconnect to continue."

---

## Navigation

| From             | Action           | To               | Type    | Description                                                                     |
|------------------|------------------|------------------|---------|---------------------------------------------------------------------------------|
| consent-expired  | reconnect_click  | consent-request  | push    | Clears stale local consent record; starts a fresh account-access-consent journey |
| consent-expired  | dismiss_click    | consent-intro    | pop     | Dismisses the renewal prompt back to the journey entry screen                   |

---

## API Endpoints

| Endpoint                                                                | Auth          | Tag     | Purpose                                                                     |
|-------------------------------------------------------------------------|---------------|---------|-----------------------------------------------------------------------------|
| GET /obie/open-banking/v4.0/aisp/account-access-consents/{ConsentId}   | Bearer (PSU)  | Consent | Confirm current consent status (EXPD/RJCT/CANC) before rendering copy      |

---

## Design Tokens

| Token                           | Value           | Usage                                                                              |
|---------------------------------|-----------------|------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B         | "Reconnect" filled button fill                                                     |
| colors.light.on_primary         | #FFFFFF         | "Reconnect" filled button text                                                     |
| colors.light.primary_container  | #CDEDA3         | Status-check banner background                                                     |
| colors.light.background         | #F9FAEF         | Screen background, root container                                                  |
| colors.light.surface            | #FFFFFF         | Info card fill                                                                     |
| colors.light.on_surface         | #1A1C16         | "Time to reconnect" headline; info card heading; check banner message text         |
| colors.light.on_surface_variant | #44483D         | Subtitle body copy; info card body points; reference note; dismiss button text variant context |
| colors.light.secondary          | #386663         | Hero icon tint; "Not now" text button colour                                       |
| colors.light.error              | #BA1A1A         | (reserved — no error-state icon on this screen; error falls back to generic copy) |
| typography.headline_medium      | Outfit 28sp/400 | "Time to reconnect" headline                                                       |
| typography.title_small          | Outfit 14sp/500 | "When you reconnect:" info card heading                                            |
| typography.body_medium          | Outfit 14sp/400 | Subtitle; info card body points                                                    |
| typography.body_small           | Outfit 12sp/400 | Reference status note; check banner message                                        |
| typography.label_large          | Outfit 14sp/500 | "Reconnect" and "Not now" button labels                                            |
| radius.md                       | 8dp             | "Reconnect" button corners; check banner corners                                   |
| radius.lg                       | 16dp            | Info card corners                                                                  |

---

_Generated by /idea export | 2026-06-14_
