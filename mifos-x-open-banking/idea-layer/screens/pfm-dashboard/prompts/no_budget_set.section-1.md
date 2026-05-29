# pfm-dashboard — no_budget_set state — section 1/2

> Composition fragment. Compose into the parent (no_budget_set.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
1. **text** (#pfm_title) — label: "Spending Insights", content: "Spending Insights"
2. **stack** (#period_selector_row) — label: "Period selector row"
3. **chip** (#period_chip_this_month) — label: "This Month", content: "This Month"
4. **chip** (#period_chip_last_month) — label: "Last Month", content: "Last Month"
5. **chip** (#period_chip_last_3_months) — label: "Last 3 Months", content: "Last 3 Months"
6. **chip** (#period_chip_custom) — label: "Custom", content: "Custom"
7. **text** (#pfm_period_label) — label: "May 2026", content: "May 2026"
8. **box** (#this_month_summary_card) — label: "This Month summary", content: "This Month summary"
9. **text** (#summary_section_label) — label: "This Month", content: "This Month"
10. **stack** (#summary_metrics_row) — label: "Summary metrics"
11. **stack** (#spent_col) — label: "Total spent column"
12. **text** (#spent_label) — label: "Total Spent", content: "Total Spent"
13. **text** (#spent_amount) — label: "£1,029.80", content: "£1,029.80"
14. **stack** (#received_col) — label: "Total received column"
15. **text** (#received_label) — label: "Total Received", content: "Total Received"
16. **text** (#received_amount) — label: "£3,200.00", content: "£3,200.00"
17. **stack** (#net_col) — label: "Net balance column"
18. **text** (#net_label) — label: "Net", content: "Net"
19. **text** (#net_amount) — label: "+£2,170.20", content: "+£2,170.20"
20. **box** (#overall_budget_card) — label: "Overall budget card", content: "Overall budget card"
21. **stack** (#overall_budget_header_row) — label: "Overall budget header"
22. **text** (#overall_budget_title) — label: "Monthly Budget", content: "Monthly Budget"
23. **text** (#overall_budget_percent) — label: "68% used", content: "68% used"
24. **stack** (#overall_budget_amounts_row) — label: "Overall budget amounts"
25. **text** (#overall_budget_spent) — label: "£1,029.80 spent", content: "£1,029.80 spent"
26. **text** (#overall_budget_remaining) — label: "£470.20 left", content: "£470.20 left"
27. **box** (#overall_budget_progress_track) — label: "Overall budget progress track"
28. **box** (#overall_budget_progress_fill) — label: "Overall budget progress fill"
29. **text** (#overall_budget_of_total) — label: "of £1,500.00 monthly budget", content: "of £1,500.00 monthly budget"
30. **text** (#category_section_label) — label: "Spending by Category", content: "Spending by Category"
31. **box** (#category_pie_chart) — label: "Spending category pie chart", content: "Spending category pie chart"
32. **stack** (#category_legend_col) — label: "Category legend"
33. **stack** (#category_row_food) — label: "Food and Dining category row"
34. **box** (#category_dot_food)
35. **text** (#category_name_food) — label: "Food & Dining", content: "Food & Dining"
36. **text** (#category_amount_food) — label: "£320.50", content: "£320.50"
37. **stack** (#category_row_transport) — label: "Transport category row"
38. **box** (#category_dot_transport)
39. **text** (#category_name_transport) — label: "Transport", content: "Transport"
40. **text** (#category_amount_transport) — label: "£125.00", content: "£125.00"
41. **stack** (#category_row_shopping) — label: "Shopping category row"
42. **box** (#category_dot_shopping)
43. **text** (#category_name_shopping) — label: "Shopping", content: "Shopping"
44. **text** (#category_amount_shopping) — label: "£89.30", content: "£89.30"
45. **stack** (#category_row_bills) — label: "Bills category row"
46. **box** (#category_dot_bills)
47. **text** (#category_name_bills) — label: "Bills", content: "Bills"
48. **text** (#category_amount_bills) — label: "£450.00", content: "£450.00"
49. **stack** (#category_row_entertainment) — label: "Entertainment category row"
50. **box** (#category_dot_entertainment)
51. **text** (#category_name_entertainment) — label: "Entertainment", content: "Entertainment"
52. **text** (#category_amount_entertainment) — label: "£45.00", content: "£45.00"
53. **text** (#budgets_section_label) — label: "Budget Progress", content: "Budget Progress"
54. **box** (#budget_food_dining) — label: "Food and Dining budget", content: "Food and Dining budget"
55. **stack** (#food_dining_header) — label: "Food and Dining header"
56. **text** (#food_dining_category) — label: "Food & Dining", content: "Food & Dining"
57. **text** (#food_dining_amounts) — label: "£320.50 / £350.00", content: "£320.50 / £350.00"
58. **box** (#food_dining_progress_track) — label: "Food and Dining progress track"
59. **box** (#food_dining_progress_fill) — label: "Food and Dining progress fill"
60. **box** (#budget_transport) — label: "Transport budget", content: "Transport budget"
61. **stack** (#transport_header) — label: "Transport header"
62. **text** (#transport_category) — label: "Transport", content: "Transport"
63. **text** (#transport_amounts) — label: "£125.00 / £200.00", content: "£125.00 / £200.00"
64. **box** (#transport_progress_track) — label: "Transport progress track"
65. **box** (#transport_progress_fill) — label: "Transport progress fill"
66. **box** (#budget_shopping) — label: "Shopping budget", content: "Shopping budget"
67. **stack** (#shopping_header) — label: "Shopping header"
68. **text** (#shopping_category) — label: "Shopping", content: "Shopping"
69. **text** (#shopping_amounts) — label: "£89.30 / £150.00", content: "£89.30 / £150.00"
70. **box** (#shopping_progress_track) — label: "Shopping progress track"
71. **box** (#shopping_progress_fill) — label: "Shopping progress fill"
72. **box** (#budget_bills) — label: "Bills budget", content: "Bills budget"
73. **stack** (#bills_header) — label: "Bills header"
74. **text** (#bills_category) — label: "Bills", content: "Bills"
75. **text** (#bills_amounts) — label: "£450.00 / £500.00", content: "£450.00 / £500.00"
76. **box** (#bills_progress_track) — label: "Bills progress track"
77. **box** (#bills_progress_fill) — label: "Bills progress fill"
78. **box** (#budget_entertainment) — label: "Entertainment budget", content: "Entertainment budget"
79. **stack** (#entertainment_header) — label: "Entertainment header"
80. **text** (#entertainment_category) — label: "Entertainment", content: "Entertainment"
81. **text** (#entertainment_amounts) — label: "£45.00 / £100.00", content: "£45.00 / £100.00"
82. **box** (#entertainment_progress_track) — label: "Entertainment progress track"
83. **box** (#entertainment_progress_fill) — label: "Entertainment progress fill"
84. **button** (#manage_budgets_button) — label: "Manage Budgets"
85. **text** (#merchants_section_label) — label: "Top Merchants", content: "Top Merchants"
86. **box** (#merchants_card) — label: "Top merchants card", content: "Top merchants card"
87. **list_item** (#merchant_row_tesco) — label: "Tesco"
88. **text** (#merchant_name_tesco) — label: "Tesco", content: "Tesco"
89. **text** (#merchant_meta_tesco) — label: "8 transactions", content: "8 transactions"
90. **text** (#merchant_amount_tesco) — label: "£142.30", content: "£142.30"
91. **list_item** (#merchant_row_netflix) — label: "Netflix"
92. **text** (#merchant_name_netflix) — label: "Netflix", content: "Netflix"
93. **text** (#merchant_meta_netflix) — label: "1 transaction", content: "1 transaction"
94. **text** (#merchant_amount_netflix) — label: "£17.99", content: "£17.99"
95. **list_item** (#merchant_row_spotify) — label: "Spotify"

↓↓↓ MOCKUP PROMPT

Design the **no_budget_set** state of the Pfm Dashboard screen for **Mifos X Open Banking**, a open banking KMP super-app delivering consumer retail banking and field officer agent banking. Section 1 of 2.

Palette: background #12140E, surface #12140E, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, onPrimaryContainer #CDEDA3, secondary #A0CFCB, surfaceContainer #1E201A, surfaceContainerHigh #282A24, outline #8F9285, outlineVariant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 - Text Label** (full width minus 32dp insets): dashboard archetype. "Spending Insights" Outfit Medium 14sp #E3E3D8.

**Component 2 - Row Group** (full width minus 32dp insets): dashboard archetype. "Period selector row" Outfit Medium 14sp #E3E3D8.

**Component 3 - Filter Chip** (full width minus 32dp insets): dashboard archetype. "This Month" Outfit Medium 14sp #E3E3D8.

**Component 4 - Filter Chip** (full width minus 32dp insets): dashboard archetype. "Last Month" Outfit Medium 14sp #E3E3D8.

**Component 5 - Filter Chip** (full width minus 32dp insets): dashboard archetype. "Last 3 Months" Outfit Medium 14sp #E3E3D8.

**Component 6 - Filter Chip** (full width minus 32dp insets): dashboard archetype. "Custom" Outfit Medium 14sp #E3E3D8.

**Component 7 - Text Label** (full width minus 32dp insets): dashboard archetype. "May 2026" Outfit Medium 14sp #E3E3D8.

**Component 8 - Card** (full width minus 32dp insets): dashboard archetype. "This Month summary" Outfit Medium 14sp #E3E3D8.

**Component 9 - Text Label** (full width minus 32dp insets): dashboard archetype. "This Month" Outfit Medium 14sp #E3E3D8.

**Component 10 - Row Group** (full width minus 32dp insets): dashboard archetype. "Summary metrics" Outfit Medium 14sp #E3E3D8.

**Component 11 - Row Group** (full width minus 32dp insets): dashboard archetype. "Total spent column" Outfit Medium 14sp #E3E3D8.

**Component 12 - Text Label** (full width minus 32dp insets): dashboard archetype. "Total Spent" Outfit Medium 14sp #E3E3D8.

**Component 13 - Text Label** (full width minus 32dp insets): dashboard archetype. "£1,029.80" Outfit Medium 14sp #E3E3D8.

**Component 14 - Row Group** (full width minus 32dp insets): dashboard archetype. "Total received column" Outfit Medium 14sp #E3E3D8.

**Component 15 - Text Label** (full width minus 32dp insets): dashboard archetype. "Total Received" Outfit Medium 14sp #E3E3D8.

**Component 16 - Text Label** (full width minus 32dp insets): dashboard archetype. "£3,200.00" Outfit Medium 14sp #E3E3D8.

**Component 17 - Row Group** (full width minus 32dp insets): dashboard archetype. "Net balance column" Outfit Medium 14sp #E3E3D8.

**Component 18 - Text Label** (full width minus 32dp insets): dashboard archetype. "Net" Outfit Medium 14sp #E3E3D8.

**Component 19 - Text Label** (full width minus 32dp insets): dashboard archetype. "+£2,170.20" Outfit Medium 14sp #E3E3D8.

**Component 20 - Card** (full width minus 32dp insets): dashboard archetype. "Overall budget card" Outfit Medium 14sp #E3E3D8.

**Component 21 - Row Group** (full width minus 32dp insets): dashboard archetype. "Overall budget header" Outfit Medium 14sp #E3E3D8.

**Component 22 - Text Label** (full width minus 32dp insets): dashboard archetype. "Monthly Budget" Outfit Medium 14sp #E3E3D8.

**Component 23 - Text Label** (full width minus 32dp insets): dashboard archetype. "68% used" Outfit Medium 14sp #E3E3D8.

**Component 24 - Row Group** (full width minus 32dp insets): dashboard archetype. "Overall budget amounts" Outfit Medium 14sp #E3E3D8.

**Component 25 - Text Label** (full width minus 32dp insets): dashboard archetype. "£1,029.80 spent" Outfit Medium 14sp #E3E3D8.

**Component 26 - Text Label** (full width minus 32dp insets): dashboard archetype. "£470.20 left" Outfit Medium 14sp #E3E3D8.

**Component 27 - Card** (full width minus 32dp insets): dashboard archetype. "Overall budget progress track" Outfit Medium 14sp #E3E3D8.

**Component 28 - Card** (full width minus 32dp insets): dashboard archetype. "Overall budget progress fill" Outfit Medium 14sp #E3E3D8.

**Component 29 - Text Label** (full width minus 32dp insets): dashboard archetype. "of £1,500.00 monthly budget" Outfit Medium 14sp #E3E3D8.

**Component 30 - Text Label** (full width minus 32dp insets): dashboard archetype. "Spending by Category" Outfit Medium 14sp #E3E3D8.

**Component 31 - Card** (full width minus 32dp insets): dashboard archetype. "Spending category pie chart" Outfit Medium 14sp #E3E3D8.

**Component 32 - Row Group** (full width minus 32dp insets): dashboard archetype. "Category legend" Outfit Medium 14sp #E3E3D8.

**Component 33 - Row Group** (full width minus 32dp insets): dashboard archetype. "Food and Dining category row" Outfit Medium 14sp #E3E3D8.

**Component 34 - Card** (full width minus 32dp insets): dashboard archetype. "category dot food" Outfit Medium 14sp #E3E3D8.

**Component 35 - Text Label** (full width minus 32dp insets): dashboard archetype. "Food & Dining" Outfit Medium 14sp #E3E3D8.

**Component 36 - Text Label** (full width minus 32dp insets): dashboard archetype. "£320.50" Outfit Medium 14sp #E3E3D8.

**Component 37 - Row Group** (full width minus 32dp insets): dashboard archetype. "Transport category row" Outfit Medium 14sp #E3E3D8.

**Component 38 - Card** (full width minus 32dp insets): dashboard archetype. "category dot transport" Outfit Medium 14sp #E3E3D8.

**Component 39 - Text Label** (full width minus 32dp insets): dashboard archetype. "Transport" Outfit Medium 14sp #E3E3D8.

**Component 40 - Text Label** (full width minus 32dp insets): dashboard archetype. "£125.00" Outfit Medium 14sp #E3E3D8.

**Component 41 - Row Group** (full width minus 32dp insets): dashboard archetype. "Shopping category row" Outfit Medium 14sp #E3E3D8.

**Component 42 - Card** (full width minus 32dp insets): dashboard archetype. "category dot shopping" Outfit Medium 14sp #E3E3D8.

**Component 43 - Text Label** (full width minus 32dp insets): dashboard archetype. "Shopping" Outfit Medium 14sp #E3E3D8.

**Component 44 - Text Label** (full width minus 32dp insets): dashboard archetype. "£89.30" Outfit Medium 14sp #E3E3D8.

**Component 45 - Row Group** (full width minus 32dp insets): dashboard archetype. "Bills category row" Outfit Medium 14sp #E3E3D8.

**Component 46 - Card** (full width minus 32dp insets): dashboard archetype. "category dot bills" Outfit Medium 14sp #E3E3D8.

**Component 47 - Text Label** (full width minus 32dp insets): dashboard archetype. "Bills" Outfit Medium 14sp #E3E3D8.

**Component 48 - Text Label** (full width minus 32dp insets): dashboard archetype. "£450.00" Outfit Medium 14sp #E3E3D8.

**Component 49 - Row Group** (full width minus 32dp insets): dashboard archetype. "Entertainment category row" Outfit Medium 14sp #E3E3D8.

**Component 50 - Card** (full width minus 32dp insets): dashboard archetype. "category dot entertainment" Outfit Medium 14sp #E3E3D8.

**Component 51 - Text Label** (full width minus 32dp insets): dashboard archetype. "Entertainment" Outfit Medium 14sp #E3E3D8.

**Component 52 - Text Label** (full width minus 32dp insets): dashboard archetype. "£45.00" Outfit Medium 14sp #E3E3D8.

**Component 53 - Text Label** (full width minus 32dp insets): dashboard archetype. "Budget Progress" Outfit Medium 14sp #E3E3D8.

**Component 54 - Card** (full width minus 32dp insets): dashboard archetype. "Food and Dining budget" Outfit Medium 14sp #E3E3D8.

**Component 55 - Row Group** (full width minus 32dp insets): dashboard archetype. "Food and Dining header" Outfit Medium 14sp #E3E3D8.

**Component 56 - Text Label** (full width minus 32dp insets): dashboard archetype. "Food & Dining" Outfit Medium 14sp #E3E3D8.

**Component 57 - Text Label** (full width minus 32dp insets): dashboard archetype. "£320.50 / £350.00" Outfit Medium 14sp #E3E3D8.

**Component 58 - Card** (full width minus 32dp insets): dashboard archetype. "Food and Dining progress track" Outfit Medium 14sp #E3E3D8.

**Component 59 - Card** (full width minus 32dp insets): dashboard archetype. "Food and Dining progress fill" Outfit Medium 14sp #E3E3D8.

**Component 60 - Card** (full width minus 32dp insets): dashboard archetype. "Transport budget" Outfit Medium 14sp #E3E3D8.

**Component 61 - Row Group** (full width minus 32dp insets): dashboard archetype. "Transport header" Outfit Medium 14sp #E3E3D8.

**Component 62 - Text Label** (full width minus 32dp insets): dashboard archetype. "Transport" Outfit Medium 14sp #E3E3D8.

**Component 63 - Text Label** (full width minus 32dp insets): dashboard archetype. "£125.00 / £200.00" Outfit Medium 14sp #E3E3D8.

**Component 64 - Card** (full width minus 32dp insets): dashboard archetype. "Transport progress track" Outfit Medium 14sp #E3E3D8.

**Component 65 - Card** (full width minus 32dp insets): dashboard archetype. "Transport progress fill" Outfit Medium 14sp #E3E3D8.

**Component 66 - Card** (full width minus 32dp insets): dashboard archetype. "Shopping budget" Outfit Medium 14sp #E3E3D8.

**Component 67 - Row Group** (full width minus 32dp insets): dashboard archetype. "Shopping header" Outfit Medium 14sp #E3E3D8.

**Component 68 - Text Label** (full width minus 32dp insets): dashboard archetype. "Shopping" Outfit Medium 14sp #E3E3D8.

**Component 69 - Text Label** (full width minus 32dp insets): dashboard archetype. "£89.30 / £150.00" Outfit Medium 14sp #E3E3D8.

**Component 70 - Card** (full width minus 32dp insets): dashboard archetype. "Shopping progress track" Outfit Medium 14sp #E3E3D8.

**Component 71 - Card** (full width minus 32dp insets): dashboard archetype. "Shopping progress fill" Outfit Medium 14sp #E3E3D8.

**Component 72 - Card** (full width minus 32dp insets): dashboard archetype. "Bills budget" Outfit Medium 14sp #E3E3D8.

**Component 73 - Row Group** (full width minus 32dp insets): dashboard archetype. "Bills header" Outfit Medium 14sp #E3E3D8.

**Component 74 - Text Label** (full width minus 32dp insets): dashboard archetype. "Bills" Outfit Medium 14sp #E3E3D8.

**Component 75 - Text Label** (full width minus 32dp insets): dashboard archetype. "£450.00 / £500.00" Outfit Medium 14sp #E3E3D8.

**Component 76 - Card** (full width minus 32dp insets): dashboard archetype. "Bills progress track" Outfit Medium 14sp #E3E3D8.

**Component 77 - Card** (full width minus 32dp insets): dashboard archetype. "Bills progress fill" Outfit Medium 14sp #E3E3D8.

**Component 78 - Card** (full width minus 32dp insets): dashboard archetype. "Entertainment budget" Outfit Medium 14sp #E3E3D8.

**Component 79 - Row Group** (full width minus 32dp insets): dashboard archetype. "Entertainment header" Outfit Medium 14sp #E3E3D8.

**Component 80 - Text Label** (full width minus 32dp insets): dashboard archetype. "Entertainment" Outfit Medium 14sp #E3E3D8.

**Component 81 - Text Label** (full width minus 32dp insets): dashboard archetype. "£45.00 / £100.00" Outfit Medium 14sp #E3E3D8.

**Component 82 - Card** (full width minus 32dp insets): dashboard archetype. "Entertainment progress track" Outfit Medium 14sp #E3E3D8.

**Component 83 - Card** (full width minus 32dp insets): dashboard archetype. "Entertainment progress fill" Outfit Medium 14sp #E3E3D8.

**Component 84 - Button** (full width minus 32dp insets): dashboard archetype. "Manage Budgets" Outfit Medium 14sp #E3E3D8.

**Component 85 - Text Label** (full width minus 32dp insets): dashboard archetype. "Top Merchants" Outfit Medium 14sp #E3E3D8.

**Component 86 - Card** (full width minus 32dp insets): dashboard archetype. "Top merchants card" Outfit Medium 14sp #E3E3D8.

**Component 87 - List Item** (full width minus 32dp insets): dashboard archetype. "Tesco" Outfit Medium 14sp #E3E3D8.

**Component 88 - Text Label** (full width minus 32dp insets): dashboard archetype. "Tesco" Outfit Medium 14sp #E3E3D8.

**Component 89 - Text Label** (full width minus 32dp insets): dashboard archetype. "8 transactions" Outfit Medium 14sp #E3E3D8.

**Component 90 - Text Label** (full width minus 32dp insets): dashboard archetype. "£142.30" Outfit Medium 14sp #E3E3D8.

**Component 91 - List Item** (full width minus 32dp insets): dashboard archetype. "Netflix" Outfit Medium 14sp #E3E3D8.

**Component 92 - Text Label** (full width minus 32dp insets): dashboard archetype. "Netflix" Outfit Medium 14sp #E3E3D8.

**Component 93 - Text Label** (full width minus 32dp insets): dashboard archetype. "1 transaction" Outfit Medium 14sp #E3E3D8.

**Component 94 - Text Label** (full width minus 32dp insets): dashboard archetype. "£17.99" Outfit Medium 14sp #E3E3D8.

**Component 95 - List Item** (full width minus 32dp insets): dashboard archetype. "Spotify" Outfit Medium 14sp #E3E3D8.

DO NOT use em-dash anywhere in text. DO NOT make any headline more than 3 lines or any subtitle more than 25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green primary #B2D188 anchors budget indicators, chart accents, and CTA buttons, creating a balanced and premium feel calibrated to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
