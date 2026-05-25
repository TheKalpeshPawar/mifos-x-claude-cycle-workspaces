# Visual Specification — Spending Insights (PFM Dashboard)

| Field | Value |
|---|---|
| Feature | pfm-dashboard |
| Flavor | consumer |
| Archetype | dashboard |

---

## Screen Layout

Top app bar: "Spending Insights" title, back arrow, tune (settings) icon. Bottom navigation: Home, Accounts, Insights (active), Cards, More. Main content — vertically scrollable column (background #FCF8FF):

1. **Page title** — "Spending Insights" headline_large, #1800B1, bold, padding horizontal 20, top 16
2. **Period label** — "May 2026" body_medium, #888888, padding horizontal 20, bottom 16
3. **Daily spending chart** — Rounded card (radius 20, background #F8F4FF, height 200, elevation 1, margin horizontal 20, bottom 20)
   - "Daily Spending — May" label_medium, #888888, centered, at bottom of card
4. **This Month summary card** — White card (radius 20, elevation 2, padding 20, margin horizontal 20, bottom 20, border #F0F0F0)
   - "This Month" heading title_medium semi-bold
   - Three-column metric row (Total Spent | Total Received | Net)
5. **"Budget Progress" section heading** — title_medium, semi-bold, #111111, padding horizontal 20
6. **Groceries budget card** — White card, radius 16, elevation 1, margin horizontal 20, bottom 10
7. **Transport budget card** — White card, radius 16, elevation 1
8. **Dining Out budget card** — White card, radius 16, elevation 1
9. **"Manage Budgets" button** — Outlined #1800B1, centered, radius 12, margin horizontal 20, bottom 24

---

## Components

### Daily Spending Chart Card
- **Position:** Top of content area, below period label
- **Style:** Background #F8F4FF (soft lavender), corner_radius 20, height 200dp, elevation 1, padding 16
- **Content:** Bar chart showing day-by-day spending for May 2026; peak spending day annotated (10 May)
- **Label:** "Daily Spending — May" centered label_medium #888888
- **Interaction:** Tap to expand full-screen chart view

### This Month Summary Card
- **Position:** Below chart card
- **Style:** White background, radius 20, elevation 2, padding 20, border #F0F0F0 1dp
- **"This Month" heading:** title_medium, semi-bold, #111111, padding bottom 16
- **Three-column layout (flex equal-width):**

  | Column | Label | Value | Color |
  |---|---|---|---|
  | Left | "Total Spent" label_small #888888 | "£1,843.60" title_large bold | #FF5252 (red) |
  | Center | "Total Received" label_small #888888 | "£3,200.00" title_large bold | #4CAF50 (green) |
  | Right | "Net" label_small #888888 | "+£1,356.40" title_large bold | #1800B1 (primary) |

### Budget Progress Cards

**Groceries — 78% (approaching)**
- Category: "Groceries" body_medium semi-bold #111111
- Amounts: "£312 / £400" body_medium #555555 (right-aligned)
- Progress track: #E0E0E0, height 8, full width, radius 4
- Progress fill: #FF9800 (orange — approaching limit), width 78%

**Transport — 45% (healthy)**
- Category: "Transport" body_medium semi-bold #111111
- Amounts: "£68 / £150" body_medium #555555
- Progress fill: #4CAF50 (green — well within budget), width 45%

**Dining Out — 97% (critical)**
- Category: "Dining Out" body_medium semi-bold #111111
- Amounts: "£195 / £200" body_medium **#FF5252** semi-bold (red — critical near-limit)
- Progress fill: #FF5252 (red — at limit), width 97%

### Manage Budgets Button
- **Style:** Outlined variant, #1800B1 border, #1800B1 text, corner_radius 12, padding horizontal 24 vertical 14, label_large
- **Position:** Centered (align_self center), margin horizontal 20, top 8, bottom 24

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| monthly_chart_placeholder | Tap | open_chart_detail action — full-screen chart expands |
| budget_groceries | Tap | edit_budget action — budget edit sheet opens for Groceries |
| budget_transport | Tap | edit_budget action — budget edit sheet opens for Transport |
| budget_dining | Tap | edit_budget action — budget edit sheet opens for Dining Out |
| manage_budgets_button | Tap | manage_budgets action — budget management bottom sheet |
| top app bar tune icon | Tap | open_pfm_settings action — PFM settings |
| top app bar back arrow | Tap | navigate_back to home |

---

## Content Data

| Metric | Value |
|---|---|
| Reporting period | May 2026 |
| Total spent | £1,843.60 |
| Total received | £3,200.00 |
| Net balance | +£1,356.40 |
| Groceries budget | £312 spent / £400 limit = 78% |
| Transport budget | £68 spent / £150 limit = 45% |
| Dining Out budget | £195 spent / £200 limit = 97% |

---

## Design Notes

**Color Usage:**
- Net amount uses primary #1800B1 — positive brand association with healthy finances
- Spent uses #FF5252 (error-adjacent red) — signals outflow without being alarming
- Received uses #4CAF50 (success green) — signals inflow positively
- Budget bars use a traffic-light semantic: green (healthy) → orange (approaching) → red (critical) based on percentage consumed

**Typography:**
- Summary metrics: title_large bold — largest text on screen after the heading, creates impact
- Metric labels: label_small with letter_spacing 0.4 — creates a deliberate uppercase-adjacent feel for sub-labels
- Budget category names: body_medium semi-bold — balanced weight within the card

**Chart Area:**
- The #F8F4FF lavender background deliberately separates the chart from the white summary card and page background, creating a distinct data-viz zone

**Accessibility:**
- Summary card has a single descriptive label for screen readers: "This month summary. Spent £1,843.60, received £3,200.00, net positive £1,356.40."
- Budget cards read out full context: "Groceries budget. Spent £312 of £400 budget. 78% used."
- Progress bars have role="progressbar" with value described in the card-level a11y label

*Generated by /idea export | 2026-05-25*
