# Visual Specification — New Customer Onboarding

| Field  | Value                          |
|--------|-------------------------------|
| Feature | customer-onboarding          |
| Flavor  | fieldOfficer                 |

---

## Screen Layout

The screen is a single-screen wizard with a sticky progress header and scrollable form body. Component hierarchy top-to-bottom:

```
[ Top App Bar — "New Customer Onboarding" (back arrow) ]
[ progress_stepper — horizontal 4-step indicator, white bg, bottom border ]
[ step_indicator_text — "Step N of 4: {Step Name}" ]
[ --- scrollable form content (step-dependent) --- ]
[ nav_button_row — sticky at bottom: Back | Next ]
```

Step 4 replaces nav_button_row with submit_button above the nav row.

---

## Components

### progress_stepper

A fixed-height horizontal strip (paddingVertical: 16, paddingHorizontal: 12) on white (#FFFFFF) with a 1px bottom border (#E0E0E0). Contains four circular step indicators (28×28dp, borderRadius 20) connected by flex-1 dividers (2px height).

- Completed step: green (#4CAF50) circle with white checkmark icon (size 16)
- Active step: primary purple (#1800B1) circle with white step number (label_medium, weight 700)
- Upcoming step: grey (#E0E0E0) circle with grey number (#999999)
- Active connector (left of active): green (#4CAF50)
- Inactive connector: grey (#E0E0E0)

### step_indicator_text

`body_medium`, color #1800B1, paddingHorizontal 16, paddingTop 12, paddingBottom 4.
Example: "Step 2 of 4: Address Information"

### Step 1 — Personal Information Fields

Six outlined text fields stacked vertically (marginHorizontal 16, marginBottom 12 each):
- First Name — no placeholder (required indicator)
- Last Name — no placeholder (required indicator)
- Date of Birth — placeholder "14/03/1985", taps to open date picker
- National ID Number — placeholder "KE12345678" (required)
- Mobile Phone — prefix "+254", placeholder "722 123 456" (required)
- Email Address — placeholder "john.mwangi@gmail.com" (optional)

All fields use `variant: outlined` with #1800B1 focus ring.

### Step 2 — Address Fields

Four outlined fields:
- Street Address — placeholder "123 Moi Avenue"
- City — placeholder "Nairobi"
- County — dropdown: Nairobi | Mombasa | Kisumu | Nakuru | Eldoret | Nyeri | Thika | Kitale
- Postcode — placeholder "00100"

### Step 3 — KYC Documents

Dropdown (ID Document Type) + three full-width buttons:
- ID type dropdown: National ID | Passport | Driver's License
- "Upload ID — Front Side" — outlined, border #1800B1, icon camera, fills width
- "Upload ID — Back Side" — outlined, border #1800B1, icon camera, fills width
- "Capture Selfie / Liveness Check" — outlined, border #008B8B, text #008B8B, icon face, fills width

### Step 4 — Review Summary Card

White card (borderRadius 12, padding 16, marginHorizontal 16, elevation 2):
- "John Kamau Mwangi" — title_medium, #1A1A1A, weight 600
- "National ID: KE12345678" — body_medium, #666666
- "Phone: +254 722 123 456" — body_medium, #666666
- "123 Moi Avenue, Nairobi, 00100" — body_medium, #666666

Below card: "Submit Application" — filled button, bg #1800B1, white text, full width.

### nav_button_row

Horizontal stack (justifyContent: space_between, paddingHorizontal 16, paddingVertical 16, gap 12):
- "Back" — outlined, border #1800B1, text #1800B1, flex 1
- "Next" — filled, bg #1800B1, white text, flex 1

Back button is hidden or disabled on step_1.

---

## Interaction Patterns

- **Step advance**: Tap "Next" → validate current step fields → animate slide-left to next step, update stepper
- **Step back**: Tap "Back" → animate slide-right to previous step, restore saved values
- **Date picker**: Tap dob_input → system date picker dialog opens; selected date fills field in DD/MM/YYYY
- **County picker**: Tap county_select → bottom sheet with county list options
- **Document upload**: Tap front/back buttons → system file picker or camera chooser (ACTION_GET_CONTENT / camera intent)
- **Selfie capture**: Tap selfie button → open liveness camera flow; on completion, returns to step_3
- **Submit**: Tap "Submit Application" → show submitting overlay → run 10-step OBP chain sequentially → on success, navigate to kyc-review; on failure, show error banner

---

## Content Data

| Field                | Sample Value              |
|----------------------|---------------------------|
| First Name           | John                      |
| Last Name            | Mwangi                    |
| Date of Birth        | 14/03/1985                |
| National ID          | KE12345678                |
| Mobile Phone         | +254 722 123 456          |
| Email                | john.mwangi@gmail.com     |
| Street               | 123 Moi Avenue            |
| City                 | Nairobi                   |
| County               | Nairobi                   |
| Postcode             | 00100                     |
| Review Name          | John Kamau Mwangi         |
| Review Address       | 123 Moi Avenue, Nairobi, 00100 |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 used for active step, input focus rings, Next/Submit buttons, step label text, Back button border
- Green #4CAF50 for completed steps and connector lines — signals safe forward progress
- Teal #008B8B for the selfie/liveness button to differentiate biometric capture from document upload
- Error red #BA1A1A for field validation messages

**Typography:**
- Step indicator text: label_medium (weight 700) on step circles
- Step label below stepper: body_medium
- Form labels: body_medium outlined input labels
- Review card name: title_medium weight 600
- Review card details: body_medium, color #666666

**Spacing:**
- All form fields: marginHorizontal 16dp, marginBottom 12dp
- Stepper: paddingHorizontal 12dp, paddingVertical 16dp
- Nav button row: paddingHorizontal 16dp, paddingVertical 16dp, gap 12dp between buttons

**Accessibility:**
- Each step indicator has contentDescription: "Step N {Name} — Completed/Current/Upcoming"
- Role: progressbar on the stepper box
- All required fields declare contentDescription with ", required" suffix
- Phone field describes Kenya country code context
- Nav buttons describe direction: "Go back to previous step" / "Continue to next step"
- Submit button: "Submit customer application"

*Generated by /idea export | 2026-05-25*
