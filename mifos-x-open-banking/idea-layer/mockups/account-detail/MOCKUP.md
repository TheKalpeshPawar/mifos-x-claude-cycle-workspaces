# Visual Specification — Account Detail
**Feature:** account-detail | **Flavor:** consumer

---

## Screen Layout

Full-screen vertical scroll with a top app bar ("Account Details" + back arrow) and persistent bottom navigation:

```
┌────────────────────────────────────┐
│ ← Account Details                  │  ← top app bar (#1800B1 bg)
├────────────────────────────────────┤
│  Primary Checking                  │
│  £4,250.00                         │  ← account_header_card (bg #1800B1)
│  [GBP] [CHECKING]                  │
├────────────────────────────────────┤
│ ┌──────────────────────────────┐   │
│ │ IBAN                    [⎘] │   │  ← account_info_card (elevation 3,
│ │ DE89 3704 0044 0532 0130 00  │   │    margin_top -16 overlapping hero)
│ │──────────────────────────────│   │
│ │ BIC / SWIFT             [⎘] │   │
│ │ COBADEFFXXX                  │   │
│ └──────────────────────────────┘   │
├────────────────────────────────────┤
│ [Send Money] [Request] [Statement] │  ← action_row
├────────────────────────────────────┤
│  Recent Transactions      View All │  ← transactions_header_row
│ ┌──────────────────────────────┐   │
│ │ 🛒 Tesco Supermarket          │   │
│ │    23 May 2026         -£42.50│   │  ← detail_txn_row_1
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ 💰 Salary Payment             │   │
│ │    22 May 2026      +£3,200.00│   │  ← detail_txn_row_2
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ ⚡ EDF Energy                 │   │
│ │    20 May 2026         -£94.20│   │  ← detail_txn_row_3
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ 📦 Amazon Prime               │   │
│ │    18 May 2026          -£8.99│   │  ← detail_txn_row_4
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ ☕ Costa Coffee               │   │
│ │    17 May 2026          -£3.75│   │  ← detail_txn_row_5
│ └──────────────────────────────┘   │
├────────────────────────────────────┤
│  [Home] [Accounts*] [Pay] [Cards] [More] │
└────────────────────────────────────┘
```

---

## Components

### account_header_card — Hero Section
- **Background:** #1800B1 (Mifos deep purple), full width, no border radius
- **Padding:** horizontal 24, top 20, bottom 32
- **account_header_label:** "Primary Checking" — label_large, color #FFFFFFB3 (70% white), padding_bottom 4
- **account_header_balance:** "£4,250.00" — display_large, #FFFFFF, font_weight 700, padding_bottom 4
- **Badges (horizontal stack, spacing 8):**
  - GBP badge: background #FFFFFF1A, border_radius 6, padding h/v 8/4, text label_small #FFFFFF
  - CHECKING badge: same pill style

### account_info_card — Routing Information
- **Position:** margin_top -16 (overlaps hero for visual continuity), margin_horizontal 20
- **Background:** #FFFFFF, border_radius 16, elevation 3, padding 20
- **IBAN row (space-between):**
  - Left col: "IBAN" label (label_small, #666666, letter_spacing 0.5) above "DE89 3704 0044 0532 0130 00" (body_medium, #1A1A1A, monospace)
  - Right: content_copy icon 22px, #1800B1 (tappable)
- **Divider:** #F0F0F0 horizontal rule, margin_bottom 16
- **BIC row:** same layout — "BIC / SWIFT" / "COBADEFFXXX" / copy icon

### action_row
- **Layout:** horizontal, spacing 10, padding_horizontal 20, padding_bottom 24
- **btn_send_money:** variant=tonal, bg #E8E4FF, text #1800B1, icon send, border_radius 12, flex 1
- **btn_request_payment:** variant=outlined, border #1800B1, text #1800B1, icon request_quote, flex 1
- **btn_download_statement:** variant=outlined, border #1800B1, text #1800B1, icon download, flex 1

### Transaction Rows (detail_txn_row_1..5)
- **Background:** #FFFFFF, border_radius 12, padding 16, margin_horizontal 20, elevation 1
- **Layout:** horizontal, align center, spacing 12
- **Icon avatars (44×44 circles):**
  - Tesco: shopping_basket icon on #FFEBEE, icon color #FF5252
  - Salary: payments icon on #E8F5E9, icon color #4CAF50
  - EDF: bolt icon on #FFF3E0, icon color #FF9800
  - Amazon: subscriptions icon on #EDE7F6, icon color #673AB7
  - Costa: local_cafe icon on #FBE9E7, icon color #BF360C
- **Center stack:** merchant name (body_medium, #1A1A1A) / date (body_small, #888888)
- **Right:** signed amount — debits: #FF5252; credits: #4CAF50; body_large, weight 600

---

## Interaction Patterns

| Target | Gesture | Outcome |
|---|---|---|
| Top app bar back arrow | Tap | Pop to accounts |
| copy_iban_button | Tap | Copies IBAN to clipboard; ibanCopied=true (brief toast) |
| copy_bic_button | Tap | Copies BIC to clipboard; bicCopied=true |
| btn_send_money | Tap | Navigate → send-money |
| btn_request_payment | Tap | Trigger payment request flow |
| btn_download_statement | Tap | Initiate PDF statement download; isDownloadingStatement=true |
| view_all_transactions_link | Tap | Navigate → transactions |
| Transaction rows | None (not tappable in this view) | — |

---

## Content Data

| Element | Value |
|---|---|
| Account name | Primary Checking |
| Balance | £4,250.00 |
| Currency | GBP |
| Account type | CHECKING |
| IBAN | DE89 3704 0044 0532 0130 00 |
| BIC/SWIFT | COBADEFFXXX |
| Txn 1 | Tesco Supermarket / 23 May 2026 / -£42.50 |
| Txn 2 | Salary Payment / 22 May 2026 / +£3,200.00 |
| Txn 3 | EDF Energy / 20 May 2026 / -£94.20 |
| Txn 4 | Amazon Prime / 18 May 2026 / -£8.99 |
| Txn 5 | Costa Coffee / 17 May 2026 / -£3.75 |

---

## Design Notes

- **Hero overlap:** The info card uses margin_top -16 to visually bridge the hero to the scrollable content — creates a floating card effect that is a Material Design 3 elevation pattern.
- **Color contrast:** White text on #1800B1 hero exceeds WCAG AA. Badge backgrounds (#FFFFFF1A = 10% white) provide subtle grouping without disrupting legibility.
- **Copy affordance:** content_copy icons in #1800B1 are intentionally larger (22px with 8px padding) to meet 44dp minimum tap target.
- **Transaction direction coding:** Debit amounts (#FF5252 red) vs credit amounts (#4CAF50 green) follow universal banking convention — no text prefix needed beyond +/- sign.
- **Skeleton loading:** Hero block remains full purple during load; info card and actions skeleton with #E0E0E0 grey blocks maintaining spatial layout.
- **Typography ladder:** display_large (balance) → title_large (section heading) → body_medium (routing values) → body_small (dates/secondary) — 4 distinct steps ensuring clear hierarchy.

---

_Generated by /idea export | 2026-05-25_
