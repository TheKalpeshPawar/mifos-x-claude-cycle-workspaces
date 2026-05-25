# Feature Specification — Account Applications

| Field         | Value                          |
|---------------|-------------------------------|
| Feature       | account-applications          |
| Flavor        | fieldOfficer                  |
| Status        | enriched                      |
| Quality Score | 81                            |

---

## Overview

The Account Applications screen is the Field Officer's pipeline dashboard showing all customer account applications with their current processing status. A horizontally scrollable chip-based filter bar lets officers slice by All (8), Pending (3), Approved (3), or Rejected (2). Each application is rendered as a card showing applicant name, product name, submission date, and status badge. A floating action button launches new onboarding. Tapping any card or its Review/View Reason button navigates to application-detail.

---

## Screens

| Screen ID                    | Route                        | Layout     | Scroll   |
|------------------------------|------------------------------|------------|----------|
| account-applications-main    | /applications                | index_list | vertical |

---

## Components

| ID                      | Type   | Description                                                                      |
|-------------------------|--------|----------------------------------------------------------------------------------|
| page_title              | text   | "Account Applications" — headline_large, #1800B1, paddingTop 20, role heading h1 |
| status_filter_tabs      | stack  | Horizontally scrollable chip row (gap 8): All (8) · Pending (3) · Approved (3) · Rejected (2) |
| filter_all              | input  | Radio chip — "All (8)", selected bg #1800B1, text white; unselected: #F0F0F0 bg |
| filter_pending          | input  | Radio chip — "Pending (3)", selected bg #FF8F00 (amber)                          |
| filter_approved         | input  | Radio chip — "Approved (3)", selected bg #4CAF50 (green)                         |
| filter_rejected         | input  | Radio chip — "Rejected (2)", selected bg #FF5252 (red)                           |
| app_card_1              | box    | Card: John Mwangi · KCB Savings Account · Pending Review · Submitted 20 May 2026 |
| app_card_2              | box    | Card: Sarah Odhiambo · M-Shwari Checking Account · Approved ✓ · Submitted 18 May 2026 |
| app_card_3              | box    | Card: Peter Kamau · Business Current Account · Rejected ✗ · Submitted 12 May 2026 |
| new_application_fab     | button | Extended FAB, bg #1800B1, icon add, label "New Application", position bottom-right |

**Per-card sub-components (app_card_1 as canonical example):**

| ID                      | Type  | Description                                                     |
|-------------------------|-------|-----------------------------------------------------------------|
| app_card_1_name         | text  | Applicant name — title_medium, weight 700, #1A1A1A             |
| app_card_1_status_chip  | box   | Pending: #FFF8E1 bg, #FFB300 border, "Pending Review" #E65100  |
| app_card_1_product      | text  | Product name — body_medium, color #1800B1                      |
| app_card_1_date         | text  | "Submitted: 20 May 2026" — body_small, #999999                 |
| app_card_1_review_btn   | button| "Review" — filled, bg #1800B1, white text → application-detail |

---

## States

| ID      | Trigger                         | Description                                                         |
|---------|---------------------------------|---------------------------------------------------------------------|
| loading | Screen open / filter change     | Shimmer skeleton cards while fetching from GET account-applications |
| content | Data loaded                     | Scrollable card list with filter chips, bg #F5F5F5                 |
| empty   | No applications match filter    | Empty state: icon assignment, "No Applications Found", subtitle "No account applications match the selected filter" |
| error   | API call fails                  | Error banner with retry                                             |

---

## State Model

**ViewModel:** `AccountApplicationsViewModel`

| State Field           | Type                      | Default | Values                       |
|-----------------------|---------------------------|---------|------------------------------|
| applications          | List\<AccountApplication\>| emptyList | —                          |
| activeFilter          | ApplicationFilter         | ALL     | ALL, PENDING, APPROVED, REJECTED |
| filteredApplications  | List\<AccountApplication\>| emptyList | —                          |
| isLoading             | Boolean                   | true    | —                            |
| counts                | ApplicationCounts         | —       | all=8, pending=3, approved=3, rejected=2 |

**Events:** FilterChanged, ApplicationSelected, NewApplicationStarted

**Actions:** filter, navigate, new_application

**DI Dependencies:** AccountApplicationRepository

**Errors:** LOAD_FAILED, NETWORK_UNAVAILABLE

---

## Navigation

| From                  | To                   | Trigger                       | Type     |
|-----------------------|----------------------|-------------------------------|----------|
| account-applications  | application-detail   | Tap any card / Review button  | navigate |
| account-applications  | application-detail   | "View Reason" link on rejected| navigate |
| account-applications  | customer-onboarding  | FAB "New Application"         | navigate |

---

## API Endpoints

| Endpoint                                               | Auth        | Purpose                                                   |
|--------------------------------------------------------|-------------|-----------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications   | DirectLogin | Fetch all account applications for the bank               |

**Response fields:** account_application_id, product_code, user, customer, date_of_application, date_last_modified, status

**Errors:** 400 BAD_REQUEST · 401 UNAUTHORIZED

---

## Design Tokens

| Token           | Value   | Usage                                                   |
|-----------------|---------|---------------------------------------------------------|
| primary         | #1800B1 | Page title, "All" chip selected bg, product name text, Review button, FAB |
| background      | #F5F5F5 | Screen background in content state                     |
| surface         | #FFFFFF | Application cards                                       |
| pending_bg      | #FFF8E1 | Pending status chip background                         |
| pending_border  | #FFB300 | Pending status chip border                             |
| pending_text    | #E65100 | Pending status chip text                               |
| approved_bg     | #E8F5E9 | Approved status chip background                        |
| approved_border | #4CAF50 | Approved status chip border                            |
| approved_text   | #2E7D32 | Approved status chip text                              |
| rejected_bg     | #FFEBEE | Rejected status chip background                        |
| rejected_border | #FF5252 | Rejected status chip border                            |
| rejected_text   | #C62828 | Rejected status chip text                              |
| on_surface      | #1A1A1A | Application card names                                  |
| muted           | #999999 | Submission date text                                    |

---

*Generated by /idea export | 2026-05-25*
