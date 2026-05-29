# SPEC — Field Officer Dashboard

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | fo-dashboard             |
| Flavor        | fieldOfficer             |
| Status        | approved                 |
| Quality Score | 97                       |
| ViewModel     | FoDashboardViewModel     |

---

## Overview

The Field Officer Dashboard is the primary landing screen for Field Officer persona users after authentication. It shows a personalised greeting ("Good morning, Priya 👋"), today's date and branch context ("Monday, 25 May 2026 · Mifos Nairobi Branch"), and a 2-column KPI grid with four tappable stat cards: Active Customers (124, border #4C662B), Pending Applications (5, border #E8A317), KYC Pending (3, border #BA1A1A), and Meetings Today (2, border #386663, fill #DCE7C8). Each KPI card navigates to its operational screen. Below the grid an "Action Needed" section surfaces three urgency-coded alert rows — John Mwangi KYC expires in 3 days (#E8A317 border, "Review KYC" button), Sarah Odhiambo application pending 7 days (#BA1A1A border, "View Application" button), and a new lead for Peter Kamau — Retail account request (#4C662B border, "Start Onboarding" button) — followed by two corporate-level action cards: Acme Trading Ltd new business account inquiry (→ corporate-onboarding) and a Complete Agent Registration prompt (→ agent-registration). A "Today's Schedule" section lists two meetings: 10:00 AM Mary Wanjiku · Loan Review, and 2:30 PM James Otieno · New Account Discussion. Data is fetched from OBP Customers and Account-Applications endpoints on screen entry and on RetryLoadEvent. initial_state is loading; shimmer skeleton renders for all cards during load.

---

## Screens

| ID                | Name                    | Route         | Layout | Scroll   |
|-------------------|-------------------------|---------------|--------|----------|
| fo_dashboard_main | Field Officer Dashboard | /fo-dashboard | Column | Vertical |

**Shell:** fieldOfficer flavor bottom navigation bar (M3, 80dp height, #F9FAEF background, #C5C8BA border-top). Active indicator: #DCE7C8 pill.

**Top app bar (inline, not a separate component):** Profile icon (account_circle, 32dp, #4C662B, absolute top:20 right:16 → profile) + Settings icon (settings, 24dp, #44483D, absolute top:24 right:56 → settings).

---

## Components

| ID                                  | Type   | Description                                                                                                           |
|-------------------------------------|--------|-----------------------------------------------------------------------------------------------------------------------|
| greeting_text                       | text   | "Good morning, Priya 👋" — Outfit/headline_medium, #4C662B, 600 weight, 20dp top pad, 16dp horizontal pad           |
| top_bar_profile_icon                | icon   | account_circle, 32dp, #4C662B — navigates to profile                                                                 |
| top_bar_settings_icon               | icon   | settings, 24dp, #44483D — navigates to settings                                                                      |
| date_branch_context                 | text   | "Monday, 25 May 2026 · Mifos Nairobi Branch" — Outfit/body_medium, #44483D                                          |
| stats_grid                          | grid   | 2-column grid, 12dp gap, 16dp padding — contains 4 KPI stat cards                                                    |
| stat_active_customers               | box    | #CDEDA3 fill, 12dp radius, 4dp left border #4C662B — taps to customer-search                                         |
| stat_active_customers_value         | text   | "124" — Outfit/display_small, #4C662B, 700 weight                                                                    |
| stat_active_customers_label         | text   | "Active Customers" — Outfit/body_medium, #1A1C16, 500 weight                                                         |
| stat_pending_applications           | box    | #CDEDA3 fill, 12dp radius, 4dp left border #E8A317 — taps to account-applications                                    |
| stat_pending_applications_value     | text   | "5" — Outfit/display_small, #44483D, 700 weight (contrast-safe on #CDEDA3)                                           |
| stat_pending_applications_label     | text   | "Pending Applications" — Outfit/body_medium, #1A1C16, 500 weight                                                     |
| stat_kyc_pending                    | box    | #CDEDA3 fill, 12dp radius, 4dp left border #BA1A1A — taps to kyc-review                                              |
| stat_kyc_pending_value              | text   | "3" — Outfit/display_small, #BA1A1A, 700 weight                                                                      |
| stat_kyc_pending_label              | text   | "KYC Pending" — Outfit/body_medium, #1A1C16, 500 weight                                                              |
| stat_meetings_today                 | box    | #DCE7C8 fill, 12dp radius, 4dp left border #386663 — taps to meetings                                                |
| stat_meetings_today_value           | text   | "2" — Outfit/display_small, #386663, 700 weight                                                                      |
| stat_meetings_today_label           | text   | "Meetings Today" — Outfit/body_medium, #1A1C16, 500 weight                                                           |
| action_needed_header                | text   | "Action Needed" — Outfit/title_large, #1A1C16, 700 weight, heading level 2                                           |
| alert_kyc_expiry_john               | box    | #CDEDA3 fill, 12dp radius, 4dp left border #E8A317, row layout — taps to kyc-review                                  |
| alert_kyc_expiry_john_text          | text   | "John Mwangi — KYC expires in 3 days" — Outfit/body_medium, #1A1C16                                                  |
| alert_kyc_review_button             | button | "Review KYC" — outlined, #44483D border+text, 8dp radius, label_small (a11y-safe on #CDEDA3)                        |
| alert_application_pending_sarah     | box    | #CDEDA3 fill, 12dp radius, 4dp left border #BA1A1A, row layout — taps to account-applications                       |
| alert_application_pending_sarah_text| text   | "Sarah Odhiambo — Application pending 7 days" — Outfit/body_medium, #1A1C16                                         |
| alert_view_application_button       | button | "View Application" — outlined, #BA1A1A border+text, 8dp radius, label_small                                          |
| alert_new_lead_peter                | box    | #CDEDA3 fill, 12dp radius, 4dp left border #4C662B, row layout — taps to customer-search                            |
| alert_new_lead_peter_text           | text   | "New lead: Peter Kamau — Retail account request" — Outfit/body_medium, #1A1C16                                       |
| alert_start_onboarding_button       | button | "Start Onboarding" — outlined, #4C662B border+text, 8dp radius, label_small                                          |
| action_corporate_onboard            | box    | #CDEDA3 fill, 12dp radius, 16dp padding — taps to corporate-onboarding                                               |
| action_corporate_title              | text   | "Acme Trading Ltd — New business account inquiry" — Outfit/body_medium, #1A1C16                                      |
| action_corporate_btn                | button | "Start Corporate Onboarding" — text variant, #386663, label_medium                                                   |
| action_register_as_agent            | box    | #CDEDA3 fill, 12dp radius, row layout — taps to agent-registration                                                   |
| action_register_as_agent_title      | text   | "Complete Agent Registration" — Outfit/body_medium, #1A1C16                                                          |
| action_register_as_agent_btn        | button | "Register" — text variant, #386663, label_medium                                                                     |
| schedule_header                     | text   | "Today's Schedule" — Outfit/title_medium, #1A1C16, 600 weight, heading level 2                                       |
| meeting_row_1                       | box    | #FFFFFF fill, 10dp radius, 1dp elevation, row layout — taps to meetings                                              |
| meeting_1_time                      | text   | "10:00 AM" — Outfit/label_large, #4C662B, 600 weight, 72dp fixed width                                              |
| meeting_1_details                   | text   | "Mary Wanjiku · Loan Review" — Outfit/body_medium, #1A1C16                                                           |
| meeting_row_2                       | box    | #FFFFFF fill, 10dp radius, 1dp elevation, row layout — taps to meetings                                              |
| meeting_2_time                      | text   | "2:30 PM" — Outfit/label_large, #4C662B, 600 weight, 72dp fixed width                                               |
| meeting_2_details                   | text   | "James Otieno · New Account Discussion" — Outfit/body_medium, #1A1C16                                                |

---

## States

| ID      | Trigger                             | Description                                                                                                                                                                                                          |
|---------|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoadEvent       | Greeting + date/branch always visible. Stats grid, all 4 KPI cards, all action alerts (kyc/application/lead/corporate/agent), both meeting rows show skeleton (shimmer_duration: short4 = 200ms; reduced-motion fallback: static_placeholder). |
| content | Data load success                   | Full screen: greeting, date/branch, 2×2 KPI grid (124/5/3/2), action needed section (3 inline alerts + 2 action cards), today's schedule (2 meetings at 10:00 AM and 2:30 PM). |
| error   | Network or API failure on any fetch | Greeting + date/branch visible. Stats grid, action section, schedule section hidden. Banner: "Unable to load dashboard data. Check your connection and try again." Retry button (id: error_retry_button, label: "Try Again", action: retry_load). |
| empty   | All API responses return empty data | Greeting + date/branch visible. Stats/action/schedule sections hidden. Empty message: "No dashboard data available yet. Start by onboarding a customer." Icon: dashboard_customize. CTA: "Onboard a Customer" → customer-search. |

---

## State Model

**ViewModel:** `FoDashboardViewModel`

| Name                    | Type                  | Default              |
|-------------------------|-----------------------|----------------------|
| officerName             | String                | "Priya"              |
| branchName              | String                | "Mifos Nairobi Branch"|
| activeCustomerCount     | Int                   | 0                    |
| pendingApplicationCount | Int                   | 0                    |
| kycPendingCount         | Int                   | 0                    |
| meetingsTodayCount      | Int                   | 0                    |
| actionAlerts            | List\<ActionAlert\>   | emptyList()          |
| todayMeetings           | List\<Meeting\>       | emptyList()          |
| isLoading               | Boolean               | true                 |
| networkError            | String?               | null                 |

**Events:** `StatCardClickedEvent`, `AlertActionClickedEvent`, `MeetingClickedEvent`, `RetryLoadEvent`

**Actions:** `navigate`, `retry_load`

**DI Dependencies:** `CustomerRepository`, `AccountApplicationRepository`, `MeetingRepository`, `NavigationService`

**Errors:**
- `networkError`: "Unable to load dashboard data. Check your connection and try again."

---

## Navigation

| From         | To                   | Trigger                              | Type |
|--------------|----------------------|--------------------------------------|------|
| fo-dashboard | customer-search      | stat_active_customers tap            | push |
| fo-dashboard | account-applications | stat_pending_applications tap        | push |
| fo-dashboard | kyc-review           | stat_kyc_pending tap                 | push |
| fo-dashboard | meetings             | stat_meetings_today tap              | push |
| fo-dashboard | kyc-review           | alert_kyc_expiry_john tap            | push |
| fo-dashboard | kyc-review           | alert_kyc_review_button tap          | push |
| fo-dashboard | account-applications | alert_application_pending_sarah tap  | push |
| fo-dashboard | account-applications | alert_view_application_button tap    | push |
| fo-dashboard | customer-search      | alert_new_lead_peter tap             | push |
| fo-dashboard | customer-search      | alert_start_onboarding_button tap    | push |
| fo-dashboard | corporate-onboarding | action_corporate_onboard tap         | push |
| fo-dashboard | corporate-onboarding | action_corporate_btn tap             | push |
| fo-dashboard | agent-registration   | action_register_as_agent tap         | push |
| fo-dashboard | agent-registration   | action_register_as_agent_btn tap     | push |
| fo-dashboard | meetings             | meeting_row_1 tap                    | push |
| fo-dashboard | meetings             | meeting_row_2 tap                    | push |
| fo-dashboard | profile              | top_bar_profile_icon tap             | push |
| fo-dashboard | settings             | top_bar_settings_icon tap            | push |

---

## API Endpoints

| Endpoint                                               | Auth        | Tag                  | Purpose                                                                      |
|--------------------------------------------------------|-------------|----------------------|------------------------------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers               | DirectLogin | Customers            | Active customer count; KYC-pending count; expiring-soon filter; new-lead filter |
| GET /obp/v5.1.0/banks/{bankId}/account-applications    | DirectLogin | Account-Applications | Pending application count; days-pending filter; corporate inquiry filter     |

---

## Design Tokens

| Token                              | Value           | Usage                                                                                     |
|------------------------------------|-----------------|-------------------------------------------------------------------------------------------|
| colors.light.primary               | #4C662B         | Greeting text, active-customers KPI left border, new-lead alert border, meeting time labels, start-onboarding button border/text, profile icon |
| colors.light.primary_container     | #CDEDA3         | Active-customers, pending-applications, and KYC-pending KPI card fills; all three alert card fills; corporate + agent card fills |
| colors.light.nav_active_indicator  | #DCE7C8         | Meetings Today KPI card fill                                                              |
| colors.light.secondary             | #386663         | Meetings Today KPI left border, corporate-onboarding btn text, agent-register btn text    |
| colors.light.error                 | #BA1A1A         | KYC Pending KPI left border + value text; overdue application alert left border; "View Application" button border/text |
| colors.light.pending               | #E8A317         | Pending Applications KPI left border; KYC-expiry alert left border                       |
| colors.light.on_surface            | #1A1C16         | KPI label text, alert body text, schedule meeting details, section headers                |
| colors.light.on_surface_variant    | #44483D         | Date/branch context, settings icon; stat_pending_applications_value (a11y fix: 7.26:1 PASS on #CDEDA3); "Review KYC" button border/text |
| colors.light.surface               | #FFFFFF         | Meeting row card fills                                                                    |
| colors.light.background            | #F9FAEF         | Screen base                                                                               |
| typography.headline_medium         | Outfit 28sp/400 | Greeting text                                                                             |
| typography.display_small           | Outfit 32sp/600 | KPI stat values (124, 5, 3, 2)                                                            |
| typography.title_large             | Outfit 22sp/400 | "Action Needed" section header                                                            |
| typography.title_medium            | Outfit 16sp/500 | "Today's Schedule" section header                                                         |
| typography.body_medium             | Outfit 14sp/400 | Alert body text, meeting details, date/branch context, KPI labels                        |
| typography.label_large             | Outfit 14sp/500 | Meeting time labels (10:00 AM, 2:30 PM)                                                  |
| typography.label_medium            | Outfit 12sp/500 | Corporate "Start Corporate Onboarding" + "Register" button text                          |
| typography.label_small             | Outfit 11sp/500 | Alert action buttons ("Review KYC", "View Application", "Start Onboarding")              |
| radius.md                          | 12dp            | KPI stat cards, alert cards, corporate + agent action cards                               |
| radius.sm                          | 8dp             | Alert action buttons (border-radius)                                                      |
| elevation.level1                   | 1dp             | Meeting row cards                                                                         |
| spacing.md                         | 16dp            | Horizontal content padding throughout                                                     |
| spacing.sm                         | 8dp             | KPI grid gap, alert bottom margin                                                         |
| motion.duration.short4             | 200ms           | Skeleton shimmer cycle during loading state                                               |

---

_Generated by /idea export | 2026-05-30_
