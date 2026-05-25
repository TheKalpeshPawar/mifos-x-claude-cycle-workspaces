# Feature Specification: Field Officer Dashboard

| Field | Value |
|---|---|
| Feature | fo-dashboard |
| Flavor | fieldOfficer |
| Status | enriched |
| Quality Score | 83 |

## Overview

The Field Officer Dashboard is the primary home screen for Mifos field agents, providing a real-time snapshot of their portfolio health and daily workload. It surfaces four key KPIs — active customers, pending applications, KYC pending count, and meetings today — alongside contextual action alerts and a chronological schedule for the current day. The dashboard is designed for rapid triage: every stat card and alert row is tappable and navigates directly to the relevant workflow.

## Screens

| Screen ID | Name | Route | Layout | Scroll |
|---|---|---|---|---|
| fo_dashboard_main | Field Officer Dashboard | /fo-dashboard | dashboard | vertical |

## Components

| ID | Type | Description |
|---|---|---|
| greeting_text | text | Time-aware greeting: "Good morning, Priya" with headline_medium typography in brand purple |
| date_branch_context | text | Current date and branch context: "Monday, 25 May 2026 · Mifos Nairobi Branch" |
| top_bar_profile_icon | icon | account_circle icon (32px) — navigates to profile screen |
| top_bar_settings_icon | icon | settings icon (24px) — navigates to settings screen |
| stats_grid | grid | 2-column grid of 4 stat cards with 12px gap |
| stat_active_customers | box | Purple-tinted card showing 124 active customers; navigates to customer-search |
| stat_pending_applications | box | Amber-tinted card showing 5 pending applications; navigates to account-applications |
| stat_kyc_pending | box | Red-tinted card showing 3 KYC pending; navigates to kyc-review |
| stat_meetings_today | box | Teal-tinted card showing 2 meetings today; navigates to meetings |
| action_needed_header | text | Section heading "Action Needed" (title_large, bold) |
| alert_kyc_expiry_john | box | Amber alert: "John Mwangi — KYC expires in 3 days" with Review KYC outlined button |
| alert_application_pending_sarah | box | Red alert: "Sarah Odhiambo — Application pending 7 days" with View Application button |
| alert_new_lead_peter | box | Green alert: "New lead: Peter Kamau — Retail account request" with Start Onboarding button |
| action_corporate_onboard | box | Amber card: "Acme Trading Ltd — New business account inquiry" with Start Corporate Onboarding |
| schedule_header | text | "Today's Schedule" section heading |
| meeting_row_1 | box | 10:00 AM — Mary Wanjiku · Loan Review |
| meeting_row_2 | box | 2:30 PM — James Otieno · New Account Discussion |

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen mount, API call in flight | Greeting and date visible; stats grid, action section, schedule show skeleton shimmer |
| content | API response success | All 4 stat cards, action alerts, and meeting rows fully populated |
| error | API call fails / network unavailable | Greeting and date remain; stats grid, action section, schedule hidden; error message shown |

## State Model

**ViewModel:** `FoDashboardViewModel`

| Field | Type | Default |
|---|---|---|
| officerName | String | "Priya" |
| branchName | String | "Mifos Nairobi Branch" |
| activeCustomerCount | Int | 0 |
| pendingApplicationCount | Int | 0 |
| kycPendingCount | Int | 0 |
| meetingsTodayCount | Int | 0 |
| actionAlerts | List\<ActionAlert\> | emptyList() |
| todayMeetings | List\<Meeting\> | emptyList() |
| isLoading | Boolean | true |
| networkError | String? | null |

**Events:** `StatCardClickedEvent`, `AlertActionClickedEvent`, `MeetingClickedEvent`

**Actions:** `navigate`

**DI Dependencies:** `CustomerRepository`, `AccountApplicationRepository`, `MeetingRepository`, `NavigationService`

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| fo-dashboard | customer-search | stat_active_customers / alert_new_lead_peter / alert_start_onboarding_button | push |
| fo-dashboard | account-applications | stat_pending_applications / alert_view_application_button | push |
| fo-dashboard | kyc-review | stat_kyc_pending / alert_kyc_review_button / alert_kyc_expiry_john | push |
| fo-dashboard | meetings | stat_meetings_today / meeting_row_1 / meeting_row_2 | push |
| fo-dashboard | corporate-onboarding | action_corporate_onboard / action_corporate_btn | push |
| fo-dashboard | profile | top_bar_profile_icon | push |
| fo-dashboard | settings | top_bar_settings_icon | push |

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/banks/{bankId}/customers | DirectLogin token | Fetch customer list; activeCustomerCount derived from response |
| GET /obp/v5.1.0/banks/{bankId}/account-applications | DirectLogin token | Fetch pending applications; pendingApplicationCount derived from response |

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Greeting text, active-customers card accent, meeting time labels |
| stat_active_bg | #EDE7FF | Active customers card background |
| stat_pending_bg | #FFF8E1 | Pending applications card background |
| stat_kyc_bg | #FFEBEE | KYC pending card background |
| stat_meetings_bg | #E0F7FA | Meetings today card background |
| alert_amber | #FF8F00 | KYC expiry and application-pending alert accents |
| alert_red | #FF5252 | Application pending alert accent |
| alert_green | #4CAF50 | New lead alert accent |
| background | #FCF8FF | Screen background |
| error | #BA1A1A | Error state messaging |

---
_Generated by /idea export | 2026-05-25_
