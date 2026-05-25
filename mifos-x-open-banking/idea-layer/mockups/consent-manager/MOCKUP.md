# Mockup — Connected Apps (Consent Manager)

| Field | Value |
|---|---|
| Feature | consent-manager |
| Flavor | consumer |
| Archetype | index_list |
| States | populated, revoke_confirm, empty, error |

---

## State: populated — Three Connected Apps

```
┌──────────────────────────────────────────────┐
│ ←  Connected Apps                        ⓘ  │  ← Top App Bar, #1800B1 nav+action icons
├──────────────────────────────────────────────┤
│                                              │
│  Connected Apps                              │  ← headline_large, #1800B1, bold, px 20
│  Manage third-party apps that have           │  ← body_medium, #666666, px 20
│  access to your account data                 │
│                                              │
│ ┌──────────────────────────────────────────┐ │  ← consent_moneymanager card
│ │ [MM]  MoneyManager Pro          [ACTIVE] │ │    #FFFFFF bg, radius 16, elevation 2
│ │       Granted 1 Mar 2026 ·               │ │    [MM]: 40×40, #E3F2FD bg, radius 10
│ │       Expires 1 Mar 2027                 │ │    [ACTIVE]: #E8F5E9 bg, #2E7D32 text
│ │                                          │ │
│ │  [Read Accounts][View Transactions]      │ │  ← scope chips: #EDE7F6 bg, #4527A0 text
│ │  [Check Balances]                        │ │    radius 8, label_small
│ │                                          │ │
│ │                       [Revoke Access ↗]  │ │  ← outlined, #FF5252, radius 10, align_end
│ └──────────────────────────────────────────┘ │
│                                              │
│ ┌──────────────────────────────────────────┐ │  ← consent_taxhelper card
│ │ [TH]  TaxHelper                 [ACTIVE] │ │    #FFFFFF bg, radius 16, elevation 2
│ │       Granted 15 Jan 2026 ·              │ │    [TH]: 40×40, #FFF3E0 bg, radius 10
│ │       Expires 15 Jan 2027                │ │    [ACTIVE]: #E8F5E9 bg, #2E7D32 text
│ │                                          │ │
│ │  [View Transactions][Read Accounts]      │ │  ← scope chips: #EDE7F6 bg, #4527A0 text
│ │                                          │ │
│ │                       [Revoke Access ↗]  │ │  ← outlined, #FF5252, radius 10, align_end
│ └──────────────────────────────────────────┘ │
│                                              │
│ ┌──────────────────────────────────────────┐ │  ← consent_budgetwise card (dimmed)
│ │ [BW]  BudgetWise               [EXPIRED] │ │    #FAFAFA bg, radius 16, elevation 1
│ │       Granted 10 Oct 2025 ·              │ │    [BW]: 40×40, #E8F5E9 bg, radius 10
│ │       Expired 10 Apr 2026                │ │    [EXPIRED]: #FFF3E0 bg, #E65100 text
│ │                                          │ │    name text: #888888 (greyed)
│ │  [Check Balances]                        │ │  ← scope chip: #F0F0F0 bg, #9E9E9E text
│ │                                          │ │
│ │                              [Remove]    │ │  ← text variant, #9E9E9E, align_end
│ └──────────────────────────────────────────┘ │
│                                              │
└──────────────────────────────────────────────┘
```

**Layout notes:**
- Cards: mx 20, mb 12 between cards.
- Active cards: #FFFFFF bg, elevation 2, 1dp border #F0F0F0.
- Expired card: #FAFAFA bg, elevation 1, 1dp border #EEEEEE.
- Scope chip row overflows horizontally with scroll on narrow viewports.

---

## State: revoke_confirm — Revoke Confirmation Dialog Overlay

```
┌──────────────────────────────────────────────┐
│ ←  Connected Apps                        ⓘ  │
├──────────────────────────────────────────────┤
│ ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ │
│ ▒  Connected Apps                         ▒ │  ← background list still visible,
│ ▒  Manage third-party apps...             ▒ │    dimmed under scrim #80000000
│ ▒                                         ▒ │
│ ▒ ┌── MoneyManager Pro card (dimmed) ───┐ ▒ │
│ ▒ │  [MM]  MoneyManager Pro  [ACTIVE]  │ ▒ │
│ ▒ │        Granted 1 Mar 2026...       │ ▒ │
│ ▒ └────────────────────────────────────┘ ▒ │
│ ▒                                         ▒ │
│ ▒     ┌──────────────────────────────┐    ▒ │
│ ▒     │                              │    ▒ │  ← revoke_confirm_dialog
│ ▒     │  Revoke access?              │    ▒ │    #FFFFFF bg, radius 24, elevation 8
│ ▒     │                              │    ▒ │    px 24, py 28, mx 32
│ ▒     │  This will immediately       │    ▒ │
│ ▒     │  remove this app's access    │    ▒ │
│ ▒     │  to your account data. You   │    ▒ │
│ ▒     │  can reconnect it at any     │    ▒ │
│ ▒     │  time.                       │    ▒ │
│ ▒     │                              │    ▒ │
│ ▒     │          [Cancel]  [Revoke]  │    ▒ │  ← Cancel: text, #1800B1
│ ▒     │                              │    ▒ │    Revoke: filled, #FF5252 bg, #FFF text
│ ▒     └──────────────────────────────┘    ▒ │
│ ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ │
└──────────────────────────────────────────────┘
```

**Interaction notes:**
- Scrim: #80000000 (50% black) over full screen behind dialog.
- "Cancel" fires `dismiss_revoke_dialog` → list returns to `populated`.
- "Revoke" fires `confirm_revoke_consent` → DELETE API call → removes card from list.
- Back gesture = Cancel behaviour.

---

## State: empty — No Connected Apps

```
┌──────────────────────────────────────────────┐
│ ←  Connected Apps                        ⓘ  │
├──────────────────────────────────────────────┤
│                                              │
│  Connected Apps                              │  ← headline_large, #1800B1
│  Manage third-party apps that have           │  ← body_medium, #666666
│  access to your account data                 │
│                                              │
│                                              │
│                                              │
│                  [🔗✕]                       │  ← ic_link_off, 80×80, #CCCCCC tint
│                                              │    (centered)
│            No apps connected                 │  ← title_medium, #444444, semibold
│                                              │
│   Third-party apps you authorise will        │  ← body_medium, #888888, center, px 32
│   appear here. Visit your bank's app         │
│   marketplace to connect apps.               │
│                                              │
│                                              │
└──────────────────────────────────────────────┘
```

**Notes:**
- Triggers when `GET /obp/v5.1.0/my/consents` returns an empty `consents` array.
- No action buttons — connecting new apps is handled externally via the bank's marketplace.
- Top app bar info action remains available (PSD2 info sheet).

---

## State: error — Load Failure

```
┌──────────────────────────────────────────────┐
│ ←  Connected Apps                        ⓘ  │
├──────────────────────────────────────────────┤
│                                              │
│  Connected Apps                              │  ← headline_large, #1800B1
│  Manage third-party apps that have           │  ← body_medium, #666666
│  access to your account data                 │
│                                              │
│                                              │
│                                              │
│                  [☁✕]                        │  ← cloud_off icon, centred, #CCCCCC
│                                              │
│       Unable to load connected apps          │  ← error_title, title_medium, #444444
│                                              │
│     Check your connection and try again      │  ← error_message, body_medium, #888888
│                                              │
│                  [ Try Again ]               │  ← filled button, #1800B1 bg, #FFF text
│                                              │
└──────────────────────────────────────────────┘
```

**Notes:**
- Triggers on network timeout or API error (401/403/5xx) from the GET consents call.
- "Try Again" fires `RetryLoad` event in `ConsentManagerViewModel`.
- Generic message is used — no API error codes surfaced to avoid leaking internals.

---

## Permission Badge Reference

| Badge Label | Background | Text Colour | Trigger |
|---|---|---|---|
| ACTIVE | #E8F5E9 | #2E7D32 | consent status = ACCEPTED |
| EXPIRED | #FFF3E0 | #E65100 | consent status = EXPIRED |
| REVOKED | #F5F5F5 | #9E9E9E | consent status = REVOKED |
| PENDING | #E3F2FD | #1565C0 | consent status = INITIATED |

## Scope Chip Reference

| Scope Label | Active (ACCEPTED) | Expired/Revoked |
|---|---|---|
| Read Accounts | #EDE7F6 bg / #4527A0 text | #F0F0F0 bg / #9E9E9E text |
| View Transactions | #EDE7F6 bg / #4527A0 text | #F0F0F0 bg / #9E9E9E text |
| Check Balances | #EDE7F6 bg / #4527A0 text | #F0F0F0 bg / #9E9E9E text |

---

## Design Notes

**Visual Differentiation — Active vs. Expired:**
- Active card: #FFFFFF bg, elevation 2, purple scope chips (#EDE7F6 / #4527A0), green ACTIVE badge — visually prominent.
- Expired card: #FAFAFA bg, elevation 1, grey scope chips (#F0F0F0 / #9E9E9E), orange EXPIRED badge — visually receded. Name text greyed to #888888.
- Differential treatment lets users scan instantly to identify live data-access risks.

**Revoke vs. Remove Actions:**
- "Revoke Access" uses #FF5252 red on an outlined button — a deliberate danger signal to prevent accidental taps.
- "Remove" for expired consents uses text variant with #9E9E9E — no danger signal because access is already gone; the action is housekeeping.

**Dialog UX:**
- The confirmation dialog requires an explicit "Revoke" tap. The destructive action is right-aligned per Material 3 convention. Cancel is always the safer default path.

**Accessibility:**
- Each consent card carries a full composite a11y label: app name + grant date + expiry + scopes + status.
- Revoke/Remove buttons describe their target: "Revoke MoneyManager Pro access to your account data."
- Status badges use `role: status` so screen readers announce state changes live.

---

*Generated by /idea export | 2026-05-25*
