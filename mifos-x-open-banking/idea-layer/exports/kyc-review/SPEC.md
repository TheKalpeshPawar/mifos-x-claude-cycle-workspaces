# Feature Specification — KYC Document Review

| Field         | Value                          |
|---------------|-------------------------------|
| Feature       | kyc-review                    |
| Flavor        | fieldOfficer                  |
| Status        | enriched                      |
| Quality Score | 83                            |

---

## Overview

The KYC Document Review screen allows a Field Officer to examine customer identity documents and make an approval or rejection decision. The screen displays the customer's uploaded documents (National ID front/back, selfie/liveness, optional proof of address) each with their upload status. The officer selects a risk level, optionally enters a rejection reason, and either approves (PUT kyc_check + PUT kyc_statuses → navigate to customer-detail) or rejects (updates status, shows rejection banner) or requests more documents (navigates to customer-messages).

---

## Screens

| Screen ID       | Route                                  | Layout        | Scroll   |
|-----------------|----------------------------------------|---------------|----------|
| kyc-review-main | /customers/{customerId}/kyc-review     | detail_screen | vertical |

---

## Components

| ID                         | Type    | Description                                                                 |
|----------------------------|---------|-----------------------------------------------------------------------------|
| customer_mini_header       | box     | Deep purple header bar with customer avatar initials + name + "KYC Review Required" label |
| customer_avatar            | box     | 40×40dp white circle with "JM" initials in primary purple, label_large     |
| header_customer_name       | text    | "John Mwangi" — title_medium, white, weight 700                            |
| header_kyc_label           | text    | "KYC Review Required" — body_small, #B0B8FF                                |
| kyc_status_badge_row       | box     | Horizontal row: "KYC Status:" label + status chip                          |
| kyc_status_chip            | box     | Amber chip (#FFF8E1, border #FFB300): "In Progress" in #E65100, weight 600 |
| documents_section_heading  | text    | "Documents" — title_medium, role heading level 2                           |
| doc_national_id_front      | box     | Document card: thumbnail + "National ID — Front", "Uploaded ✓ · 22 May 2026" in green, View link |
| doc_national_id_back       | box     | Document card: placeholder icon + "National ID — Back", "Pending Upload" in amber |
| doc_selfie                 | box     | Document card: circular thumbnail with green border + "Selfie / Liveness Check", "Passed ✓ · 22 May 2026" |
| doc_proof_of_address       | box     | Document card: home icon placeholder + "Proof of Address (Optional)", "Not uploaded", Upload button |
| risk_section_heading       | text    | "Risk Assessment" — title_medium, role heading level 2                     |
| risk_level_select          | input   | Dropdown: Low, Medium, High, Declined                                      |
| rejection_reason_input     | input   | Textarea (conditionalVisible — shown when risk_level = Declined or reject tapped), 3-6 lines |
| approve_kyc_button         | button  | Filled green (#4CAF50) "Approve KYC" — navigates to customer-detail        |
| reject_kyc_button          | button  | Outlined red (border/text #FF5252) "Reject KYC" — updates KYC status       |
| request_more_docs_button   | button  | Text button, #1800B1 "Request More Documents" — navigates to customer-messages |

---

## States

| ID         | Trigger                                   | Description                                                       |
|------------|-------------------------------------------|-------------------------------------------------------------------|
| loading    | Screen open                               | Shimmer skeleton while fetching KYC documents from API            |
| reviewing  | Data loaded                               | Full document list + risk assessment form visible, bg #F5F5F5     |
| verifying  | Approve/Reject tapped                     | Progress overlay: "Verifying documents..."                        |
| approved   | OBP kyc_check + kyc_statuses succeed      | Success banner, KYC Status chip updates to "Verified"            |
| rejected   | Rejection confirmed with reason           | Rejection banner shown, status chip updates to "Rejected"        |
| error      | API call fails                            | Error banner with retry option                                    |

---

## State Model

**ViewModel:** `KycReviewViewModel`

| State Field        | Type                     | Default | Values               |
|--------------------|--------------------------|---------|----------------------|
| customerId         | String                   | —       | —                    |
| kycStatus          | KycStatus                | —       | IN_PROGRESS, VERIFIED, REJECTED |
| documents          | List\<KycDocument\>      | —       | —                    |
| riskLevel          | RiskLevel (nullable)     | null    | LOW, MEDIUM, HIGH, DECLINED |
| rejectionReason    | String (nullable)        | null    | —                    |
| showRejectionField | Boolean                  | false   | —                    |
| isVerifying        | Boolean                  | false   | —                    |

**Events:** KycApproved, KycRejected, MoreDocsRequested, DocumentViewed, RiskLevelChanged

**Actions:** approve_kyc, reject_kyc, request_more_docs, view_document, select_risk_level

**DI Dependencies:** KycRepository, CustomerMessagingService

**Errors:** APPROVAL_FAILED, REJECTION_FAILED, DOCUMENT_LOAD_FAILED, NETWORK_UNAVAILABLE

---

## Navigation

| From        | To                  | Trigger                   | Type     |
|-------------|---------------------|---------------------------|----------|
| kyc-review  | customer-detail     | Approve KYC               | navigate |
| kyc-review  | kyc-review          | Reject KYC (stays, banner)| refresh  |
| kyc-review  | customer-messages   | Request More Documents    | navigate |

---

## API Endpoints

| Endpoint                                                                                  | Auth        | Purpose                                          |
|-------------------------------------------------------------------------------------------|-------------|--------------------------------------------------|
| GET /obp/v5.1.0/customers/{customerId}/kyc_documents                                      | DirectLogin | Load all KYC documents for the customer          |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}          | DirectLogin | Update individual document status (is_valid)     |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}              | DirectLogin | Record officer's KYC check (satisfied + how)     |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses                        | DirectLogin | Set final KYC status (ok: true/false, appends)  |

---

## Design Tokens

| Token          | Value   | Usage                                            |
|----------------|---------|--------------------------------------------------|
| primary        | #1800B1 | Header background, avatar initials, Upload chip, Request More Docs text |
| on_primary     | #FFFFFF | Header text, avatar circle                       |
| success        | #4CAF50 | Approve KYC button, doc verified status text, selfie border |
| error_action   | #FF5252 | Reject KYC button border and text               |
| error          | #BA1A1A | System error messages                            |
| warning_bg     | #FFF8E1 | KYC Status "In Progress" chip background        |
| warning_border | #FFB300 | Status chip border                              |
| warning_text   | #E65100 | Status chip text, risk/rejection context        |
| avatar_label   | #B0B8FF | "KYC Review Required" subtitle in header        |
| surface        | #FFFFFF | Document cards                                  |
| background     | #F5F5F5 | Screen background in reviewing state            |

---

*Generated by /idea export | 2026-05-25*
