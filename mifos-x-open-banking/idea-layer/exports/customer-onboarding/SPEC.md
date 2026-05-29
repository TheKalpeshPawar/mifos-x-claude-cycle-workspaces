# SPEC — New Customer Onboarding

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | customer-onboarding            |
| Flavor        | fieldOfficer                   |
| Status        | design_partial                 |
| Quality Score | 94                             |
| ViewModel     | CustomerOnboardingViewModel    |

---

## Overview

New Customer Onboarding is a 4-step guided form used by Field Officers to register new individual customers in the Mifos X Open Banking system. The flow walks through: Step 1 Personal Information (first/last name, date of birth, national ID number, mobile phone with +254 prefix, email), Step 2 Address (street, city, county dropdown, postcode), Step 3 KYC Documents (ID document type selector, front-side ID upload, back-side ID upload, selfie/liveness capture), and Step 4 Review & Submit (summary card showing Kipchoge Rotich, National ID KE12345678, +254 723 456 789, 14 Ngong Road Nairobi, then Submit button). A horizontal progress stepper (4 circles + 3 connectors) sits pinned at the top of every step — completed steps carry a check icon on a #4C662B circle, the current step is a numbered #4C662B circle with white text, and upcoming steps are #E1E4D5 circles with #44483D numbers. A step counter label ("Step 2 of 4: Address Information") in body_medium #4C662B sits below the stepper. Navigation uses Back (outlined, flex 1) and Next (filled, flex 1) in a horizontal row at the bottom. Step 4 shows Submit Application (full-width filled) instead of Next. On submit, the ViewModel chains through 10 sequential OBP API calls; validation errors surface inline before step advancement.

---

## Screens

| ID                       | Name                    | Route                | Layout | Scroll   |
|--------------------------|-------------------------|----------------------|--------|----------|
| customer-onboarding-main | New Customer Onboarding | /customer-onboarding | Column | Vertical |

**Shell:** Field Officer bottom navigation bar visible. Top app bar with back arrow — pops to customer-search.

| Nav Item     | ID               | Icon        | Target               | Badge |
|--------------|------------------|-------------|----------------------|-------|
| Dashboard    | nav_dashboard    | dashboard   | fo-dashboard         | true  |
| Customers    | nav_customers    | people      | customer-search      | false |
| Applications | nav_applications | description | account-applications | true  |
| Messages     | nav_messages     | mail        | customer-messages    | true  |
| More         | nav_more         | more_vert   | settings             | false |

---

## Components

| ID                      | Type    | Description                                                                                                           |
|-------------------------|---------|-----------------------------------------------------------------------------------------------------------------------|
| progress_stepper        | box     | Horizontal stepper bar: 4 circles + 3 divider connectors; #FFFFFF bg; 1dp border-bottom #E1E4D5; pad V16/H8          |
| stepper_stack           | stack   | Direction horizontal, justify space_between, align center, full_width                                                 |
| step1_indicator         | box     | 28×28dp circle, #4C662B fill, 20dp radius — contains check icon 16dp #FFFFFF; completed state                        |
| step1_check             | icon    | "check", 16dp, #FFFFFF — checkmark on completed step 1                                                                |
| step_connector_1        | divider | Flex 1, 2dp height, #4C662B — completed connector between steps 1 and 2                                               |
| step2_indicator         | box     | 28×28dp circle, #4C662B fill, 20dp radius — "2" Outfit/label_medium #FFFFFF weight 700; current active step          |
| step2_number            | text    | "2", Outfit/label_medium, #FFFFFF, weight 700                                                                          |
| step_connector_2        | divider | Flex 1, 2dp height, #E1E4D5 — upcoming connector between steps 2 and 3                                               |
| step3_indicator         | box     | 28×28dp circle, #E1E4D5 fill, 20dp radius — "3" Outfit/label_medium #44483D weight 700; upcoming                     |
| step3_number            | text    | "3", Outfit/label_medium, #44483D, weight 700                                                                          |
| step_connector_3        | divider | Flex 1, 2dp height, #E1E4D5 — upcoming connector between steps 3 and 4                                               |
| step4_indicator         | box     | 28×28dp circle, #E1E4D5 fill, 20dp radius — "4" Outfit/label_medium #44483D weight 700; upcoming                     |
| step4_number            | text    | "4", Outfit/label_medium, #44483D, weight 700                                                                          |
| step_indicator_text     | text    | "Step 2 of 4: Address Information" — Outfit/body_medium, #4C662B; pad H16/T8/B4                                       |
| first_name_input        | input   | Outlined variant, "First Name", required, margin H16/B8; supports idle/hover/focus_visible/pressed/disabled states    |
| last_name_input         | input   | Outlined variant, "Last Name", required, margin H16/B8                                                                |
| dob_input               | input   | Outlined variant, "Date of Birth (DD/MM/YYYY)", placeholder "14/03/1985"; tap opens date picker                       |
| national_id_input       | input   | Outlined variant, "National ID Number", required, placeholder "KE12345678"                                            |
| phone_input             | input   | Outlined variant, "Mobile Phone", required, prefix "+254", placeholder "722 123 456"                                  |
| email_input             | input   | Outlined email variant, "Email Address", optional, placeholder "john.mwangi@gmail.com"                                |
| street_input            | input   | Outlined variant, "Street Address", placeholder "123 Moi Avenue", margin H16/B8                                       |
| city_input              | input   | Outlined variant, "City", placeholder "Nairobi"                                                                       |
| county_select           | input   | Outlined select, "County" — options: Nairobi, Mombasa, Kisumu, Nakuru, Eldoret, Nyeri, Thika, Kitale                 |
| postcode_input          | input   | Outlined variant, "Postcode", placeholder "00100"                                                                     |
| id_type_select          | input   | Outlined select, "ID Document Type" — options: National ID, Passport, Driver's License                                |
| upload_id_front_button  | button  | Outlined, "Upload ID — Front Side", camera icon, #4C662B border + text, full_width, margin H16/B8                    |
| upload_id_back_button   | button  | Outlined, "Upload ID — Back Side", camera icon, #4C662B border + text, full_width, margin H16/B8                     |
| capture_selfie_button   | button  | Outlined, "Capture Selfie / Liveness Check", face icon, #386663 border + text, full_width, margin H16/B8             |
| review_summary_card     | box     | #FFFFFF bg, 12dp radius, 16dp padding, margin H16/B16, elevation 2 — contains 4 review text rows                     |
| review_name             | text    | "John Kamau Mwangi" — Outfit/title_medium, #1A1C16, weight 600, margin_bottom spacing.xs                              |
| review_id               | text    | "National ID: KE12345678" — Outfit/body_medium, #44483D, margin_bottom 2dp                                            |
| review_phone            | text    | "Phone: +254 722 123 456" — Outfit/body_medium, #44483D, margin_bottom 2dp                                            |
| review_address          | text    | "123 Moi Avenue, Nairobi, 00100" — Outfit/body_medium, #44483D                                                        |
| submit_button           | button  | Filled full-width "Submit Application" — #4C662B bg, #FFFFFF text, margin H16/B8                                      |
| nav_button_row          | stack   | Horizontal, justify space_between, pad H16/V16, gap 12 — contains back_button + next_button                          |
| back_button             | button  | Outlined "Back" — #4C662B border + text, flex 1; on_click: go_back → previous_step                                   |
| next_button             | button  | Filled "Next" — #4C662B bg, #FFFFFF text, flex 1; on_click: go_next → next_step                                      |

---

## States

| ID        | Trigger                      | Visible Components                                                                                      | Description                                                                   |
|-----------|------------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| step_1    | Initial screen entry         | progress_stepper, step_indicator_text, first_name_input, last_name_input, dob_input, national_id_input, phone_input, email_input, nav_button_row | Personal information collection; email optional |
| step_2    | Next from step_1 valid       | progress_stepper, step_indicator_text, street_input, city_input, county_select, postcode_input, nav_button_row | Address collection; county is a dropdown |
| step_3    | Next from step_2 valid       | progress_stepper, step_indicator_text, id_type_select, upload_id_front_button, upload_id_back_button, capture_selfie_button, nav_button_row | KYC document upload + liveness |
| step_4    | Next from step_3 valid       | progress_stepper, step_indicator_text, review_summary_card, submit_button, nav_button_row | Full summary review before submission |
| loading   | submit_button tapped         | Progress overlay shown, overlayMessage "Submitting application…"; inputs locked | All 10 OBP calls in flight |
| submitted | All 10 API calls succeed     | Success banner shown | Routes to kyc-review |
| error     | API failure at any step      | Error banner shown | Shows error message + retry |
| empty     | Onboarding unavailable       | Empty state: person_off icon + "Customer onboarding unavailable. Contact support." | Fallback when feature unavailable |

**content** state alias maps to step_1 (same components — used as default alias).

---

## State Model

**ViewModel:** `CustomerOnboardingViewModel`
**Screen State Type:** `CustomerOnboardingScreenState`

| Name             | Type                   | Default    |
|------------------|------------------------|------------|
| currentStep      | Int                    | 1          |
| personalInfo     | PersonalInfoDraft      | —          |
| addressInfo      | AddressDraft           | —          |
| kycDraft         | KycDraft               | —          |
| isSubmitting     | Boolean                | false      |
| validationErrors | Map\<String, String\>  | emptyMap() |

**Events:** `StepAdvanced`, `StepBacked`, `DocumentUploaded`, `SelfieCaptured`, `ApplicationSubmitted`

**Actions:** `go_next`, `go_back`, `upload_document`, `capture_selfie`, `submit`, `open_date_picker`, `open_county_picker`

**DI Dependencies:** `CustomerRepository`, `DocumentUploadService`, `FormValidator`

**Errors:**
- `SUBMIT_FAILED`: "Application submission failed. Please try again."
- `VALIDATION_FAILED`: Map of field → error message.
- `UPLOAD_FAILED`: "Document upload failed. Check connection and retry."
- `NETWORK_UNAVAILABLE`: "No internet connection. Cannot submit application."

---

## Navigation

| From                | To              | Trigger                                 | Type  |
|---------------------|-----------------|-----------------------------------------|-------|
| customer-onboarding | step_2          | next_button — step 1 validation passes  | state |
| customer-onboarding | step_3          | next_button — step 2 validation passes  | state |
| customer-onboarding | step_4          | next_button — step 3 validation passes  | state |
| customer-onboarding | previous step   | back_button                             | state |
| customer-onboarding | kyc-review      | submit_button + all 10 API calls succeed| push  |
| customer-onboarding | customer-search | top app bar back arrow                  | pop   |

---

## API Endpoints

| Endpoint                                                                             | Auth        | Tag                 | Step | Purpose                       |
|--------------------------------------------------------------------------------------|-------------|---------------------|------|-------------------------------|
| POST /obp/v5.0.0/banks/{bankId}/customers                                            | DirectLogin | Customer            | 1    | Create customer record        |
| POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/address                       | DirectLogin | Customer            | 2    | Add customer address          |
| POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/tax-residence                 | DirectLogin | Customer            | 3    | Add tax residence             |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}  | DirectLogin | KYC                 | 4    | Upload KYC document           |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}         | DirectLogin | KYC                 | 5    | Record KYC check result       |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses                   | DirectLogin | KYC                 | 6    | Set KYC status (appends)      |
| POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute                     | DirectLogin | Customer-Attribute  | 7    | Add customer attribute        |
| POST /obp/v4.0.0/banks/{bankId}/user_customer_links                                  | DirectLogin | Customer            | 8    | Link user to customer         |
| POST /obp/v3.1.0/banks/{bankId}/account-applications                                 | DirectLogin | Account-Application | 9    | Create account application    |
| POST /obp/v5.0.0/banks/{bankId}/customer-account-links                               | DirectLogin | Customer            | 10   | Link customer to account      |

---

## Design Tokens

| Token                           | Value   | Usage                                                                                       |
|---------------------------------|---------|---------------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B | Completed step circles + connectors, current step circle, step counter text, next/submit btn fill |
| colors.light.on_primary         | #FFFFFF | Text/icons on all filled #4C662B surfaces (step numbers, button labels, step check icon)    |
| colors.light.secondary          | #386663 | Selfie capture button — border + text color                                                 |
| colors.light.surface_variant    | #E1E4D5 | Upcoming step circle fill + upcoming connectors; stepper bar bottom border                  |
| colors.light.on_surface_variant | #44483D | Upcoming step numbers (3, 4); review ID/phone/address text                                  |
| colors.light.on_surface         | #1A1C16 | Review applicant name (Kipchoge Rotich)                                                     |
| colors.light.surface            | #FFFFFF | Stepper bar background; review summary card background                                      |
| colors.light.background         | #F9FAEF | Screen base                                                                                 |
| typography.body_medium          | Outfit 14sp/400 | Step indicator label; review data rows                                            |
| typography.label_medium         | Outfit 12sp/500 | Step circle numbers                                                               |
| typography.title_medium         | Outfit 16sp/500 | Review applicant name                                                             |
| typography.label_large          | Outfit 14sp/500 | Button labels (Next, Back, Submit, upload buttons)                                |
| radius.xs                       | 4dp     | Text field corners                                                                          |
| radius.md                       | 12dp    | Review summary card                                                                         |
| radius.pill                     | 999dp   | Submit / Next / Back buttons                                                                |
| spacing.md                      | 16dp    | Horizontal content padding; field margin                                                    |
| spacing.sm                      | 8dp     | Stepper horizontal padding; field bottom gap                                                |
| spacing.xs                      | 4dp     | Review row vertical gap                                                                     |
| elevation.level2                | 3dp     | Review summary card elevation                                                               |
| touchTargets.min_touch_target   | 48dp    | All buttons and inputs meet 48dp minimum touch target                                       |

---

_Generated by /idea export | 2026-05-30_
