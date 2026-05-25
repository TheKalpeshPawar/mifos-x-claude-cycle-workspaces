# Visual Specification — Application Detail

| Field   | Value                         |
|---------|------------------------------|
| Feature | application-detail           |
| Flavor  | fieldOfficer                 |

---

## Screen Layout

Detail screen with a branded purple header, two info cards, a KYC status indicator, a document section, review notes, and three action buttons at the bottom:

```
[ application_header — deep purple full-width bar ]
  [ "Application #OBP-2026-00234" — title_large white ]
  [ status chip "Pending Review" + submitted date ]

[ customer_info_card — white card ]
  [ "CUSTOMER" label ]
  [ "John Kamau Mwangi" — View Profile link ]

[ application_details_card — white card ]
  [ "APPLICATION DETAILS" label ]
  [ Account Type: KCB Savings Account ]
  [ Requested Limit: KES 500,000 (monospace) ]
  [ Purpose: Personal savings and salary credit ]

[ kyc_status_row — green row ]
  [ verified_user icon + "KYC Status: Verified ✓" ]

[ documents_heading — "Supporting Documents" ]
[ doc_national_id_card — verified ]
[ doc_proof_address_card — pending upload ]

[ review_notes_input — internal textarea ]
[ approve_application_button — green filled ]
[ reject_application_button — red outlined ]
[ request_info_button — purple text button ]
```

---

## Components

### application_header

Full-width deep purple bar (#1800B1, paddingVertical 18, paddingHorizontal 16).

**app_reference_number**: "Application #OBP-2026-00234" in title_large, white, weight 700, marginBottom 6. The reference number uses the full label style to clearly identify which application the officer is reviewing.

**app_header_meta**: Horizontal stack (gap 10) containing:
- Status chip: bg #FFF8E1, borderRadius 12, paddingHorizontal 10, paddingVertical 4
  - "Pending Review" in label_small, #E65100, weight 600
- "Submitted: 20 May 2026" in body_small, color #B0B8FF (lavender on purple — secondary metadata)

### customer_info_card

White card (borderRadius 12, padding 16, marginHorizontal 16, marginTop 16, marginBottom 10, elevation 2).

- "CUSTOMER" section label: label_medium, #999999, textTransform uppercase, letterSpacing 0.8, marginBottom 6
- Horizontal row (space-between, alignItems center):
  - "John Kamau Mwangi" — title_medium, weight 700, #1A1A1A
  - "View Profile" link — label_medium, #1800B1, underlined → navigates to customer-detail

### application_details_card

White card (borderRadius 12, padding 16, marginHorizontal 16, marginBottom 10, elevation 2).

- "APPLICATION DETAILS" section label: label_medium, #999999, uppercase, letterSpacing 0.8, marginBottom 10

Three rows:
1. **Account Type row** (horizontal, space-between, marginBottom 8):
   - Label: "Account Type" — body_medium, #666666
   - Value: "KCB Savings Account" — body_medium, weight 600, #1A1A1A

2. **Requested Limit row** (horizontal, space-between, marginBottom 8):
   - Label: "Requested Limit" — body_medium, #666666
   - Value: "KES 500,000" — body_medium, weight 600, #1A1A1A, fontFamily monospace (financial figure precision)

3. **Purpose row** (vertical, gap 4):
   - Label: "Purpose" — body_medium, #666666
   - Value: "Personal savings and salary credit" — body_medium, #1A1A1A

### kyc_status_row

Green row (bg #E8F5E9, borderRadius 12, padding 14, marginHorizontal 16, marginBottom 10, border 1px #4CAF50). Horizontal stack (gap 8):
- verified_user icon — size 20, color #4CAF50
- "KYC Status: Verified ✓" — body_medium, #2E7D32, weight 600

### documents_heading

"Supporting Documents" — title_medium, #1A1A1A, paddingHorizontal 16, paddingTop 8, paddingBottom 8. Role: heading level 2.

### doc_national_id_card (verified)

White card (borderRadius 10, padding 14, marginHorizontal 16, marginBottom 8, elevation 1, border #E0E0E0). Horizontal stack (gap 12):
- Thumbnail: 56×40dp, borderRadius 6, objectFit cover, borderWidth 1, borderColor #4CAF50 — green border signals verified
- Info column (flex 1):
  - "National ID" — body_large, weight 600, marginBottom 2
  - "Verified ✓" — body_small, color #4CAF50
- "View" link — label_medium, #1800B1, underlined

### doc_proof_address_card (pending)

White card (same structure). Horizontal stack:
- Placeholder box: 56×40dp, bg #F5F5F5, border 1px #FFB300 (amber — signals attention needed)
  - home icon: size 20, color #FFB300
- Info column:
  - "Proof of Address" — body_large, weight 600, marginBottom 2
  - "Pending Upload" — body_small, color #FF8F00
- "Upload" button — outlined, border #1800B1, text #1800B1, paddingHorizontal 12, paddingVertical 6, label_small

### review_notes_input

Outlined textarea (variant outlined, marginHorizontal 16, marginBottom 16, minLines 3, maxLines 6).
Placeholder: "Add internal notes about this application — e.g. income verified via payslip, employer confirmed, recommend approval..."
Labeled: "Review Notes". Not visible to customer.

### Action Buttons

- **approve_application_button**: filled, bg #4CAF50, white text, "Approve Application", full width, marginHorizontal 16, marginBottom 8
- **reject_application_button**: outlined, border #FF5252, text #FF5252, "Reject Application", full width, marginHorizontal 16, marginBottom 8
- **request_info_button**: text variant, color #1800B1, "Request Information", marginHorizontal 16, marginBottom 24

---

## Interaction Patterns

- **View Profile**: Tap "View Profile" link → navigate to customer-detail for John Kamau Mwangi
- **View document**: Tap "View" link on doc_national_id_card → open full-screen document viewer
- **Upload proof of address**: Tap "Upload" button → file picker (PDF/image); file is attached to this application
- **Approve**: Tap "Approve Application" → optional confirmation dialog → PUT applications/{id} status: APPROVED → success banner "Application approved successfully" → after 1.5s navigate to customer-detail
- **Reject**: Tap "Reject Application" → PUT applications/{id} status: REJECTED → rejection banner shown, officer remains on screen to optionally document the reason via notes
- **Request Information**: Tap text button → navigate to customer-messages with application context pre-filled (no API call at this step)

---

## Content Data

| Field               | Value                                |
|---------------------|--------------------------------------|
| Reference number    | Application #OBP-2026-00234          |
| Status              | Pending Review                       |
| Submitted date      | 20 May 2026                          |
| Customer name       | John Kamau Mwangi                    |
| Account type        | KCB Savings Account                  |
| Requested limit     | KES 500,000                          |
| Purpose             | Personal savings and salary credit   |
| KYC status          | Verified ✓                           |
| National ID doc     | Verified ✓                           |
| Proof of address    | Pending Upload                       |

---

## Design Notes

**Color Usage:**
- Deep purple header (#1800B1) with the reference number in title_large is the strongest visual anchor — officers should be able to identify the case from across the room
- #B0B8FF for submission date in the header: lavender is legible on purple without competing with the reference number
- Green row for KYC Verified (#E8F5E9/#4CAF50) provides immediate confidence signal before the officer scrolls to documents
- Amber proof-of-address placeholder border (#FFB300) softly flags that this doc is optional but missing — amber is less alarming than red
- Approve button green (#4CAF50) and reject button red (#FF5252) — color semantics directly map to consequence

**Typography:**
- title_large for application reference: the largest type on the screen, clearly scoped to this specific application
- Section labels ("CUSTOMER", "APPLICATION DETAILS"): uppercase label_medium in #999999 — Material 3 card section heading pattern
- "KES 500,000" in monospace: financial figures should use monospace for digit alignment and precision perception

**Spacing:**
- Cards use marginHorizontal 16 and elevation 2 — same grid as account-applications cards for consistency
- kyc_status_row has borderRadius 12 to match the card system, not a flat bar
- 24dp marginBottom on the last action button — accounts for gesture navigation bar height on modern Android

**Accessibility:**
- application_header contentDescription covers the full summary: "Application OBP-2026-00234, Pending Review, submitted 20 May 2026"
- kyc_status_row: "KYC Status: Verified" — role status
- doc_national_id_card: "National ID document — Verified"
- doc_proof_address_card: "Proof of Address — Pending upload"
- review_notes_input: "Internal review notes, not visible to customer" — privacy context for screen reader users
- Approve button: "Approve this account application"
- Reject button: "Reject this account application"

*Generated by /idea export | 2026-05-25*
