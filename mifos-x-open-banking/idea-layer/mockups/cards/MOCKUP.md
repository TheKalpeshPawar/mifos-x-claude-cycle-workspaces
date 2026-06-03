# My Cards — Visual Specification

| Field     | Value          |
|-----------|----------------|
| Feature   | cards          |
| Flavor    | consumer       |
| Archetype | index_list     |
| ViewModel | CardsViewModel |
| States    | loading, content, empty, error |
| Updated   | 2026-06-02 — CardsViewModel + API bindings (obp_get_cards / obp_get_card_transactions) |

---

## Screen Layout

Top-to-bottom layout on a vertically scrolling list screen with bottom navigation:

```
[ Top App Bar: "My Cards"          🔔 ]  ← notifications_outlined action
──────────────────────────────────────
[ Headline: "My Cards"               ]  ← #1800B1, headline_large
═══════ CARD CAROUSEL (horiz scroll) ═══════
┌──────────────────────────────────────┐
│  Mifos Debit Visa              VISA  │  ← gradient #1800B1→#4B35E8, 320×200
│                                      │
│  ●●●● ●●●● ●●●● 4521                │  ← white monospace, letter-spacing 4
│  ALEX JOHNSON            [Active ✓] │  ← E0DDFF uppercase | green chip
└──────────────────────────────────────┘
┌──────────────────────────────────────┐
│  Mifos Business Mastercard    ◎◎    │  ← gradient #008B8B→#005F5F
│                                      │
│  ●●●● ●●●● ●●●● 7834                │  ← white monospace
│  ALEX JOHNSON          [Frozen ❄️]   │  ← grey chip
└──────────────────────────────────────┘
═════════════════════════════════════════
─── QUICK ACTIONS ROW (space_evenly) ────
[❄️ Freeze] [⚙️ Set Limit] [🔑 View PIN] [⚠️ Report Lost]
─────────────────────────────────────────
[ Card Transactions              →     ]  ← title_large, semibold
┌─────────────────────────────────────┐
│ Netflix           -£15.99  20May26  │
│ Tesco Express     -£34.56           │
│ Uber              -£12.40  18May26  │
│ Amazon.co.uk      -£67.99  17May26  │
│ Starbucks         -£5.85   17May26  │
└─────────────────────────────────────┘
[ + Order New Card  (outlined, full-w) ]
──────────────────────────────────────
[ Bottom Navigation Bar                ]
```

---

## Components

### cards_title
- Typography: `headline_large`, color `#1800B1`
- Padding bottom: 4dp
- First element after the top bar content area

### card_carousel (card_debit_visa)
- Container: horizontal stack, spacing 16dp, horizontally scrollable
- Each card: 320dp wide × 200dp tall, corner radius 20dp, elevation 8
- Debit Visa gradient: start `#1800B1`, end `#4B35E8`, diagonal direction
- Padding: 24dp all sides
- Card number `••••  ••••  ••••  4521`: `title_large`, white, monospace, letter-spacing 4
- Cardholder "ALEX JOHNSON": `body_large`, `#E0DDFF`, uppercase
- Active chip: background `#4CAF50`, corner radius 12dp, white text `label_small`
- Visa logo: 56×20dp, white tinted, bottom-right positioned

### card_business_mastercard
- Gradient: start `#008B8B`, end `#005F5F`, diagonal
- Same card dimensions as debit (320×200)
- Frozen chip: background `#9E9E9E`, white text
- Mastercard logo: 48×30dp (overlapping circles, no tint)

### quick_actions_row
- Horizontal stack with `space_evenly` distribution
- Each button: text variant, icon on top, label below (vertical orientation)
- Freeze/Set Limit/View PIN: icon + text both `#1800B1`
- Report Lost: icon `report_problem` + text both `#FF5252`
- Icon size: implied ~24dp, padding 8dp each button
- Typography: `label_small`

### Transaction rows (card_tx_netflix, etc.)
- Each row: white card, corner radius 12dp, elevation 1, border `#F0F0F0` 1dp
- Padding: 16dp horizontal, 14dp vertical
- Merchant name: `body_medium`, `#111111`
- Amount "-£X.XX": `body_large`, `#FF5252`, medium weight (debit color)
- Date: `body_small`, `#888888`
- Tapping navigates to transaction-detail

### order_new_card_button
- Variant: outlined, full-width
- Border + text: `#1800B1`
- Leading icon: `add_card`
- Typography: `label_large`, corner radius 12dp, padding vertical 14dp

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Swipe left/right in carousel | card_carousel | Scrolls to next card |
| Tap card visual | card_debit_visa / card_business_mastercard | Navigate to card-detail |
| Tap "Freeze" | freeze_unfreeze_action | Triggers freeze confirmation, then toggle |
| Tap "Set Limit" | set_limit_action | Opens spending limit bottom sheet |
| Tap "View PIN" | view_pin_action | Biometric prompt, reveals PIN overlay |
| Tap "Report Lost" | report_lost_action | Confirmation dialog, then card blocked |
| Tap transaction row | card_tx_* | Navigate to transaction-detail |
| Tap "Order New Card" | order_new_card_button | Opens card ordering flow |

---

## Content Data

| Element | Value |
|---|---|
| Card 1 | Mifos Debit Visa, •••• •••• •••• 4521, Alex Johnson, Active |
| Card 2 | Mifos Business Mastercard, •••• •••• •••• 7834, Alex Johnson, Frozen |
| Transaction 1 | Netflix, -£15.99, 20 May 2026 |
| Transaction 2 | Tesco Express, -£34.56 |
| Transaction 3 | Uber, -£12.40, 18 May 2026 |
| Transaction 4 | Amazon.co.uk, -£67.99, 17 May 2026 |
| Transaction 5 | Starbucks, -£5.85, 17 May 2026 |

---

## Design Notes

**Dual-card gradient contrast:** The first card (Visa, deep purple) and second card (Business Mastercard, teal) are deliberately distinct to make multi-card scanning effortless. Both share the same 20dp corner radius and card dimensions for visual harmony.

**Status chips on cards:** Active = green reinforces safety; Frozen = grey signals temporary pause without alarm. Both use `label_small` to avoid competing with card number legibility.

**Quick actions as text+icon vertical buttons:** Mirrors iOS Wallet / Monzo pattern. `space_evenly` ensures no crowding on 360dp minimum screen width.

**Transaction amounts in #FF5252:** Strong red signals money leaving the account — consistent with industry-standard debit color coding.

**Empty state:** `credit_card_off` icon + "No cards yet" + "Order your first Mifos card to start making payments" — actionable copy tied directly to the Order New Card button.

**Accessibility:** Card visuals carry full `content_description` including masked number, status, and action hint. Report Lost uses red for color, but also `report_problem` icon and descriptive a11y label as non-color signal.

*Generated by /idea export | 2026-05-25*
