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

The KYC Document Review screen is the field officer's primary interface for verifying customer identity documents and completing regulatory compliance checks. Accessed from Customer Detail or Meetings after scheduling an in-person or virtual review session, it presents all uploaded KYC artefacts for customer John Mwangi in a scrollable detail layout. The officer reviews National ID (front/back), a selfie/liveness check, and optional proof of address, selects a risk level (Low/Medium/High/Declined), optionally enters a rejection reason, then approves or rejects via four OBP KYC API calls. On approval the officer is taken back to customer-detail; on rejection a banner is shown inline.

---

## Screens

| ID               | Name             | Route                              | Layout | Scroll   |
|------------------|------------------|------------------------------------|--------|----------|
| kyc-review-main  | KYC Verification | /customers/{customerId}/kyc-review | Column | Vertical |

**Shell:** fieldOfficer flavor — Top app bar with back arrow. No bottom navigation on this detail screen.

| Nav Item     | ID                | Icon        | Target               |
|--------------|-------------------|-------------|----------------------|
| Dashboard    | nav_dashboard     | dashboard   | fo-dashboard         |
| Customers    | nav_customers     | people      | customer-search      |
| Applications | nav_applications  | description | account-applications |
| Messages     | nav_messages      | mail        | customer-messages    |
| More         | nav_more          | more_vert   | settings             |

---

## Components

| ID                        | Type   | Description                                                                                                                                     |
|---------------------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| customer_mini_header      | box    | Green header band (`#4C662B`), 16dp vertical padding. Contains horizontal stack: 40×40 white avatar circle (initials "JM", label_large `#4C662B` bold) + vertical group: "John Mwangi" (title_medium, `#FFFFFF`, weight 700) / "KYC Review Required" (body_small, `#CDEDA3`) |
| kyc_status_badge_row      | box    | Horizontal row, 14dp top padding. "KYC Status:" (body_medium, `#44483D`, weight 500) + chip: `#CDEDA3` bg, 16dp radius, 1dp `#E8A317` border, "In Progress" (label_medium, `#44483D`, weight 600) |
| documents_section_heading | text   | "Documents" — title_medium, `#1A1C16`, heading level 2, 8dp vertical padding, 16dp horizontal padding                                         |
| doc_national_id_front     | box    | White card (`#FFFFFF`, 10dp radius, 14dp padding, 1dp `#E1E4D5` border, elevation 1). Row: 56×40 thumbnail (6dp radius, cover) + "National ID — Front" (body_large, `#1A1C16`, bold) + "Uploaded ✓ · 22 May 2026" (body_small, `#4C662B`) + "View" link (label_medium, `#4C662B`, underline) |
| doc_national_id_back      | box    | White card. Row: 56×40 placeholder (`#F9FAEF`, 1dp `#E1E4D5`, image_not_supported icon `#44483D` 20dp) + "National ID — Back" (body_large, bold) + "Pending Upload" (body_small, `#44483D`) |
| doc_selfie                | box    | White card. Row: 56×40 circular selfie thumbnail (28dp radius, 2dp `#4C662B` border) + "Selfie / Liveness Check" (body_large, bold) + "Passed ✓ · 22 May 2026" (body_small, `#4C662B`) |
| doc_proof_of_address      | box    | White card. Row: 56×40 placeholder (home icon `#44483D` 20dp) + "Proof of Address (Optional)" (body_large, bold) + "Not uploaded" (body_small, `#44483D`) + "Upload" outlined button (`#386663` border/text, label_small) |
| risk_section_heading      | text   | "Risk Assessment" — title_medium, `#1A1C16`, heading level 2, 16dp horizontal padding                                                         |
| risk_level_select         | input  | Outlined select dropdown, 16dp margin horizontal. Options: Low / Medium / High / Declined. Label: "Risk Level"                                  |
| rejection_reason_input    | input  | Outlined textarea (3–6 lines), placeholder "Explain why KYC cannot be approved — e.g. National ID does not match selfie, blurry documents, suspected fraud…", conditionally visible when risk = Declined |
| approve_kyc_button        | button | Filled, `#4C662B` bg, `#FFFFFF` text, full-width — "Approve KYC". On tap: PUT kyc_check + PUT kyc_statuses → navigate customer-detail          |
| reject_kyc_button         | button | Outlined, `#BA1A1A` border/text, full-width — "Reject KYC". On tap: PUT kyc_check (satisfied:false) + PUT kyc_statuses (ok:false)              |
| request_more_docs_button  | button | Text button, `#4C662B` text — "Request More Documents". Navigates to customer-messages                                                          |

---

## States

| ID        | Trigger                             | Description                                                                   |
|-----------|-------------------------------------|-------------------------------------------------------------------------------|
| loading   | Screen entry                        | Shimmer skeletons over document cards; action buttons disabled                |
| reviewing | Documents loaded                    | All 4 document cards, risk selector, and action row visible; bg `#F9FAEF`    |
| verifying | "Approve KYC" tapped                | Progress overlay "Verifying documents…" while PUT calls in flight             |
| approved  | PUT kyc_statuses returns ok=true    | Success banner; approve button disabled; auto-navigate to customer-detail     |
| rejected  | PUT kyc_statuses returns ok=false   | Rejection banner shown with officer-entered reason                            |
| content   | Loaded state alias                  | Same layout as reviewing; canonical loaded state                              |
| empty     | Customer has zero KYC documents     | Empty state: "No KYC documents to review"                                     |
| error     | Network or auth failure             | Error banner with retry button; 16dp padding                                  |

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

**Actions:** `approve_kyc()`, `reject_kyc()`, `request_more_docs()`, `view_document(docId: String)`, `select_risk_level(level: RiskLevel)`

**DI Dependencies:** `KycRepository`, `CustomerMessagingService`

**Errors:**
- `APPROVAL_FAILED`: "KYC approval failed. Please try again."
- `REJECTION_FAILED`: "KYC rejection failed. Please try again."
- `DOCUMENT_LOAD_FAILED`: "Could not load KYC documents."
- `NETWORK_UNAVAILABLE`: "No network connection. Please check and retry."

---

## Navigation

| From       | To               | Trigger                                    | Type |
|------------|------------------|--------------------------------------------|------|
| kyc-review | customer-detail  | approve_kyc_button tap (on API success)    | pop  |
| kyc-review | customer-messages| request_more_docs_button tap               | push |
| kyc-review | kyc-review       | reject_kyc_button tap (rejection banner inline) | — |
| kyc-review | customer-detail  | Top app bar back arrow                     | pop  |

---

## API Endpoints

| Endpoint                                                                              | Auth        | Tag | Purpose                                      |
|---------------------------------------------------------------------------------------|-------------|-----|----------------------------------------------|
| GET /obp/v5.1.0/customers/{customerId}/kyc_documents                                  | DirectLogin | KYC | Fetch all KYC documents for customer         |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}      | DirectLogin | KYC | Update document status (is_valid)            |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}         | DirectLogin | KYC | Record officer's KYC check result            |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses                    | DirectLogin | KYC | Append final KYC pass/fail status            |

---

## Design Tokens

| Token                         | Value     | Usage                                                               |
|-------------------------------|-----------|---------------------------------------------------------------------|
| color.light.primary           | #4C662B   | Header band, avatar initials, verified doc status text, approve button, selfie border, View link, Request More Docs text |
| color.light.primary_container | #CDEDA3   | KYC status chip background                                          |
| color.pending                 | #E8A317   | KYC status chip border accent                                       |
| color.light.secondary         | #386663   | Upload proof of address outlined button border/text                 |
| color.light.error             | #BA1A1A   | Reject KYC button border/text                                       |
| color.light.surface           | #FFFFFF   | Document cards background                                           |
| color.light.background        | #F9FAEF   | Screen background, document placeholder fill                        |
| color.light.on_surface        | #1A1C16   | Document card titles, section headings                              |
| color.light.on_surface_variant| #44483D   | KYC Status label, pending/optional status text, captions            |
| color.light.outline_variant   | #E1E4D5   | Document card borders, placeholder borders                          |
| color.light.on_primary        | #FFFFFF   | Approve button text, header customer name                           |
| typography.title_medium       | —         | Documents section heading, Risk Assessment heading                  |
| typography.body_large         | —         | Document card titles                                                |
| typography.body_medium        | —         | KYC Status label                                                    |
| typography.body_small         | —         | Document upload date/status, selfie date                            |
| typography.label_medium       | —         | KYC status chip text                                                |
| typography.label_small        | —         | Upload outlined button text                                         |
| spacing.md                    | 16dp      | Horizontal padding throughout, card margin                          |
| spacing.sm                    | 8dp       | Chip padding-vertical, card margin-bottom                           |
| radius.md                     | 12dp      | Card border-radius (10dp per source — closest token)                |

---

_Generated by /idea export | 2026-05-29_
