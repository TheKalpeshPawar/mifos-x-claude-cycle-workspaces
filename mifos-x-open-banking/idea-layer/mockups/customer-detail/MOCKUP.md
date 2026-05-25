# Mockup Specification: Customer 360 Profile

| Field | Value |
|---|---|
| Feature | customer-detail |
| Flavor | fieldOfficer |
| Archetype | detail_screen |

---

## Screen Layout

```
[ Status Bar — white icons on purple ]
┌─────────────────────────────────────────────┐
│  [JM]  John Mwangi                   #1800B1 │
│  ●●●   Customer since Jan 2024       header  │
│  [KYC Verified]  ← green pill badge         │
└─────────────────────────────────────────────┘
[ Quick Stats Bar ] bg:#F5F5F5, pv:12
  "2 Accounts" #1800B1  |  "KES 145,200" #212121  |  "3 days ago" #757575
──────────────────────────────────────────────────
[ Tab Bar ] bg:#FFFFFF, bottom-border #E0E0E0
  [Overview ▂] [KYC] [Accounts] [Applications] [Messages]
  active tab: #1800B1 indicator line, 3px thick
──────────────────────────────────────────────────
  === OVERVIEW TAB CONTENT ===
[ Personal Information Card ]              ← bg:#FFFFFF br:12 elevation:1, mh:16 mt:16
  "Personal Information" title_small #1800B1 bold
  "John Kamau Mwangi"     body_medium #212121 bold
  "DOB: 14 Mar 1985"      body_small #616161
  "National ID: KE12345678" body_small #616161
  "Phone: +254 722 123 456" body_small #616161
  "Email: john.mwangi@gmail.com" body_small #1800B1
  [ View Full Profile → ] link #1800B1
[ Address Card ]                           ← bg:#FFFFFF br:12 elevation:1
  "Address" title_small #1800B1 bold
  "123 Moi Avenue, Nairobi, Kenya" body_medium #424242
[ Relationship Manager Card ]              ← row layout, bg:#FFFFFF
  "Assigned to: Priya Sharma" body_medium bold  |  "Reassign" link #1800B1
[ KYC Verified Banner ]                    ← bg:#E8F5E9, left-border 4px #4CAF50
  "KYC Verified · Last checked 15 Apr 2026" body_medium #2E7D32
──────────────────────────────────────────────────
[ SPACER — 80px for FAB clearance ]
[ [message] Send Message ] ← outlined full-width #1800B1, mh:16 mb:16
──────────────────────────────────────────────────
[ FAB: [add] Create Application ]         ← fixed bottom-right, bg:#1800B1 white text
                                            bottom:88 right:16, elevation:6
[ Bottom Nav Bar ]
```

---

## Components

### Customer Header
- **Background:** #1800B1 (deep brand purple) spanning full width, padding_horizontal:16 padding_top:20 padding_bottom:24
- **Avatar:** 60px circle, white background (#FFFFFF), initials "JM" in #1800B1, headline_small, margin_right:16
- **Name:** headline_small, white (#FFFFFF), font_weight 700
- **Tenure:** "Customer since Jan 2024", body_medium, color #C5CAE9 (lavender-white)
- **KYC Badge:** "KYC Verified" pill — background #4CAF50, white text, label_small, border_radius:12, padding 10px/4px, margin_top:6

### Quick Stats Bar
- **Background:** #F5F5F5, padding_vertical:12, horizontal layout space_around
- **Stats:** 3 equal columns, center-aligned
  - "2 Accounts" — title_small #1800B1 bold
  - "KES 145,200" — title_small #212121 bold
  - "3 days ago" — title_small #757575

### Tab Bar
- 5 tabs: Overview (selected), KYC, Accounts, Applications, Messages
- Selected tab: label_medium in #1800B1 with 3px bottom border in #1800B1
- Unselected tabs: label_medium in #757575
- Horizontal scroll if viewport too narrow

### Content Cards (Overview Tab)
- All cards: bg:#FFFFFF, border_radius:12, elevation:1, padding:16, margin_horizontal:16
- Section headings within cards: title_small #1800B1, font_weight 600
- Data rows: body_medium/body_small in #212121 or #616161
- Email field rendered in #1800B1 (tappable implication)

### KYC Status Banner
- Verified: bg:#E8F5E9, 4px left border #4CAF50, text #2E7D32
- Pending: bg:#FFF8E1, 4px left border #FF8F00, text #E65100 bold

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Tab: Overview | Tap | Shows personal info, address, relationship manager, KYC banner |
| Tab: KYC | Tap | Pushes to /kyc-review screen |
| Tab: Accounts | Tap | Shows accounts list within tab |
| Tab: Applications | Tap | Shows applications list within tab |
| Tab: Messages | Tap | Shows messages thread within tab |
| View Full Profile → | Tap | Push navigate to /customer-profile |
| Reassign link | Tap | Opens reassign dialog (inline action) |
| Create Application FAB | Tap | Push navigate to /account-applications |
| Send Message button | Tap | Push navigate to /customer-messages |

**Loading state:** Header bar shows solid purple; avatar, name, stats, tabs, and all cards render shimmer skeletons.

---

## Content Data

| Field | Value |
|---|---|
| Customer name | John Mwangi |
| Full legal name | John Kamau Mwangi |
| Customer since | Jan 2024 |
| KYC status | Verified (last checked 15 Apr 2026) |
| Accounts | 2 |
| Total balance | KES 145,200 |
| Last activity | 3 days ago |
| Date of birth | 14 Mar 1985 |
| National ID | KE12345678 |
| Phone | +254 722 123 456 |
| Email | john.mwangi@gmail.com |
| Address | 123 Moi Avenue, Nairobi, Kenya |
| Relationship manager | Priya Sharma |

---

## Design Notes

**Header color blocking:** The full-bleed #1800B1 header creates strong visual hierarchy and brand presence at the top of what is the most information-dense screen in the app. White initials on white card avatar creates intentional inversion of the header palette.

**Tab indicator:** 3px bottom border on active tab in #1800B1 follows Material 3 tab strip conventions. Inactive tabs use #757575 for clear affordance differentiation.

**Fixed FAB positioning:** Create Application FAB is positioned at bottom:88 to sit above the bottom nav bar, right:16. elevation:6 ensures it floats above scrolling content. Label-large text ("Create Application") on the extended FAB makes its purpose unambiguous.

**Accessibility:** Header region has role: region with label "Customer header: John Kamau Mwangi". Quick stats row has role: group. KYC pending banner has role: alert. All tabs have role: tab with selected state communicated.

**Balance formatting:** KES 145,200 uses monospaced number formatting for alignment consistency. Currency code (KES) precedes the amount.

---
_Generated by /idea export | 2026-05-25_
