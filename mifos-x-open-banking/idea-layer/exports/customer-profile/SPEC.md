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

Customer Profile is a detail_screen for Field Officers to view and optionally edit a customer's full record. It is accessed from customer-detail or customer-search and presents three collapsible sections: Personal Information (full name, date of birth, national ID, KRA tax PIN, phone, email), Address (street, county, postcode), and Employment (employer, monthly income, employment type). Each data row is a white horizontal row with a label in body_medium #44483D and a value in body_large #1A1C16, grouped on #F9FAEF background with #E1E4D5 dividers between sections. Phone and email values are tappable links — phone initiates a dialler intent, email opens mail client. The Edit Information button at the bottom transitions the screen to editing mode. Data is loaded from the OBP Customer endpoint; errors surface with a retry banner.

---

## Screens

| ID                    | Name                 | Route              | Layout | Scroll   |
|-----------------------|----------------------|--------------------|--------|----------|
| customer-profile-main | Customer Information | /customer-profile  | Column | Vertical |

**Shell:** Field Officer top app bar with back navigation (no bottom nav on detail screens).

| Nav Item  | ID          | Icon          | Target          |
|-----------|-------------|---------------|-----------------|
| Back      | nav_back    | arrow_back    | customer-detail |
| Search    | nav_search  | search        | customer-search |
| Profile   | nav_profile | account_circle| profile         |

---

## Components

| ID                    | Type    | Description                                                                                              |
|-----------------------|---------|----------------------------------------------------------------------------------------------------------|
| personal_info_heading | text    | "Personal Information" — Outfit/title_large, #4C662B; heading level 2                                   |
| full_name_row         | box     | Horizontal row: "Full Name" label + "John Kamau Mwangi" value; #FFFFFF bg, radius 8, pad V12/H16        |
| full_name_label       | text    | "Full Name" — Outfit/body_medium, #44483D, weight 500                                                   |
| full_name_value       | text    | "John Kamau Mwangi" — Outfit/body_large, #1A1C16, weight 600                                            |
| dob_row               | box     | Horizontal row: "Date of Birth" label + "14 March 1985 (Age: 41)" value                                  |
| dob_label             | text    | "Date of Birth" — Outfit/body_medium, #44483D, weight 500                                               |
| dob_value             | text    | "14 March 1985 (Age: 41)" — Outfit/body_large, #1A1C16                                                  |
| national_id_row       | box     | Horizontal row: "National ID" label + "KE12345678" value (monospace)                                     |
| national_id_label     | text    | "National ID" — Outfit/body_medium, #44483D, weight 500                                                  |
| national_id_value     | text    | "KE12345678" — Outfit/body_large, #1A1C16, monospace font family                                        |
| tax_pin_row           | box     | Horizontal row: "Tax PIN (KRA)" label + "A001234567M" value (monospace)                                  |
| tax_pin_label         | text    | "Tax PIN (KRA)" — Outfit/body_medium, #44483D, weight 500                                               |
| tax_pin_value         | text    | "A001234567M" — Outfit/body_large, #1A1C16, monospace                                                   |
| phone_row             | box     | Horizontal row: "Phone" label + tappable "+254 722 123 456" link                                         |
| phone_label           | text    | "Phone" — Outfit/body_medium, #44483D, weight 500                                                       |
| phone_link            | link    | "+254 722 123 456" — Outfit/body_large, #4C662B, underline; navigates tel:+254722123456                 |
| email_row             | box     | Horizontal row: "Email" label + tappable "john.mwangi@gmail.com" link                                    |
| email_label           | text    | "Email" — Outfit/body_medium, #44483D, weight 500                                                       |
| email_link            | link    | "john.mwangi@gmail.com" — Outfit/body_large, #4C662B, underline; navigates mailto:                      |
| address_divider       | divider | Horizontal divider #E1E4D5, margin V16 — separates Personal from Address                                 |
| address_heading       | text    | "Address" — Outfit/title_large, #4C662B; heading level 2                                                 |
| address_street_row    | box     | "123 Moi Avenue, Nairobi" — Outfit/body_large, #1A1C16; #FFFFFF bg, radius 8                            |
| address_county_row    | box     | "Nairobi County, Kenya" — Outfit/body_large, #1A1C16                                                    |
| address_postcode_row  | box     | "Postcode: 00100" — Outfit/body_large, #1A1C16                                                          |
| employment_divider    | divider | Horizontal divider #E1E4D5, margin V16 — separates Address from Employment                               |
| employment_heading    | text    | "Employment" — Outfit/title_large, #4C662B; heading level 2                                              |
| employer_row          | box     | "Employer" label + "Safaricom PLC" value                                                                 |
| employer_label        | text    | "Employer" — Outfit/body_medium, #44483D, weight 500                                                     |
| employer_value        | text    | "Safaricom PLC" — Outfit/body_large, #1A1C16                                                            |
| income_row            | box     | "Monthly Income" label + "KES 85,000" value (monospace)                                                  |
| income_label          | text    | "Monthly Income" — Outfit/body_medium, #44483D, weight 500                                               |
| income_value          | text    | "KES 85,000" — Outfit/body_large, #1A1C16, monospace                                                    |
| employment_type_row   | box     | "Employment Type" label + "Permanent" value                                                              |
| employment_type_label | text    | "Employment Type" — Outfit/body_medium, #44483D, weight 500                                              |
| employment_type_value | text    | "Permanent" — Outfit/body_large, #1A1C16                                                                 |
| edit_info_button      | button  | Outlined full-width "Edit Information" — #4C662B border+text, margin T8/B24                              |

---

## States

| ID      | Trigger                       | Description                                                                              |
|---------|-------------------------------|------------------------------------------------------------------------------------------|
| loading | Screen entry                  | Skeleton shimmer on all data rows; section headings visible; #F9FAEF background          |
| content | API load success              | All data rows populated with John Kamau Mwangi's real data; Edit button active           |
| editing | edit_info_button tap          | Inline edit mode — data row values become editable inputs; keyboard shown                |
| saving  | Save changes tapped           | Progress overlay "Saving changes…"; inputs locked                                        |
| error   | Network or API failure        | Error banner "Could not load customer profile. Please try again." + Retry button         |
| empty   | Customer data unavailable     | "Customer profile data not available" message centered                                   |

---

## State Model

**ViewModel:** `CustomerProfileViewModel`
**Screen State Type:** `CustomerProfileScreenState`

| Name       | Type               | Default |
|------------|--------------------|---------|
| customer   | CustomerDetail?    | null    |
| isLoading  | Boolean            | true    |
| isEditing  | Boolean            | false   |
| isSaving   | Boolean            | false   |
| editDraft  | CustomerEditDraft? | null    |
| loadError  | String?            | null    |

**Events:** `EditStarted`, `EditCancelled`, `CustomerSaved`, `CallInitiated`, `EmailInitiated`

**Actions:** `edit_customer_info`, `save_customer_info`, `cancel_edit`, `call_customer`, `email_customer`

**DI Dependencies:** `CustomerRepository`, `ContactActionHandler`

**Errors:**
- `CUSTOMER_LOAD_FAILED`: "Could not load customer profile. Please try again."
- `SAVE_FAILED`: "Changes could not be saved. Please try again."
- `NETWORK_UNAVAILABLE`: "No internet connection."

---

## Navigation

| From             | To              | Trigger                          | Type  |
|------------------|-----------------|----------------------------------|-------|
| customer-profile | customer-detail | top app bar back arrow           | pop   |
| customer-profile | tel: dialler    | phone_link tap (call_customer)   | intent|
| customer-profile | mail client     | email_link tap (email_customer)  | intent|

---

## API Endpoints

| Endpoint                                                       | Auth        | Tag       | Purpose                                       |
|----------------------------------------------------------------|-------------|-----------|-----------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}          | DirectLogin | Customers | Load full customer record for profile display |
| PUT /obp/v5.1.0/banks/{bankId}/customers/{customerId}          | DirectLogin | Customers | Save edited customer details                  |

---

## Design Tokens

| Token                          | Value   | Usage                                                                    |
|--------------------------------|---------|--------------------------------------------------------------------------|
| color.light.primary            | #4C662B | Section headings, phone/email link text, edit button border+text         |
| color.light.on_surface_variant | #44483D | Row label text (body_medium)                                             |
| color.light.on_surface         | #1A1C16 | Row value text (body_large)                                              |
| color.light.surface            | #FFFFFF | Data row card backgrounds                                                |
| color.light.background         | #F9FAEF | Screen background                                                        |
| color.light.surface_variant    | #E1E4D5 | Section dividers                                                         |
| typography.title_large         | —       | Section heading labels                                                   |
| typography.body_large          | —       | Data row values                                                          |
| typography.body_medium         | —       | Data row labels                                                          |
| radius.sm                      | 8dp     | Data row cards                                                           |
| radius.pill                    | 999dp   | Edit Information button                                                  |

---

_Generated by /idea export | 2026-05-29_
