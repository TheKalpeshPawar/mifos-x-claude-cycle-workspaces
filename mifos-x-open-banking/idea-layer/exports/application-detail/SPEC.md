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

The Application Detail screen is the Field Officer's primary review surface for a pending account application. It presents the full application record — reference number, status chip, applicant identity, account type, requested credit limit, stated purpose, KYC verification status, and supporting document thumbnails — in a scrollable detail layout (#F9FAEF background). Officers can add internal review notes via an outlined textarea, then approve, reject, or request additional information from the applicant. Approve navigates back to Customer Detail; Request Information opens a Customer Messages thread with the applicant; Reject updates the application status in-place and shows a rejection banner. The screen uses a field-officer detail flow (top app bar with back navigation, no bottom nav bar). Data is loaded from two OBP Account-Applications endpoints on screen entry.

---

## Screens

| ID                       | Name                 | Route               | Layout | Scroll   |
|--------------------------|----------------------|---------------------|--------|----------|
| application-detail-main  | Application Review   | /application-detail | Column | Vertical |

**Shell:** Top app bar ("Application Detail") with back arrow. No bottom navigation bar (fieldOfficer detail flow).

---

## Components

| ID                        | Type    | Description                                                                                                       |
|---------------------------|---------|-------------------------------------------------------------------------------------------------------------------|
| application_header        | box     | Full-width #4C662B header, 16dp vertical + horizontal padding; contains reference number and status/date meta row  |
| app_reference_number      | text    | "Application #OBP-2026-00234" — Outfit/title_large (22sp/400), #FFFFFF, weight 700, margin-bottom 6dp            |
| app_header_meta           | stack   | Horizontal row, align-items center, 10dp gap — contains status chip + submitted date                              |
| app_status_chip           | box     | #CDEDA3 fill, radius 12dp, 8dp horizontal + 4dp vertical padding — current status indicator                       |
| app_status_text           | text    | "Pending Review" — Outfit/label_small (11sp/500), #44483D, weight 600 (WCAG AA on #CDEDA3: ≥7.25:1)              |
| app_submitted_date        | text    | "Submitted: 20 May 2026" — Outfit/body_small (12sp/400), #CDEDA3                                                 |
| customer_info_card        | box     | White card, radius 12dp, elevation 2, 16dp padding, 16dp horizontal margin, 16dp top margin, 8dp bottom margin    |
| customer_card_heading     | text    | "Customer" — Outfit/label_medium (12sp/500), #44483D, uppercase, letter-spacing 0.8, margin-bottom 6dp           |
| customer_info_row         | stack   | Horizontal, space-between, align-center — customer name + view profile link                                       |
| customer_name             | text    | "John Kamau Mwangi" — Outfit/title_medium (16sp/500), #1A1C16, weight 700                                        |
| customer_profile_link     | link    | "View Profile" — Outfit/label_medium (12sp/500), #4C662B, underline; navigates to customer-detail                |
| application_details_card  | box     | White card, radius 12dp, elevation 2, 16dp padding, 16dp horizontal margin, 8dp bottom margin                     |
| app_details_heading       | text    | "Application Details" — Outfit/label_medium (12sp/500), #44483D, uppercase, letter-spacing 0.8                   |
| account_type_row          | stack   | Horizontal, space-between — label "Account Type" + value "KCB Savings Account"                                    |
| account_type_label        | text    | "Account Type" — Outfit/body_medium (14sp/400), #44483D                                                          |
| account_type_value        | text    | "KCB Savings Account" — Outfit/body_medium (14sp/400), #1A1C16, weight 600                                       |
| requested_limit_row       | stack   | Horizontal, space-between — label "Requested Limit" + value "KES 500,000"                                         |
| limit_label               | text    | "Requested Limit" — Outfit/body_medium (14sp/400), #44483D                                                       |
| limit_value               | text    | "KES 500,000" — Outfit/body_medium (14sp/400), #1A1C16, weight 600, font-family monospace                        |
| purpose_row               | stack   | Vertical, 4dp gap — label "Purpose" above value "Personal savings and salary credit"                              |
| purpose_label             | text    | "Purpose" — Outfit/body_medium (14sp/400), #44483D                                                               |
| purpose_value             | text    | "Personal savings and salary credit" — Outfit/body_medium (14sp/400), #1A1C16                                    |
| kyc_status_row            | box     | #CDEDA3 fill, radius 12dp, 1px #4C662B border, 14dp padding, 16dp horizontal margin, 8dp bottom margin           |
| kyc_row_stack             | stack   | Horizontal, align-center, 8dp gap — icon + status label                                                          |
| kyc_verified_icon         | icon    | verified_user, 20dp, #4C662B; supports idle/hover/focus_visible/pressed/disabled states                           |
| kyc_status_label          | text    | "KYC Status: Verified ✓" — Outfit/body_medium (14sp/400), #4C662B, weight 600                                    |
| documents_heading         | text    | "Supporting Documents" — Outfit/title_medium (16sp/500), #1A1C16, role heading level 2, 16dp all-side padding     |
| doc_national_id_card      | box     | White card, radius 10dp, elevation 1, 1px #E1E4D5 border, 14dp padding, 16dp horizontal margin, 8dp bottom margin |
| doc_id_row                | stack   | Horizontal, align-center, 12dp gap — thumbnail + info box + view link                                             |
| doc_id_thumbnail          | image   | 56×40dp, radius 6dp, cover fit, 1px #4C662B border — National ID scan thumbnail                                  |
| doc_id_title              | text    | "National ID" — Outfit/body_large (16sp/400), #1A1C16, weight 600, margin-bottom 2dp                             |
| doc_id_status             | text    | "Verified ✓" — Outfit/body_small (12sp/400), #4C662B                                                             |
| doc_id_view_link          | link    | "View" — Outfit/label_medium (12sp/500), #4C662B, underline; triggers view_document(national_id_doc)             |
| doc_proof_address_card    | box     | White card, radius 10dp, elevation 1, 1px #E1E4D5 border, 14dp padding, 16dp horizontal margin, 16dp bottom margin|
| doc_address_row           | stack   | Horizontal, align-center, 12dp gap — placeholder box + info box + upload button                                   |
| doc_address_placeholder   | box     | 56×40dp, radius 6dp, #F9FAEF fill, 1px #E8A317 border, center-aligned home icon                                  |
| doc_address_icon          | icon    | home, 20dp, #44483D (A11Y fix: was #E8A317 ≤2.17:1 FAIL; #44483D ≥7.25:1 PASS)                                  |
| doc_address_title         | text    | "Proof of Address" — Outfit/body_large (16sp/400), #1A1C16, weight 600, margin-bottom 2dp                        |
| doc_address_status        | text    | "Pending Upload" — Outfit/body_small (12sp/400), #44483D (A11Y fix applied)                                      |
| upload_address_doc_button | button  | "Upload" — outlined, #4C662B border + text, 8dp horizontal + 4dp vertical padding, label_small; triggers upload_document(proof_of_address) |
| review_notes_input        | input   | "Review Notes" — outlined textarea, 3–6 lines, 16dp horizontal margin, 16dp bottom margin; placeholder: "Add internal notes about this application — e.g. income verified via payslip, employer confirmed, recommend approval…" |
| approve_application_button| button  | "Approve Application" — filled #4C662B, #FFFFFF text, full-width, pill radius, 16dp horizontal margin; triggers approve_application → navigates to customer-detail |
| reject_application_button | button  | "Reject Application" — outlined #BA1A1A border + text, full-width, pill radius, 16dp horizontal margin; triggers reject_application |
| request_info_button       | button  | "Request Information" — text #4C662B, 16dp horizontal margin, 24dp bottom margin; triggers request_info → navigates to customer-messages |

---

## States

| ID        | Trigger                                | Description                                                                               |
|-----------|----------------------------------------|-------------------------------------------------------------------------------------------|
| loading   | Screen entry / data fetch              | Skeleton shimmer over header, cards, document rows; motion shimmer_duration short4 (200ms); no interactive elements; reduced_motion_fallback: static_placeholder |
| content   | Data load success                      | All components visible; alias for reviewing state — same layout, default loaded alias     |
| reviewing | Application loaded, decision pending   | Full layout — header, customer card, application card, KYC row, documents, review notes, action buttons |
| approved  | approve_application success            | #CDEDA3 success banner "Application approved successfully" shown above layout; action buttons disabled |
| rejected  | reject_application success             | Rejection banner (#FFDAD6/#BA1A1A) shown above layout; action buttons disabled            |
| empty     | Application record not found           | "Application details not available" centred, 16dp padding, no action buttons              |
| error     | Network or auth failure                | Error banner + "Try Again" retry button centred; error_outline icon 48dp #BA1A1A          |

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

**ApplicationDecision values:** `PENDING`, `APPROVED`, `REJECTED`

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

| From               | To                | Trigger                           | Type |
|--------------------|-------------------|-----------------------------------|------|
| application-detail | customer-detail   | customer_profile_link tap         | push |
| application-detail | customer-detail   | approve_application_button tap    | pop  |
| application-detail | application-detail| reject_application_button tap     | inline (state change) |
| application-detail | customer-messages | request_info_button tap           | push |

---

## API Endpoints

| Endpoint                                                                       | Auth        | Tag                  | Purpose                                          |
|--------------------------------------------------------------------------------|-------------|----------------------|--------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}           | DirectLogin | Account-Applications | Load application record, customer identity, status, account routing |
| PUT /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}           | DirectLogin | Account-Applications | Submit approval (APPROVED) or rejection (REJECTED) decision |

---

## Design Tokens

| Token                           | Value     | Usage                                                                           |
|---------------------------------|-----------|---------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Header fill, KYC banner border+icon+text, status/view/upload links, approve button fill, verified icon |
| colors.light.primary_container  | #CDEDA3   | Status chip fill, KYC banner fill, submitted date text, success banner fill     |
| colors.light.on_primary         | #FFFFFF   | Header text, approve button text                                                |
| colors.light.error              | #BA1A1A   | Reject button border + text, error icon, rejection banner text                  |
| colors.light.error_container    | #FFDAD6   | Rejection banner background                                                     |
| colors.light.on_surface         | #1A1C16   | Customer name, document titles, application value fields                        |
| colors.light.on_surface_variant | #44483D   | Status chip text, section headings (uppercase), pending upload text, address icon (A11Y fix) |
| colors.light.surface            | #FFFFFF   | Customer info card, application details card, document cards                    |
| colors.light.surface_variant    | #E1E4D5   | Document card borders                                                           |
| colors.light.background         | #F9FAEF   | Screen background, address placeholder fill                                     |
| colors.light.pending            | #E8A317   | Proof of Address placeholder box border (pending upload indicator)              |
| typography.title_large          | Outfit 22sp/400 | Application reference number                                               |
| typography.title_medium         | Outfit 16sp/500 | Customer name, Supporting Documents heading                                |
| typography.body_large           | Outfit 16sp/400 | Document card titles (National ID, Proof of Address)                       |
| typography.body_medium          | Outfit 14sp/400 | Field labels + values throughout application details                       |
| typography.body_small           | Outfit 12sp/400 | Document status lines, submitted date                                      |
| typography.label_medium         | Outfit 12sp/500 | Section headings (uppercase), View + Upload link labels                    |
| typography.label_small          | Outfit 11sp/500 | Status chip text ("Pending Review")                                        |
| radius.md                       | 12dp      | Customer info card, application details card, KYC row, status chip         |
| radius.sm                       | 8dp       | Document card radius (10dp — between sm and md)                            |
| elevation.level1                | 1dp       | Document cards                                                              |
| elevation.level2                | 3dp       | Customer info card, application details card                                |
| spacing.md                      | 16dp      | Horizontal content padding, card margins                                   |
| spacing.sm                      | 8dp       | Gap between status chip and date; gap between KYC icon and label           |
| spacing.xs                      | 4dp       | Chip vertical padding; purpose row vertical gap                            |
| motion.duration.short4          | 200ms     | Loading shimmer animation duration                                         |

---

_Generated by /idea export | 2026-05-30_
