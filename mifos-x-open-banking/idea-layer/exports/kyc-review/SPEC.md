# SPEC — KYC Document Review

| Field         | Value                  |
|---------------|------------------------|
| Feature       | kyc-review             |
| Flavor        | fieldOfficer           |
| Status        | approved               |
| Quality Score | 94                     |
| ViewModel     | KycReviewViewModel     |

---

## Overview

The KYC Document Review screen is the field officer's primary interface for verifying customer identity documents and completing regulatory compliance checks. Accessed from Customer Detail or the field-officer Meetings flow after scheduling an in-person or virtual review session, it presents all uploaded KYC artefacts for a customer (demo: John Mwangi) in a scrollable detail layout on a `#F9FAEF` earth-green background. The officer reviews up to four document cards — National ID front (uploaded, verified 22 May 2026), National ID back (pending upload), Selfie / Liveness Check (passed 22 May 2026), and Proof of Address (optional, not yet uploaded) — then selects a risk level (Low / Medium / High / Declined) via an outlined select dropdown. When risk is Declined a rejection-reason textarea appears conditionally. The officer completes the review by tapping "Approve KYC" (issues PUT kyc_check + PUT kyc_statuses → navigate back to customer-detail) or "Reject KYC" (same two PUTs, satisfied/ok=false → inline rejection banner). A "Request More Documents" text button navigates to customer-messages. All four OBP API calls (GET documents + PUT document update + PUT kyc_check + PUT kyc_statuses) are coordinated by KycReviewViewModel via KycRepository.

---

## Screens

| ID               | Name             | Route                              | Layout | Scroll   |
|------------------|------------------|------------------------------------|--------|----------|
| kyc-review-main  | KYC Verification | /customers/{customerId}/kyc-review | Column | Vertical |

**Shell:** fieldOfficer flavor — Top app bar with back arrow. No bottom navigation bar on this detail screen.

| Nav Item     | ID                | Icon        | Target               |
|--------------|-------------------|-------------|----------------------|
| Dashboard    | nav_dashboard     | dashboard   | fo-dashboard         |
| Customers    | nav_customers     | people      | customer-search      |
| Applications | nav_applications  | description | account-applications |
| Messages     | nav_messages      | mail        | customer-messages    |
| More         | nav_more          | more_vert   | settings             |

---

## Components

| ID                        | Type   | Description                                                                                                                                                                                                              |
|---------------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer_mini_header      | box    | Full-width header band, `#4C662B` fill, 16dp vertical padding, 16dp horizontal padding, 0dp radius. Horizontal stack (12dp gap, center-aligned): 40×40 white avatar circle (`#FFFFFF`, 24dp radius) with initials "JM" (label_large `#4C662B`, weight 700); vertical group: "John Mwangi" (title_medium `#FFFFFF`, weight 700) + "KYC Review Required" (body_small `#CDEDA3`). A11y: "Customer: John Mwangi — KYC Review Required" |
| kyc_status_badge_row      | box    | Horizontal row, 16dp horizontal padding, 14dp top / 8dp bottom padding, 8dp gap. "KYC Status:" text (body_medium, `#44483D`, weight 500) + status chip: `#CDEDA3` bg, 16dp radius, 1dp `#E8A317` border, "In Progress" (label_medium `#44483D`, weight 600). A11y role: status |
| documents_section_heading | text   | "Documents" — title_medium, `#1A1C16`, heading level 2, 8dp vertical / 16dp horizontal padding                                                                                                                           |
| doc_national_id_front     | box    | White card (`#FFFFFF`, 10dp radius, 14dp padding, 1dp `#E1E4D5` border, elevation 1, 16dp horizontal margin, 8dp bottom margin). Horizontal row (12dp gap): 56×40 thumbnail image (6dp radius, cover fit) + flex column: "National ID — Front" (body_large `#1A1C16`, weight 600) + "Uploaded ✓ · 22 May 2026" (body_small `#4C662B`); right-aligned "View" link (label_medium `#4C662B`, underline, action: view_document → kyc_id_front) |
| doc_national_id_back      | box    | White card (same dimensions). Horizontal row: 56×40 placeholder (`#F9FAEF`, 1dp `#E1E4D5`, image_not_supported icon `#44483D` 20dp) + flex column: "National ID — Back" (body_large `#1A1C16`, weight 600) + "Pending Upload" (body_small `#44483D`). No action link.                                                                           |
| doc_selfie                | box    | White card. Horizontal row: 56×40 circular selfie thumbnail (28dp radius, 2dp `#4C662B` border, cover fit) + flex column: "Selfie / Liveness Check" (body_large `#1A1C16`, weight 600) + "Passed ✓ · 22 May 2026" (body_small `#4C662B`). No action link.                                                                                         |
| doc_proof_of_address      | box    | White card, 16dp bottom margin. Horizontal row: 56×40 placeholder (home icon `#44483D` 20dp) + flex column: "Proof of Address (Optional)" (body_large `#1A1C16`, weight 600) + "Not uploaded" (body_small `#44483D`); right-aligned "Upload" outlined button (`#386663` border/text, label_small, action: view_document → proof_of_address)           |
| risk_section_heading      | text   | "Risk Assessment" — title_medium, `#1A1C16`, heading level 2, 16dp horizontal padding, 8dp bottom padding                                                                                                               |
| risk_level_select         | input  | Outlined select dropdown, 16dp horizontal margin, 8dp bottom margin. Label: "Risk Level". Options: Low / Medium / High / Declined. Action: select_risk_level. A11y role: spinner                                          |
| rejection_reason_input    | input  | Outlined textarea (3–6 lines), 16dp horizontal margin, 16dp bottom margin. Placeholder: "Explain why KYC cannot be approved — e.g. National ID does not match selfie, blurry documents, suspected fraud…". Conditionally visible (shown when risk = Declined). A11y role: textField, label_source: visible_label                                                 |
| approve_kyc_button        | button | Filled, `#4C662B` bg, `#FFFFFF` text, full-width, 16dp horizontal margin, 8dp bottom margin — "Approve KYC". On tap: PUT kyc_check (satisfied:true) + PUT kyc_statuses (ok:true) → navigate to customer-detail. A11y: "Approve KYC for this customer"  |
| reject_kyc_button         | button | Outlined, `#BA1A1A` border/text, full-width, 16dp horizontal margin, 8dp bottom margin — "Reject KYC". On tap: PUT kyc_check (satisfied:false) + PUT kyc_statuses (ok:false) → inline rejection banner. A11y: "Reject KYC for this customer"                        |
| request_more_docs_button  | button | Text button, `#4C662B` text, 16dp horizontal margin, 24dp bottom margin — "Request More Documents". Navigates to customer-messages. A11y: "Request additional documents from the customer"                                |

---

## States

| ID        | Trigger                                          | Description                                                                                        |
|-----------|--------------------------------------------------|----------------------------------------------------------------------------------------------------|
| loading   | Screen entry                                     | Vertical scroll, 0dp padding. Shimmer skeletons replace document cards; action buttons disabled.   |
| reviewing | KYC documents loaded                             | All 4 document cards visible, risk selector and action buttons active. `#F9FAEF` background.       |
| verifying | "Approve KYC" tapped                             | Progress overlay "Verifying documents…" while PUT kyc_check and kyc_statuses in flight. `#F9FAEF`.|
| approved  | PUT kyc_statuses returns ok=true                 | Success banner shown; approve button disabled; auto-navigate to customer-detail. `#F9FAEF`.        |
| rejected  | PUT kyc_statuses returns ok=false                | Rejection banner shown inline with officer-entered reason. `#F9FAEF`.                              |
| content   | Alias for loaded state                           | Same layout as reviewing. `#F9FAEF`. Note: default loaded state alias.                             |
| empty     | Customer has zero KYC documents                  | 16dp padding. Empty state card: "No KYC documents to review". `#F9FAEF`.                           |
| error     | Network or auth failure / DOCUMENT_LOAD_FAILED   | 16dp padding. Error banner with retry button.                                                      |

---

## State Model

**ViewModel:** `KycReviewViewModel`
**Screen State Type:** `KycReviewScreenState`

| Name               | Type                | Default     |
|--------------------|---------------------|-------------|
| customerId         | String              | —           |
| kycStatus          | KycStatus           | IN_PROGRESS |
| documents          | List\<KycDocument\> | emptyList() |
| riskLevel          | RiskLevel?          | null        |
| rejectionReason    | String?             | null        |
| showRejectionField | Boolean             | false       |
| isVerifying        | Boolean             | false       |

**KycStatus values:** `IN_PROGRESS`, `VERIFIED`, `REJECTED`

**RiskLevel values:** `LOW`, `MEDIUM`, `HIGH`, `DECLINED`

**Events:** `KycApproved`, `KycRejected`, `MoreDocsRequested`, `DocumentViewed`, `RiskLevelChanged`

**Actions:** `approve_kyc()`, `reject_kyc()`, `request_more_docs()`, `view_document(docId: String)`, `select_risk_level(level: RiskLevel)`, `focus_field(field: String)`

**DI Dependencies:** `KycRepository`, `CustomerMessagingService`

**Errors:**
- `APPROVAL_FAILED`: "KYC approval failed. Please try again."
- `REJECTION_FAILED`: "KYC rejection failed. Please try again."
- `DOCUMENT_LOAD_FAILED`: "Could not load KYC documents."
- `NETWORK_UNAVAILABLE`: "No network connection. Please check and retry."

---

## Navigation

| From       | To                | Trigger                                         | Type |
|------------|-------------------|-------------------------------------------------|------|
| kyc-review | customer-detail   | approve_kyc_button tap (API ok=true)            | pop  |
| kyc-review | customer-messages | request_more_docs_button tap                    | push |
| kyc-review | kyc-review        | reject_kyc_button tap (rejection banner inline) | —    |
| kyc-review | customer-detail   | Top app bar back arrow                          | pop  |

---

## API Endpoints

| Endpoint                                                                              | Auth        | Tag | Purpose                                      |
|---------------------------------------------------------------------------------------|-------------|-----|----------------------------------------------|
| GET /obp/v5.1.0/customers/{customerId}/kyc_documents                                  | DirectLogin | KYC | Fetch all KYC documents for customer         |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}      | DirectLogin | KYC | Update individual document status (is_valid) |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}          | DirectLogin | KYC | Record officer's KYC check result            |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses                    | DirectLogin | KYC | Append final KYC pass/fail status            |

---

## Design Tokens

| Token                           | Value     | Usage                                                                                              |
|---------------------------------|-----------|----------------------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Header band fill, avatar initials color, verified doc status text, approve button bg, selfie thumbnail border, View link, Request More Docs text color |
| colors.light.primary_container  | #CDEDA3   | KYC status chip background                                                                         |
| colors.light.pending            | #E8A317   | KYC status chip border accent                                                                      |
| colors.light.secondary          | #386663   | Upload proof-of-address outlined button border/text                                                |
| colors.light.error              | #BA1A1A   | Reject KYC button border/text                                                                      |
| colors.light.surface            | #FFFFFF   | Document card backgrounds, customer avatar fill                                                    |
| colors.light.background         | #F9FAEF   | Screen background, document placeholder fill                                                       |
| colors.light.on_surface         | #1A1C16   | Document card titles ("National ID — Front" etc.), section headings                               |
| colors.light.on_surface_variant | #44483D   | "KYC Status:" label text, pending/not-uploaded status text, placeholder icons                     |
| colors.light.outline_variant    | #E1E4D5   | Document card borders, placeholder container borders                                               |
| colors.light.on_primary         | #FFFFFF   | Approve button text, header customer name text                                                     |
| typography.title_medium         | Outfit 16sp/500 | "Documents" + "Risk Assessment" section headings                                              |
| typography.body_large           | Outfit 16sp/400 | Document card titles, weight 600 applied                                                      |
| typography.body_medium          | Outfit 14sp/400 | "KYC Status:" label                                                                           |
| typography.body_small           | Outfit 12sp/400 | Document upload date/status, selfie date, "KYC Review Required" subhead                      |
| typography.label_large          | Outfit 14sp/500 | Avatar initials "JM"                                                                          |
| typography.label_medium         | Outfit 12sp/500 | KYC status chip text "In Progress"                                                            |
| typography.label_small          | Outfit 11sp/500 | "Upload" outlined button text                                                                 |
| spacing.md                      | 16dp      | Horizontal padding throughout, card horizontal margin, header padding                              |
| spacing.sm                      | 8dp       | Card bottom margin, chip padding-vertical, bottom margin between most elements                     |
| spacing.xs                      | 4dp       | Chip padding-vertical (chip uses sm=8 horizontal + xs=4 vertical)                                 |
| spacing.lg                      | 24dp      | Request More Docs button bottom margin                                                             |
| radius.pill                     | 999dp     | KYC status chip (16dp radius per source — nearest token: lg=16dp)                                 |
| elevation.level1                | 1dp       | Document cards                                                                                     |

---

_Generated by /idea export | 2026-05-30_
