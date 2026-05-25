# Visual Specification — Products

| Field | Value |
|---|---|
| Feature | products |
| Flavor | consumer |
| Archetype | index_list |

---

## Screen Layout

Top app bar with "Products" title, back arrow, and search icon. Bottom navigation bar with 5 items (Home, Accounts, Products active, Cards, More). Main content is a scrollable vertical column (background #FCF8FF):

1. **Page title** — "Products" headline_large, #1800B1, bold, padding horizontal 20, top 16
2. **Category tabs row** — Horizontal scrollable row of 5 pill buttons: All (filled #1800B1), Current / Savings / Loans / Cards (outlined, unselected), padding horizontal 20, bottom 16
3. **Product card — Current Plus Account** (margin horizontal 20, bottom 12)
4. **Product card — Flex Saver** (margin horizontal 20, bottom 12)
5. **Product card — Personal Loan** (margin horizontal 20, bottom 12)
6. **Bottom spacer** — 24dp

---

## Components

### Category Tabs Row
- **Style:** Horizontal scrollable; each tab is a pill button with corner_radius 20, padding horizontal 16 vertical 8
- **Active (All):** Filled #1800B1, white text, label_medium
- **Inactive:** Outlined #CCCCCC border, #666666 text
- **Tab items:** All | Current | Savings | Loans | Cards

### Product Card — Current Plus Account
- **Container:** White background, corner_radius 16, elevation 2, padding horizontal/vertical 16, border #F0F0F0 1dp
- **Name:** "Current Plus Account" — title_medium, #111111, semi-bold, bottom 4
- **Description:** "A flexible everyday current account with no monthly fee and free transfers across the UK." — body_medium, #555555, bottom 12
- **Feature badges (horizontal row):**
  - "No monthly fee" — #EDE7F6 background, #4527A0 text, radius 8, label_small
  - "Free UK transfers" — #E8F5E9 background, #2E7D32 text, radius 8, label_small
- **Actions (right-aligned row):**
  - "Learn More" — outlined #1800B1 border, #1800B1 text, radius 8, label_medium
  - "Apply" — filled #1800B1, white text, radius 8, label_medium

### Product Card — Flex Saver
- **Container:** Same card style as above
- **Name:** "Flex Saver" — title_medium, #111111, semi-bold
- **Description:** "Earn 4.5% AER on your savings with instant access. No minimum deposit required." — body_medium, #555555
- **Feature badges:**
  - "4.5% AER" — #E8F5E9 background, #2E7D32 text
  - "Instant access" — #E3F2FD background, #1565C0 text
- **Actions:** "Learn More" outlined + "Apply" filled (same as above)

### Product Card — Personal Loan
- **Container:** Same card style
- **Name:** "Personal Loan" — title_medium, #111111, semi-bold
- **Description:** "Borrow from £1,000 to £25,000 at a representative 6.9% APR over 1–7 years." — body_medium, #555555
- **Feature badges:**
  - "From 6.9% APR" — #FFF3E0 background, #E65100 text
  - "Up to £25,000" — #EDE7F6 background, #4527A0 text
- **Actions:** "Learn More" outlined + "Apply" filled

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| tab_all / tab_current / tab_savings / tab_loans / tab_cards | Tap | Category filter applied; visible cards update instantly (client-side filter) |
| product card body | Tap | expand_product_detail action — inline detail section expands below description |
| current_plus_learn_more / savings_flex_learn_more / personal_loan_learn_more | Tap | Product detail expands inline |
| current_plus_apply / savings_flex_apply / personal_loan_apply | Tap | Navigates to account-applications screen |
| top app bar search icon | Tap | search_products action — search mode activates |
| top app bar back arrow | Tap | Pops to home screen |

---

## Content Data

| Product | Name | Key Feature 1 | Key Feature 2 |
|---|---|---|---|
| Current account | Current Plus Account | No monthly fee | Free UK transfers |
| Savings account | Flex Saver | 4.5% AER | Instant access |
| Loan | Personal Loan | From 6.9% APR | Up to £25,000 |

**Current Plus Account description:** "A flexible everyday current account with no monthly fee and free transfers across the UK."

**Flex Saver description:** "Earn 4.5% AER on your savings with instant access. No minimum deposit required."

**Personal Loan description:** "Borrow from £1,000 to £25,000 at a representative 6.9% APR over 1–7 years."

---

## Design Notes

**Color Usage:**
- Primary #1800B1 is the dominant interactive colour: active tab, apply buttons, learn-more button borders, top-bar title
- Feature badges use a semantic colour system — purple for account features, green for financial gains, blue for access, orange for rates — creating immediate visual recognition of benefit type

**Typography:**
- Product names: title_medium semi-bold creates a clear card heading hierarchy
- Descriptions: body_medium #555555 — readable secondary text that doesn't compete with the headline
- Feature badges: label_small — small text with high colour contrast for quick scanning

**Card Layout:**
- All cards have consistent corner_radius 16 and elevation 2, providing a unified catalogue feel
- Internal padding of 16dp horizontal/vertical keeps content comfortable
- Feature badge rows use horizontal spacing of 8dp between badges

**Accessibility:**
- Each product card has a full accessibility label combining name, key features and action hint
- Category tabs use role="tab" with selected state declared for screen readers
- Apply and Learn More buttons have distinct content descriptions per product

*Generated by /idea export | 2026-05-25*
