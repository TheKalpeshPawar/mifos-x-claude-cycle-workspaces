# Visual Specification — Corporate Customer Onboarding

| Field   | Value                         |
|---------|------------------------------|
| Feature | corporate-onboarding         |
| Flavor  | fieldOfficer                 |

---

## Screen Layout

Single-screen 4-step wizard with a fixed progress header and scrollable step-specific content:

```
[ Top App Bar — "New Corporate Customer" (back arrow) ]
[ progress_stepper — horizontal 4-step, white strip, bottom border ]
[ step_label — "Step N of 4: {Step Name}" ]
[ --- scrollable step content --- ]
[ nav_buttons — Back | Next (sticky bottom row) ]
```

Step 4 adds submit_corporate_button above the nav_buttons row.

---

## Components

### progress_stepper

Identical structure to customer-onboarding stepper (28×28dp circles, 2px flex connectors). Starting state has step 1 active (purple #1800B1), steps 2-4 in grey (#E0E0E0). As steps complete, circles turn purple and connectors turn green.

### step_label

`body_medium`, color #1800B1, paddingHorizontal 16, paddingTop 12, paddingBottom 4.
Example: "Step 1 of 4: Company Information"

### Step 1 — Company Information

Six outlined fields (marginHorizontal 16, marginBottom 12):
- Legal Company Name — placeholder "Kamau Enterprises Limited" (required)
- Business Registration Number — placeholder "CPR/2019/123456" (required)
- KRA PIN — placeholder "P051234567A" (required)
- Industry — dropdown: Manufacturing | Retail | Services | Agriculture | Technology | Finance | Construction | Transport & Logistics
- Entity Type — dropdown: Sole Proprietorship | Partnership | Limited Company | NGO | Co-operative Society | Public Benefit Organization
- Year Established — number input, placeholder "2019"

### Step 2 — Beneficial Owners

Two owner cards followed by ownership validator and add button.

**owner_1_card** (white, borderRadius 10, padding 14, elevation 1, border #E0E0E0):
- "James Otieno Kamau" — body_large, #1A1A1A, weight 600
- "Ownership: 60%" — body_medium, color #008B8B
- "National ID: KE78901234" — body_small, color #666666

**owner_2_card** (identical structure):
- "Grace Wanjiku Muthoni" — body_large, #1A1A1A, weight 600
- "Ownership: 25%" — body_medium, color #008B8B
- "National ID: KE23456789" — body_small, color #666666

**ownership_validator** (amber box, bg #FFF8E1, border #FFB300, borderRadius 8, padding 12):
- "Total ownership: 85% — must sum to 100%" — body_medium, color #E65100, weight 500
- Role: alert — shown when ownershipTotal != 100

**add_owner_button** — outlined, border #1800B1, text #1800B1, icon person_add, full width

### Step 3 — Documents

Three full-width outlined buttons stacked (marginHorizontal 16, marginBottom 8):
- "Upload Certificate of Incorporation" — border #1800B1, text #1800B1, icon upload_file
- "Upload Tax Compliance Certificate" — border #1800B1, text #1800B1, icon upload_file
- "Upload Directors' ID Documents" — border #008B8B, text #008B8B, icon badge

### Step 4 — Corporate Review Card

White card (borderRadius 12, padding 16, elevation 2, marginHorizontal 16):
- "Kamau Enterprises Limited" — title_medium, weight 700, #1A1A1A
- "Reg: CPR/2019/123456 · KRA: P051234567A" — body_medium, #666666
- "Limited Company · Technology · Est. 2019" — body_medium, #666666
- "2 Beneficial Owners · 85% accounted" — body_medium, color #E65100 (warning — ownership not 100%)

Below: "Submit Corporate Application" — filled, bg #1800B1, white text, full width.

### nav_buttons

Horizontal row: "Back" (outlined, border #1800B1) and "Next" (filled, bg #1800B1), each flex 1, gap 12.

---

## Interaction Patterns

- **Step advance**: Tap "Next" → validate step fields (step 2 also checks ownershipTotal == 100 before allowing advance) → slide-left animation to next step
- **Ownership guard**: If ownershipTotal != 100 when tapping Next from step_2, show ownership_validator warning and block advance
- **Add owner**: Tap "Add Beneficial Owner" → opens bottom sheet to enter owner name, ID, and ownership percentage; on save, recalculates ownershipTotal
- **Document upload**: Each upload button triggers file picker (PDF/image chooser via ACTION_OPEN_DOCUMENT)
- **Submit**: Tap "Submit Corporate Application" → submitting overlay → OBP API chain (create customer → attributes for each owner → KYC docs → KYC check → KYC status → account application) → success navigates to account-applications

---

## Content Data

| Field                  | Sample Value                              |
|------------------------|-------------------------------------------|
| Legal Company Name     | Kamau Enterprises Limited                 |
| Registration Number    | CPR/2019/123456                           |
| KRA PIN                | P051234567A                               |
| Industry               | Technology                                |
| Entity Type            | Limited Company                           |
| Year Established       | 2019                                      |
| Owner 1 Name           | James Otieno Kamau                        |
| Owner 1 Ownership      | 60%                                       |
| Owner 1 ID             | KE78901234                                |
| Owner 2 Name           | Grace Wanjiku Muthoni                     |
| Owner 2 Ownership      | 25%                                       |
| Owner 2 ID             | KE23456789                                |
| Ownership Total (demo) | 85% — warning shown                       |
| Review Company         | Kamau Enterprises Limited                 |
| Review Reg+KRA         | Reg: CPR/2019/123456 · KRA: P051234567A  |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 for active step, form field focus, Next/Submit buttons, Back button outlines
- Teal #008B8B for Directors' ID button — semantically distinct (biometric/person documents vs corporate docs)
- Amber #FFF8E1/#FFB300/#E65100 for the ownership validator — acts as an inline form-level error without blocking input
- #008B8B used for ownership percentage display — teal signals a factual data value (not a warning)

**Typography:**
- Company name on review card: title_medium weight 700 — heaviest weight to signal legal entity name
- Owner names in cards: body_large weight 600
- Ownership percentage: body_medium in teal #008B8B

**Spacing:**
- Owner cards: borderRadius 10, padding 14, marginHorizontal 16, marginBottom 10, elevation 1
- Ownership validator: borderRadius 8, padding 12, marginHorizontal 16, marginBottom 8
- Upload buttons: marginHorizontal 16, marginBottom 8 (tighter than form fields — grouped visually)

**Accessibility:**
- ownership_validator role: alert — screen readers announce when total changes
- Step indicators each describe their label and state (Current/Upcoming/Completed)
- All buttons have distinct contentDescriptions matching their action context
- "Add Beneficial Owner" describes the action: "Add another beneficial owner"

*Generated by /idea export | 2026-05-25*
