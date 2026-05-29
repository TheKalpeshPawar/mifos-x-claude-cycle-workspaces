# MOCKUP — Corporate Customer Onboarding

**Archetype:** form
**Shell:** Top app bar ("New Corporate Customer") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: step_1 (Company Information)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │  ← TopAppBar, back arrow
├─────────────────────────────────────┤
│  ●─────○─────○─────○                │  ← step stepper: 1 active (#4C662B), 2-4 grey
│    1       2       3       4        │     connectors #E1E4D5, circles 28dp
│  Step 1 of 4: Company Information   │  ← body_medium, #4C662B
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Legal Company Name *       │    │  ← OutlinedTextField, required
│  │  Kamau Enterprises Limited  │    │     placeholder shown greyed when empty
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Business Reg. Number *     │    │
│  │  CPR/2019/123456            │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  KRA PIN *                  │    │
│  │  P051234567A                │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Industry          ▾        │    │  ← ExposedDropdownMenu
│  │  Technology                 │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Entity Type       ▾        │    │
│  │  Limited Company            │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Year Established           │    │
│  │  2019                       │    │
│  └─────────────────────────────┘    │
│                                     │
│  [ Back ]         [ Next → ]        │  ← outlined + filled, flex:1 each, 16dp gap
└─────────────────────────────────────┘
```

**Layout notes:**
- All text fields: 56dp height, 4dp radius, `#C5C8BA` border, `#4C662B` focused border.
- 16dp horizontal margin on all form fields.
- Back button outlined `#4C662B`; Next filled `#4C662B` white text.
- Step circle 1: `#4C662B` bg, white "1". Circles 2-4: `#E1E4D5` bg, `#44483D` numbers.

---

## Screen: step_2 (Beneficial Owners)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓─────●─────○─────○                │  ← step 1 complete (tick/green), 2 active
│  Step 2 of 4: Beneficial Owners     │  ← body_medium, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │
│  │  James Otieno Kamau           │  │  ← owner card, white, 10dp radius, elev 1
│  │  Ownership: 60%               │  │     ownership in #386663 (secondary)
│  │  National ID: KE78901234      │  │     ID in body_small #44483D
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Grace Wanjiku Muthoni        │  │  ← owner 2 card
│  │  Ownership: 25%               │  │
│  │  National ID: KE23456789      │  │
│  └───────────────────────────────┘  │
│                                     │
│  ⚠  Total ownership: 85%           │  ← warning box, #CDEDA3 bg, #E8A317 border
│     — must sum to 100%              │     text #44483D (7.25:1 contrast)
│                                     │
│  ┌ + Add Beneficial Owner ────────┐ │  ← outlined #4C662B, person_add icon, full-width
│  └────────────────────────────────┘ │
│                                     │
│  [ Back ]         [ Next → ]        │
└─────────────────────────────────────┘
```

**Layout notes:** Owner cards: white, 10dp radius, 1dp `#E1E4D5` border, 14dp padding. Ownership in `body_medium` `#386663`. Validator box: 12dp padding, 4dp `#E8A317` left border accent would be ideal here; corner 8dp radius.

---

## Screen: step_3 (Documents)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓─────✓─────●─────○                │  ← steps 1+2 complete, step 3 active
│  Step 3 of 4: Documents             │
│                                     │
│  ┌ ↑ Upload Certificate of ───────┐ │  ← outlined #4C662B, upload_file icon
│  │   Incorporation                 │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌ ↑ Upload Tax Compliance ───────┐ │  ← outlined #4C662B, upload_file icon
│  │   Certificate                  │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌ 🪪 Upload Directors' ID ───────┐ │  ← outlined #386663 (secondary), badge icon
│  │   Documents                    │ │
│  └────────────────────────────────┘ │
│                                     │
│  [ Back ]         [ Next → ]        │
└─────────────────────────────────────┘
```

**Layout notes:** Upload buttons: full-width, outlined with icon leading. Certificate + tax: `#4C662B`. Directors' IDs: `#386663` secondary teal colour. All 40dp height, 4dp radius.

---

## Screen: step_4 (Review & Submit)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│  ✓─────✓─────✓─────●                │  ← steps 1-3 complete, step 4 active
│  Step 4 of 4: Review                │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Kamau Enterprises Limited    │  │  ← review card, white, 12dp radius, elev 2
│  │  Reg: CPR/2019/123456         │  │  ← title_medium bold #1A1C16
│  │  KRA: P051234567A             │  │  ← body_medium #44483D
│  │  Limited Company · Technology │  │
│  │  Est. 2019                    │  │
│  │  2 Beneficial Owners          │  │
│  │  85% accounted                │  │  ← NOTE: 85% warning still present
│  └───────────────────────────────┘  │
│                                     │
│  ┌ Submit Corporate Application ─┐  │  ← FilledButton, #4C662B, white, full-width
│  └────────────────────────────────┘  │
│                                     │
│  [ Back ]                           │  ← only Back on final step; no Next
└─────────────────────────────────────┘
```

**Layout notes:** Review card: 16dp internal padding, all submitted data displayed. Submit button: full-width, 40dp height, 4dp radius. Only Back button on step 4 (no Next).

---

## Screen: loading (Submission in progress)

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│                                     │
│              ○                      │  ← CircularProgressIndicator, 48dp, #4C662B
│                                     │
│     Submitting corporate            │  ← body_medium, #44483D, centered
│     application...                  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen overlay with scrim. Centred spinner and message. All form inputs blocked.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  New Corporate Customer           │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ⚠  Could not submit          │  │  ← error banner, #FFDAD6 bg, #BA1A1A text
│  │     application. Please       │  │
│  │     try again.                │  │
│  └───────────────────────────────┘  │
│                                     │
│  [Step 4 review content repeats]    │  ← form re-enabled, user can retry
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
│              💼                     │  ← business_center icon, 48dp, #C5C8BA
│                                     │
│  Corporate onboarding unavailable.  │  ← body_medium, centered, #44483D
│  Contact support.                   │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow, "New Corporate Customer" title
- [ ] 4-step horizontal stepper: 28dp circles, `#4C662B` active, `#E1E4D5` upcoming
- [ ] Connector lines 2dp `#E1E4D5` between step circles (flex:1)
- [ ] Step label `body_medium` `#4C662B` updates on each step advance
- [ ] All form fields: OutlinedTextField 56dp height, 4dp radius, `#C5C8BA` → `#4C662B` focused
- [ ] Dropdown fields: ExposedDropdownMenu with chevron trailing icon
- [ ] Owner cards: white, 10dp radius, 1dp `#E1E4D5` border, ownership in `#386663`
- [ ] Ownership validator: `#CDEDA3` bg, `#E8A317` left-accent border, `#44483D` text (WCAG AA pass)
- [ ] Upload buttons: full-width OutlinedButton with leading icon; Incorporation+Tax `#4C662B`, Directors' IDs `#386663`
- [ ] Review card: white, 12dp radius, elevation 2
- [ ] "Submit Corporate Application": full-width FilledButton `#4C662B`
- [ ] Back (outlined) + Next (filled) navigation row — 12dp gap, flex:1 each
- [ ] Loading: CircularProgressIndicator 48dp `#4C662B` + message centred over scrim
- [ ] Error banner: `#FFDAD6` bg, `#BA1A1A` text, 8dp radius
- [ ] All text: Outfit typeface; required field markers visible
- [ ] Touch targets ≥ 48dp on all buttons
