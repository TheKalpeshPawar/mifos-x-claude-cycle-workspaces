# Visual Specification — KYC Document Review

| Field   | Value                         |
|---------|------------------------------|
| Feature | kyc-review                   |
| Flavor  | fieldOfficer                 |

---

## Screen Layout

Detail screen with a branded colored header, scrollable document list, risk assessment section, and action buttons at the bottom:

```
[ customer_mini_header — deep purple full-width bar ]
[ kyc_status_badge_row — "KYC Status: [In Progress]" chip ]
[ documents_section_heading — "Documents" ]
[ doc_national_id_front — card with thumbnail ]
[ doc_national_id_back — card with placeholder ]
[ doc_selfie — card with circular photo thumbnail ]
[ doc_proof_of_address — card with Upload button ]
[ risk_section_heading — "Risk Assessment" ]
[ risk_level_select — Low / Medium / High / Declined ]
[ rejection_reason_input — conditionally visible textarea ]
[ approve_kyc_button — green filled ]
[ reject_kyc_button — red outlined ]
[ request_more_docs_button — text button ]
```

---

## Components

### customer_mini_header

Full-width deep purple bar (#1800B1, paddingVertical 16, paddingHorizontal 16, borderRadius 0 — edge-to-edge). Contains horizontal stack with avatar circle and text group.

**customer_avatar** — 40×40dp white circle (borderRadius 24), centered content:
- "JM" in label_large, color #1800B1, weight 700 — initials of "John Mwangi"

**header_customer_name** — "John Mwangi" in title_medium, white, weight 700

**header_kyc_label** — "KYC Review Required" in body_small, color #B0B8FF (muted lavender on purple)

### kyc_status_badge_row

Horizontal row (paddingHorizontal 16, paddingTop 14, paddingBottom 8, gap 8):
- "KYC Status:" label in body_medium, #666666, weight 500
- Amber chip: bg #FFF8E1, border #FFB300, borderRadius 16, paddingHorizontal 12, paddingVertical 4
  - "In Progress" in label_medium, color #E65100, weight 600

### Document Cards

Each document card is a white box (borderRadius 10, padding 14, marginHorizontal 16, marginBottom 8, elevation 1, border #E0E0E0). Internal layout: horizontal stack (gap 12) of thumbnail + info column + optional action.

**doc_national_id_front** (uploaded):
- Thumbnail: 56×40dp image, borderRadius 6, objectFit cover — shows front of ID
- Info: "National ID — Front" (body_large, weight 600) + "Uploaded ✓ · 22 May 2026" (body_small, #4CAF50)
- "View" link (label_medium, #1800B1, underlined)

**doc_national_id_back** (pending):
- Placeholder: 56×40dp grey box (#F5F5F5), centered image_not_supported icon (size 20, #BDBDBD)
- Info: "National ID — Back" (body_large, weight 600) + "Pending Upload" (body_small, #FF8F00)
- No view link

**doc_selfie** (passed):
- Thumbnail: 56×40dp circular (borderRadius 28), green border (2px, #4CAF50), objectFit cover — selfie photo
- Info: "Selfie / Liveness Check" (body_large, weight 600) + "Passed ✓ · 22 May 2026" (body_small, #4CAF50)
- No action button

**doc_proof_of_address** (optional, not uploaded):
- Placeholder: 56×40dp grey box, centered home icon (size 20, #BDBDBD)
- Info: "Proof of Address (Optional)" (body_large, weight 600) + "Not uploaded" (body_small, #999999)
- "Upload" button: outlined, border #008B8B, text #008B8B, paddingHorizontal 12, paddingVertical 6, label_small

### risk_section_heading + risk_level_select

"Risk Assessment" heading (title_medium, #1A1A1A, paddingHorizontal 16, paddingBottom 8), followed by dropdown:
- Risk Level select: outlined variant, options Low | Medium | High | Declined
- Selecting "Declined" triggers conditional display of rejection_reason_input

### rejection_reason_input

Outlined textarea (minLines 3, maxLines 6, marginHorizontal 16, marginBottom 16). Visible only when risk = Declined or reject tapped.
Placeholder: "Explain why KYC cannot be approved — e.g. National ID does not match selfie, blurry documents, suspected fraud..."

### Action Buttons

- **approve_kyc_button**: filled, bg #4CAF50, white text, full width, marginHorizontal 16, marginBottom 8
- **reject_kyc_button**: outlined, border #FF5252, text #FF5252, full width, marginHorizontal 16, marginBottom 8
- **request_more_docs_button**: text variant, color #1800B1, marginHorizontal 16, marginBottom 24

---

## Interaction Patterns

- **Risk level selection**: Tap dropdown → choose Low/Medium/High/Declined. On "Declined", rejection_reason_input slides in below the dropdown with smooth expand animation
- **View document**: Tap "View" link on doc_national_id_front → open full-screen document viewer
- **Upload proof of address**: Tap "Upload" button on doc_proof_of_address → file picker (can upload mid-review)
- **Approve KYC**: Tap "Approve KYC" → confirm dialog ("Approve KYC for John Mwangi?") → verifying overlay → PUT kyc_check (satisfied: true) + PUT kyc_statuses (ok: true) → success banner → navigate to customer-detail
- **Reject KYC**: Tap "Reject KYC" → validates rejectionReason not empty → verifying overlay → PUT kyc_check (satisfied: false) + PUT kyc_statuses (ok: false) → rejection banner stays on screen
- **Request More Documents**: Tap text button → navigate to customer-messages with pre-filled template about missing documents

---

## Content Data

| Field                    | Sample Value               |
|--------------------------|----------------------------|
| Customer name            | John Mwangi                |
| Avatar initials          | JM                         |
| KYC Status               | In Progress                |
| ID Front upload date     | 22 May 2026                |
| ID Front status          | Uploaded ✓                 |
| ID Back status           | Pending Upload             |
| Selfie status            | Passed ✓ · 22 May 2026     |
| Proof of Address status  | Not uploaded               |
| Rejection reason example | "National ID does not match selfie, blurry documents, suspected fraud" |

---

## Design Notes

**Color Usage:**
- Deep purple #1800B1 for the customer header creates strong visual separation from the document review zone below
- #B0B8FF (light lavender) for "KYC Review Required" subtitle — visible on purple without full white contrast
- Green #4CAF50 for approve button and document verified states — consistent semantic signal throughout the app
- Red #FF5252 for reject button — less alarming than error red (#BA1A1A) since this is a deliberate officer action, not a system failure
- Teal #008B8B for the optional proof-of-address upload — same teal used for optional/biometric actions across the app
- Amber #E65100 for "In Progress" chip — matches the status chip design pattern from account-applications

**Typography:**
- Document card titles: body_large weight 600 — heavier than status lines to establish hierarchy
- Document status lines: body_small — subdued to let status color communicate state
- "View" and "Upload" action text: label_medium/label_small — compact inline actions

**Spacing:**
- Header is edge-to-edge (borderRadius 0), other cards have borderRadius 10-16
- 16dp marginHorizontal on all cards and inputs for consistent gutters
- 8dp marginBottom between document cards; 16dp before risk section
- 24dp marginBottom after the last text button — breathing room above system navigation

**Accessibility:**
- customer_mini_header has full contentDescription: "Customer: John Mwangi — KYC Review Required"
- kyc_status_chip role: status — announces value changes when risk selection changes status
- rejection_reason_input describes itself as "required when rejecting"
- Approve button: "Approve KYC for this customer"
- Selfie circular crop uses borderColor green to visually indicate pass status (also conveyed in text)

*Generated by /idea export | 2026-05-25*
