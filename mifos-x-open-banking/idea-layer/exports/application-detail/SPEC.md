# Feature Specification — Application Detail

| Field         | Value                          |
|---------------|-------------------------------|
| Feature       | application-detail            |
| Flavor        | fieldOfficer                  |
| Status        | enriched                      |
| Quality Score | 82                            |

---

## Overview

The Application Detail screen gives a Field Officer a complete view of a single account application and the tools to act on it. A branded deep-purple header carries the application reference number, status chip, and submission date. Two cards below present customer info (with a "View Profile" link) and application details (account type, requested limit KES 500,000, purpose). A KYC verified status row and document cards (National ID verified, proof of address pending) follow. The officer adds internal review notes and taps Approve, Reject, or Request Information.

---

## Screens

| Screen ID               | Route                                              | Layout        | Scroll   |
|-------------------------|----------------------------------------------------|---------------|----------|
| application-detail-main | /applications/{applicationId}                      | detail_screen | vertical |

---

## Components

| ID                        | Type   | Description                                                                        |
|---------------------------|--------|------------------------------------------------------------------------------------|
| application_header        | box    | Deep purple header: ref number "Application #OBP-2026-00234", status chip, submitted date |
| app_reference_number      | text   | "Application #OBP-2026-00234" — title_large, white, weight 700                    |
| app_status_chip           | box    | Amber chip: bg #FFF8E1, "Pending Review" in #E65100, weight 600                   |
| app_submitted_date        | text   | "Submitted: 20 May 2026" — body_small, color #B0B8FF (lavender on purple)         |
| customer_info_card        | box    | White card: "CUSTOMER" label + "John Kamau Mwangi" + "View Profile" link          |
| customer_name             | text   | "John Kamau Mwangi" — title_medium, weight 700, #1A1A1A                           |
| customer_profile_link     | link   | "View Profile" — label_medium, #1800B1, underlined → customer-detail              |
| application_details_card  | box    | White card: account type row + requested limit row + purpose row                  |
| account_type_value        | text   | "KCB Savings Account" — body_medium, weight 600, #1A1A1A                         |
| limit_value               | text   | "KES 500,000" — body_medium, weight 600, monospace                               |
| purpose_value             | text   | "Personal savings and salary credit" — body_medium, #1A1A1A                      |
| kyc_status_row            | box    | Green row (bg #E8F5E9, border #4CAF50): verified_user icon + "KYC Status: Verified ✓" |
| documents_heading         | text   | "Supporting Documents" — title_medium, role heading h2                            |
| doc_national_id_card      | box    | Document card: ID thumbnail with green border + "National ID" Verified ✓ + View link |
| doc_proof_address_card    | box    | Document card: home icon placeholder + "Proof of Address" Pending Upload + Upload button |
| review_notes_input        | input  | Outlined textarea, 3-6 lines, internal review notes (not visible to customer)     |
| approve_application_button| button | Filled green (#4CAF50) "Approve Application" → customer-detail                   |
| reject_application_button | button | Outlined red (#FF5252) "Reject Application" → stays on screen                    |
| request_info_button       | button | Text button, #1800B1 "Request Information" → customer-messages                   |

---

## States

| ID        | Trigger                           | Description                                                         |
|-----------|-----------------------------------|---------------------------------------------------------------------|
| loading   | Screen open                       | Shimmer skeleton while fetching GET account-applications/{id}       |
| reviewing | Data loaded, no decision yet      | Full detail view, all action buttons enabled, bg #F5F5F5            |
| approved  | Approve Application succeeds      | Success banner: "Application approved successfully", bg #F5F5F5     |
| rejected  | Reject Application succeeds       | Rejection banner shown, bg #F5F5F5                                  |
| error     | API call fails                    | Error banner with retry                                             |

---

## State Model

**ViewModel:** `ApplicationDetailViewModel`

| State Field   | Type                     | Default | Values                     |
|---------------|--------------------------|---------|----------------------------|
| applicationId | String                   | —       | —                          |
| application   | AccountApplicationDetail (nullable) | null | —             |
| reviewNotes   | String                   | ""      | —                          |
| isSubmitting  | Boolean                  | false   | —                          |
| decisionMade  | ApplicationDecision      | PENDING | PENDING, APPROVED, REJECTED |

**Events:** ApplicationApproved, ApplicationRejected, InfoRequested, DocumentViewed, CustomerProfileOpened

**Actions:** approve_application, reject_application, request_info, view_document, upload_document, navigate

**DI Dependencies:** AccountApplicationRepository, CustomerMessagingService

**Errors:** APPROVAL_FAILED, REJECTION_FAILED, LOAD_FAILED, NETWORK_UNAVAILABLE

---

## Navigation

| From                | To                  | Trigger                   | Type     |
|---------------------|---------------------|---------------------------|----------|
| application-detail  | customer-detail     | Approve Application       | navigate |
| application-detail  | customer-detail     | "View Profile" link       | navigate |
| application-detail  | customer-messages   | Request Information       | navigate |
| application-detail  | application-detail  | Reject (stays, banner)    | refresh  |

---

## API Endpoints

| Endpoint                                                             | Auth        | Purpose                                               |
|----------------------------------------------------------------------|-------------|-------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId} | DirectLogin | Fetch full application detail                         |
| PUT /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId} | DirectLogin | Update application status (APPROVED or REJECTED)     |

**GET Response fields:** account_application_id, product_code, user, customer, date_of_application, date_last_modified, status, account_routing

**PUT Response fields:** account_application_id, status, date_last_modified

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 404 APPLICATION_NOT_FOUND

---

## Design Tokens

| Token          | Value   | Usage                                                       |
|----------------|---------|-------------------------------------------------------------|
| primary        | #1800B1 | Header background, "View Profile" link, product text, Request Info button |
| on_primary     | #FFFFFF | Header text                                                 |
| avatar_muted   | #B0B8FF | Submitted date in header (lavender on purple)               |
| success_bg     | #E8F5E9 | KYC verified row background                                |
| success_border | #4CAF50 | KYC verified row border, approve button, doc thumbnail border |
| success_text   | #2E7D32 | KYC status label text                                       |
| error_action   | #FF5252 | Reject button border and text                               |
| pending_bg     | #FFF8E1 | Status chip background                                      |
| pending_border | #FFB300 | Status chip border; proof-of-address placeholder border     |
| pending_text   | #E65100 | Status chip text                                            |
| pending_amber  | #FF8F00 | "Pending Upload" document status text                       |
| surface        | #FFFFFF | Customer info card, application details card, document cards |
| background     | #F5F5F5 | Screen background                                           |
| section_label  | #999999 | Card heading labels ("CUSTOMER", "APPLICATION DETAILS")     |
| monospace      | system  | "KES 500,000" requested limit value                        |

---

*Generated by /idea export | 2026-05-25*
