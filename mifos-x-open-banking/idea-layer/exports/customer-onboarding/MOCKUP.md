# MOCKUP — New Customer Onboarding

**Archetype:** form
**Shell:** Field Officer bottom navigation bar (5 tabs). Top app bar with back arrow to customer-search.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: step_1 (Personal Information)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │  ← Top app bar, back to customer-search
├─────────────────────────────────────┤
│ ●──●──○──○                          │  ← Progress stepper (step 1 active, rest upcoming)
│   Step 1 of 4: Personal Information │  ← body_medium #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  First Name *                │   │  ← Outlined input
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Last Name *                 │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Date of Birth (DD/MM/YYYY)  │   │  ← Placeholder "14/03/1985"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  National ID Number *        │   │  ← Placeholder "KE12345678"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  +254  Mobile Phone *        │   │  ← Prefix "+254"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Email Address               │   │  ← Optional
│  └──────────────────────────────┘   │
│                                     │
│  [ Back (disabled) ] [   Next   ]   │  ← Back disabled on step 1
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:**
- Stepper: 4 circles 28dp each + 3 connectors flex 1. Step 1 = #4C662B circle with check (if returning). Upcoming = #E1E4D5.
- All inputs: outlined style, margin H16/B8, 56dp height, radius 4dp (text field token).
- Back button outlined, disabled on step 1. Next filled #4C662B.
- Nav row: space-between, pad H16/V16, gap 12.

---

## Screen: step_2 (Address)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│ ✓──●──○──○                          │  ← Step 1 completed (check), step 2 active
│   Step 2 of 4: Address Information  │  ← body_medium #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Street Address              │   │  ← "123 Moi Avenue"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  City                        │   │  ← "Nairobi"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  County           ▾          │   │  ← Select: Nairobi / Mombasa / Kisumu…
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Postcode                    │   │  ← "00100"
│  └──────────────────────────────┘   │
│                                     │
│  [   Back   ]       [   Next   ]    │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: step_3 (KYC Documents)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│ ✓──✓──●──○                          │  ← Steps 1+2 complete, step 3 active
│   Step 3 of 4: KYC Documents        │
│                                     │
│  ┌──────────────────────────────┐   │
│  │  ID Document Type     ▾      │   │  ← National ID / Passport / Driver's License
│  └──────────────────────────────┘   │
│                                     │
│  [ 📷 Upload ID — Front Side    ]   │  ← Outlined btn #4C662B, full-width
│  [ 📷 Upload ID — Back Side     ]   │  ← Outlined btn #4C662B, full-width
│                                     │
│  [ 🤳 Capture Selfie / Liveness ]   │  ← Outlined btn #386663, full-width
│                                     │
│  [   Back   ]       [   Next   ]    │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: step_4 (Review)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│ ✓──✓──✓──●                          │  ← All steps complete, step 4 active
│   Step 4 of 4: Review & Submit       │
│                                     │
│  ┌──────────────────────────────┐   │  ← Review summary card #FFFFFF, radius 12
│  │  John Kamau Mwangi           │   │    title_medium #1A1C16 bold
│  │  National ID: KE12345678     │   │    body_medium #44483D
│  │  Phone: +254 722 123 456     │   │
│  │  123 Moi Avenue, Nairobi…    │   │
│  └──────────────────────────────┘   │
│                                     │
│  [     Submit Application      ]    │  ← Filled full-width #4C662B
│                                     │
│  [   Back   ]                       │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: loading (submitting)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│                                     │
│           ◌  ──  ◌  ──  ◌          │  ← Dimmed form content
│                                     │
│  ┌──────────────────────────────┐   │
│  │  ●  Submitting application…  │   │  ← Progress overlay with spinner
│  └──────────────────────────────┘   │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Semi-transparent scrim over form content. Progress indicator centered with "Submitting application…" body_medium text. No navigation possible during submission.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│  ┌──────────────────────────────┐   │
│  │ ⚠ Application submission     │   │  ← Error banner #FFDAD6, error icon #BA1A1A
│  │   failed. Please try again.  │   │
│  │      [ Try Again ]           │   │
│  └──────────────────────────────┘   │
│                                     │
│  (Step 4 content remains visible)   │
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] Horizontal stepper: 4 circles 28dp, 3 flex connectors — completed=green check, current=green number, upcoming=grey
- [ ] All outlined inputs 56dp height, radius 4dp, #75796C border, labeled
- [ ] County and ID Type selects show dropdown chevron icon
- [ ] Upload buttons full-width outlined, camera icon leading, radius pill
- [ ] Selfie button: #386663 border + text (distinguishable from ID upload buttons)
- [ ] Review summary card: white bg, radius 12, elevation 2, 16dp padding
- [ ] Submit Application: filled full-width #4C662B pill
- [ ] Back / Next row: space-between, gap 12, both flex 1
- [ ] Loading overlay: semi-transparent scrim + centered spinner + text
- [ ] Error banner: M3 error container (#FFDAD6) + error icon + retry button
- [ ] All text Outfit typeface; 16dp horizontal padding for inputs
