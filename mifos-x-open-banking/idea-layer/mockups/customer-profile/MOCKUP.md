# Mockup Specification: Customer Profile

| Field | Value |
|---|---|
| Feature | customer-profile |
| Flavor | fieldOfficer |
| Archetype | detail_screen |

---

## Screen Layout

```
[ Top App Bar — "Customer Profile" back arrow ]
──────────────────────────────────────────────────
[ Screen Background: #F5F5F5 ]
[ "Personal Information" ] ← title_large #1800B1 pt:20 pb:8
┌─ Full Name row ──────────────────────────────── ┐
│  Full Name            John Kamau Mwangi          │  bg:#FFFFFF br:8
└──────────────────────────────────────────────────┘
┌─ Date of Birth row ──────────────────────────── ┐
│  Date of Birth        14 March 1985 (Age: 41)    │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
┌─ National ID row ────────────────────────────── ┐
│  National ID          KE12345678 [mono]          │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
┌─ Tax PIN row ────────────────────────────────── ┐
│  Tax PIN (KRA)        A001234567M [mono]         │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
┌─ Phone row ──────────────────────────────────── ┐
│  Phone                +254 722 123 456 [link]    │  #1800B1 underline tappable
└──────────────────────────────────────────────────┘
┌─ Email row ──────────────────────────────────── ┐
│  Email                john.mwangi@gmail.com [→]  │  #1800B1 underline tappable
└──────────────────────────────────────────────────┘
──────────────── divider #E0E0E0 mv:16 ────────────
[ "Address" ] ← title_large #1800B1 pb:8
┌─ Street ────────────────────────────────────────┐
│  123 Moi Avenue, Nairobi                        │  bg:#FFFFFF br:8
└──────────────────────────────────────────────────┘
┌─ County ────────────────────────────────────────┐
│  Nairobi County, Kenya                          │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
┌─ Postcode ──────────────────────────────────────┐
│  Postcode: 00100                                 │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
──────────────── divider #E0E0E0 mv:16 ────────────
[ "Employment" ] ← title_large #1800B1 pb:8
┌─ Employer ──────────────────────────────────────┐
│  Employer             Safaricom PLC              │  bg:#FFFFFF br:8
└──────────────────────────────────────────────────┘
┌─ Monthly Income ────────────────────────────────┐
│  Monthly Income       KES 85,000 [mono]          │  bg:#FFFFFF
└──────────────────────────────────────────────────┘
┌─ Employment Type ───────────────────────────────┐
│  Employment Type      Permanent                  │  bg:#FFFFFF mb:16
└──────────────────────────────────────────────────┘
[ Edit Information ] ← outlined button #1800B1 full-width mt:8 mb:24
──────────────────────────────────────────────────
[ Bottom Nav Bar ]
```

---

## Components

### Section Headings
- **Style:** title_large (22sp), color #1800B1, padding_bottom:8
- **Three sections:** Personal Information, Address, Employment
- Each is preceded by a divider (except the first) in #E0E0E0 with margin_vertical:16

### Data Rows
- **Outer box:** bg:#FFFFFF, border_radius:8, padding_vertical:10-12, padding_horizontal:16, margin_bottom:2
- **Inner stack:** Horizontal, space-between, items center-aligned, fill width
- **Label column:** body_medium, color #666666, weight 500
- **Value column:** body_large, color #1A1A1A (default) or #1800B1 (links)

### Contactable Links (Phone, Email)
- **Phone:** Tappable link — color #1800B1, underline decoration, launches `tel:+254722123456`
- **Email:** Tappable link — color #1800B1, underline decoration, launches `mailto:john.mwangi@gmail.com`
- Both have role: button for accessibility

### Monospace Values
- **National ID:** KE12345678 — monospace font for consistent character spacing
- **Tax PIN:** A001234567M — monospace font
- **Monthly Income:** KES 85,000 — monospace font for number alignment

### Edit Information Button
- **Style:** outlined variant, border #1800B1, text #1800B1, fill width, margin_top:8 margin_bottom:24
- **Edit state:** All rows convert to outlined text fields with validation; Save/Cancel CTA appears

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Phone link | Tap | Launches device dialer with +254722123456 pre-filled |
| Email link | Tap | Launches device mail client to john.mwangi@gmail.com |
| Edit Information | Tap | Switches all rows to editable text inputs (editing state) |
| Save (editing mode) | Tap | Submits PUT /customers/{id}; shows saving state; returns to content |
| Cancel (editing mode) | Tap | Discards editDraft; returns to content state |

**Saving state:** Progress overlay appears on top of the form; all inputs disabled; spinner on Save button; no partial-save race conditions.

---

## Content Data

| Section | Field | Value |
|---|---|---|
| Personal | Full Name | John Kamau Mwangi |
| Personal | Date of Birth | 14 March 1985 (Age: 41) |
| Personal | National ID | KE12345678 |
| Personal | Tax PIN (KRA) | A001234567M |
| Personal | Phone | +254 722 123 456 |
| Personal | Email | john.mwangi@gmail.com |
| Address | Street | 123 Moi Avenue, Nairobi |
| Address | County | Nairobi County, Kenya |
| Address | Postcode | 00100 |
| Employment | Employer | Safaricom PLC |
| Employment | Monthly Income | KES 85,000 |
| Employment | Employment Type | Permanent |

---

## Design Notes

**Grouped table pattern:** Rows with bg:#FFFFFF against the #F5F5F5 screen background create a native-settings-style grouped table look, familiar to mobile users across platforms. border_radius:8 softens the card edges.

**Monospace formatting:** Identifier fields (National ID, Tax PIN) and monetary values use monospace font family to ensure predictable character widths — important for quick visual verification against physical documents.

**Section dividers:** #E0E0E0 horizontal dividers with 16px vertical margins cleanly separate Personal, Address, and Employment sections without requiring heavy background changes.

**Typography scale:** Section headings at title_large (22sp) create strong hierarchy. Labels at body_medium (14sp) in muted #666666 recede appropriately while values at body_large (16sp) in #1A1A1A command visual attention.

**Accessibility:** Phone and email links carry role: button and descriptive contentDescription for screen readers ("Call +254 722 123 456", "Send email to john.mwangi@gmail.com"). Address rows have full-sentence contentDescription for TalkBack users.

---
_Generated by /idea export | 2026-05-25_
