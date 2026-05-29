# SPEC — New Customer Onboarding

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | customer-onboarding            |
| Flavor        | fieldOfficer                   |
| Status        | approved                       |
| Quality Score | 94                             |
| ViewModel     | CustomerOnboardingViewModel    |

---

## Overview

New Customer Onboarding is a 4-step guided form used by Field Officers to register new individual customers. It walks through: Step 1 Personal Information (name, date of birth, national ID, phone, email), Step 2 Address (street, city, county, postcode), Step 3 KYC Documents (ID type, front/back upload, selfie liveness check), and Step 4 Review & Submit. A horizontal progress stepper at the top always shows current position — completed steps show a check icon on #4C662B, the current step is a numbered #4C662B circle, and upcoming steps are #E1E4D5. Navigation uses Back / Next buttons at the bottom. Step 4 exposes a summary review card followed by Submit Application, which chains through 10 sequential OBP API calls. Validation errors surface inline per field before step advancement is allowed.

---

## Screens

| ID                       | Name                    | Route                | Layout | Scroll   |
|--------------------------|-------------------------|----------------------|--------|----------|
| customer-onboarding-main | New Customer Onboarding | /customer-onboarding | Column | Vertical |

**Shell:** Field Officer bottom navigation bar visible. Top app bar with back arrow navigating to customer-search.

| Nav Item     | ID               | Icon         | Target               | Badge |
|--------------|------------------|--------------|----------------------|-------|
| Dashboard    | nav_dashboard    | dashboard    | fo-dashboard         | true  |
| Customers    | nav_customers    | people       | customer-search      | false |
| Applications | nav_applications | description  | account-applications | true  |
| Messages     | nav_messages     | mail         | customer-messages    | true  |
| More         | nav_more         | more_vert    | settings             | false |

---

## Components

| ID                      | Type    | Description                                                                                               |
|-------------------------|---------|-----------------------------------------------------------------------------------------------------------|
| progress_stepper        | box     | Horizontal stepper bar: 4 circles + 3 connectors, #FFFFFF bg, border-bottom #E1E4D5; pad V16/H8          |
| step1_indicator         | box     | 28×28 circle, #4C662B fill — check icon #FFFFFF 16dp; completed                                          |
| step_connector_1        | divider | Flex 1, 2dp, #4C662B — completed connector                                                               |
| step2_indicator         | box     | 28×28 circle, #4C662B fill — "2" Outfit/label_medium #FFFFFF bold; current                               |
| step_connector_2        | divider | Flex 1, 2dp, #E1E4D5 — upcoming connector                                                                |
| step3_indicator         | box     | 28×28 circle, #E1E4D5 fill — "3" Outfit/label_medium #44483D bold; upcoming                              |
| step_connector_3        | divider | Flex 1, 2dp, #E1E4D5 — upcoming connector                                                                |
| step4_indicator         | box     | 28×28 circle, #E1E4D5 fill — "4" Outfit/label_medium #44483D bold; upcoming                              |
| step_indicator_text     | text    | "Step 2 of 4: Address Information" — Outfit/body_medium, #4C662B; pad H16/T8/B4                          |
| first_name_input        | input   | Outlined "First Name" — required, margin H16/B8                                                          |
| last_name_input         | input   | Outlined "Last Name" — required, margin H16/B8                                                           |
| dob_input               | input   | Outlined "Date of Birth (DD/MM/YYYY)" — placeholder "14/03/1985"; taps open date picker                  |
| national_id_input       | input   | Outlined "National ID Number" — required, placeholder "KE12345678"                                       |
| phone_input             | input   | Outlined "Mobile Phone" — required, prefix "+254", placeholder "722 123 456"                             |
| email_input             | input   | Outlined email "Email Address" — optional, placeholder "john.mwangi@gmail.com"                           |
| street_input            | input   | Outlined "Street Address" — placeholder "123 Moi Avenue", margin H16/B8                                  |
| city_input              | input   | Outlined "City" — placeholder "Nairobi"                                                                   |
| county_select           | input   | Outlined select "County" — options: Nairobi, Mombasa, Kisumu, Nakuru, Eldoret, Nyeri, Thika, Kitale      |
| postcode_input          | input   | Outlined "Postcode" — placeholder "00100"                                                                 |
| id_type_select          | input   | Outlined select "ID Document Type" — options: National ID, Passport, Driver's License                    |
| upload_id_front_button  | button  | Outlined "Upload ID — Front Side", camera icon, #4C662B border+text, full-width                          |
| upload_id_back_button   | button  | Outlined "Upload ID — Back Side", camera icon, #4C662B border+text, full-width                           |
| capture_selfie_button   | button  | Outlined "Capture Selfie / Liveness Check", face icon, #386663 border+text, full-width                   |
| review_summary_card     | box     | #FFFFFF bg, radius 12, pad 16, elevation 2 — name, ID, phone, address                                    |
| review_name             | text    | "John Kamau Mwangi" — Outfit/title_medium, #1A1C16, weight 600                                           |
| review_id               | text    | "National ID: KE12345678" — Outfit/body_medium, #44483D                                                  |
| review_phone            | text    | "Phone: +254 722 123 456" — Outfit/body_medium, #44483D                                                  |
| review_address          | text    | "123 Moi Avenue, Nairobi, 00100" — Outfit/body_medium, #44483D                                           |
| submit_button           | button  | Filled full-width "Submit Application" — #4C662B bg, #FFFFFF text                                        |
| back_button             | button  | Outlined "Back" — #4C662B border+text, flex 1                                                            |
| next_button             | button  | Filled "Next" — #4C662B bg, #FFFFFF text, flex 1                                                         |

---

## States

| ID        | Trigger                      | Description                                                                                  |
|-----------|------------------------------|----------------------------------------------------------------------------------------------|
| step_1    | Initial entry                | Personal info fields: first/last name, DOB, national ID, phone, email + nav buttons          |
| step_2    | Next from step_1 valid       | Address fields: street, city, county select, postcode + nav buttons                         |
| step_3    | Next from step_2 valid       | KYC: ID type select + upload front/back + selfie capture + nav buttons                      |
| step_4    | Next from step_3 valid       | Review summary card + Submit Application + Back button                                       |
| loading   | Submit tapped                | Progress overlay "Submitting application…"; inputs locked                                    |
| submitted | All 10 API calls succeed     | Success banner; routes to kyc-review                                                         |
| error     | API failure at any step      | Error banner with message + retry button                                                     |
| empty     | Onboarding unavailable       | person_off icon + "Customer onboarding unavailable. Contact support."                       |

---

## State Model

**ViewModel:** `CustomerOnboardingViewModel`
**Screen State Type:** `CustomerOnboardingScreenState`

| Name             | Type                  | Default    |
|------------------|-----------------------|------------|
| currentStep      | Int                   | 1          |
| personalInfo     | PersonalInfoDraft     | —          |
| addressInfo      | AddressDraft          | —          |
| kycDraft         | KycDraft              | —          |
| isSubmitting     | Boolean               | false      |
| validationErrors | Map\<String, String\> | emptyMap() |

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

| From                 | To              | Trigger                            | Type  |
|----------------------|-----------------|------------------------------------|-------|
| customer-onboarding  | step_2          | next_button — step 1 valid         | state |
| customer-onboarding  | step_3          | next_button — step 2 valid         | state |
| customer-onboarding  | step_4          | next_button — step 3 valid         | state |
| customer-onboarding  | previous step   | back_button                        | state |
| customer-onboarding  | kyc-review      | submit_button success              | push  |
| customer-onboarding  | customer-search | top app bar back arrow             | pop   |

---

## API Endpoints

| Endpoint                                                                              | Auth        | Tag                 | Step | Purpose                       |
|---------------------------------------------------------------------------------------|-------------|---------------------|------|-------------------------------|
| POST /obp/v5.0.0/banks/{bankId}/customers                                             | DirectLogin | Customer            | 1    | Create customer record        |
| POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/address                        | DirectLogin | Customer            | 2    | Add customer address          |
| POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/tax-residence                  | DirectLogin | Customer            | 3    | Add tax residence             |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}   | DirectLogin | KYC                 | 4    | Upload KYC document           |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}          | DirectLogin | KYC                 | 5    | Record KYC check result       |
| PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses                    | DirectLogin | KYC                 | 6    | Set KYC status (appends)      |
| POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute                      | DirectLogin | Customer-Attribute  | 7    | Add customer attribute        |
| POST /obp/v4.0.0/banks/{bankId}/user_customer_links                                   | DirectLogin | Customer            | 8    | Link user to customer         |
| POST /obp/v3.1.0/banks/{bankId}/account-applications                                  | DirectLogin | Account-Application | 9    | Create account application    |
| POST /obp/v5.0.0/banks/{bankId}/customer-account-links                                | DirectLogin | Customer            | 10   | Link customer to account      |

---

## Design Tokens

| Token                          | Value   | Usage                                                               |
|--------------------------------|---------|---------------------------------------------------------------------|
| color.light.primary            | #4C662B | Completed step circles, connectors, current step, submit/next btn   |
| color.light.secondary          | #386663 | Selfie capture button border + text                                 |
| color.light.surface_variant    | #E1E4D5 | Upcoming step connector and circle fill                             |
| color.light.on_surface_variant | #44483D | Upcoming step number, review supporting text                        |
| color.light.on_surface         | #1A1C16 | Review applicant name                                               |
| color.light.surface            | #FFFFFF | Stepper bar bg, review card bg                                      |
| color.light.background         | #F9FAEF | Screen background                                                   |
| typography.body_medium         | —       | Step counter label, review data rows                                |
| typography.label_medium        | —       | Stepper step number text                                            |
| typography.title_medium        | —       | Review applicant name                                               |
| radius.md                      | 12dp    | Review summary card                                                 |
| radius.pill                    | 999dp   | Submit / Next / Back buttons                                        |

---

_Generated by /idea export | 2026-05-29_
