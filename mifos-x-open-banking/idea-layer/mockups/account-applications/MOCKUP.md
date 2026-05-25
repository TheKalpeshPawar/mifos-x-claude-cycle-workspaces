# Visual Specification — Account Applications

| Field   | Value                         |
|---------|------------------------------|
| Feature | account-applications         |
| Flavor  | fieldOfficer                 |

---

## Screen Layout

Index-list dashboard with a large page title, horizontally scrollable filter chips, and a vertical scroll list of application cards. A floating action button is pinned to the bottom-right corner:

```
[ page_title — "Account Applications" headline in primary purple ]
[ status_filter_tabs — horizontal scrollable chips: All(8) Pending(3) Approved(3) Rejected(2) ]
[ --- vertically scrollable card list --- ]
  [ app_card_1 — John Mwangi / KCB Savings / Pending Review / Review button ]
  [ app_card_2 — Sarah Odhiambo / M-Shwari Checking / Approved ✓ ]
  [ app_card_3 — Peter Kamau / Business Current / Rejected ✗ / View Reason ]
  [ ... more cards ... ]
[ new_application_fab — extended FAB pinned bottom-right ]
```

---

## Components

### page_title

"Account Applications" in headline_large, color #1800B1, paddingHorizontal 16, paddingTop 20, paddingBottom 4. Role: heading level 1. Establishes screen identity immediately below the top app bar.

### status_filter_tabs

Horizontally scrollable row (paddingHorizontal 16, paddingVertical 10, gap 8). Contains 4 radio-style chips (borderRadius 20, paddingHorizontal 14, paddingVertical 6):

| Chip         | Selected bg | Selected text | Unselected bg | Label        |
|--------------|-------------|---------------|---------------|--------------|
| All          | #1800B1     | #FFFFFF       | #F0F0F0       | "All (8)"    |
| Pending      | #FF8F00     | #FFFFFF       | #F0F0F0       | "Pending (3)"|
| Approved     | #4CAF50     | #FFFFFF       | #F0F0F0       | "Approved (3)"|
| Rejected     | #FF5252     | #FFFFFF       | #F0F0F0       | "Rejected (2)"|

Each chip's selected background color matches the semantic status color, giving the filter bar a traffic-light pattern that previews what selecting it reveals.

### Application Cards (canonical: app_card_1)

White card (borderRadius 12, padding 14, marginHorizontal 16, marginBottom 10, elevation 2). Entire card is tappable (navigates to application-detail).

Internal layout:
```
[ header row: applicant name — status chip ]
[ product name (primary color) ]
[ footer row: submission date — Review/View Reason button ]
```

**Card 1 — John Mwangi (Pending):**
- Name: "John Mwangi" — title_medium, weight 700, #1A1A1A
- Status chip: bg #FFF8E1, border #FFB300, borderRadius 12, "Pending Review" in label_small, #E65100, weight 600
- Product: "KCB Savings Account" — body_medium, #1800B1
- Date: "Submitted: 20 May 2026" — body_small, #999999
- Review button: filled, bg #1800B1, white text, paddingHorizontal 16, paddingVertical 6, label_medium, borderRadius 8

**Card 2 — Sarah Odhiambo (Approved):**
- Name: "Sarah Odhiambo" — title_medium, weight 700, #1A1A1A
- Status chip: bg #E8F5E9, border #4CAF50, "Approved ✓" in label_small, #2E7D32, weight 600
- Product: "M-Shwari Checking Account" — body_medium, #1800B1
- Date: "Submitted: 18 May 2026" — body_small, #999999
- No action button (already resolved)

**Card 3 — Peter Kamau (Rejected):**
- Name: "Peter Kamau" — title_medium, weight 700, #1A1A1A
- Status chip: bg #FFEBEE, border #FF5252, "Rejected ✗" in label_small, #C62828, weight 600
- Product: "Business Current Account" — body_medium, #1800B1
- Date: "Submitted: 12 May 2026" — body_small, #999999
- "View Reason" link: label_medium, #FF5252, underlined

### new_application_fab

Extended FAB (shape: extended_fab) pinned at bottom-right (marginBottom 24, marginRight 16, elevation 6). Background #1800B1, icon add, label "New Application" in white. Tapping navigates to customer-onboarding.

---

## Interaction Patterns

- **Filter tap**: Tap any chip → highlight chip with its semantic color → filter card list to matching status → update count badges. Transition is instant (client-side filter, data already loaded).
- **Card tap**: Tap anywhere on a card (card has on_click navigate → application-detail) — navigates to full detail view
- **Review button**: Secondary tap target within pending cards — navigates to application-detail for action
- **View Reason link**: Red underlined link on rejected cards — navigates to application-detail showing rejection context
- **FAB tap**: Navigates to customer-onboarding wizard to start new individual application
- **Empty state**: When filtered list is empty — shows icon (assignment), "No Applications Found", subtitle "No account applications match the selected filter"; no card list

---

## Content Data

| Applicant       | Product                    | Status         | Submitted     |
|-----------------|----------------------------|----------------|---------------|
| John Mwangi     | KCB Savings Account        | Pending Review | 20 May 2026   |
| Sarah Odhiambo  | M-Shwari Checking Account  | Approved ✓     | 18 May 2026   |
| Peter Kamau     | Business Current Account   | Rejected ✗     | 12 May 2026   |
| Total count     | 8 applications             | 3 pending      | 3 approved / 2 rejected |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 for page title and product names makes the page branding clear and connects product labels visually
- Each filter chip uses the same color as its status chips in cards — the filter's selected color previews what you'll see
- Card elevation 2 creates subtle shadow separation against #F5F5F5 background
- FAB elevation 6 floats clearly above card content

**Typography:**
- headline_large for page title — the largest type in the app, signals primary navigation destination
- title_medium weight 700 for applicant names — bold for scannability in a long list
- body_medium #1800B1 for product names — small but in brand color, reinforces the banking product context
- body_small #999999 for dates — clearly secondary, doesn't compete with name/product

**Spacing:**
- Filter chips: gap 8, chip padding 14h×6v — comfortable tap targets without oversizing
- Cards: marginHorizontal 16, marginBottom 10, elevation 2 — standard Material card grid
- FAB: marginBottom 24, marginRight 16 — above system gesture area

**Accessibility:**
- Filter chips: role tablist / tab — screen readers announce "Show pending applications, 3 total"
- Each card: role button with contentDescription summarizing applicant + product + status
- FAB: "Start a new account application"
- Empty state: announces emptyTitle and emptySubtitle when filter yields zero results

*Generated by /idea export | 2026-05-25*
