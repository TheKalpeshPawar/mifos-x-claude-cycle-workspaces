# Mockup Specification: Field Officer Dashboard

| Field | Value |
|---|---|
| Feature | fo-dashboard |
| Flavor | fieldOfficer |
| Archetype | dashboard |

---

## Screen Layout

Top-to-bottom component hierarchy for the content state:

```
[ Status Bar ]
[ Greeting: "Good morning, Priya 👋" ]           ← headline_medium, #1800B1, pt:20 ph:16
[ Profile icon (top-right, absolute) ]            ← account_circle 32px #1800B1
[ Settings icon (top-right offset, absolute) ]    ← settings 24px #616161
[ Date/Branch: "Monday, 25 May 2026 · Mifos Nairobi Branch" ] ← body_medium #616161
──────────────────────────────────────────────────
[ STATS GRID (2-col, gap 12, ph:16) ]
  [ Active Customers       ] [ Pending Applications ]
    #EDE7FF, left accent #1800B1    #FFF8E1, accent #FF8F00
    "124" display_small #1800B1     "5" display_small #FF8F00
    "Active Customers"              "Pending Applications"
  [ KYC Pending           ] [ Meetings Today ]
    #FFEBEE, accent #FF5252         #E0F7FA, accent #008B8B
    "3" display_small #FF5252       "2" display_small #008B8B
    "KYC Pending"                   "Meetings Today"
──────────────────────────────────────────────────
[ "Action Needed" ] ← title_large bold #212121 ph:16
[ ALERT: KYC Expiry — John Mwangi ]
  bg:#FFF8E1, left-border:#FF8F00, row layout
  "John Mwangi — KYC expires in 3 days"  [Review KYC] outlined amber
[ ALERT: Long Pending — Sarah Odhiambo ]
  bg:#FFEBEE, left-border:#FF5252, row layout
  "Sarah Odhiambo — Application pending 7 days"  [View Application] outlined red
[ ALERT: New Lead — Peter Kamau ]
  bg:#E8F5E9, left-border:#4CAF50, row layout
  "New lead: Peter Kamau — Retail account request"  [Start Onboarding] outlined green
[ ACTION: Corporate — Acme Trading Ltd ]
  bg:#FFF8E1, "Acme Trading Ltd — New business account inquiry"
  [Start Corporate Onboarding] text teal
──────────────────────────────────────────────────
[ "Today's Schedule" ] ← title_medium bold #212121
[ Meeting Row: 10:00 AM | Mary Wanjiku · Loan Review ]
  bg:#FFFFFF, elevation:1, row, label_large #1800B1 | body_medium #424242
[ Meeting Row: 2:30 PM  | James Otieno · New Account Discussion ]
  bg:#FFFFFF, elevation:1, row, label_large #1800B1 | body_medium #424242
[ Bottom Nav Bar ]
```

---

## Components

### Greeting Text
- **Position:** Top of scroll content, padding_top:20 padding_horizontal:16
- **Style:** headline_medium, color #1800B1, font_weight 600
- **Content:** "Good morning, Priya 👋" — greeting prefix varies by time of day

### Stats Grid
- **Position:** Below date/branch context, full-width with padding_horizontal:16
- **Style:** 2-column grid, 12px gap, border_radius:12 cards with colored left accent border (4px)
- **Cards:** Each card has a tinted background, a display_small number in accent color, and a body_medium label in #424242
- **Tap behavior:** Every card navigates to its respective feature screen

### Action Alert Rows
- **Position:** Below "Action Needed" heading, margin_horizontal:16, margin_bottom:8 each
- **Style:** Horizontal row with colored left accent border (4px), 14px padding, border_radius:12
- **Content:** Text (`flex:1`) + outlined action button on the right
- **Button sizes:** label_small, padding_horizontal:12 padding_vertical:6, border_radius:8
- **Colors:** Amber (#FF8F00), Red (#FF5252), Green (#4CAF50) — background always tinted version of accent

### Meeting Rows
- **Position:** Below "Today's Schedule" heading, margin_horizontal:16
- **Style:** bg:#FFFFFF, border_radius:10, elevation:1, horizontal row, 14px padding
- **Content:** Time label (72px width, label_large #1800B1 bold) | Detail text (body_medium #424242, flex:1)

---

## Interaction Patterns

| Element | Tap Target | Result |
|---|---|---|
| stat_active_customers card | Full card (48px+ height) | Push navigate to /customer-search |
| stat_pending_applications card | Full card | Push navigate to /account-applications |
| stat_kyc_pending card | Full card | Push navigate to /kyc-review |
| stat_meetings_today card | Full card | Push navigate to /meetings |
| alert_kyc_review_button | "Review KYC" button | Push navigate to /kyc-review |
| alert_view_application_button | "View Application" button | Push navigate to /account-applications |
| alert_start_onboarding_button | "Start Onboarding" button | Push navigate to /customer-search |
| action_corporate_onboard | Full card | Push navigate to /corporate-onboarding |
| meeting_row_1 / meeting_row_2 | Full row | Push navigate to /meetings |
| top_bar_profile_icon | 32px icon touch target | Push navigate to /profile |
| top_bar_settings_icon | 24px icon touch target | Push navigate to /settings |

**Loading state:** stats_grid, action section, and schedule render skeleton shimmer; greeting and date remain solid.

---

## Content Data

| Element | Sample Value |
|---|---|
| Officer name | Priya |
| Branch | Mifos Nairobi Branch |
| Date | Monday, 25 May 2026 |
| Active customers | 124 |
| Pending applications | 5 |
| KYC pending | 3 |
| Meetings today | 2 |
| Alert 1 | John Mwangi — KYC expires in 3 days |
| Alert 2 | Sarah Odhiambo — Application pending 7 days |
| Alert 3 | New lead: Peter Kamau — Retail account request |
| Corporate lead | Acme Trading Ltd — New business account inquiry |
| Meeting 1 | 10:00 AM · Mary Wanjiku · Loan Review |
| Meeting 2 | 2:30 PM · James Otieno · New Account Discussion |

---

## Design Notes

**Color usage:** Brand purple #1800B1 anchors the greeting and all primary stat card accents. Semantic color coding used throughout — amber (#FF8F00) for warnings/pending, red (#FF5252) for urgent/KYC, green (#4CAF50) for opportunities, teal (#008B8B) for meetings. Background uses Material surface #FFFFFF for cards against #FCF8FF page background.

**Typography:** Greeting uses headline_medium (28sp); stat values use display_small (36sp) for visual hierarchy; section headers use title_large (22sp) and title_medium (16sp); alert text and row details use body_medium (14sp); action buttons use label_small (11sp).

**Spacing:** Consistent 16px horizontal padding. Cards in grid use internal 16px padding. Alert rows use 14px internal padding with 8px bottom margin. Section headers use 8px top + 8px bottom padding.

**Accessibility:** All interactive elements have descriptive a11y labels. Stat cards include full context in label (e.g. "Active customers: 124. Tap to view customer list"). Alert roles set to `alert` for KYC and application urgency items. Meeting rows are `listitem`.

**Stat card left border:** 4px width colored border on left edge provides quick color-coded scanning for officers who check the dashboard frequently.

---
_Generated by /idea export | 2026-05-25_
