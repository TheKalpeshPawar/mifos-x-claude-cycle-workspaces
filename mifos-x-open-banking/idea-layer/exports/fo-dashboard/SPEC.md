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

The Field Officer Dashboard is the primary landing screen for Field Officer persona users. It provides a personalized greeting ("Good morning, Priya"), today's date and branch context ("Monday, 25 May 2026 · Mifos Nairobi Branch"), a 2-column KPI stats grid (Active Customers: 124, Pending Applications: 5, KYC Pending: 3, Meetings Today: 2), an "Action Needed" section with urgency-coded alert rows for KYC expiry, overdue applications, new leads, corporate inquiries, and agent registration, followed by a "Today's Schedule" section with two time-slotted meetings. All data is fetched from OBP Customers and Account-Applications endpoints. The screen is responsive: single column on mobile, 2 columns on tablet (600dp+), 3 columns on desktop (840dp+).

---

## Screens

| ID               | Name                    | Route        | Layout  | Scroll   |
|------------------|-------------------------|--------------|---------|----------|
| fo_dashboard_main| Field Officer Dashboard | /fo-dashboard| Column  | Vertical |

**Shell:** fieldOfficer flavor bottom navigation bar (5 items — Dashboard active).

| Nav Item     | ID                   | Icon        | Target              | Badge |
|--------------|----------------------|-------------|---------------------|-------|
| Dashboard    | nav_dashboard        | dashboard   | fo-dashboard        | true  |
| Customers    | nav_customers        | people      | customer-search     | false |
| Applications | nav_applications     | description | account-applications| true  |
| Messages     | nav_messages         | mail        | customer-messages   | true  |
| More         | nav_more             | more_vert   | settings            | false |

**Top app bar:** Profile icon (account_circle, 32dp, #4C662B → profile) + Settings icon (settings, 24dp, #44483D → settings), positioned absolute top-right.

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

| ID      | Trigger                          | Description                                                                               |
|---------|----------------------------------|-------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoadEvent    | Greeting + date visible; stats grid, action cards, meeting rows all show skeleton shimmer |
| content | Data load success                | All KPI cards, action alerts, schedule rows fully populated with live data                |
| error   | Network or auth failure          | Greeting + date visible; stats/actions/schedule hidden; error message with retry          |
| empty   | No customers / data returned yet | Greeting + date + empty state card ("No dashboard data, start by onboarding a customer") |

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

---

## Navigation

| From         | To                   | Trigger                            | Type |
|--------------|----------------------|------------------------------------|------|
| fo-dashboard | customer-search      | stat_active_customers tap          | push |
| fo-dashboard | account-applications | stat_pending_applications tap      | push |
| fo-dashboard | kyc-review           | stat_kyc_pending tap               | push |
| fo-dashboard | meetings             | stat_meetings_today tap            | push |
| fo-dashboard | kyc-review           | alert_kyc_review_button tap        | push |
| fo-dashboard | account-applications | alert_view_application_button tap  | push |
| fo-dashboard | customer-search      | alert_start_onboarding_button tap  | push |
| fo-dashboard | corporate-onboarding | action_corporate_btn tap           | push |
| fo-dashboard | agent-registration   | action_register_as_agent_btn tap   | push |
| fo-dashboard | meetings             | meeting_row_1 / meeting_row_2 tap  | push |
| fo-dashboard | profile              | top_bar_profile_icon tap           | push |
| fo-dashboard | settings             | top_bar_settings_icon tap          | push |

---

## API Endpoints

| Endpoint                                              | Auth        | Tag                   | Purpose                                          |
|-------------------------------------------------------|-------------|-----------------------|--------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers              | DirectLogin | Customers             | Customer list: active count, KYC pending, new leads |
| GET /obp/v5.1.0/banks/{bankId}/account-applications  | DirectLogin | Account-Applications  | Application count: pending + corporate inquiries |

---

## Design Tokens

| Token                              | Value     | Usage                                                               |
|------------------------------------|-----------|---------------------------------------------------------------------|
| colors.light.primary               | #4C662B   | Greeting text, stat card border (customers), time labels, nav icons |
| colors.light.primary_container     | #CDEDA3   | KPI card fills (3 of 4), alert card fills, corporate/agent cards    |
| colors.light.nav_active_indicator  | #DCE7C8   | Meetings Today KPI card fill                                        |
| colors.light.secondary             | #386663   | Meetings Today border accent, corporate + agent button text         |
| colors.light.error                 | #BA1A1A   | KYC Pending value text, KYC border, application alert border        |
| colors.light.pending               | #E8A317   | Pending Applications border accent, KYC expiry alert border         |
| colors.light.on_surface            | #1A1C16   | Alert text, schedule details, section headers                       |
| colors.light.on_surface_variant    | #44483D   | Date/branch context text, settings icon, KYC review button text     |
| colors.light.surface               | #FFFFFF   | Meeting row cards                                                   |
| typography.headline_medium         | Outfit 28sp | Greeting text                                                     |
| typography.display_small           | Outfit 32sp/600 | KPI stat values (124, 5, 3, 2)                                |
| typography.title_large             | Outfit 22sp | "Action Needed" section header                                    |
| typography.title_medium            | Outfit 16sp/500 | "Today's Schedule" header                                     |
| typography.body_medium             | Outfit 14sp/400 | Alert text, meeting details, date/branch context              |
| typography.label_large             | Outfit 14sp/500 | Meeting time labels                                           |
| typography.label_medium            | Outfit 12sp/500 | Corporate/agent button text                                   |
| typography.label_small             | Outfit 11sp/500 | Alert action buttons (Review KYC, View Application, etc.)     |
| radius.md                          | 12dp      | KPI stat cards, alert cards                                         |
| radius.sm                          | 8dp       | Alert action buttons                                                |
| elevation.level1                   | 1dp       | Meeting row cards                                                   |

---

_Generated by /idea export | 2026-05-29_
