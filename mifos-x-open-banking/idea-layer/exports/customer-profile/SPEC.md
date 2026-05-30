<!-- source: screens/customer-profile/ui.yaml -->
<!-- source_hash: sha256:309a5ac86cc382ad7b7333e325ccf5397a30c4efd14eef7be87a77946b59c13d -->
<!-- generated: 2026-05-30T13:30:00Z -->
<!-- generated_from_feature_version: 1.1.0 -->
<!-- generated_from_contract_version: 1.1.0 -->
<!-- prior_version: — -->

# SPEC — Customer Profile

| Field         | Value                       |
|---------------|-----------------------------|
| Feature       | customer-profile            |
| Flavor        | fieldOfficer                |
| Status        | approved                    |
| Quality Score | 98                          |
| ViewModel     | CustomerProfileViewModel    |

---

## Overview

Customer Profile is a `detail_screen` for Field Officers to view and optionally edit a customer's full record. It is accessed from the customer-search and kyc-review flows and presents three labelled sections: **Personal Information** (full name, date of birth, national ID, KRA tax PIN, phone, email), **Address** (street, county, postcode), and **Employment** (employer, monthly income, employment type). Each data row is a white horizontal box (8dp radius, 16dp horizontal padding, 12dp vertical padding) with a label in body_medium `#44483D` on the left and a value in body_large `#1A1C16` on the right. Phone and email values are tappable links — phone initiates a dialler intent (`tel:`), email opens the mail client (`mailto:`). An **Edit Information** outlined button at the bottom transitions the screen to editing mode.

Data is loaded from `GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}` (OBP Customers tag). Each row declares component_states: a skeleton shimmer on loading, a retry banner on error, and a contextual empty box when the field is absent. The initial state is `loading`. Transitions: `loading → content`, `loading → error`, `content → editing`, `editing → saving`, `saving → content`, `saving → error`. Sections are separated by `#E1E4D5` dividers. Screen background: `#F9FAEF`.

---

## Capabilities

| Capability | Description |
|------------|-------------|
| has_ui     | Full screen UI with detail_screen archetype |
| has_api    | OBP GET + PUT customer endpoints wired |

---

## Screens

| ID                     | Name                  | Route              | Layout | Scroll   |
|------------------------|-----------------------|--------------------|--------|----------|
| customer-profile-main  | Customer Information  | /customer-profile  | Column | Vertical |

**Shell:** Standard top app bar ("Customer Profile", back arrow). No bottom navigation bar on this detail screen.

---

## Components

| ID                     | Type    | Description                                                                                                    |
|------------------------|---------|----------------------------------------------------------------------------------------------------------------|
| personal_info_heading  | text    | "Personal Information" — Outfit/title_large, #4C662B, 20dp top padding, 8dp bottom padding; heading level 2  |
| full_name_row          | box     | Horizontal row — white fill, 8dp radius, 16dp h-pad, 12dp v-pad, 2dp margin-bottom; api: obp_get_customer_profile |
| full_name_label        | text    | "Full Name" — Outfit/body_medium, #44483D, weight 500                                                        |
| full_name_value        | text    | "Wanjiru Kamau" — Outfit/body_large, #1A1C16, weight 600                                                     |
| dob_row                | box     | Horizontal row — same card style; api: obp_get_customer_profile                                               |
| dob_label              | text    | "Date of Birth" — Outfit/body_medium, #44483D, weight 500                                                    |
| dob_value              | text    | "22 March 1988 (Age: 38)" — Outfit/body_large, #1A1C16                                                       |
| national_id_row        | box     | Horizontal row — same card style; api: obp_get_customer_profile                                               |
| national_id_label      | text    | "National ID" — Outfit/body_medium, #44483D, weight 500                                                      |
| national_id_value      | text    | "28456789" — Outfit/body_large, #1A1C16, monospace                                                           |
| tax_pin_row            | box     | Horizontal row — same card style; api: obp_get_customer_profile                                               |
| tax_pin_label          | text    | "Tax PIN (KRA)" — Outfit/body_medium, #44483D, weight 500                                                    |
| tax_pin_value          | text    | "A987654321W" — Outfit/body_large, #1A1C16, monospace                                                        |
| phone_row              | box     | Horizontal row — same card style; api: obp_get_customer_profile                                               |
| phone_label            | text    | "Phone" — Outfit/body_medium, #44483D, weight 500                                                            |
| phone_link             | link    | "+254 712 345 678" — Outfit/body_large, #4C662B, underline; on_click: call_customer (tel:+254712345678)      |
| email_row              | box     | Horizontal row — same card style; api: obp_get_customer_profile                                               |
| email_label            | text    | "Email" — Outfit/body_medium, #44483D, weight 500                                                            |
| email_link             | link    | "wanjiru.kamau@gmail.com" — Outfit/body_large, #4C662B, underline; on_click: email_customer (mailto:)        |
| address_divider        | divider | Horizontal rule — 16dp margin-vertical, #E1E4D5                                                               |
| address_heading        | text    | "Address" — Outfit/title_large, #4C662B, 8dp bottom padding; heading level 2                                 |
| address_street_row     | box     | Single-value row — white fill, 8dp radius, 10dp v-pad, 16dp h-pad, 2dp margin-bottom                         |
| address_street         | text    | "26 Westlands Road, Westlands" — Outfit/body_large, #1A1C16                                                  |
| address_county_row     | box     | Single-value row — same style                                                                                  |
| address_county         | text    | "Nairobi County, Kenya" — Outfit/body_large, #1A1C16                                                         |
| address_postcode_row   | box     | Single-value row — same style                                                                                  |
| address_postcode       | text    | "Postcode: 00100" — Outfit/body_large, #1A1C16                                                               |
| employment_divider     | divider | Horizontal rule — 16dp margin-vertical, #E1E4D5                                                               |
| employment_heading     | text    | "Employment" — Outfit/title_large, #4C662B, 8dp bottom padding; heading level 2                              |
| employer_row           | box     | Horizontal row — white fill, 8dp radius, 16dp h-pad, 12dp v-pad, 2dp margin-bottom                           |
| employer_label         | text    | "Employer" — Outfit/body_medium, #44483D, weight 500                                                         |
| employer_value         | text    | "Safaricom PLC" — Outfit/body_large, #1A1C16                                                                 |
| income_row             | box     | Horizontal row — same card style                                                                               |
| income_label           | text    | "Monthly Income" — Outfit/body_medium, #44483D, weight 500                                                   |
| income_value           | text    | "KES 85,000" — Outfit/body_large, #1A1C16, monospace                                                         |
| employment_type_row    | box     | Horizontal row — same card style, 16dp margin-bottom                                                          |
| employment_type_label  | text    | "Employment Type" — Outfit/body_medium, #44483D, weight 500                                                  |
| employment_type_value  | text    | "Permanent" — Outfit/body_large, #1A1C16                                                                     |
| edit_info_button       | button  | "Edit Information" — outlined, #4C662B border + text, pill radius, fill-width, 8dp margin-top                 |

### Component States (per data row)

Each `box` data row declares three component states bound to `obp_get_customer_profile`:

| State   | Type     | Behaviour                                                                   |
|---------|----------|-----------------------------------------------------------------------------|
| loading | skeleton | 1 shimmer row matching the label-value layout (short4 = 200ms duration)    |
| error   | banner   | "Could not load customer profile. Please try again." with retry affordance  |
| empty   | box      | Contextual message per field (e.g. "Customer name not available.") with icon |

---

## States

| ID      | Trigger                              | Description                                                                                       |
|---------|--------------------------------------|---------------------------------------------------------------------------------------------------|
| loading | Screen entry (initial_state)         | All data rows show skeleton shimmers; shimmer duration short4 (200ms); reduced motion → static placeholder |
| content | API load success                     | All three sections populated with live data; Edit Information button active                       |
| editing | edit_customer_info action            | Screen enters edit mode — fields become editable inputs; keyboard shown                           |
| saving  | save_customer_info action            | Progress overlay shown while PUT request in flight                                                |
| error   | Network or OBP error on load         | Error banner per affected row with retry; full-screen error if all rows fail                      |
| empty   | Field value absent in API response   | Per-row empty box with contextual icon and message                                                |

---

## State Model

**ViewModel:** `CustomerProfileViewModel`
**Screen State Type:** `CustomerProfileScreenState`

| Name        | Type                | Default  |
|-------------|---------------------|----------|
| customer    | CustomerDetail?     | null     |
| isLoading   | Boolean             | true     |
| isEditing   | Boolean             | false    |
| isSaving    | Boolean             | false    |
| editDraft   | CustomerEditDraft?  | null     |
| loadError   | String?             | null     |

**Events:** `EditStarted`, `EditCancelled`, `CustomerSaved`, `CallInitiated`, `EmailInitiated`

**Actions:** `edit_customer_info`, `save_customer_info`, `cancel_edit`, `call_customer`, `email_customer`

**Errors:**
- `CUSTOMER_LOAD_FAILED`: "Could not load customer profile. Please try again."
- `SAVE_FAILED`: "Unable to save changes. Please check your connection."
- `NETWORK_UNAVAILABLE`: "No network connection. Please try again."

**DI Dependencies:** `CustomerRepository`, `ContactActionHandler`

---

## App-Shell

Resolved shell for `customer-profile` (flavor: fieldOfficer, screen override: `bottom_nav: false`):

| Element      | Value                                                   |
|--------------|---------------------------------------------------------|
| Bottom nav   | hidden (screen override suppresses fieldOfficer 5-tab)  |
| Top app bar  | visible — title "Customer Profile", navigation_icon: arrow_back |
| FAB          | not shown (suppressed on detail screens)                |
| Safe area    | standard                                                |

---

## Navigation

| From             | To                  | Trigger                    | Type   |
|------------------|---------------------|----------------------------|--------|
| customer-profile | customer-search     | Back arrow tap             | pop    |
| customer-profile | kyc-review          | Back (from KYC flow)       | pop    |
| customer-profile | customer-messages   | (future — deep link)       | push   |
| customer-profile | tel:+254712345678   | phone_link tap             | intent |
| customer-profile | mailto:wanjiru...   | email_link tap             | intent |

---

## API Endpoints

| Endpoint                                                              | Auth        | Tag       | Purpose                                            |
|-----------------------------------------------------------------------|-------------|-----------|----------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}                | DirectLogin | Customers | Fetch full customer record for profile display     |
| PUT /obp/v5.1.0/banks/{bankId}/customers/{customerId}                | DirectLogin | Customers | Submit updated customer information                |

---

## Dependencies

| Feature          | Type    | Required | Check                                      |
|------------------|---------|----------|--------------------------------------------|
| customer-search  | feature | true     | Entry point — navigates to this screen     |
| kyc-review       | feature | false    | May navigate to this screen from KYC flow  |
| customer-messages| feature | false    | Future deep-link target                    |

---

## Design Tokens

| Token                           | Value     | Usage                                                                                  |
|---------------------------------|-----------|----------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Section headings (Personal Info / Address / Employment), phone + email link colour      |
| colors.light.on_surface         | #1A1C16   | Data value text (full_name_value, dob_value, national_id_value, etc.)                 |
| colors.light.on_surface_variant | #44483D   | Label text (full_name_label, dob_label, phone_label, etc.)                             |
| colors.light.surface            | #FFFFFF   | Data row card fill                                                                      |
| colors.light.surface_variant    | #E1E4D5   | Section dividers; skeleton shimmer base colour                                          |
| colors.light.background         | #F9FAEF   | Screen background                                                                       |
| colors.light.error              | #BA1A1A   | Error banner text                                                                       |
| colors.light.error_container    | #FFDAD6   | Error banner background                                                                 |
| typography.title_large          | Outfit 22sp/400 | Section headings                                                                   |
| typography.body_large           | Outfit 16sp/400 | Data values; phone and email link text                                             |
| typography.body_medium          | Outfit 14sp/400 | Field labels                                                                       |
| radius.sm                       | 8dp       | Data row card corners                                                                   |
| radius.pill                     | 999dp     | Edit Information button                                                                 |
| motion.duration.short4          | 200ms     | Skeleton shimmer animation duration                                                     |
| spacing.md                      | 16dp      | Horizontal content padding, row h-pad                                                   |
| spacing.lg                      | 24dp      | Section spacing (title paddingTop)                                                      |
| touchTargets.min_touch_target   | 48dp      | phone_link and email_link tap zones                                                     |

---

_Generated by /idea export | 2026-05-30_
