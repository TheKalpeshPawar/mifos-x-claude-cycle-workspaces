# SPEC — Access Not Granted (Consent Declined)

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | consent-declined             |
| Flavor        | consumer                     |
| Status        | enriched                     |
| Quality Score | 96                           |
| ViewModel     | ConsentDeclinedViewModel     |

---

## Overview

The Access Not Granted screen is the terminal feedback screen reached when the PSU does not complete authorisation at HSBC. It is navigated to from the `auth-callback` handler whenever the deep-link callback carries an `error` parameter (e.g. `access_denied`, `login_required`) or when the resolved consent `Status` is `RJCT` (rejected) or `CANC` (cancelled). The screen makes no live OBIE call; the declined outcome is delivered as navigation arguments from the callback handler.

The screen opens in one of two states. In the `content` state — the clean decline, when the PSU simply tapped Cancel or Deny at HSBC without an explicit OAuth error code — the layout shows a large `block` icon (72dp `#BA1A1A`), a reassuring headline "Access wasn't granted", a subtitle confirming no data was shared and nothing was changed, and a white reasons card listing three common causes (chose Cancel or Deny, approval timed out, HSBC couldn't verify identity). In the `error` state the same layout is shown, but a muted technical reference line appears below the reasons card, rendering the resolved `consentStatus` (RJCT or CANC) and the callback `callbackError` param (e.g. `access_denied`).

The primary CTA "Try again" (filled `#4C662B`) clears the stale local consent record and navigates back to `consent-request` to restart the journey. The secondary "Maybe later" text button (`#386663`) navigates to `consent-intro` to let the PSU step away without pressure. There is no top bar and no bottom navigation — this is a full-screen terminal feedback shell.

---

## Screens

| ID               | Name               | Route              | Layout | Scroll   |
|------------------|--------------------|--------------------|--------|----------|
| consent-declined | Access Not Granted | /consent-declined  | Column | None     |

**Shell:** No Top App Bar. No bottom navigation bar. Full-screen terminal feedback layout.

| Action       | Label        | Trigger                                       |
|--------------|--------------|-----------------------------------------------|
| retry_click  | Try again    | navigate to consent-request (clear stale consent first) |
| dismiss_click | Maybe later | navigate to consent-intro                     |

---

## Components

| ID                       | Type   | Description                                                                                                                        |
|--------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------|
| declined_root            | stack  | Column, `#F9FAEF` bg, `spacing.lg` padding, center alignment — root container                                                     |
| declined_hero_icon       | icon   | `block` — 72dp, `#BA1A1A`, centered, `spacing.md` bottom padding; a11y "Access was not granted"                                   |
| declined_title           | text   | "Access wasn't granted" — Outfit/headline_medium, `#1A1C16`, bold (700), centered, `spacing.xs` bottom padding; heading level 1   |
| declined_subtitle        | text   | "You didn't finish granting access at HSBC, so we couldn't connect your account. No data was shared and nothing was changed." — Outfit/body_medium, `#44483D`, centered, `spacing.lg` bottom padding |
| declined_reasons_card    | card   | Filled, `#FFFFFF` bg, 16dp radius, `spacing.lg` padding, `spacing.md` bottom margin, full width; a11y group "Why this can happen" |
| declined_reasons_heading | text   | "This can happen if:" — Outfit/title_small, `#1A1C16`, bold (700), `spacing.sm` bottom padding; heading level 2                   |
| declined_reason_one      | text   | "You chose 'Cancel' or 'Deny' on the HSBC approval screen" — Outfit/body_medium, `#44483D`, `spacing.xs` bottom padding           |
| declined_reason_two      | text   | "The approval timed out before it was confirmed" — Outfit/body_medium, `#44483D`, `spacing.xs` bottom padding                     |
| declined_reason_three    | text   | "HSBC couldn't verify your identity during sign-in" — Outfit/body_medium, `#44483D`                                               |
| declined_status_note     | text   | "Reference: access_denied · consent RJCT" — Outfit/body_small, `#44483D`, centered, `spacing.lg` bottom padding; visible in `error` state only; data-driven from callback nav args |
| declined_retry_button    | button | "Try again" — filled, `#4C662B` bg, `#FFFFFF` text, Outfit/label_large, 8dp radius, `spacing.md` padding, full width; navigates to consent-request |
| declined_cancel_button   | button | "Maybe later" — text variant, `#386663` text, Outfit/label_large, `spacing.md` padding, full width; navigates to consent-intro    |

---

## States

| ID      | Trigger                                                                    | Description                                                                                                                                     |
|---------|----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| content | Callback without explicit `error` param (`callbackError = null`)           | Hero icon, title, subtitle, reasons card, Try again button, Maybe later button — technical reference line hidden                                 |
| error   | Callback carried explicit `error` param OR consent Status is RJCT/CANC    | Same layout as content + `declined_status_note` visible, showing the resolved `callbackError` and `consentStatus` (e.g. "Reference: access_denied · consent RJCT") |

---

## State Model

**ViewModel:** `ConsentDeclinedViewModel`
**Screen State Type:** `ConsentDeclinedUiState`
**Pattern:** MVI

| Name          | Type          | Default              | Note                                                                                                  |
|---------------|---------------|----------------------|-------------------------------------------------------------------------------------------------------|
| consentStatus | ConsentStatus | ConsentStatus.RJCT   | enum { AWAU, AUTH, RJCT, CANC, EXPD } — only RJCT or CANC reach this screen                          |
| callbackError | String?       | null                 | OAuth error param from deep-link (e.g. `access_denied`, `login_required`) — null = clean cancel       |
| hasErrorCode  | Boolean       | false                | Drives visibility of `declined_status_note` — true when `callbackError` is non-null                   |

**Events:**
- `ConsentDeclinedEvent.NavigateToConsentRequest`
- `ConsentDeclinedEvent.NavigateToConsentIntro`

**Actions:**
- `ConsentDeclinedAction.RetryClicked` — clears stale RJCT/CANC consent record, emits NavigateToConsentRequest
- `ConsentDeclinedAction.DismissClicked` — emits NavigateToConsentIntro

**DI Dependencies:** `ConsentRepository` (read-only — clears stale consent on retry)

---

## Navigation

| From             | Action        | To              | Type | Description                                                              |
|------------------|---------------|-----------------|------|--------------------------------------------------------------------------|
| consent-declined | retry_click   | consent-request | push | "Try again" — clears stale local consent record, restarts consent journey |
| consent-declined | dismiss_click | consent-intro   | pop  | "Maybe later" — abandons attempt, returns to onboarding entry screen     |

---

## API Endpoints

_(none — this screen performs no network calls; navigation/redirect only)_

This is a terminal feedback screen. The declined outcome (consentStatus, callbackError) is delivered via navigation arguments from the auth-callback handler. On "Try again", the navigation to `consent-request` re-issues `POST /obie/open-banking/v4.0/aisp/account-access-consents` from that screen, not from here. Demo data is sourced from `screens/consent-declined/demo-data.yaml`.

---

## Design Tokens

| Token                           | Value             | Usage                                                                                  |
|---------------------------------|-------------------|----------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B           | "Try again" button fill                                                                |
| colors.light.on_primary         | #FFFFFF            | "Try again" button label                                                              |
| colors.light.error              | #BA1A1A           | Hero `block` icon colour                                                               |
| colors.light.background         | #F9FAEF           | Screen base                                                                            |
| colors.light.surface            | #FFFFFF           | Reasons card fill                                                                      |
| colors.light.on_surface         | #1A1C16           | Title; reasons card heading                                                            |
| colors.light.on_surface_variant | #44483D           | Subtitle; reason items; technical reference note                                       |
| colors.light.secondary          | #386663           | "Maybe later" text button label                                                        |
| typography.headline_medium      | Outfit 28sp / 400 | "Access wasn't granted" title                                                          |
| typography.title_small          | Outfit 14sp / 500 | "This can happen if:" heading inside the reasons card                                  |
| typography.body_medium          | Outfit 14sp / 400 | Subtitle; reason item text                                                             |
| typography.body_small           | Outfit 12sp / 400 | Technical reference note (`declined_status_note`)                                      |
| typography.label_large          | Outfit 14sp / 500 | "Try again" and "Maybe later" button labels                                            |
| radius.lg                       | 16dp              | Reasons card corner radius                                                             |
| radius.sm                       | 8dp               | "Try again" button corner radius                                                       |

---

_Generated by /idea export | 2026-06-15_
