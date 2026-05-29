# MOCKUP — Customer 360 Profile

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow (no bottom navigation — fieldOfficer flavor). Fixed FAB at bottom-right (88dp from bottom, 16dp from right).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Overview tab — KYC Verified)

```
┌─────────────────────────────────────┐
│ ←  Wanjiru Kamau                    │  ← M3 TopAppBar, back arrow; #1A1C16 title
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← customer_header_box: solid green hero
│                                     │     20dp top pad · spacing.lg bottom pad
│  ○WK○   Wanjiru Kamau               │  ← customer_avatar: 60×60dp circle, #FFFFFF bg
│          Customer since Jan 2024    │     initials "WK" Outfit/headline_small #4C662B bold
│          [KYC Verified]             │     customer_full_name: headline_small #FFFFFF bold
│                                     │     customer_since_text: body_medium #44483D
│                                     │     kyc_verified_badge: #4C662B bg, white label_small
├─────────────────────────────────────┤
│  2 Accounts │ KES 230,250 │ 3 days  │  ← quick_stats_row: #F9FAEF bg, spacing.sm vert
│  title_sm   │  title_sm   │title_sm │     #4C662B / #1A1C16 / #44483D respectively
│  #4C662B    │   #1A1C16   │ #44483D │
├─────────────────────────────────────┤
│ [Overview*][KYC][Accounts][App][Msg]│  ← tab_bar: #FFFFFF bg, 1dp #E1E4D5 border-bottom
│             ───                     │     Overview active: #4C662B text + 3dp underline
├─────────────────────────────────────┤
│                                     │
│  ┌──────────────────────────────┐   │  ← kyc_status_banner_verified
│  ┃ ✓ KYC Verified · Last chk   │   │     #CDEDA3 bg · 4dp left border #4C662B · 10dp radius
│  ┃   15 Apr 2026                │   │     body_medium #4C662B medium weight
│  └──────────────────────────────┘   │
│                                     │
│  ┌───────────────────────────────┐  │  ← personal_info_card: #FFFFFF, 12dp radius, elev 1
│  │  Personal Information         │  │     personal_info_label: title_small #4C662B bold
│  │  ─────────────────────────── │  │
│  │  Wanjiru Kamau                │  │  ← personal_info_name: body_medium #1A1C16 medium
│  │  DOB: 22 Mar 1988             │  │  ← personal_info_dob: body_small #44483D
│  │  National ID: (KYC doc)       │  │  ← personal_info_id: body_small #44483D
│  │  Phone: +254 712 345 678      │  │  ← personal_info_phone: body_small #44483D
│  │  Email: wanjiru.kamau@gmail.com│ │  ← personal_info_email: body_small #4C662B (tappable)
│  │                               │  │
│  │  View Full Profile →          │  │  ← view_full_profile_link: body_medium #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← address_card: #FFFFFF, 12dp radius, elev 1
│  │  Address                      │  │     address_label: title_small #4C662B bold
│  │  ─────────────────────────── │  │
│  │  123 Moi Avenue, Nairobi, KE  │  │  ← address_value: body_medium #1A1C16
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← relationship_manager_card: #FFFFFF, 12dp radius
│  │  Assigned to: Priya Sharma    │  │     relationship_manager_label: body_medium #1A1C16 medium
│  │                   [Reassign]  │  │  ← reassign_link: label_medium #4C662B trailing
│  └───────────────────────────────┘  │
│                                     │
│  ┌── [✉] Send Message ───────────┐  │  ← send_message_button: outlined #4C662B, 12dp radius
│  └────────────────────────────────┘ │     message icon leading, full-width, label_large
│  ░░░░░░░░░ 80dp spacer ░░░░░░░░░░  │  ← bottom_actions_spacer: scroll clearance for FAB
│                                     │
│                  ╔═══════════════╗  │  ← create_application_fab: #4C662B filled
│                  ║ [+] Create    ║  │     add icon, label_large #FFFFFF, 16dp radius
│                  ║  Application  ║  │     fixed: bottom 88dp, right 16dp, elevation 6
│                  ╚═══════════════╝  │
└─────────────────────────────────────┘
```

**Layout notes:**
- Hero header: 100% width `#4C662B`; 20dp top, spacing.lg (24dp) bottom padding; spacing.md (16dp) horizontal.
- Customer avatar: 60×60dp circle, white bg `#FFFFFF`; initials `Outfit/headline_small` bold `#4C662B`; 16dp right margin, flex-shrink 0.
- Quick-stats row: `#F9FAEF` bg, `space_around` justify, thin inset dividers between columns.
- Tab bar: white, 1dp `#E1E4D5` border-bottom. Active tab underline: 3dp solid `#4C662B`, text `#4C662B`.
- KYC verified banner: `#CDEDA3` bg, 4dp left border `#4C662B`, 10dp radius, 14dp padding, row layout with checkmark.
- All content cards: `#FFFFFF`, 12dp radius, elevation 1, 16dp padding, spacing.md (16dp) horizontal margin, spacing.sm (8dp) bottom margin.
- FAB: `#4C662B` filled, `add` icon + "Create Application" label_large `#FFFFFF`; fixed position 88dp from bottom, 16dp from right; elevation 6.
- "Send Message" button: full-width outlined `#4C662B`; `message` icon leading; 12dp radius; spacing.md margin.

---

## Screen: content (Overview tab — KYC Pending)

```
┌─────────────────────────────────────┐
│ ←  Wanjiru Kamau                    │  ← TopAppBar
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← hero header (same green)
│  ○WK○   Wanjiru Kamau               │
│          Customer since Jan 2024    │
│          (no KYC badge shown)       │  ← kyc_verified_badge hidden when kyc_status=false
├─────────────────────────────────────┤
│  2 Accounts │ KES 230,250 │ 3 days  │
├─────────────────────────────────────┤
│ [Overview*][KYC][Accounts][App][Msg]│
├─────────────────────────────────────┤
│                                     │
│  ┌──────────────────────────────┐   │  ← kyc_status_banner_pending
│  ┃ ⚠ KYC Pending — Action Req. │   │     #CDEDA3 bg · 4dp left border #E8A317 · 10dp radius
│  └──────────────────────────────┘   │     kyc_pending_text: body_medium #44483D bold
│                                     │     (WCAG AA: #44483D = 7.25:1 vs #CDEDA3 bg — PASS)
│  [same personal info + address      │
│   + RM cards as verified state]     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Amber `#E8A317` left border on the pending banner signals action required visually without using amber for text (which fails WCAG AA at 2.17:1 on `#CDEDA3`). Text `#44483D` passes at 7.25:1. The `kyc_verified_badge` does not render when `kyc_status = false`.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │  ← TopAppBar (placeholder title until data loads)
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← customer_header_box: static green (always visible)
│  ████  ███████████████████          │  ← skeleton: avatar circle + name lines
│        ████████████████             │     shimmer: #E1E4D5, short4 (200ms) animation
│        ████████████                 │
├─────────────────────────────────────┤
│  ████████  │  ████████  │  ████████ │  ← skeleton: quick_stats_row 3 blocks
├─────────────────────────────────────┤
│  ████  ████  ████  ████  ████       │  ← skeleton: 5 tab label bars
├─────────────────────────────────────┤
│                                     │
│  ████████████████████████████████   │  ← skeleton card ~180dp (personal info placeholder)
│  ████████████████████████           │
│  ████████████████████               │
│                                     │
│  ████████████████████████████████   │  ← skeleton card ~80dp (address placeholder)
│                                     │
│  ████████████████████████████████   │  ← skeleton card ~60dp (RM card placeholder)
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Green hero header always visible as persistent chrome during load (customer_header_box shown in loading layout). All content cards and stats are skeleton blocks with shimmer on `#E1E4D5`. No FAB during loading state. `reduced_motion_fallback: static_placeholder` — shimmer is replaced by a static grey block when system reduced-motion is enabled.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │  ← TopAppBar
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← customer_header_box (visible, no data)
│                                     │
│                                     │
│      ⚠                              │  ← error icon, centered
│                                     │
│   Unable to load customer details.  │  ← body_medium #44483D, centered
│   Check your connection and         │
│   try again.                        │
│                                     │
│  ┌───────────────────────────────┐  │
│  │           Retry               │  │  ← FilledButton #4C662B, label_large #FFFFFF
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Hero header visible with no customer data. Quick-stats row, tab bar, all cards, FAB, and Send Message button are hidden. Error message centred. Retry triggers `RetryLoadEvent`.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │
├─────────────────────────────────────┤
│                                     │
│                                     │
│   Customer record not found.        │  ← body_medium, centered, #44483D
│   The customer may have been        │
│   archived or the ID is invalid.    │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** No hero header — `customer_header_box` hidden per empty state `show_components: []`. All tabs, cards, FAB, and buttons hidden. Plain message centred on `#F9FAEF` background. No retry (customer ID is definitively invalid / archived).

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow; title = customer legal name (loaded from API)
- [ ] Hero header: `#4C662B` full-width, 20dp top + 24dp bottom padding, 16dp horizontal padding
- [ ] Avatar: 60×60dp circle, `#FFFFFF` bg, Outfit/headline_small bold `#4C662B` initials (e.g. "WK"), 16dp right margin
- [ ] Customer full name: Outfit/headline_small bold `#FFFFFF`
- [ ] Customer-since: Outfit/body_medium `#44483D`
- [ ] KYC Verified badge: `#4C662B` bg, `#FFFFFF` label_small bold, 12dp radius — hidden when `kyc_status=false`
- [ ] Quick-stats row: `#F9FAEF` bg, 3-column space_around, title_small; accounts `#4C662B`, balance `#1A1C16`, activity `#44483D`
- [ ] Tab bar: `#FFFFFF` bg, 1dp `#E1E4D5` border-bottom; Overview active: `#4C662B` text + 3dp solid underline
- [ ] KYC Verified banner: `#CDEDA3` bg, 4dp left border `#4C662B`, 10dp radius, 14dp padding; body_medium `#4C662B`
- [ ] KYC Pending banner: `#CDEDA3` bg, 4dp left border `#E8A317`, 10dp radius; body_medium `#44483D` bold (NOT amber text — WCAG AA fail at 2.17:1)
- [ ] Personal info card: `#FFFFFF`, 12dp radius, elevation 1, 16dp padding, 16dp horizontal margin; section label title_small `#4C662B` bold
- [ ] Personal info fields: name body_medium `#1A1C16`; DOB/ID/phone body_small `#44483D`; email body_small `#4C662B`
- [ ] "View Full Profile →" link: body_medium `#4C662B`, 20dp horizontal, spacing.sm top padding
- [ ] Address card: same card style; address_label title_small `#4C662B` bold; address_value body_medium `#1A1C16`
- [ ] RM card: horizontal row space-between; name body_medium `#1A1C16`; "Reassign" label_medium `#4C662B` trailing
- [ ] FAB "Create Application": `#4C662B` filled, `add` icon leading, label_large `#FFFFFF`, 16dp radius, fixed bottom-88dp right-16dp, elevation 6
- [ ] "Send Message" button: outlined `#4C662B`, `message` icon leading, full-width, 12dp radius, label_large
- [ ] Loading state: green header visible; all content shimmer skeleton on `#E1E4D5` (200ms short4); static placeholder on reduced-motion
- [ ] 80dp bottom spacer ensuring scrollable content clears fixed FAB
- [ ] All typeface: Outfit; minimum touch target 48dp; 16dp horizontal content padding throughout
