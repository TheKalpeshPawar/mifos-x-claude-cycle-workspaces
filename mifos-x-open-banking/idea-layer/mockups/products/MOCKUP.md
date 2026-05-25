# Visual Specification — Products

| Field | Value |
|---|---|
| Feature | products |
| Flavor | consumer |
| Archetype | index_list |
| States | loading, populated, empty, error |

---

## Screen Layout (populated state)

Top app bar: title "Products", back arrow (left), search icon (right).
Bottom navigation: 5 items — Home | Accounts | **Products (active)** | Send | More.
Main content: vertically scrollable column, background #FCF8FF.

```
┌─────────────────────────────────┐
│ ← Products                   🔍 │  ← top app bar
├─────────────────────────────────┤
│                                 │
│  Products                       │  ← headline_large #1800B1 bold
│  Explore accounts, savings,     │
│  loans and cards tailored       │
│  for you.                       │  ← body_medium #555555
│                                 │
│  [All] [Savings] [Loans]        │
│        [Cards] [Mortgages]  →   │  ← horizontal scroll chip row
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Instant Access Savings  Savings│ ← product card 1
│ │ 4.5% AER                    │ │  ← display_small #1800B1 bold
│ │ Earn 4.5% AER on every...   │ │
│ │ [4.5% AER][Instant access]  │ │  ← feature badge chips
│ │ [No minimum deposit]        │ │
│ │               [Details][Apply Now]│
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Fixed Rate Bond 1yr   Savings│  ← product card 2
│ │ 5.1% AER                    │ │
│ │ Lock in a market-leading... │ │
│ │ [5.1% AER][12-month term]   │ │
│ │ [FSCS protected]            │ │
│ │               [Details][Apply Now]│
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Personal Loan           Loans│  ← product card 3
│ │ From 6.9% APR               │ │
│ │ Borrow from £1,000 to...    │ │
│ │ [From 6.9% APR][Up to £25k] │ │
│ │ [1–7 year terms]            │ │
│ │               [Details][Apply Now]│
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ Platinum Credit Card    Cards│  ← product card 4
│ │ 0% for 20 months            │ │
│ │ 0% interest on purchases... │ │
│ │ [0% for 20 months]          │ │
│ │ [No annual fee][Contactless]│ │
│ │               [Details][Apply Now]│
│ └─────────────────────────────┘ │
│                                 │
│ ┌─────────────────────────────┐ │
│ │ 🎁 Refer a friend — earn £50 │  ← promo banner #1800B1 bg
│ │ When your friend opens any  │ │
│ │ account before 30 June 2026 │ │
│ └─────────────────────────────┘ │
│                                 │
├─────────────────────────────────┤
│  🏠  💳  🏪  ↗  ⋯              │  ← bottom nav
└─────────────────────────────────┘
```

---

## Category Filter Chip Row

- **Layout:** Horizontally scrollable row, padding_horizontal 20, spacing 8 between chips
- **Chip style:** corner_radius 20, padding_horizontal 16, padding_vertical 8, label_medium
- **Active chip (All):** Filled #1800B1, white text
- **Inactive chips:** Outlined, border #CCCCCC, text #666666
- **Chips (L→R):** All | Savings | Loans | Cards | Mortgages

---

## Product Cards — Common Structure

All four cards share the same container style:

| Property | Value |
|---|---|
| background | #FFFFFF |
| corner_radius | 16 |
| elevation | 2 |
| padding_horizontal | 16 |
| padding_vertical | 16 |
| border | #F0F0F0, 1dp |
| margin_horizontal | 20 |
| margin_bottom | 12 |

**Internal layout (top to bottom):**

1. **Header row** (horizontal, space_between): product name (title_medium, #111111, semi-bold) + category badge chip (label_small, colour-coded)
2. **Rate badge** (display_small, #1800B1, bold) — prominent rate or offer
3. **Description** (body_medium, #555555) — 1–2 line sentence
4. **Feature badges row** (horizontal scroll, spacing 8) — 2–3 colour-coded chips
5. **Actions row** (right-aligned): "Details" (outlined #1800B1) + "Apply Now" (filled #1800B1, white text), both corner_radius 8

---

## Product Card Detail — Instant Access Savings

| Element | Content | Style |
|---|---|---|
| Name | Instant Access Savings | title_medium, #111111, semi-bold |
| Category badge | Savings | #E8F5E9 bg, #2E7D32 text |
| Rate | 4.5% AER | display_small, #1800B1, bold |
| Description | "Earn 4.5% AER on every pound you save. Withdraw at any time with no notice period or penalties." | body_medium, #555555 |
| Badge 1 | 4.5% AER | #E8F5E9 bg, #2E7D32 text |
| Badge 2 | Instant access | #E3F2FD bg, #1565C0 text |
| Badge 3 | No minimum deposit | #EDE7F6 bg, #4527A0 text |
| Button 1 | Details | outlined #1800B1 |
| Button 2 | Apply Now | filled #1800B1, white text |

---

## Product Card Detail — Fixed Rate Bond 1yr

| Element | Content | Style |
|---|---|---|
| Name | Fixed Rate Bond 1yr | title_medium, #111111, semi-bold |
| Category badge | Savings | #E8F5E9 bg, #2E7D32 text |
| Rate | 5.1% AER | display_small, #1800B1, bold |
| Description | "Lock in a market-leading 5.1% AER for 12 months. Minimum deposit £1,000. Interest paid at maturity." | body_medium, #555555 |
| Badge 1 | 5.1% AER | #E8F5E9 bg, #2E7D32 text |
| Badge 2 | 12-month term | #FFF3E0 bg, #E65100 text |
| Badge 3 | FSCS protected | #EDE7F6 bg, #4527A0 text |
| Button 1 | Details | outlined #1800B1 |
| Button 2 | Apply Now | filled #1800B1, white text |

---

## Product Card Detail — Personal Loan

| Element | Content | Style |
|---|---|---|
| Name | Personal Loan | title_medium, #111111, semi-bold |
| Category badge | Loans | #FFF3E0 bg, #E65100 text |
| Rate | From 6.9% APR | display_small, #1800B1, bold |
| Description | "Borrow from £1,000 to £25,000 at a representative 6.9% APR. Flexible repayment terms from 1 to 7 years." | body_medium, #555555 |
| Badge 1 | From 6.9% APR | #FFF3E0 bg, #E65100 text |
| Badge 2 | Up to £25,000 | #EDE7F6 bg, #4527A0 text |
| Badge 3 | 1–7 year terms | #E3F2FD bg, #1565C0 text |
| Button 1 | Details | outlined #1800B1 |
| Button 2 | Apply Now | filled #1800B1, white text |

---

## Product Card Detail — Platinum Credit Card

| Element | Content | Style |
|---|---|---|
| Name | Platinum Credit Card | title_medium, #111111, semi-bold |
| Category badge | Cards | #E3F2FD bg, #1565C0 text |
| Rate | 0% for 20 months | display_small, #1800B1, bold |
| Description | "0% interest on purchases for 20 months. No annual fee. Contactless and Apple Pay / Google Pay enabled." | body_medium, #555555 |
| Badge 1 | 0% for 20 months | #E3F2FD bg, #1565C0 text |
| Badge 2 | No annual fee | #E8F5E9 bg, #2E7D32 text |
| Badge 3 | Contactless & Apple/Google Pay | #EDE7F6 bg, #4527A0 text |
| Button 1 | Details | outlined #1800B1 |
| Button 2 | Apply Now | filled #1800B1, white text |

---

## Promotional Banner

```
┌─────────────────────────────────────┐
│  🎁  Refer a friend — earn £50      │  ← title_small, #FFFFFF, semi-bold
│     When your friend opens any      │  ← body_small, #C5C0FF
│     account before 30 June 2026     │
└─────────────────────────────────────┘
```

| Property | Value |
|---|---|
| Background | #1800B1 |
| corner_radius | 12 |
| padding_horizontal | 16 |
| padding_vertical | 14 |
| margin_horizontal | 20 |
| margin_bottom | 16 |
| on_click | navigates to home (referral flow) |

---

## State — Loading

```
┌─────────────────────────────────┐
│  Products                       │
│  Explore accounts, savings...   │
│  [All] [Savings] [Loans] [Cards][Mortgages]→
│                                 │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 1
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 2
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 3
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 4
└─────────────────────────────────┘
```

- Title, subtitle, and all 5 category tabs visible
- 4 skeleton placeholders matching the card shape (shimmer animation)
- Promotional banner not shown

---

## State — Empty

```
┌─────────────────────────────────┐
│  Products                       │
│  Explore accounts, savings...   │
│  [All] [Savings] [Loans] [Cards][Mortgages]→
│                                 │
│           🏪                    │  ← store_outlined icon, large
│    No products available        │  ← title_medium
│  No products match the selected │
│  category. Try a different      │
│  filter or check back later.    │  ← body_medium #555555
└─────────────────────────────────┘
```

- Triggered when category filter returns zero matching products
- Empty-state icon: `store_outlined`
- Title: "No products available"
- Message: "No products match the selected category. Try a different filter or check back later."

---

## State — Error

```
┌─────────────────────────────────┐
│  Products                       │
│  Explore accounts, savings...   │
│  [All] [Savings] [Loans] [Cards][Mortgages]→
│                                 │
│           ☁️✗                   │  ← cloud_off icon, large
│  Unable to load products        │  ← title_medium
│  Check your connection and try  │
│  again. Your saved favourites   │
│  are still available offline.   │  ← body_medium #555555
│                                 │
│            [ Try Again ]        │  ← filled #1800B1 retry button
└─────────────────────────────────┘
```

- Error icon: `cloud_off`
- Title: "Unable to load products"
- Message: "Check your connection and try again. Your saved favourites are still available offline."
- Retry button: filled #1800B1, dispatches `RetryLoad` event

---

## Interaction Patterns

| Component | Gesture | Result |
|---|---|---|
| tab_all / tab_savings / tab_loans / tab_cards / tab_mortgages | Tap | `filter_products` action — active chip updates; product list filters client-side |
| Product card body (any) | Tap | `navigate` → application-detail with product code |
| ias_learn_more / frb_learn_more / personal_loan_learn_more / pcc_learn_more | Tap | `navigate` → application-detail (Details view) |
| ias_apply / frb_apply / personal_loan_apply / pcc_apply | Tap | `navigate` → application-detail (Apply Now entry) |
| promotions_banner | Tap | `navigate` → home (referral flow) |
| top app bar search icon | Tap | `search_products` — search overlay activates |
| top app bar back arrow | Tap | `navigate_back` → home |
| bottom nav — Home | Tap | replace → home |
| bottom nav — Accounts | Tap | replace → accounts |
| bottom nav — Send | Tap | replace → send-money |
| Retry button (error state) | Tap | `RetryLoad` event → re-fetches OBP products endpoint |

---

## Design Notes

**Rate Badge Hierarchy:**
The `display_small` rate figure is the primary visual anchor on each card. Its #1800B1 colour ties every product back to the brand, while the large size creates an instant value-scanning affordance for the user comparing rates.

**Category Colour System:**
Feature badges use a consistent semantic colour palette across all screens:
- Green (#E8F5E9 / #2E7D32) — financial gain / positive rates
- Blue (#E3F2FD / #1565C0) — access and convenience
- Orange (#FFF3E0 / #E65100) — borrowing rates and time constraints
- Purple (#EDE7F6 / #4527A0) — protection, eligibility, and amounts

**Category Badge Colour matches Feature Badge Colour:**
Each product's category badge uses the same semantic colour as the primary feature badge of that category (Savings→green, Loans→orange, Cards→blue), creating a consistent visual language.

**Promotional Banner Placement:**
Placed below all product cards so it does not interrupt the primary browsing flow but is still encountered before the user reaches the bottom of the list. The #C5C0FF secondary text provides enough contrast on the #1800B1 background while feeling softer than pure white.

**Accessibility:**
- Each product card has a full accessibility label: name + rate + primary benefit + action hint
- Category tabs declare `role: tab` and `selected` state for screen readers
- Apply Now and Details buttons have distinct `content_description` per product
- Error and empty states are announced as live regions

---

*Generated by /idea export | 2026-05-25*
