# Feature Specification — Corporate Customer Onboarding

| Field         | Value                          |
|---------------|-------------------------------|
| Feature       | corporate-onboarding          |
| Flavor        | fieldOfficer                  |
| Status        | enriched                      |
| Quality Score | 80                            |

---

## Overview

The Corporate Customer Onboarding screen is a 4-step wizard for Field Officers registering a business entity on the OBP sandbox. Step 1 collects company identity data (legal name, registration number, KRA PIN, industry, entity type, year established). Step 2 manages beneficial owners with ownership percentage validation against 100%. Step 3 handles document uploads (certificate of incorporation, tax compliance certificate, directors' IDs). Step 4 presents a review summary and submits the corporate application, navigating to account-applications on success.

---

## Screens

| Screen ID                    | Route                         | Layout  | Scroll   |
|------------------------------|-------------------------------|---------|----------|
| corporate-onboarding-main    | /onboarding/corporate/new     | form    | vertical |

---

## Components

| ID                         | Type    | Description                                                                 |
|----------------------------|---------|-----------------------------------------------------------------------------|
| progress_stepper           | box     | 4-step horizontal stepper: active step 1 (purple), steps 2-4 grey         |
| step_label                 | text    | "Step N of 4: {Step Name}" in primary purple, body_medium                  |
| company_name_input         | input   | Outlined, required, placeholder "Kamau Enterprises Limited"                |
| registration_number_input  | input   | Outlined, required, placeholder "CPR/2019/123456"                         |
| kra_pin_input              | input   | Outlined, required, placeholder "P051234567A"                              |
| industry_select            | input   | Dropdown: Manufacturing, Retail, Services, Agriculture, Technology, Finance, Construction, Transport & Logistics |
| entity_type_select         | input   | Dropdown: Sole Proprietorship, Partnership, Limited Company, NGO, Co-operative Society, Public Benefit Organization |
| year_established_input     | input   | Number input, placeholder "2019"                                           |
| owner_1_card               | box     | Card: "James Otieno Kamau", 60% ownership, National ID KE78901234         |
| owner_2_card               | box     | Card: "Grace Wanjiku Muthoni", 25% ownership, National ID KE23456789      |
| ownership_validator        | box     | Amber warning box: "Total ownership: 85% — must sum to 100%"              |
| add_owner_button           | button  | Outlined + person_add icon, opens add-owner bottom sheet                   |
| upload_cert_button         | button  | Outlined + upload_file icon — Certificate of Incorporation                |
| upload_tax_button          | button  | Outlined + upload_file icon — Tax Compliance Certificate                  |
| upload_directors_id_button | button  | Outlined + badge icon, teal border — Directors' ID Documents              |
| corporate_review_card      | box     | Review card: company name, reg/KRA, entity type, owner count               |
| submit_corporate_button    | button  | Filled primary — "Submit Corporate Application" → account-applications    |
| nav_buttons                | stack   | Horizontal: Back (outlined) + Next (filled)                               |

---

## States

| ID          | Trigger                              | Description                                                       |
|-------------|--------------------------------------|-------------------------------------------------------------------|
| step_1      | Initial load                         | Company information fields: name, reg number, KRA PIN, industry, entity type, year |
| step_2      | Next from step_1                     | Beneficial owners list with ownership validator and Add Owner button |
| step_3      | Next from step_2 (ownership = 100%) | Document upload: certificate of incorporation, tax cert, directors' IDs |
| step_4      | Next from step_3                     | Corporate review card + Submit Corporate Application button       |
| submitting  | Submit tapped                        | Progress overlay: "Submitting corporate application..."           |
| submitted   | OBP API chain completes              | Success banner, navigate to account-applications                  |
| error       | Any API failure                      | Error banner with retry option                                    |

---

## State Model

**ViewModel:** `CorporateOnboardingViewModel`

| State Field      | Type                         | Default     |
|------------------|------------------------------|-------------|
| currentStep      | Int                          | 1           |
| companyInfo      | CompanyInfoDraft             | —           |
| beneficialOwners | List\<BeneficialOwnerDraft\> | emptyList   |
| ownershipTotal   | Float                        | 0.0         |
| documents        | CorporateDocumentsDraft      | —           |
| isSubmitting     | Boolean                      | false       |
| validationErrors | Map\<String, String\>        | emptyMap    |

**Events:** StepAdvanced, StepBacked, OwnerAdded, OwnerRemoved, DocumentUploaded, ApplicationSubmitted

**Actions:** go_next, go_back, add_owner, upload_cert, upload_tax, upload_document, submit

**DI Dependencies:** CustomerRepository, DocumentUploadService, FormValidator

**Errors:** SUBMIT_FAILED, OWNERSHIP_NOT_100_PERCENT, DOCUMENT_UPLOAD_FAILED, VALIDATION_FAILED, NETWORK_UNAVAILABLE

---

## Navigation

| From                           | To                   | Trigger                       | Type     |
|--------------------------------|----------------------|-------------------------------|----------|
| corporate-onboarding (step_4)  | account-applications | Submit Corporate Application  | navigate |
| corporate-onboarding           | previous_step        | Back button                   | pop      |
| corporate-onboarding           | next_step            | Next button                   | push     |
| corporate-onboarding (step_2)  | add_owner_sheet      | Add Beneficial Owner button   | bottomSheet |

---

## API Endpoints

| Endpoint                                              | Auth        | Purpose                                           |
|-------------------------------------------------------|-------------|---------------------------------------------------|
| POST /obp/v5.1.0/banks/{bankId}/customers             | DirectLogin | Create corporate customer record with legal_name, customer_type=CORPORATE |

**Response fields:** customer_id, legal_name, customer_number, customer_type, kyc_status

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 409 CUSTOMER_ALREADY_EXISTS

---

## Design Tokens

| Token           | Value   | Usage                                              |
|-----------------|---------|----------------------------------------------------|
| primary         | #1800B1 | Active step, outlined buttons, Next/Submit buttons |
| background      | #FFFFFF | Form cards, stepper strip                         |
| surface         | #FCF8FF | Screen background                                 |
| error           | #BA1A1A | Field validation errors                           |
| secondary       | #5C5D72 | Secondary text, muted labels                      |
| warning_bg      | #FFF8E1 | Ownership validator banner background             |
| warning_border  | #FFB300 | Ownership validator banner border                 |
| warning_text    | #E65100 | Ownership validator text, review owner count      |
| teal_accent     | #008B8B | Directors' ID upload button                       |
| outline         | #E0E0E0 | Inactive step connectors, card borders            |

---

*Generated by /idea export | 2026-05-25*
