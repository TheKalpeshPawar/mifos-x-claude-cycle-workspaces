# Feature Specification — New Customer Onboarding

| Field         | Value                          |
|---------------|-------------------------------|
| Feature       | customer-onboarding           |
| Flavor        | fieldOfficer                  |
| Status        | enriched                      |
| Quality Score | 80                            |

---

## Overview

The New Customer Onboarding screen guides a Field Officer through a 4-step wizard to register a retail banking customer on the OBP sandbox. Step 1 captures personal identity (name, date of birth, national ID, phone, email). Step 2 captures the customer's physical address in Kenya. Step 3 handles KYC document capture (ID front/back and liveness selfie). Step 4 presents a summary review and triggers the 10-step OBP chain ending with a linked account application.

---

## Screens

| Screen ID                    | Route                        | Layout  | Scroll   |
|------------------------------|------------------------------|---------|----------|
| customer-onboarding-main     | /onboarding/customer/new     | form    | vertical |

---

## Components

| ID                      | Type    | Description                                                              |
|-------------------------|---------|--------------------------------------------------------------------------|
| progress_stepper        | box     | Horizontal 4-step stepper: completed (green check), active (purple), upcoming (grey) |
| step_indicator_text     | text    | Dynamic label — "Step N of 4: {Step Name}" in primary purple            |
| first_name_input        | input   | Outlined text field, required                                            |
| last_name_input         | input   | Outlined text field, required                                            |
| dob_input               | input   | Date picker trigger, format DD/MM/YYYY, placeholder "14/03/1985"        |
| national_id_input       | input   | Outlined text, required, placeholder "KE12345678"                       |
| phone_input             | input   | Outlined text, prefix "+254", placeholder "722 123 456", required       |
| email_input             | input   | Outlined email, optional, placeholder "john.mwangi@gmail.com"           |
| street_input            | input   | Outlined text, placeholder "123 Moi Avenue"                             |
| city_input              | input   | Outlined text, placeholder "Nairobi"                                    |
| county_select           | input   | Dropdown: Nairobi, Mombasa, Kisumu, Nakuru, Eldoret, Nyeri, Thika, Kitale |
| postcode_input          | input   | Outlined text, placeholder "00100"                                      |
| id_type_select          | input   | Dropdown: National ID, Passport, Driver's License                       |
| upload_id_front_button  | button  | Outlined + camera icon, triggers document capture for ID front          |
| upload_id_back_button   | button  | Outlined + camera icon, triggers document capture for ID back           |
| capture_selfie_button   | button  | Outlined + face icon, teal border, triggers liveness camera             |
| review_summary_card     | box     | White card with applicant name "John Kamau Mwangi", ID, phone, address  |
| submit_button           | button  | Filled primary — "Submit Application" → navigates to kyc-review         |
| nav_button_row          | stack   | Horizontal row: "Back" (outlined) + "Next" (filled) buttons            |

---

## States

| ID          | Trigger                             | Description                                                   |
|-------------|-------------------------------------|---------------------------------------------------------------|
| step_1      | Initial load / Back from step_2     | Shows personal information fields (name, DOB, ID, phone, email) |
| step_2      | Next from step_1                    | Shows address fields (street, city, county, postcode)         |
| step_3      | Next from step_2                    | Shows KYC document upload: ID type, front, back, selfie       |
| step_4      | Next from step_3                    | Review summary card + Submit button                           |
| submitting  | Submit tapped                       | Full-screen progress overlay: "Submitting application..."     |
| submitted   | OBP 10-step chain completes         | Success banner, navigate to kyc-review                        |
| error       | Any API failure                     | Error banner with retry option                                |

---

## State Model

**ViewModel:** `CustomerOnboardingViewModel`

| State Field      | Type                  | Default     |
|------------------|-----------------------|-------------|
| currentStep      | Int                   | 1           |
| personalInfo     | PersonalInfoDraft     | —           |
| addressInfo      | AddressDraft          | —           |
| kycDraft         | KycDraft              | —           |
| isSubmitting     | Boolean               | false       |
| validationErrors | Map\<String, String\> | emptyMap    |

**Events:** StepAdvanced, StepBacked, DocumentUploaded, SelfieCaptured, ApplicationSubmitted

**Actions:** go_next, go_back, upload_document, capture_selfie, submit, open_date_picker, open_county_picker

**DI Dependencies:** CustomerRepository, DocumentUploadService, FormValidator

**Errors:** SUBMIT_FAILED, VALIDATION_FAILED, UPLOAD_FAILED, NETWORK_UNAVAILABLE

---

## Navigation

| From                         | To              | Trigger               | Type     |
|------------------------------|-----------------|-----------------------|----------|
| customer-onboarding (step_4) | kyc-review      | Submit Application    | navigate |
| customer-onboarding          | previous_step   | Back button           | pop      |
| customer-onboarding          | next_step       | Next button           | push     |

---

## API Endpoints

| Step | Endpoint                                                                    | Auth         | Purpose                              |
|------|-----------------------------------------------------------------------------|--------------|--------------------------------------|
| 1    | POST /obp/v5.0.0/banks/{bankId}/customers                                   | DirectLogin  | Create customer record               |
| 2    | POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/address              | DirectLogin  | Add customer address                 |
| 3    | POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/tax-residence        | DirectLogin  | Add tax residence                    |
| 4    | PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{id}   | DirectLogin  | Upload KYC document (caller-supplied ID) |
| 5    | PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{id}       | DirectLogin  | Record KYC check result              |
| 6    | PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses         | DirectLogin  | Set KYC status (appends)             |
| 7    | POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute           | DirectLogin  | Add customer attribute               |
| 8    | POST /obp/v4.0.0/banks/{bankId}/user_customer_links                        | DirectLogin  | Link user to customer                |
| 9    | POST /obp/v3.1.0/banks/{bankId}/account-applications                      | DirectLogin  | Create account application           |
| 10   | POST /obp/v5.0.0/banks/{bankId}/customer-account-links                    | DirectLogin  | Link customer to account             |

---

## Design Tokens

| Token       | Value   | Usage                                  |
|-------------|---------|----------------------------------------|
| primary     | #1800B1 | Active step indicator, input borders, next button, step label text |
| success     | #4CAF50 | Completed step indicator, connector line |
| background  | #FFFFFF | Card backgrounds, stepper bar         |
| surface      | #FCF8FF | Screen background                     |
| error       | #BA1A1A | Validation error text                 |
| secondary   | #5C5D72 | Supporting text, subtitle             |
| on_surface  | #1A1A1A | Primary text (review card name)       |
| outline     | #E0E0E0 | Inactive connectors, field borders    |
| teal_accent | #008B8B | Selfie/liveness button                |

---

*Generated by /idea export | 2026-05-25*
