# MOCKUP — Corporate Customer Onboarding

**Archetype:** form
**Shell:** Top app bar ("New Corporate Customer") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: step_1 (Company Information)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │  ← TopAppBar, #F9FAEF bg, back arrow icon
├─────────────────────────────────────┤
│  ●────────○────────○────────○       │  ← progress_stepper: #FFFFFF bg, #E1E4D5 border-bottom
│  1        2        3        4       │     step1 circle: #4C662B bg, #FFFFFF "1" label_medium/700
│                                     │     circles 2-4: #E1E4D5 bg, #44483D numbers
│  Step 1 of 4: Company Information   │  ← step_label: body_medium, #4C662B; spacing.md H-pad
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Legal Company Name *        │   │  ← company_name_input: OutlinedTextField
│  │  Kamau Enterprises Limited   │   │     56dp height, 4dp radius, #C5C8BA border
│  └──────────────────────────────┘   │     focus → #4C662B border; spacing.md H-margin
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Business Registration No *  │   │  ← registration_number_input
│  │  CPR/2019/123456             │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │  KRA PIN *                   │   │  ← kra_pin_input
│  │  P051234567A                 │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Industry               ▾    │   │  ← industry_select: ExposedDropdownMenu
│  │  Technology                  │   │     options: Manufacturing / Retail / Services /
│  └──────────────────────────────┘   │     Agriculture / Technology / Finance /
│                                     │     Construction / Transport & Logistics
│  ┌──────────────────────────────┐   │
│  │  Entity Type            ▾    │   │  ← entity_type_select: ExposedDropdownMenu
│  │  Limited Company             │   │     options: Sole Proprietorship / Partnership /
│  └──────────────────────────────┘   │     Limited Company / NGO / Co-operative /
│                                     │     Public Benefit Organization
│  ┌──────────────────────────────┐   │
│  │  Year Established            │   │  ← year_established_input: number type
│  │  2019                        │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌────────────┐  ┌───────────────┐  │  ← nav_buttons: H-stack, space-between, 12dp gap
│  │   Back     │  │    Next →     │  │     back_button: outlined #4C662B, flex:1
│  └────────────┘  └───────────────┘  │     next_button: filled #4C662B/#FFFFFF, flex:1
└─────────────────────────────────────┘
```

**Layout notes:**
- All text fields: 56dp height (component_tokens.text_field.height), 4dp radius, `#C5C8BA` resting border → `#4C662B` focused border.
- `spacing.md` (16dp) horizontal margin on all form inputs.
- Step circle 1: `#4C662B` bg, `#FFFFFF` "1" at `label_medium`/700. Circles 2–4: `#E1E4D5` bg, `#44483D` numbers.
- Connector lines (connector_1..3): 2dp height, `#E1E4D5`, `flex:1`, `spacing.xs` horizontal margin.

---

## Screen: step_2 (Beneficial Owners)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓────────●────────○────────○       │  ← step 1 complete (filled), step 2 active #4C662B
│  Step 2 of 4: Beneficial Owners     │  ← body_medium, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │  ← owner_1_card: #FFFFFF bg, 10dp radius, elev 1
│  │  James Otieno Kamau           │  │     #E1E4D5 border, 14dp padding
│  │  Ownership: 60%               │  │     owner_1_name: body_large, #1A1C16, weight 600
│  │  National ID: KE78901234      │  │     owner_1_ownership: body_medium, #386663
│  └───────────────────────────────┘  │     owner_1_id: body_small, #44483D
│                                     │
│  ┌───────────────────────────────┐  │  ← owner_2_card: same token set as owner_1_card
│  │  Grace Wanjiku Muthoni        │  │
│  │  Ownership: 25%               │  │     owner_2_ownership: body_medium, #386663
│  │  National ID: KE23456789      │  │     owner_2_id: body_small, #44483D
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← ownership_validator: #CDEDA3 bg, #E8A317 1dp border
│  │  ⚠ Total ownership: 85%      │  │     role=alert, 8dp radius, 12dp padding
│  │     — must sum to 100%        │  │     text: body_medium, #44483D (7.25:1 contrast, WCAG AA ✓)
│  └───────────────────────────────┘  │
│                                     │
│  ┌ + Add Beneficial Owner ────────┐ │  ← add_owner_button: outlined #4C662B, person_add icon
│  └────────────────────────────────┘ │     full-width, spacing.md H-margin
│                                     │
│  ┌────────────┐  ┌───────────────┐  │
│  │   Back     │  │    Next →     │  │
│  └────────────┘  └───────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:**
- Owner cards: `#FFFFFF`, 10dp radius, 1dp elevation (`#E1E4D5` border), 14dp internal padding, `spacing.md` horizontal margin, 10dp bottom margin.
- Ownership percentage: `body_medium`, `#386663` (secondary teal — positive/informational).
- Validator: `#CDEDA3` bg with `#E8A317` warning border. Text `#44483D` (NOT `#E8A317` — contrast fix A11Y-002: 7.25:1 vs failing 1.68:1).

---

## Screen: step_3 (Documents)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓────────✓────────●────────○       │  ← steps 1+2 complete, step 3 active #4C662B
│  Step 3 of 4: Documents             │  ← body_medium, #4C662B
│                                     │
│  ┌ ↑ Upload Certificate of ───────┐ │  ← upload_cert_button: outlined #4C662B
│  │   Incorporation                 │ │     upload_file icon leading, full-width
│  └────────────────────────────────┘ │     spacing.md H-margin, spacing.sm bottom
│                                     │
│  ┌ ↑ Upload Tax Compliance ───────┐ │  ← upload_tax_button: outlined #4C662B
│  │   Certificate                  │ │     upload_file icon leading, full-width
│  └────────────────────────────────┘ │
│                                     │
│  ┌ 🪪 Upload Directors' ID ───────┐ │  ← upload_directors_id_button: outlined #386663 (secondary)
│  │    Documents                   │ │     badge icon leading, full-width
│  └────────────────────────────────┘ │
│                                     │
│  ┌────────────┐  ┌───────────────┐  │
│  │   Back     │  │    Next →     │  │
│  └────────────┘  └───────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:**
- Upload buttons: full-width `OutlinedButton`, leading icon, `spacing.md` horizontal margin.
- Certificate of Incorporation + Tax Compliance: `#4C662B` border and text with `upload_file` icon.
- Directors' ID: `#386663` secondary teal with `badge` icon — visually distinct from green buttons.
- All buttons 40dp height (component_tokens.button.height_default), 999dp radius (pill).

---

## Screen: step_4 (Review & Submit)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓────────✓────────✓────────●       │  ← steps 1-3 complete, step 4 active #4C662B
│  Step 4 of 4: Review                │  ← body_medium, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │  ← corporate_review_card: #FFFFFF, 12dp radius, elev 2
│  │  Kamau Enterprises Limited    │  │     review_company_name: title_medium/700, #1A1C16
│  │                               │  │
│  │  Reg: CPR/2019/123456         │  │     review_reg_number: body_medium, #44483D
│  │  KRA: P051234567A             │  │
│  │                               │  │
│  │  Limited Company · Technology │  │     review_entity_type: body_medium, #44483D
│  │  Est. 2019                    │  │
│  │                               │  │
│  │  2 Beneficial Owners          │  │     review_owners_count: body_medium, #44483D
│  │  85% accounted                │  │     (85% note: ownership incomplete — warn context)
│  └───────────────────────────────┘  │     16dp internal padding, spacing.md H-margin
│                                     │
│  ┌ Submit Corporate Application ─┐  │  ← submit_corporate_button: FilledButton #4C662B
│  └────────────────────────────────┘  │     #FFFFFF text, full-width, spacing.md H-margin
│                                     │
│  ┌────────────┐                      │  ← nav_buttons step 4: Back only (no Next)
│  │   Back     │                      │     back_button: outlined #4C662B
│  └────────────┘                      │
└─────────────────────────────────────┘
```

**Layout notes:**
- Review card: 16dp internal padding, 12dp radius, elevation 2 (3dp shadow per M3 level2). All step 1–2 data shown.
- Submit button: full-width `FilledButton`, `#4C662B` bg, `#FFFFFF` text, `label_medium` typography.
- Step 4 nav row: Back button only (flex:1 left side). No Next button visible.

---

## Screen: loading (Submission in progress)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│              ◌                      │  ← CircularProgressIndicator, 48dp, #4C662B
│                                     │
│     Submitting corporate            │  ← overlayMessage: body_medium, #44483D, centered
│     application...                  │
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen modal overlay with `#000000` scrim at low opacity. Spinner centred vertically. Message "Submitting corporate application…" from `ui.yaml#states.loading.overlayMessage`. All form inputs and buttons blocked during submission.

---

## Screen: submitted (Success)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ✓  Application submitted     │  │  ← Success banner: #CDEDA3 bg, #4C662B icon + text
│  │     successfully              │  │     Navigates → account-applications (push)
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ⚠  Could not submit          │  │  ← Error banner: #FFDAD6 bg, #BA1A1A text
│  │     application. Please       │  │     error_container + on_error_container tokens
│  │     try again.                │  │     8dp radius, spacing.md padding
│  └───────────────────────────────┘  │
│                                     │
│  [Step 4 review content re-shown]   │  ← Form re-enabled; user can edit + retry submit
│                                     │
└─────────────────────────────────────┘
```

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│                                     │
│              💼                     │  ← business_center icon, 48dp (icon-2xl), #C5C8BA
│                                     │
│  Corporate onboarding unavailable.  │  ← body_medium, #44483D, centered
│  Contact support.                   │     emptyStateMessage from ui.yaml#states.empty
│                                     │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar: "New Corporate Customer" title, back arrow icon, `#F9FAEF` background
- [ ] 4-step horizontal stepper: 28×28dp circles, `#4C662B` active, `#E1E4D5` upcoming/incomplete
- [ ] Connector lines: 2dp height, `#E1E4D5`, `flex:1`, `spacing.xs` (4dp) horizontal margin
- [ ] Step label: `body_medium` (Outfit 14sp/400), `#4C662B`; `spacing.md` horizontal padding
- [ ] All text inputs: `OutlinedTextField`, 56dp height, 4dp radius, `#C5C8BA` resting → `#4C662B` focused border
- [ ] Dropdown fields (industry, entity type): `ExposedDropdownMenu` with `▾` trailing icon
- [ ] Required field markers (`*`) visible on company name, registration number, KRA PIN
- [ ] Owner cards: `#FFFFFF` fill, 10dp radius, 1dp elevation, `#E1E4D5` border, 14dp padding
- [ ] Owner name: `body_large`/600, `#1A1C16`. Ownership: `body_medium`, `#386663`. ID: `body_small`, `#44483D`
- [ ] Ownership validator: `#CDEDA3` bg, `#E8A317` 1dp border, `#44483D` text (NOT `#E8A317` text — A11Y-002)
- [ ] Upload buttons: full-width `OutlinedButton`, `upload_file` icon; Incorporation + Tax `#4C662B`, Directors' IDs `#386663`
- [ ] Review card: `#FFFFFF`, 12dp radius, elevation 2 (3dp), 16dp padding
- [ ] "Submit Corporate Application": full-width `FilledButton`, `#4C662B` bg, `#FFFFFF` text
- [ ] Back (outlined `#4C662B`) + Next (filled `#4C662B`) nav row: `flex:1` each, 12dp gap; step 4 shows Back only
- [ ] Loading: `CircularProgressIndicator` 48dp `#4C662B`, "Submitting corporate application…" `body_medium` `#44483D` centred over scrim
- [ ] Error banner: `#FFDAD6` bg, `#BA1A1A` text, 8dp radius
- [ ] Empty state: `business_center` 48dp `#C5C8BA` icon, `body_medium` `#44483D` message
- [ ] All text: Outfit typeface. Touch targets ≥ 48dp on all buttons and interactive inputs.
- [ ] `spacing.md` (16dp) horizontal content padding throughout all steps.

---

_Generated by /idea export | 2026-05-30_
