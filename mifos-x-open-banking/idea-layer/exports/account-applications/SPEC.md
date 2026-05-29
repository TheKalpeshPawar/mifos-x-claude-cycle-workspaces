# SPEC — Account Applications

| Field         | Value                              |
|---------------|------------------------------------|
| Feature       | account-applications               |
| Flavor        | fieldOfficer                       |
| Status        | approved                           |
| Quality Score | 93                                 |
| ViewModel     | AccountApplicationsViewModel       |

---

## Overview

The Account Applications screen is the Field Officer's central pipeline view for managing new account requests submitted by customers. It displays a scrollable list of application cards filtered by status (All, Pending, Approved, Rejected), each card showing the applicant's name, requested product, submission date, and a status chip. Pending applications include a "Review" button that navigates to the Application Detail screen. A floating action button in the bottom-right corner initiates a new account application via the customer onboarding flow. Data is fetched from the OBP `/banks/{bankId}/account-applications` endpoint and filtered client-side.

---

## Screens

| ID                          | Name                        | Route                   | Layout | Scroll   |
|-----------------------------|-----------------------------|-------------------------|--------|----------|
| account-applications-main   | Account Application Pipeline| /account-applications   | Column | Vertical |

**Shell:** Field Officer bottom navigation bar with 5 items (Applications active). Top app bar visible.

| Nav Item     | ID                | Icon        | Target               |
|--------------|-------------------|-------------|----------------------|
| Dashboard    | nav_fo_dashboard  | dashboard   | fo-dashboard         |
| Customers    | nav_customers     | people      | customer-search      |
| Applications | nav_applications  | description | account-applications |
| Messages     | nav_messages      | mail        | customer-messages    |
| More         | nav_more          | more_vert   | settings             |

---

## Components

| ID                      | Type   | Description                                                                                             |
|-------------------------|--------|---------------------------------------------------------------------------------------------------------|
| page_title              | text   | "Account Applications" — headline_large (32sp), color `#4C662B`; screen identity heading               |
| status_filter_tabs      | stack  | Horizontal scrollable row of filter chips: All (8), Pending (3), Approved (3), Rejected (2)             |
| filter_all              | input  | Filter chip "All (8)" — selected: `#4C662B` bg/white text; unselected: `#F9FAEF`/`#44483D`             |
| filter_pending          | input  | Filter chip "Pending (3)" — selected: `#E8A317` bg/white text                                          |
| filter_approved         | input  | Filter chip "Approved (3)" — selected: `#4C662B` bg/white text                                         |
| filter_rejected         | input  | Filter chip "Rejected (2)" — selected: `#BA1A1A` bg/white text                                         |
| app_card_1              | box    | Elevated card (white, radius 12dp, elevation 2) — John Mwangi / KCB Savings Account / Pending Review   |
| app_card_1_name         | text   | "John Mwangi" — title_medium/Bold, color `#1A1C16`                                                     |
| app_card_1_status_chip  | box    | Status chip: `#CDEDA3` bg, `#E8A317` border; text "Pending Review" label_small/`#44483D`               |
| app_card_1_product      | text   | "KCB Savings Account" — body_medium, color `#4C662B`                                                   |
| app_card_1_date         | text   | "Submitted: 20 May 2026" — body_small, color `#44483D`                                                 |
| app_card_1_review_btn   | button | "Review" — filled `#4C662B`/white, label_medium; navigates to application-detail                       |
| app_card_2              | box    | Elevated card — Sarah Odhiambo / M-Shwari Checking Account / Approved                                  |
| app_card_2_name         | text   | "Sarah Odhiambo" — title_medium/Bold, color `#1A1C16`                                                  |
| app_card_2_status_chip  | box    | Status chip: `#CDEDA3` bg, `#4C662B` border; text "Approved ✓" label_small/`#4C662B`                   |
| app_card_2_product      | text   | "M-Shwari Checking Account" — body_medium, color `#4C662B`                                             |
| app_card_2_date         | text   | "Submitted: 18 May 2026" — body_small, color `#44483D`                                                 |
| app_card_3              | box    | Elevated card — Peter Kamau / Business Current Account / Rejected                                       |
| app_card_3_name         | text   | "Peter Kamau" — title_medium/Bold, color `#1A1C16`                                                     |
| app_card_3_status_chip  | box    | Status chip: `#CDEDA3` bg, `#BA1A1A` border; text "Rejected ✗" label_small/`#BA1A1A`                   |
| app_card_3_product      | text   | "Business Current Account" — body_medium, color `#4C662B`                                              |
| app_card_3_date         | text   | "Submitted: 12 May 2026" — body_small, color `#44483D`                                                 |
| app_card_3_reason_link  | link   | "View Reason" — label_medium, color `#BA1A1A`, underlined; navigates to application-detail             |
| new_application_fab     | button | Extended FAB "New Application" — `#4C662B` bg, white text + `add` icon; position bottom-right          |

---

## States

| ID      | Trigger                                        | Description                                                                 |
|---------|------------------------------------------------|-----------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad                       | Shimmer skeleton cards in place of application cards; filter row visible    |
| content | Data load success                              | All application cards visible with real data; filter tabs operative         |
| empty   | No applications match selected filter          | Empty state card: "No Applications Found" with `assignment` icon            |
| error   | Network or OBP API failure                     | Error banner shown above filter row with retry option                       |

---

## State Model

**ViewModel:** `AccountApplicationsViewModel`
**Screen State Type:** `AccountApplicationsScreenState`

| Name                  | Type                        | Default        |
|-----------------------|-----------------------------|----------------|
| applications          | `List<AccountApplication>`  | `emptyList()`  |
| activeFilter          | `ApplicationFilter`         | `ALL`          |
| filteredApplications  | `List<AccountApplication>`  | `emptyList()`  |
| isLoading             | `Boolean`                   | `true`         |
| counts                | `ApplicationCounts`         | _(zero counts)_|

**Events:** `FilterChanged`, `ApplicationSelected`, `NewApplicationStarted`

**Actions:** `filter`, `navigate`, `new_application`

**DI Dependencies:** `AccountApplicationRepository`

**Errors:**
- `LOAD_FAILED`: "Could not load account applications. Please try again."
- `NETWORK_UNAVAILABLE`: "No internet connection. Check your network and retry."

---

## Navigation

| From                 | To                  | Trigger                              | Type  |
|----------------------|---------------------|--------------------------------------|-------|
| account-applications | application-detail  | app_card_1 tap / app_card_1_review_btn tap | push  |
| account-applications | application-detail  | app_card_2 tap                       | push  |
| account-applications | application-detail  | app_card_3 tap / app_card_3_reason_link tap | push  |
| account-applications | customer-onboarding | new_application_fab tap              | push  |
| account-applications | fo-dashboard        | nav_fo_dashboard tab tap             | tab   |
| account-applications | customer-search     | nav_customers tab tap                | tab   |
| account-applications | customer-messages   | nav_messages tab tap                 | tab   |
| account-applications | settings            | nav_more tab tap                     | tab   |

---

## API Endpoints

| Endpoint                                                  | Auth        | Tag                  | Purpose                                            |
|-----------------------------------------------------------|-------------|----------------------|----------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications       | DirectLogin | Account-Applications | Fetch all account applications for the bank        |

---

## Design Tokens

| Token                           | Value     | Usage                                                           |
|---------------------------------|-----------|-----------------------------------------------------------------|
| colors.light.primary            | `#4C662B` | Page title, product text in cards, Review button, approved chip|
| colors.light.on_primary         | `#FFFFFF` | Review button text, selected filter chip text                   |
| colors.light.primary_container  | `#CDEDA3` | Status chip background for all states                           |
| colors.light.on_surface         | `#1A1C16` | Applicant name text in cards                                    |
| colors.light.on_surface_variant | `#44483D` | Date text, pending chip text (a11y-corrected)                   |
| colors.light.error              | `#BA1A1A` | Rejected chip border + text, "View Reason" link                 |
| colors.light.pending            | `#E8A317` | Pending chip border, pending filter selected background         |
| colors.light.background         | `#F9FAEF` | Screen background, unselected filter chip background            |
| colors.light.surface            | `#FFFFFF` | Application card background                                     |
| typography.headline_large       | 32sp/Regular | Page title                                                  |
| typography.title_medium         | 16sp/Medium  | Applicant name in cards                                     |
| typography.body_medium          | 14sp/Regular | Product name in cards                                       |
| typography.body_small           | 12sp/Regular | Submission date in cards                                    |
| typography.label_medium         | 12sp/Medium  | Filter chip labels, Review button text, View Reason link    |
| typography.label_small          | 11sp/Medium  | Status chip text                                            |
| radius.md                       | 12dp      | Application card corners, status chip radius                    |
| elevation.level2                | 3dp       | Application card elevation                                      |
| spacing.md                      | 16dp      | Card horizontal margin                                          |

---

_Generated by /idea export | 2026-05-29_
