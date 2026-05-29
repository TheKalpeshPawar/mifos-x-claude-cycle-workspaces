# MOCKUP — Customer Profile

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow ("Customer Information"). No bottom navigation on detail screens.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ←  Customer Information             │  ← Top app bar, #F9FAEF bg
├─────────────────────────────────────┤
│                                     │  ← Background #F9FAEF, pad 16
│  Personal Information               │  ← title_large, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Full Name                   │   │  ← #FFFFFF row, radius 8, pad V12/H16
│  │             John Kamau Mwangi│   │  ← body_large #1A1C16 bold, space-between
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Date of Birth               │   │
│  │    14 March 1985 (Age: 41)   │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  National ID                 │   │
│  │                   KE12345678 │   │  ← monospace
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Tax PIN (KRA)               │   │
│  │             A001234567M      │   │  ← monospace
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Phone                       │   │
│  │       +254 722 123 456 🔗    │   │  ← body_large #4C662B underline, tappable
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Email                       │   │
│  │  john.mwangi@gmail.com 🔗    │   │  ← body_large #4C662B underline, tappable
│  └──────────────────────────────┘   │
│                                     │
│  ─────────────────────────────────  │  ← Divider #E1E4D5, margin V16
│                                     │
│  Address                            │  ← title_large, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  123 Moi Avenue, Nairobi     │   │  ← body_large #1A1C16
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Nairobi County, Kenya       │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Postcode: 00100             │   │
│  └──────────────────────────────┘   │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Employment                         │  ← title_large, #4C662B
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Employer          Safaricom │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Monthly Income    KES 85,000│   │  ← monospace value
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │  Employment Type   Permanent │   │
│  └──────────────────────────────┘   │
│                                     │
│  [      Edit Information       ]    │  ← Outlined full-width #4C662B, margin T8/B24
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen pad 16dp all sides; #F9FAEF background.
- Section headings: title_large #4C662B, paddingBottom 8dp.
- Data rows: #FFFFFF bg, radius 8dp, pad V12/H16, marginBottom 2dp. Horizontal stack space-between.
- Labels: body_medium #44483D weight 500 (left). Values: body_large #1A1C16 (right).
- Monospace values (national ID, tax PIN, income): system monospace font family.
- Phone + email: body_large #4C662B underline, tap opens system dialler / mail client.
- Dividers: full-width #E1E4D5, marginVertical 16dp.
- Edit button: outlined full-width pill, #4C662B.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Customer Information             │
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │  ← Heading visible
│                                     │
│  ████████████████████████████████   │  ← Row skeleton ×6 (shimmer)
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│                                     │
│  Address                            │
│  ████████████████████████████████   │  ← Row skeleton ×3
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│                                     │
│  Employment                         │
│  ████████████████████████████████   │  ← Row skeleton ×3
│  ████████████████████████████████   │
│  ████████████████████████████████   │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Section heading labels remain visible; only data row content shimmers. Shimmer on #F0F1E6 base. Edit button hidden during loading.

---

## Screen: editing

```
┌─────────────────────────────────────┐
│ ←  Customer Information    [Save]   │  ← Save action in top bar
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │
│                                     │
│  ┌──────────────────────────────┐   │
│  │  Full Name                   │   │  ← Value becomes editable input
│  │  [John Kamau Mwangi_____]    │   │
│  └──────────────────────────────┘   │
│  (phone, email, address editable)   │
│                                     │
│  [Cancel]          [Save Changes]   │  ← Cancel outlined; Save filled #4C662B
└─────────────────────────────────────┘
```

**Layout notes:** Editable fields become outlined inputs pre-filled with current values. Keyboard shown. Cancel + Save buttons replace Edit button.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Customer Information             │
├─────────────────────────────────────┤
│                                     │
│  ┌──────────────────────────────┐   │
│  │ ⚠ Could not load customer    │   │  ← Error banner #FFDAD6, #BA1A1A icon
│  │   profile. Please try again. │   │
│  │        [ Try Again ]         │   │
│  └──────────────────────────────┘   │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] Top app bar: #F9FAEF background, back arrow left, title "Customer Information"
- [ ] Section headings: Outfit title_large #4C662B, paddingBottom 8dp
- [ ] Data rows: #FFFFFF bg, radius 8dp, pad V12/H16, marginBottom 2dp, space-between
- [ ] Label text: Outfit body_medium #44483D weight 500
- [ ] Value text: Outfit body_large #1A1C16; monospace for ID/tax-pin/income
- [ ] Phone + email: #4C662B text, underline, accessible tap target 48dp min
- [ ] Dividers: #E1E4D5, marginVertical 16dp, full width
- [ ] Edit Information: outlined full-width pill, #4C662B
- [ ] Skeleton: shimmer on row-height placeholders; headings visible
- [ ] Error banner: M3 error container (#FFDAD6), retry button
- [ ] All text Outfit; 16dp screen padding
