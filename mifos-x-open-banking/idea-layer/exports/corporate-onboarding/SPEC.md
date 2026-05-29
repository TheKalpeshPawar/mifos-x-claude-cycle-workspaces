# SPEC — Corporate Customer Onboarding

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | corporate-onboarding           |
| Flavor        | fieldOfficer                   |
| Status        | designed                       |
| Quality Score | 94                             |
| ViewModel     | CorporateOnboardingViewModel   |

---

## Overview

The Corporate Customer Onboarding screen enables Field Officers to register new corporate clients through a guided 4-step wizard. Steps are: (1) Company Information — legal company name, business registration number, KRA PIN, industry (dropdown: Manufacturing / Retail / Services / Agriculture / Technology / Finance / Construction / Transport & Logistics), entity type (dropdown: Sole Proprietorship / Partnership / Limited Company / NGO / Co-operative Society / Public Benefit Organization), and year established; (2) Beneficial Owners — owner cards (name, ownership %, national ID) with an inline ownership total validator (`#CDEDA3` alert box) warning when total < 100%, plus an "Add Beneficial Owner" outlined button; (3) Documents — three full-width outlined upload buttons for Certificate of Incorporation, Tax Compliance Certificate, and Directors' ID documents; (4) Review & Submit — a summary card (white, 12dp radius, elevation 2) showing company name, registration/KRA, entity + industry + year, and beneficial owner count before the `POST /customers` call. A horizontal 4-step progress indicator with 28dp numbered circles and `#E1E4D5` connector lines runs at the top of every step. Back/Next navigation buttons (outlined Back + filled Next, flex:1 each, 12dp gap) appear at the bottom. On success, the `submitted` state fires a success banner and navigates to `account-applications`. No bottom navigation bar — accessed from the Field Officer workflow.

---

## Screens

| ID                        | Name                   | Route                 | Layout | Scroll   |
|---------------------------|------------------------|-----------------------|--------|----------|
| corporate-onboarding-main | New Corporate Customer | /corporate-onboarding | Column | Vertical |

**Shell:** Top app bar ("New Corporate Customer", back arrow). No bottom navigation bar.

---

## Components

| ID                         | Type    | Description                                                                                                                |
|----------------------------|---------|----------------------------------------------------------------------------------------------------------------------------|
| progress_stepper           | box     | Horizontal stepper; white bg (`#FFFFFF`), `#E1E4D5` 1dp border-bottom; horizontal stack of 4 numbered circles + connectors |
| step1_indicator            | box     | 28×28dp circle; bg `#4C662B` (active step); white "1" label, `Outfit/label_medium` 700 weight                             |
| step2_indicator            | box     | 28×28dp circle; bg `#E1E4D5` (upcoming); `#44483D` "2" label, `Outfit/label_medium` 700 weight                            |
| step3_indicator            | box     | 28×28dp circle; bg `#E1E4D5`; `#44483D` "3" label                                                                         |
| step4_indicator            | box     | 28×28dp circle; bg `#E1E4D5`; `#44483D` "4" label                                                                         |
| connector_1                | divider | Horizontal, 2dp height, `#E1E4D5`; flex:1 between step 1 and step 2 circles                                               |
| connector_2                | divider | Horizontal, 2dp height, `#E1E4D5`; flex:1 between step 2 and step 3 circles                                               |
| connector_3                | divider | Horizontal, 2dp height, `#E1E4D5`; flex:1 between step 3 and step 4 circles                                               |
| step_label                 | text    | "Step 1 of 4: Company Information" — `Outfit/body_medium`, `#4C662B`; `spacing.md` horizontal padding; updates per step   |
| company_name_input         | input   | Label "Legal Company Name"; outlined variant; placeholder "Kamau Enterprises Limited"; required; text type                 |
| registration_number_input  | input   | Label "Business Registration Number"; outlined; placeholder "CPR/2019/123456"; required; text type                        |
| kra_pin_input              | input   | Label "KRA PIN"; outlined; placeholder "P051234567A"; required; text type                                                  |
| industry_select            | input   | Label "Industry"; outlined; select/dropdown; options: Manufacturing, Retail, Services, Agriculture, Technology, Finance, Construction, Transport & Logistics |
| entity_type_select         | input   | Label "Entity Type"; outlined; select/dropdown; options: Sole Proprietorship, Partnership, Limited Company, NGO, Co-operative Society, Public Benefit Organization |
| year_established_input     | input   | Label "Year Established"; outlined; placeholder "2019"; number input type                                                  |
| owner_1_card               | box     | White, 10dp radius, 1dp elevation, `#E1E4D5` border, 14dp padding; displays "James Otieno Kamau" / "Ownership: 60%" / "National ID: KE78901234" |
| owner_2_card               | box     | White, 10dp radius, 1dp elevation, `#E1E4D5` border, 14dp padding; displays "Grace Wanjiku Muthoni" / "Ownership: 25%" / "National ID: KE23456789" |
| ownership_validator        | box     | `#CDEDA3` bg, `#E8A317` 1dp border, 8dp radius, 12dp padding; role=alert; contains `ownership_total_text`                 |
| ownership_total_text       | text    | "Total ownership: 85% — must sum to 100%" — `Outfit/body_medium`, `#44483D` (7.25:1 contrast ratio, WCAG AA pass)         |
| add_owner_button           | button  | "Add Beneficial Owner"; outlined, `#4C662B` border + text, `person_add` icon leading, full-width                          |
| upload_cert_button         | button  | "Upload Certificate of Incorporation"; outlined, `#4C662B`, `upload_file` icon leading, full-width                        |
| upload_tax_button          | button  | "Upload Tax Compliance Certificate"; outlined, `#4C662B`, `upload_file` icon leading, full-width                           |
| upload_directors_id_button | button  | "Upload Directors' ID Documents"; outlined, `#386663` (secondary), `badge` icon leading, full-width                       |
| corporate_review_card      | box     | White, 12dp radius, 16dp padding, elevation 2; displays all data entered across steps 1–2                                  |
| review_company_name        | text    | "Kamau Enterprises Limited" — `Outfit/title_medium`, `#1A1C16`, weight 700                                                |
| review_reg_number          | text    | "Reg: CPR/2019/123456 · KRA: P051234567A" — `Outfit/body_medium`, `#44483D`                                               |
| review_entity_type         | text    | "Limited Company · Technology · Est. 2019" — `Outfit/body_medium`, `#44483D`                                               |
| review_owners_count        | text    | "2 Beneficial Owners · 85% accounted" — `Outfit/body_medium`, `#44483D`                                                   |
| submit_corporate_button    | button  | "Submit Corporate Application"; filled, `#4C662B` bg, `#FFFFFF` text, full-width                                           |
| back_button                | button  | "Back"; outlined, `#4C662B`, flex:1; disabled on step 1                                                                    |
| next_button                | button  | "Next"; filled, `#4C662B` bg, `#FFFFFF` text, flex:1; hidden on step 4                                                    |
| nav_buttons                | stack   | Horizontal stack; space-between; `spacing.md` horizontal padding + vertical padding; 12dp gap; contains Back + Next        |

---

## States

| ID        | Trigger                              | Description                                                                                              |
|-----------|--------------------------------------|----------------------------------------------------------------------------------------------------------|
| step_1    | Screen entry / Back from step 2      | Progress stepper (step 1 active `#4C662B`) + company info form fields (6 inputs) + Back/Next nav row    |
| step_2    | Next from step 1                     | Progress stepper (step 2 active) + 2 owner cards + ownership validator alert + Add Owner button + nav row |
| step_3    | Next from step 2                     | Progress stepper (step 3 active) + 3 document upload buttons + nav row                                   |
| step_4    | Next from step 3                     | Progress stepper (step 4 active) + review summary card + Submit button + nav row (Back only)             |
| loading   | Submit tapped                        | Full-screen overlay with `CircularProgressIndicator` + "Submitting corporate application…" message       |
| submitted | `POST /customers` returns 200 OK     | Success banner shown; navigate to `account-applications`                                                  |
| error     | API validation or network failure    | Error banner (`#FFDAD6` bg, `#BA1A1A` text); form re-enabled for retry                                  |
| content   | Alias for step_1                     | Same component set as step_1 (initial visible state)                                                     |
| empty     | Endpoint unavailable / session lost  | Empty state: `business_center` icon (48dp, `#C5C8BA`) + "Corporate onboarding unavailable. Contact support." |

---

## State Model

**ViewModel:** `CorporateOnboardingViewModel`
**Screen State Type:** `CorporateOnboardingUiState`

| Name             | Type                          | Default       |
|------------------|-------------------------------|---------------|
| currentStep      | Int                           | `1`           |
| companyInfo      | CompanyInfoDraft              | (empty draft) |
| beneficialOwners | List\<BeneficialOwnerDraft\>  | `emptyList()` |
| ownershipTotal   | Float                         | `0.0`         |
| documents        | CorporateDocumentsDraft       | (empty draft) |
| isSubmitting     | Boolean                       | `false`       |
| validationErrors | Map\<String, String\>         | `emptyMap()`  |

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

| From                 | To                   | Trigger                                          | Type  |
|----------------------|----------------------|--------------------------------------------------|-------|
| corporate-onboarding | corporate-onboarding | `next_button` tap on step 1 → advance to step 2  | state |
| corporate-onboarding | corporate-onboarding | `next_button` tap on step 2 → advance to step 3  | state |
| corporate-onboarding | corporate-onboarding | `next_button` tap on step 3 → advance to step 4  | state |
| corporate-onboarding | corporate-onboarding | `back_button` tap → return to previous step       | state |
| corporate-onboarding | account-applications | `submit_corporate_button` tap → POST 200 success  | push  |

---

## API Endpoints

| Endpoint                                  | Auth        | Tag       | Purpose                                         |
|-------------------------------------------|-------------|-----------|-------------------------------------------------|
| POST /obp/v5.1.0/banks/{bankId}/customers | DirectLogin | Customers | Create new corporate customer record on submit  |

---

## Design Tokens

| Token                          | Value   | Usage                                                                              |
|--------------------------------|---------|------------------------------------------------------------------------------------|
| colors.light.primary           | #4C662B | Active step indicator bg, step label text, outlined + filled buttons, submit btn  |
| colors.light.secondary         | #386663 | "Upload Directors' ID" button border + text                                        |
| colors.light.primary_container | #CDEDA3 | Ownership validator background                                                     |
| colors.light.surface_variant   | #E1E4D5 | Stepper connector lines, inactive step circles, card borders, stepper border-bottom |
| colors.light.surface           | #FFFFFF | Owner cards, review card, stepper background, step indicator active text           |
| colors.light.background        | #F9FAEF | Screen background                                                                  |
| colors.light.on_surface        | #1A1C16 | Review card company name, owner names                                              |
| colors.light.on_surface_variant| #44483D | Inactive step numbers, field labels, owner body text, review detail rows           |
| colors.light.on_primary        | #FFFFFF | Active step number text, filled button labels                                      |
| colors.light.error_container   | #FFDAD6 | Error banner background                                                            |
| colors.light.error             | #BA1A1A | Error banner text                                                                  |
| colors.semantic.pending        | #E8A317 | Ownership validator border (warning accent)                                        |
| colors.light.outline_variant   | #C5C8BA | Text field resting border colour                                                   |
| typography.title_medium        | Outfit 16sp/500 | Review card company name                                                  |
| typography.body_large          | Outfit 16sp/400 | Owner names in owner cards                                                |
| typography.body_medium         | Outfit 14sp/400 | Step label, field values, ownership %, review detail rows, validator text |
| typography.body_small          | Outfit 12sp/400 | Owner national ID numbers                                                 |
| typography.label_medium        | Outfit 12sp/500/0.5 | Button labels, step indicator numbers                              |
| radius.md                      | 12dp    | Review card border-radius                                                          |
| radius.sm                      | 8dp     | Ownership validator box border-radius                                              |
| radius.pill                    | 999dp   | Step indicator circles (28dp diameter — pill when radius > width/2)               |
| spacing.md                     | 16dp    | Form fields horizontal margin, nav row padding, card padding                       |
| spacing.sm                     | 8dp     | Connector horizontal margin, step label bottom padding                             |
| spacing.xs                     | 4dp     | Step label top/bottom internal spacing                                             |
| elevation.level1               | 1dp     | Owner cards                                                                        |
| elevation.level2               | 3dp     | Review summary card                                                                |

---

_Generated by /idea export | 2026-05-30_
