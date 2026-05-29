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

The Account Applications screen is the Field Officer's central pipeline view for tracking and acting on new account requests submitted by customers. Accessed via the Applications tab of the Field Officer bottom navigation bar, it renders a vertically-scrollable list of elevated application cards (`#FFFFFF`, 12dp radius, elevation 2) beneath a horizontally-scrollable filter chip row. Each card shows the applicant's legal name (title_medium/Bold, `#1A1C16`), requested product name (body_medium, `#4C662B`), submission date (body_small, `#44483D`), and a colour-coded status chip (`#CDEDA3` background, border and text vary by status). Pending cards include a "Review" filled button; Rejected cards show a "View Reason" underlined link. All cards navigate to the Application Detail screen. A fixed extended FAB (bottom-right, `#4C662B`) initiates a new application via the customer onboarding flow. Data is fetched from `GET /obp/v5.1.0/banks/{bankId}/account-applications` and filtered client-side by the `AccountApplicationsViewModel`. Demo set: 5 applications — 2 PENDING (John Mwangi, Grace Wanjiru), 2 APPROVED (Sarah Odhiambo, David Kipchoge), 1 REJECTED (Peter Kamau).

---

## Screens

| ID                          | Name                         | Route                   | Layout | Scroll   |
|-----------------------------|------------------------------|-------------------------|--------|----------|
| account-applications-main   | Account Application Pipeline | /account-applications   | Column | Vertical |

**Shell:** Field Officer bottom navigation bar with 5 items (Applications tab active).

| Nav Item     | ID               | Icon        | Target               | Active |
|--------------|------------------|-------------|----------------------|--------|
| Dashboard    | nav_fo_dashboard | dashboard   | fo-dashboard         | false  |
| Customers    | nav_customers    | people      | customer-search      | false  |
| Applications | nav_applications | description | account-applications | true   |
| Messages     | nav_messages     | mail        | customer-messages    | false  |
| More         | nav_more         | more_vert   | settings             | false  |

---

## Components

| ID                      | Type   | Description                                                                                                      |
|-------------------------|--------|------------------------------------------------------------------------------------------------------------------|
| page_title              | text   | "Account Applications" — Outfit/headline_large (32sp/Regular), color `#4C662B`; h1 heading, 16dp H pad, 20dp top pad, 4dp bottom pad |
| status_filter_tabs      | stack  | Horizontal scrollable row of 4 filter chips; 16dp H padding, 10dp V padding, 8dp gap between chips; role tablist |
| filter_all              | input  | Filter chip "All (8)" — selected: `#4C662B` bg/white text; unselected: `#F9FAEF` bg/`#44483D` text; 20dp radius, 14dp H pad, role tab |
| filter_pending          | input  | Filter chip "Pending (3)" — selected: `#E8A317` bg/white text; unselected: `#F9FAEF`/`#44483D`; 20dp radius      |
| filter_approved         | input  | Filter chip "Approved (3)" — selected: `#4C662B` bg/white text; same unselected style                           |
| filter_rejected         | input  | Filter chip "Rejected (2)" — selected: `#BA1A1A` bg/white text; same unselected style                           |
| app_card_1              | box    | Elevated card: `#FFFFFF`, 12dp radius, 14dp padding, 16dp H margin, 10dp bottom margin, elevation 2; navigates to application-detail (John Mwangi / KCB Savings Account / Pending Review) |
| app_card_1_name         | text   | "John Mwangi" — Outfit/title_medium (16sp/700), color `#1A1C16`; a11y heading "Applicant: John Mwangi"         |
| app_card_1_status_chip  | box    | `#CDEDA3` bg, `#E8A317` border (1dp), 12dp radius, 10dp H pad, 3dp V pad; text "Pending Review" label_small/`#44483D` (a11y-corrected from `#E8A317`; contrast 7.25:1 PASS) |
| app_card_1_product      | text   | "KCB Savings Account" — Outfit/body_medium (14sp/400), color `#4C662B`; label "Product: KCB Savings Account"    |
| app_card_1_date         | text   | "Submitted: 20 May 2026" — Outfit/body_small (12sp/400), color `#44483D`; label "Submitted 20 May 2026"         |
| app_card_1_review_btn   | button | "Review" — filled, `#4C662B` bg/white text, Outfit/label_medium, 8dp radius, 16dp H pad, 8dp V pad; navigates to application-detail; label "Review John Mwangi's application" |
| app_card_2              | box    | Elevated card: `#FFFFFF`, 12dp radius, 14dp padding; navigates to application-detail (Sarah Odhiambo / M-Shwari Checking Account / Approved) |
| app_card_2_name         | text   | "Sarah Odhiambo" — Outfit/title_medium/700, color `#1A1C16`                                                     |
| app_card_2_status_chip  | box    | `#CDEDA3` bg, `#4C662B` border (1dp), 12dp radius; text "Approved ✓" label_small/`#4C662B`                      |
| app_card_2_product      | text   | "M-Shwari Checking Account" — Outfit/body_medium, color `#4C662B`                                               |
| app_card_2_date         | text   | "Submitted: 18 May 2026" — Outfit/body_small, color `#44483D`                                                   |
| app_card_3              | box    | Elevated card: `#FFFFFF`, 12dp radius, 14dp padding; navigates to application-detail (Peter Kamau / Business Current Account / Rejected) |
| app_card_3_name         | text   | "Peter Kamau" — Outfit/title_medium/700, color `#1A1C16`                                                        |
| app_card_3_status_chip  | box    | `#CDEDA3` bg, `#BA1A1A` border (1dp), 12dp radius; text "Rejected ✗" label_small/`#BA1A1A`                      |
| app_card_3_product      | text   | "Business Current Account" — Outfit/body_medium, color `#4C662B`                                                |
| app_card_3_date         | text   | "Submitted: 12 May 2026" — Outfit/body_small, color `#44483D`                                                   |
| app_card_3_reason_link  | link   | "View Reason" — Outfit/label_medium (12sp), color `#BA1A1A`, underlined; navigates to application-detail; label "View rejection reason for Peter Kamau's application" |
| new_application_fab     | button | Extended FAB "New Application" — `#4C662B` bg, white text, `add` icon, fixed bottom-right; 24dp bottom margin, 16dp right margin, elevation 6; navigates to customer-onboarding |

---

## States

| ID      | Trigger                                        | Description                                                                                                  |
|---------|------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad event                 | Shimmer skeleton cards (3 cards) in place of application cards; filter chip row visible; FAB hidden; shimmer duration `short4` (200ms); reduced-motion fallback uses static placeholder |
| content | `loadApplications()` succeeds                  | All application cards rendered with live data; filter tabs operative for client-side filtering; FAB visible   |
| empty   | filteredApplications list is empty             | Centred empty state: `assignment` icon (48dp, `#44483D`) + "No Applications Found" (title_medium, `#1A1C16`) + "No account applications match the selected filter" (body_medium, `#44483D`); FAB still visible |
| error   | LOAD_FAILED or NETWORK_UNAVAILABLE             | Full-width error banner above cards (`#FFDAD6` bg, `#BA1A1A` text): "Could not load account applications" + Retry text button; filter tabs remain visible |

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
| counts                | `ApplicationCounts`         | _(all zeros)_  |

**`ApplicationFilter` values:** `ALL`, `PENDING`, `APPROVED`, `REJECTED`

**Events:** `FilterChanged(filter: ApplicationFilter)`, `ApplicationSelected(applicationId: String)`, `NewApplicationStarted`

**Actions:** `filter(target: ApplicationFilter)`, `navigate(target: String)`, `new_application`

**DI Dependencies:** `AccountApplicationRepository`

**Errors:**
- `LOAD_FAILED`: "Could not load account applications. Please try again."
- `NETWORK_UNAVAILABLE`: "No internet connection. Check your network and retry."

---

## Navigation

| From                 | To                  | Trigger                                                    | Type |
|----------------------|---------------------|------------------------------------------------------------|------|
| account-applications | application-detail  | app_card_1 tap (any zone)                                  | push |
| account-applications | application-detail  | app_card_1_review_btn tap                                  | push |
| account-applications | application-detail  | app_card_2 tap (any zone)                                  | push |
| account-applications | application-detail  | app_card_3 tap (any zone)                                  | push |
| account-applications | application-detail  | app_card_3_reason_link tap                                 | push |
| account-applications | customer-onboarding | new_application_fab tap                                    | push |
| account-applications | fo-dashboard        | nav_fo_dashboard bottom tab tap                            | tab  |
| account-applications | customer-search     | nav_customers bottom tab tap                               | tab  |
| account-applications | customer-messages   | nav_messages bottom tab tap                                | tab  |
| account-applications | settings            | nav_more bottom tab tap                                    | tab  |

---

## API Endpoints

| Endpoint                                                     | Auth        | Tag                  | Purpose                                               |
|--------------------------------------------------------------|-------------|----------------------|-------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications         | DirectLogin | Account-Applications | Fetch all account applications for the bank; filtered client-side |

---

## Design Tokens

| Token                           | Value        | Usage                                                                          |
|---------------------------------|--------------|--------------------------------------------------------------------------------|
| colors.light.primary            | `#4C662B`    | Page title, product text in all cards, Review button bg, Approved chip border+text, "All" + "Approved" filter selected bg, FAB bg |
| colors.light.on_primary         | `#FFFFFF`    | Review button text, selected filter chip text (All / Approved / Rejected)      |
| colors.light.primary_container  | `#CDEDA3`    | Status chip background for all three states (Pending/Approved/Rejected)        |
| colors.light.on_surface         | `#1A1C16`    | Applicant name text in cards                                                   |
| colors.light.on_surface_variant | `#44483D`    | Submission date text; Pending chip text (a11y-corrected from `#E8A317` — 7.25:1 ratio vs 1.68:1) |
| colors.light.error              | `#BA1A1A`    | Rejected chip border + text, "View Reason" link, Rejected filter selected bg, error banner text |
| colors.light.error_container    | `#FFDAD6`    | Error banner background                                                        |
| colors.light.pending            | `#E8A317`    | Pending chip border, Pending filter chip selected bg                           |
| colors.light.background         | `#F9FAEF`    | Screen background (`content` state), unselected filter chip bg                 |
| colors.light.surface            | `#FFFFFF`    | Application card background                                                    |
| colors.light.surface_variant    | `#E1E4D5`    | Skeleton card shimmer base                                                     |
| colors.light.surface_container  | `#F0F1E6`    | Skeleton shimmer highlight                                                     |
| typography.headline_large       | 32sp/Regular | Page title ("Account Applications")                                            |
| typography.title_medium         | 16sp/500     | Applicant name in cards (overridden to weight 700 in source)                   |
| typography.body_medium          | 14sp/Regular | Product name in cards                                                          |
| typography.body_small           | 12sp/Regular | Submission date text in cards                                                  |
| typography.label_medium         | 12sp/Medium  | Filter chip labels, Review button text, View Reason link                       |
| typography.label_small          | 11sp/Medium  | Status chip text (Pending Review / Approved ✓ / Rejected ✗)                   |
| radius.md                       | 12dp         | Application card corners, status chip radius, Review button radius (8dp)      |
| elevation.level2                | 3dp          | Application card elevation (source specifies elevation: 2 → level2 = 3dp)     |
| elevation.level3                | 6dp          | Extended FAB elevation                                                         |
| spacing.xs                      | 4dp          | Page title bottom padding; filter chip vertical padding                        |
| spacing.sm                      | 8dp          | Gap between filter chips; Review button vertical padding                       |
| spacing.md                      | 16dp         | Card horizontal margin; page title horizontal padding; Review button H padding  |
| spacing.lg                      | 24dp         | FAB bottom margin                                                              |

---

_Generated by /idea export | 2026-05-30_
