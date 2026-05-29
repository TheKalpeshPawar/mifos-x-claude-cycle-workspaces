# MOCKUP — New Customer Onboarding

**Archetype:** form
**Shell:** Field Officer bottom navigation bar (5 tabs: Dashboard/Customers/Applications/Messages/More). Top app bar with back arrow — pops to customer-search.
**Accent:** #4C662B (Earth-green). Secondary: #386663 (Teal — selfie button). Typography: Outfit. Design system: M3.

---

## Screen: step_1 (Personal Information)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │  ← Top app bar, back pops to customer-search
├─────────────────────────────────────┤
│  ●─────●─────○─────○                │  ← Progress stepper: step 1 = ✓ check #4C662B
│  1     2     3     4                │    upcoming = #E1E4D5 circles, #44483D numbers
│   Step 1 of 4: Personal Information │  ← body_medium, #4C662B; pad H16/T8/B4
│                                     │
│  ┌──────────────────────────────┐   │
│  │  First Name *                │   │  ← Outlined, required; 56dp height, radius 4dp
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Last Name *                 │   │  ← Outlined, required
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Date of Birth (DD/MM/YYYY)  │   │  ← Placeholder "14/03/1985"; tap opens date picker
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  National ID Number *        │   │  ← Required; placeholder "KE12345678"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ +254 │ Mobile Phone *        │   │  ← Prefix "+254", placeholder "722 123 456"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Email Address               │   │  ← Optional; placeholder "john.mwangi@gmail.com"
│  └──────────────────────────────┘   │
│                                     │
│  ┌───────────────┐ ┌──────────────┐ │
│  │  ← Back       │ │   Next →    ▶ │ │  ← Back: outlined #4C662B, disabled step 1
│  │  (disabled)   │ │  filled #4C6  │ │     Next: filled #4C662B, #FFFFFF text
│  └───────────────┘ └──────────────┘ │    flex 1 each, gap 12dp
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │  ← Field Officer bottom nav; 80dp height
└─────────────────────────────────────┘
```

**Layout notes:**
- Stepper bar: #FFFFFF bg, 1dp border-bottom #E1E4D5, pad V16/H8. On step 1 initial entry, step 1 indicator shows "1" (returning visit shows check icon #FFFFFF on #4C662B).
- Step connector 1: #E1E4D5 (upcoming). All step indicators 28×28dp circles, 20dp radius.
- All inputs: outlined, margin H16/B8, 56dp height (text_field token), 4dp radius.
- Nav row: pad H16/V16, space-between, gap 12dp.

---

## Screen: step_2 (Address Information)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│  ✓─────●─────○─────○                │  ← Step 1 ✓ check on #4C662B; step 2 current "2"
│  ✓     2     3     4                │    Connector 1 = #4C662B; connectors 2+3 = #E1E4D5
│   Step 2 of 4: Address Information  │  ← body_medium, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Street Address              │   │  ← Placeholder "123 Moi Avenue"; margin H16/B8
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  City                        │   │  ← Placeholder "Nairobi"
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  County                   ▾  │   │  ← Select dropdown; options: Nairobi, Mombasa,
│  └──────────────────────────────┘   │    Kisumu, Nakuru, Eldoret, Nyeri, Thika, Kitale
│  ┌──────────────────────────────┐   │
│  │  Postcode                    │   │  ← Placeholder "00100"
│  └──────────────────────────────┘   │
│                                     │
│  ┌───────────────┐ ┌──────────────┐ │
│  │   ← Back      │ │   Next →    ▶ │ │
│  └───────────────┘ └──────────────┘ │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:**
- Step 1 circle: check icon 16dp #FFFFFF on #4C662B fill (completed).
- Step connector 1 (between steps 1+2): #4C662B — completed.
- County select shows trailing chevron (▾) affordance via outlined select variant.

---

## Screen: step_3 (KYC Documents)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│  ✓─────✓─────●─────○                │  ← Steps 1+2 ✓; step 3 = "3" on #4C662B; step 4 upcoming
│  ✓     ✓     3     4                │    Connectors 1+2 = #4C662B; connector 3 = #E1E4D5
│   Step 3 of 4: KYC Documents        │  ← body_medium, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  ID Document Type         ▾  │   │  ← Select: National ID / Passport / Driver's License
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Outlined full-width button
│  │  📷  Upload ID — Front Side  │   │    #4C662B border + text; camera icon leading
│  └──────────────────────────────┘   │    margin H16/B8; pill radius
│  ┌──────────────────────────────┐   │
│  │  📷  Upload ID — Back Side   │   │  ← Same styling as front upload
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Secondary colour — differentiates liveness
│  │  🤳  Capture Selfie /        │   │    #386663 border + text; face icon leading
│  │      Liveness Check          │   │    full-width; pill radius
│  └──────────────────────────────┘   │
│                                     │
│  ┌───────────────┐ ┌──────────────┐ │
│  │   ← Back      │ │   Next →    ▶ │ │
│  └───────────────┘ └──────────────┘ │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:**
- Upload buttons use #4C662B (primary green) border + text — distinguishable but aligned with brand.
- Selfie/liveness button uses #386663 (secondary teal) — signals a distinct biometric action.
- All buttons: full_width, outlined variant, pill radius (999dp), 40dp height.

---

## Screen: step_4 (Review & Submit)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│  ✓─────✓─────✓─────●                │  ← Steps 1+2+3 ✓; step 4 current "4" on #4C662B
│  ✓     ✓     ✓     4                │    All 3 connectors = #4C662B
│   Step 4 of 4: Review & Submit       │  ← body_medium, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │  ← Review summary card
│  │  John Kamau Mwangi           │   │    #FFFFFF bg; 12dp radius; elevation 2 (3dp)
│  │  National ID: KE12345678     │   │    16dp padding; margin H16/B16
│  │  Phone: +254 722 123 456     │   │    ─ review_name: title_medium, #1A1C16, w600
│  │  123 Moi Avenue, Nairobi,    │   │    ─ review_id/phone/addr: body_medium, #44483D
│  │  00100                       │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Submit Application
│  │     Submit Application       │   │    Filled full-width; #4C662B bg; #FFFFFF text
│  └──────────────────────────────┘   │    pill radius; margin H16/B8
│                                     │
│  ┌───────────────┐                  │
│  │   ← Back      │                  │  ← Back only; no Next on step 4
│  └───────────────┘                  │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:**
- Demo data in review card comes from demo-data.yaml: Kipchoge Rotich / KE12345678 (ui.yaml uses "John Kamau Mwangi" as the review_name content; both are valid demo personas).
- Submit replaces Next button. Back is present (outlined, flex unset, naturally wide).
- review_name uses weight 600 (SemiBold) for visual emphasis.

---

## Screen: loading (Submitting Application)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│                                     │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← Form content dimmed behind scrim #00000066
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│                                     │
│        ┌────────────────────┐       │  ← Centered progress overlay card
│        │   ⟳                │       │    #FFFFFF; 12dp radius; 16dp pad
│        │  Submitting         │       │    body_medium, #1A1C16
│        │  application…       │       │
│        └────────────────────┘       │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Progress overlay rendered via `showProgressOverlay: true` + `overlayMessage: "Submitting application…"`.
- All interactive elements (inputs, nav buttons) are locked / pointer-events disabled.
- Spinner uses M3 circular progress indicator, primary color #4C662B.

---

## Screen: submitted (Success)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│                                     │
│  ┌──────────────────────────────┐   │  ← Success banner
│  │  ✓  Application submitted    │   │    #CDEDA3 bg (primary_container)
│  │     successfully!            │   │    body_medium, #102000 text
│  │                              │   │    check_circle icon 24dp #4C662B
│  └──────────────────────────────┘   │
│                                     │
│     (Navigates to kyc-review)        │  ← Auto-push navigation on render
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: error (Submission Failed)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│  ┌──────────────────────────────┐   │  ← Error banner
│  │  ⚠ Application submission    │   │    #FFDAD6 bg (error_container)
│  │    failed. Please try again. │   │    body_medium, #410002 text
│  │                              │   │    error_outline icon 24dp #BA1A1A
│  │       [ Try Again ]          │   │  ← Outlined retry btn; #4C662B
│  └──────────────────────────────┘   │
│                                     │
│  (Step 4 form remains visible       │  ← User can review before retrying
│   below the error banner)           │
│                                     │
│  ┌──────────────────────────────┐   │
│  │  John Kamau Mwangi           │   │
│  │  National ID: KE12345678     │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │     Submit Application       │   │
│  └──────────────────────────────┘   │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: empty (Onboarding Unavailable)

```
┌─────────────────────────────────────┐
│ ←  New Customer Onboarding          │
├─────────────────────────────────────┤
│                                     │
│                                     │
│         [ person_off icon ]         │  ← icon-2xl (48dp), #44483D
│                                     │
│   Customer onboarding unavailable.  │  ← title_medium, #1A1C16, center
│        Contact support.             │  ← body_medium, #44483D, center
│                                     │
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:**
- Empty state: 16dp padding all sides, centered column layout.
- Icon uses `person_off` Material Symbol, 48dp (icon-2xl token), #44483D.
- No CTA button — message directs user to support channel.

---

## Design Checklist (Figma / Stitch)

- [ ] Progress stepper: 4 circles 28×28dp, 20dp radius; 3 flex-1 connectors 2dp height; completed = #4C662B + check icon; current = #4C662B + white number; upcoming = #E1E4D5 + #44483D number
- [ ] Stepper bar background: #FFFFFF; 1dp border-bottom #E1E4D5; pad V16/H8
- [ ] Step indicator text: body_medium Outfit 14sp/400; #4C662B; pad H16/T8/B4
- [ ] All text inputs: outlined variant; 56dp height; 4dp radius; #75796C border; margin H16/B8
- [ ] County select and ID type select: outlined with trailing chevron ▾ affordance
- [ ] Upload ID front/back buttons: outlined full-width; camera icon leading; #4C662B border + text; pill radius (999dp); 40dp height
- [ ] Selfie/liveness button: outlined full-width; face icon leading; #386663 border + text — distinct from ID upload buttons
- [ ] Review summary card: #FFFFFF bg; 12dp radius; elevation level2 (3dp shadow); 16dp padding; margin H16/B16
- [ ] Review name (John Kamau Mwangi): title_medium 16sp/500; #1A1C16; weight 600
- [ ] Review data rows (ID/phone/address): body_medium 14sp/400; #44483D; 2dp margin-bottom between rows
- [ ] Submit Application: filled full-width; #4C662B bg; #FFFFFF text; Label Large 14sp/500; pill radius; margin H16/B8
- [ ] Back/Next nav row: horizontal; space-between; gap 12dp; pad H16/V16; both flex 1
- [ ] Back button: outlined; #4C662B border + text; disabled on step_1
- [ ] Next button: filled; #4C662B bg; #FFFFFF text
- [ ] Loading state: semi-transparent scrim #00000066; centered card with M3 circular progress indicator (#4C662B) + "Submitting application…" body_medium
- [ ] Success banner: #CDEDA3 bg; check_circle icon #4C662B; body_medium text #102000
- [ ] Error banner: #FFDAD6 bg; error_outline icon #BA1A1A; body_medium text #410002; retry button outlined #4C662B
- [ ] Empty state: person_off icon 48dp (icon-2xl) #44483D; centered column; 16dp padding
- [ ] All text: Outfit typeface. Touch targets 48dp minimum. 16dp horizontal content padding throughout.
- [ ] Bottom nav: 5 tabs (Dashboard/Customers/Applications/Messages/More); 80dp height; #F9FAEF bg; #C5C8BA border-top

---

_Generated by /idea export | 2026-05-30_
