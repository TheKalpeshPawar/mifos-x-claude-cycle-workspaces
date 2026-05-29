# SPEC — Application Detail

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | application-detail             |
| Flavor        | fieldOfficer                   |
| Status        | approved                       |
| Quality Score | 94                             |
| ViewModel     | ApplicationDetailViewModel     |

---

## Overview

The Application Detail screen is the Field Officer's primary review surface for a pending account application. It presents the full application record — reference number, status chip, applicant identity, account type, requested credit limit, stated purpose, KYC verification status, and supporting document thumbnails — in a scrollable detail layout. Officers can add internal review notes, then approve, reject, or request additional information from the applicant. The approved path navigates back to Customer Detail; the request-info path opens a Customer Messages thread with the applicant.

---

## Screens

| ID                       | Name                 | Route               | Layout | Scroll   |
|--------------------------|----------------------|---------------------|--------|----------|
| application-detail-main  | Application Review   | /application-detail | Column | Vertical |

**Shell:** Top app bar with back navigation. No bottom navigation bar (fieldOfficer detail flow).

---

## Components

| ID                        | Type    | Description                                                                                                    |
|---------------------------|---------|----------------------------------------------------------------------------------------------------------------|
| application_header        | box     | #4C662B header bar containing reference number and status/date meta row                                        |
| app_reference_number      | text    | "Application #OBP-2026-00234" — Outfit/title_large, #FFFFFF, weight 700                                       |
| app_status_chip           | box     | Rounded chip (#CDEDA3, radius 12) showing current status                                                       |
| app_status_text           | text    | "Pending Review" — Outfit/label_small, #44483D, weight 600                                                     |
| app_submitted_date        | text    | "Submitted: 20 May 2026" — Outfit/body_small, #CDEDA3                                                         |
| customer_info_card        | box     | White card (radius 12, elevation 2, 16dp padding) with customer name + View Profile link                       |
| customer_card_heading     | text    | "CUSTOMER" — Outfit/label_medium, #44483D, uppercase, letter-spacing 0.8                                       |
| customer_name             | text    | "John Kamau Mwangi" — Outfit/title_medium, #1A1C16, weight 700                                                 |
| customer_profile_link     | link    | "View Profile" — Outfit/label_medium, #4C662B, underline; navigates to customer-detail                        |
| application_details_card  | box     | White card (radius 12, elevation 2) with account type, requested limit, purpose rows                           |
| account_type_value        | text    | "KCB Savings Account" — Outfit/body_medium, #1A1C16, weight 600                                               |
| limit_value               | text    | "KES 500,000" — Outfit/body_medium, #1A1C16, weight 600, monospace                                            |
| purpose_value             | text    | "Personal savings and salary credit" — Outfit/body_medium, #1A1C16                                            |
| kyc_status_row            | box     | #CDEDA3 banner (radius 12, #4C662B 1px border) with verified_user icon + status label                         |
| kyc_status_label          | text    | "KYC Status: Verified ✓" — Outfit/body_medium, #4C662B, weight 600                                            |
| documents_heading         | text    | "Supporting Documents" — Outfit/title_medium, #1A1C16, role heading                                           |
| doc_national_id_card      | box     | White card (radius 10, elevation 1, #E1E4D5 border) with National ID thumbnail, "Verified ✓", View link       |
| doc_id_title              | text    | "National ID" — Outfit/body_large, #1A1C16, weight 600                                                        |
| doc_id_status             | text    | "Verified ✓" — Outfit/body_small, #4C662B                                                                     |
| doc_id_view_link          | link    | "View" — Outfit/label_medium, #4C662B; triggers view_document for national_id_doc                             |
| doc_proof_address_card    | box     | White card (radius 10, elevation 1, #E1E4D5 border) with address icon placeholder + "Pending Upload" status   |
| doc_address_title         | text    | "Proof of Address" — Outfit/body_large, #1A1C16, weight 600                                                   |
| doc_address_status        | text    | "Pending Upload" — Outfit/body_small, #44483D                                                                 |
| upload_address_doc_button | button  | "Upload" — outlined, #4C662B border/text; triggers upload_document for proof_of_address                       |
| review_notes_input        | input   | "Review Notes" textarea (3–6 lines) — placeholder: "Add internal notes about this application…"               |
| approve_application_button| button  | "Approve Application" — filled #4C662B, full-width; navigates to customer-detail on success                   |
| reject_application_button | button  | "Reject Application" — outlined #BA1A1A border/text, full-width                                               |
| request_info_button       | button  | "Request Information" — text #4C662B; navigates to customer-messages                                          |

---

## States

| ID        | Trigger                                | Description                                                                              |
|-----------|----------------------------------------|------------------------------------------------------------------------------------------|
| loading   | Screen entry / data fetch              | Skeleton shimmer over header, cards, document rows; no interactive elements              |
| content   | Data load success                      | All components visible; alias for reviewing state                                        |
| reviewing | Application loaded, decision pending   | Full layout — header, customer card, application card, KYC row, documents, review notes  |
| approved  | approve_application action success     | Success banner "Application approved successfully" shown above layout                    |
| rejected  | reject_application action success      | Rejection banner shown above layout                                                      |
| empty     | Application record not found           | Empty state card "Application details not available" centred with 16dp padding           |
| error     | Network or auth failure                | Error banner with retry option                                                           |

---

## State Model

**ViewModel:** `ApplicationDetailViewModel`
**Screen State Type:** `ApplicationDetailUiState`

| Name             | Type                     | Default   |
|------------------|--------------------------|-----------|
| applicationId    | String                   | ""        |
| application      | AccountApplicationDetail? | null     |
| reviewNotes      | String                   | ""        |
| isSubmitting     | Boolean                  | false     |
| decisionMade     | ApplicationDecision      | PENDING   |

**Events:** `ApplicationApproved`, `ApplicationRejected`, `InfoRequested`, `DocumentViewed`, `CustomerProfileOpened`

**Actions:** `approve_application()`, `reject_application()`, `request_info()`, `view_document()`, `upload_document()`, `navigate()`

**DI Dependencies:** `AccountApplicationRepository`, `CustomerMessagingService`

**Errors:**
- `APPROVAL_FAILED`: "Failed to approve application. Please try again."
- `REJECTION_FAILED`: "Failed to reject application. Please try again."
- `LOAD_FAILED`: "Unable to load application details. Check your connection."
- `NETWORK_UNAVAILABLE`: "No network connection. Please try again."

---

## Navigation

| From               | To               | Trigger                          | Type |
|--------------------|------------------|----------------------------------|------|
| application-detail | customer-detail  | customer_profile_link tap        | push |
| application-detail | customer-detail  | approve_application_button tap   | pop  |
| application-detail | customer-messages| request_info_button tap          | push |

---

## API Endpoints

| Endpoint                                                                       | Auth        | Tag                  | Purpose                                          |
|--------------------------------------------------------------------------------|-------------|----------------------|--------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}           | DirectLogin | Account-Applications | Load application record, customer, KYC status    |
| PUT /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}           | DirectLogin | Account-Applications | Submit approval or rejection decision            |

---

## Design Tokens

| Token                           | Value     | Usage                                                              |
|---------------------------------|-----------|--------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Header background, KYC border, profile/view links, approve button  |
| colors.light.primary_container  | #CDEDA3   | Status chip background, KYC banner fill, submitted date color      |
| colors.light.on_primary         | #FFFFFF   | Header text, approve button text                                   |
| colors.light.error              | #BA1A1A   | Reject button border and text                                      |
| colors.light.on_surface         | #1A1C16   | Customer name, document titles, purpose text                       |
| colors.light.on_surface_variant | #44483D   | Status chip text, section headings (CUSTOMER), pending upload text |
| colors.light.surface            | #FFFFFF   | Customer info card, application details card, document cards       |
| colors.light.surface_variant    | #E1E4D5   | Document card borders                                              |
| colors.light.background         | #F9FAEF   | Screen background, document address placeholder fill               |
| typography.title_large          | 22sp/400  | Application reference number                                       |
| typography.title_medium         | 16sp/500  | Customer name, documents section heading                           |
| typography.body_medium          | 14sp/400  | Field labels and values throughout                                 |
| typography.body_large           | 16sp/400  | Document card titles                                               |
| typography.label_medium         | 12sp/500  | Section headings (uppercase), View/Upload links                    |
| typography.label_small          | 11sp/500  | Status chip text                                                   |
| radius.md                       | 12dp      | Customer info card, application details card, KYC row              |
| elevation.level2                | 3dp       | Customer info card and application details card shadows            |

---

_Generated by /idea export | 2026-05-29_
