# SPEC — Corporate Customer Onboarding

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | corporate-onboarding           |
| Flavor        | fieldOfficer                   |
| Status        | approved                       |
| Quality Score | 94                             |
| ViewModel     | CorporateOnboardingViewModel   |

---

## Overview

The Corporate Customer Onboarding screen enables Field Officers to register new corporate clients through a guided 4-step wizard. Steps are: (1) Company Information — legal name, registration number, KRA PIN, industry, entity type, year established; (2) Beneficial Owners — add and validate owner records (name, ownership %, national ID) ensuring total ownership sums to 100%; (3) Documents — upload Certificate of Incorporation, KRA Tax Compliance Certificate, and Directors' ID documents; (4) Review & Submit — a summary card confirms all entered data before the final `POST /customers` call. A horizontal step indicator at the top shows progress. Back/Next navigation buttons appear at the bottom of each step. On successful submission, the screen transitions to `submitted` state with a success banner and navigates to Account Applications. The screen has no bottom navigation bar — it is accessed from the Field Officer workflow.

---

## Screens

| ID                       | Name                    | Route                  | Layout | Scroll   |
|--------------------------|-------------------------|------------------------|--------|----------|
| corporate-onboarding-main| New Corporate Customer  | /corporate-onboarding  | Column | Vertical |

**Shell:** Top app bar ("New Corporate Customer", back arrow). No bottom navigation bar.

---

## Components

| ID                          | Type     | Description                                                                                               |
|-----------------------------|----------|-----------------------------------------------------------------------------------------------------------|
| progress_stepper            | box      | Horizontal step indicator; white bg, `#E1E4D5` border-bottom; 4 numbered circles connected by lines      |
| step1_indicator             | box      | Circle 28×28dp; bg `#4C662B` (current), `#E1E4D5` (upcoming); number "1" in white/`#44483D`              |
| step2_indicator             | box      | Circle 28×28dp; bg `#E1E4D5`; number "2" in `#44483D`                                                    |
| step3_indicator             | box      | Circle 28×28dp; bg `#E1E4D5`; number "3" in `#44483D`                                                    |
| step4_indicator             | box      | Circle 28×28dp; bg `#E1E4D5`; number "4" in `#44483D`                                                    |
| connector_1..3              | divider  | Horizontal lines 2dp height, `#E1E4D5`, between step circles                                             |
| step_label                  | text     | "Step 1 of 4: Company Information" — `body_medium`, color `#4C662B`; updates per step                    |
| company_name_input          | input    | Label "Legal Company Name"; placeholder "Kamau Enterprises Limited"; required                             |
| registration_number_input   | input    | Label "Business Registration Number"; placeholder "CPR/2019/123456"; required                            |
| kra_pin_input               | input    | Label "KRA PIN"; placeholder "P051234567A"; required                                                      |
| industry_select             | input    | Label "Industry"; select/dropdown; options: Manufacturing, Retail, Services, Agriculture, Technology, Finance, Construction, Transport & Logistics |
| entity_type_select          | input    | Label "Entity Type"; select; options: Sole Proprietorship, Partnership, Limited Company, NGO, Co-operative Society, Public Benefit Organization |
| year_established_input      | input    | Label "Year Established"; placeholder "2019"; number input                                                |
| owner_1_card                | box      | White card, 10dp radius, elevation 1, `#E1E4D5` border; owner: "James Otieno Kamau", ownership 60%, ID KE78901234 |
| owner_2_card                | box      | White card; owner: "Grace Wanjiku Muthoni", ownership 25%, ID KE23456789                                  |
| ownership_validator         | box      | `#CDEDA3` bg, `#E8A317` border, 8dp radius; "Total ownership: 85% — must sum to 100%"; role: alert       |
| ownership_total_text        | text     | "Total ownership: 85% — must sum to 100%" — `body_medium`, `#44483D` (7.25:1 contrast pass)              |
| add_owner_button            | button   | "Add Beneficial Owner" — outlined, `#4C662B`, `person_add` icon, full-width                              |
| upload_cert_button          | button   | "Upload Certificate of Incorporation" — outlined, `#4C662B`, `upload_file` icon, full-width              |
| upload_tax_button           | button   | "Upload Tax Compliance Certificate" — outlined, `#4C662B`, `upload_file` icon, full-width                |
| upload_directors_id_button  | button   | "Upload Directors' ID Documents" — outlined, `#386663` (secondary), `badge` icon, full-width             |
| corporate_review_card       | box      | White card, 12dp radius, elevation 2; review summary of all entered data                                  |
| review_company_name         | text     | "Kamau Enterprises Limited" — `title_medium`, `#1A1C16`, bold                                            |
| review_reg_number           | text     | "Reg: CPR/2019/123456 · KRA: P051234567A" — `body_medium`, `#44483D`                                    |
| review_entity_type          | text     | "Limited Company · Technology · Est. 2019" — `body_medium`, `#44483D`                                    |
| review_owners_count         | text     | "2 Beneficial Owners · 85% accounted" — `body_medium`, `#44483D`                                         |
| submit_corporate_button     | button   | "Submit Corporate Application" — filled, `#4C662B`, white, full-width                                    |
| back_button                 | button   | "Back" — outlined, `#4C662B`, flex:1; disabled on step 1                                                 |
| next_button                 | button   | "Next" — filled, `#4C662B`, white, flex:1                                                                |

---

## States

| ID        | Trigger                              | Description                                                                    |
|-----------|--------------------------------------|--------------------------------------------------------------------------------|
| step_1    | Screen entry / Back from step 2      | Progress stepper (step 1 active) + company info form fields + Back/Next nav    |
| step_2    | Next from step 1                     | Progress stepper (step 2 active) + owner cards + ownership validator + Add Owner button |
| step_3    | Next from step 2                     | Progress stepper (step 3 active) + 3 document upload buttons                  |
| step_4    | Next from step 3                     | Progress stepper (step 4 active) + review summary card + Submit button         |
| loading   | Submit tapped                        | Full-screen overlay with "Submitting corporate application…" progress message  |
| submitted | API returns 200 OK                   | Success banner; navigate to account-applications                               |
| error     | API validation or network failure    | Error banner with failure message; form re-enabled                             |
| content   | Alias for step_1                     | Same as step_1                                                                 |
| empty     | Endpoint unavailable / session lost  | Empty state: `business_center` icon + "Corporate onboarding unavailable. Contact support." |

---

## State Model

**ViewModel:** `CorporateOnboardingViewModel`
**Screen State Type:** `CorporateOnboardingUiState`

| Name              | Type                       | Default       |
|-------------------|----------------------------|---------------|
| currentStep       | Int                        | `1`           |
| companyInfo       | CompanyInfoDraft           | (empty draft) |
| beneficialOwners  | List\<BeneficialOwnerDraft\> | `emptyList()` |
| ownershipTotal    | Float                      | `0.0`         |
| documents         | CorporateDocumentsDraft    | (empty draft) |
| isSubmitting      | Boolean                    | `false`       |
| validationErrors  | Map\<String, String\>      | `emptyMap()`  |

**Events:** `StepAdvanced`, `StepBacked`, `OwnerAdded`, `OwnerRemoved`, `DocumentUploaded`, `ApplicationSubmitted`, `RetryLoadEvent`

**Actions:** `go_next`, `go_back`, `add_owner`, `upload_cert`, `upload_tax`, `upload_document`, `submit`, `retry_load`

**DI Dependencies:** `CustomerRepository`, `DocumentUploadService`, `FormValidator`

**Errors:**
- `SUBMIT_FAILED`: "Could not submit application. Please try again."
- `OWNERSHIP_NOT_100_PERCENT`: "Total beneficial ownership must equal 100% before proceeding."
- `DOCUMENT_UPLOAD_FAILED`: "Document upload failed. Please check the file and try again."
- `VALIDATION_FAILED`: "Please correct the highlighted fields before continuing."
- `NETWORK_UNAVAILABLE`: "No internet connection. Please try again."

---

## Navigation

| From                 | To                    | Trigger                    | Type  |
|----------------------|-----------------------|----------------------------|-------|
| corporate-onboarding | corporate-onboarding  | `next_button` → step 2/3/4 | state |
| corporate-onboarding | corporate-onboarding  | `back_button` → prev step  | state |
| corporate-onboarding | account-applications  | `submit_corporate_button` → POST success | push |

---

## API Endpoints

| Endpoint                                      | Auth        | Tag       | Purpose                                          |
|-----------------------------------------------|-------------|-----------|--------------------------------------------------|
| POST /obp/v5.1.0/banks/{bankId}/customers     | DirectLogin | Customers | Create new corporate customer record on submit    |

---

## Design Tokens

| Token                          | Value   | Usage                                                                  |
|--------------------------------|---------|------------------------------------------------------------------------|
| color.light.primary            | #4C662B | Active step indicator bg, step label text, all outlined buttons, filled buttons, submit button |
| color.light.secondary          | #386663 | "Upload Directors' ID" button border + text                            |
| color.light.background         | #F9FAEF | Screen background                                                      |
| color.light.surface            | #FFFFFF | Owner cards, review card, stepper background                           |
| color.light.on_surface         | #1A1C16 | Review card company name, owner names                                  |
| color.light.on_surface_variant | #44483D | Field labels, owner ownership %, ID numbers, review detail text        |
| color.light.surface_variant    | #E1E4D5 | Stepper connectors, inactive step circles, card borders                |
| color.light.primary_container  | #CDEDA3 | Ownership validator background                                         |
| color.semantic.pending         | #E8A317 | Ownership validator warning border                                     |
| color.light.on_primary         | #FFFFFF | Active step number text, filled button text                            |
| typography.body_medium         | —       | Step label, form field values, owner card body, review card details     |
| typography.body_large          | —       | Owner names in owner cards                                             |
| typography.body_small          | —       | Owner ID numbers, ownership percentage detail                          |
| typography.title_medium        | —       | Review card company name                                               |
| typography.label_medium        | —       | Button labels, step indicator numbers                                  |
| radius.md                      | 12dp    | Review card border-radius                                              |
| radius.sm                      | 8dp     | Owner cards, ownership validator                                       |
| radius.pill                    | 999dp   | Step indicator circles (28dp = pill when radius > width/2)             |
| spacing.md                     | 16dp    | Form fields horizontal margin, card padding                            |

---

_Generated by /idea export | 2026-05-29_
