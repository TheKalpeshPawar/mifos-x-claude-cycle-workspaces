# MOCKUP — Customer 360 Profile

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow (no bottom navigation — fieldOfficer flavor). Fixed FAB at bottom-right.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Overview tab — KYC Verified)

```
┌─────────────────────────────────────┐
│ ←  John Mwangi                      │  ← TopAppBar, back arrow
├─────────────────────────────────────┤
│ █████████████ #4C662B ██████████████│  ← green hero header
│                                     │
│  ○JM○   John Mwangi                 │  ← 60dp circle avatar: white bg, #4C662B initials
│          Customer since Jan 2024    │     customer_full_name: headline_small white bold
│          [KYC Verified]             │     customer_since: body_medium #44483D
│                                     │     kyc badge: #4C662B bg, white, label_small
├─────────────────────────────────────┤
│  2 Accounts  │ KES 145,200 │ 3 days │  ← quick stats, space_around; #F9FAEF bg
│  (accounts)  │  (balance)  │(activ.)│     title_small: #4C662B / #1A1C16 / #44483D
├─────────────────────────────────────┤
│ [Overview][KYC][Accounts][App.][Msg]│  ← tab bar, white bg, #E1E4D5 border-bottom
│                                     │     Overview active: #4C662B text + 3dp underline
├─────────────────────────────────────┤
│                                     │
│  ┌ KYC Verified · Last chk 15 Apr ┐ │  ← KYC banner, #CDEDA3 bg, 4dp #4C662B left border
│  └────────────────────────────────┘ │     body_medium #4C662B medium
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Personal Information         │  │  ← white card, 12dp radius, elevation 1
│  │  ─────────────────────────── │  │     section label: title_small #4C662B bold
│  │  John Kamau Mwangi            │  │  ← body_medium #1A1C16 medium
│  │  DOB: 14 Mar 1985             │  │  ← body_small #44483D
│  │  National ID: KE12345678      │  │
│  │  Phone: +254 722 123 456      │  │
│  │  Email: john.mwangi@gmail.com │  │  ← email in #4C662B (tappable)
│  │                               │  │
│  │  View Full Profile →          │  │  ← body_medium #4C662B link
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Address                      │  │  ← white card, 12dp radius, elevation 1
│  │  ─────────────────────────── │  │
│  │  123 Moi Avenue, Nairobi, KE  │  │  ← body_medium #1A1C16
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Assigned to: Priya Sharma  Reassign│ ← rm card; label_medium #4C662B trailing
│  └───────────────────────────────┘  │
│                                     │
│  ┌── Send Message ────────────────┐ │  ← outlined #4C662B, message icon, full-width
│  └────────────────────────────────┘ │
│                                     │
│                      [+ Create App]  │  ← fixed FAB, #4C662B, 16dp radius, elevation 6
└─────────────────────────────────────┘
```

**Layout notes:**
- Hero header: 100% width, `#4C662B`, 20dp top padding, 24dp bottom.
- Customer avatar: 60×60dp circle, white bg, `#4C662B` initials. 16dp margin-right to name stack.
- Quick-stats row: `#F9FAEF` bg, 16dp vertical padding, 3 columns with thin vertical dividers.
- Tab bar: white, 1dp `#E1E4D5` border-bottom. Active tab: `#4C662B` text + 3dp underline.
- KYC banner: `#CDEDA3` bg, 4dp left border `#4C662B`, 10dp radius, 14dp padding.
- All content cards: white, 12dp radius, elevation 1, 16dp padding, 16dp horizontal margin.
- FAB: `#4C662B`, `add` icon + "Create Application" text, fixed 88dp from bottom, 16dp from right, elevation 6.
- "Send Message" button: full-width outlined `#4C662B`, 12dp radius, `message` icon.

---

## Screen: content (Overview tab — KYC Pending)

```
┌─────────────────────────────────────┐
│ ←  John Mwangi                      │
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │
│  ○JM○   John Mwangi                 │
│          Customer since Jan 2024    │
│          (no KYC badge)             │  ← badge hidden when kyc_status = false
├─────────────────────────────────────┤
│  2 Accounts  │ KES 145,200 │ 3 days │
├─────────────────────────────────────┤
│ [Overview][KYC][Accounts][App.][Msg]│
├─────────────────────────────────────┤
│                                     │
│  ┌ ⚠ KYC Pending — Action Req'd ──┐ │  ← pending banner, #CDEDA3 bg, 4dp #E8A317 left border
│  └────────────────────────────────┘ │     body_medium #44483D bold (7.25:1 contrast pass)
│                                     │
│  [same cards as content/verified]   │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Amber (`#E8A317`) left border on the pending KYC banner signals action required. Text uses `#44483D` not amber — WCAG AA requirement.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← hero header visible (static green)
│  ████  ██████████████               │  ← skeleton: avatar + name lines
│        ████████████                 │
│        █████████                    │
├─────────────────────────────────────┤
│  ████████  │  ████████  │  ████████ │  ← skeleton: 3 quick-stat blocks
├─────────────────────────────────────┤
│  ████ ████ ████ ████ ████           │  ← skeleton: 5 tab labels
├─────────────────────────────────────┤
│  ████████████████████████████████   │  ← skeleton card ~180dp
│                                     │
│  ████████████████████████████████   │  ← skeleton card ~80dp
│                                     │
│  ████████████████████████████████   │  ← skeleton card ~60dp
└─────────────────────────────────────┘
```

**Layout notes:** Green hero header always visible as chrome. Shimmer animation on all skeleton blocks (`#E1E4D5` shimmer). No FAB during loading.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │
├─────────────────────────────────────┤
│ ████████████ #4C662B ████████████   │  ← hero header stub (no customer data)
│                                     │
│                                     │
│   Unable to load customer details.  │  ← body_medium, #44483D, centered
│   Check your connection and         │
│   try again.                        │
│                                     │
│  ┌───────────────────────────────┐  │
│  │          Retry                │  │  ← FilledButton, #4C662B
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Hero header visible but empty (no customer data loaded). Error message and retry button centred in content area.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Customer Profile                 │
├─────────────────────────────────────┤
│                                     │
│   Customer record not found.        │  ← body_medium, centered, #44483D
│   The customer may have been        │
│   archived or the ID is invalid.    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** No hero header (customer_header_box hidden in empty state per `show_components: []`). Message centred. No FAB.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow; title = customer's name
- [ ] Green hero header `#4C662B` full-width; 60×60dp circular avatar white bg + initials
- [ ] Customer name `headline_small` white bold; customer-since `body_medium` `#44483D`
- [ ] KYC Verified badge: `#4C662B` bg, white text, 12dp radius — hidden when `kyc_status=false`
- [ ] Quick-stats row: `#F9FAEF` bg, 3-column `space_around` with thin vertical dividers
- [ ] Stats: accounts `#4C662B`, balance `#1A1C16`, activity `#44483D` — all `title_small` bold
- [ ] Tab bar: white bg, `#E1E4D5` 1dp border-bottom; active tab `#4C662B` + 3dp underline
- [ ] KYC Verified banner: `#CDEDA3` bg, 4dp `#4C662B` left accent border
- [ ] KYC Pending banner: `#CDEDA3` bg, 4dp `#E8A317` left accent border, `#44483D` text (contrast pass)
- [ ] Personal info card: white, 12dp radius, elevation 1, section label `title_small` `#4C662B`
- [ ] Email text in `#4C662B` (tappable mailto link)
- [ ] "View Full Profile →" link `body_medium` `#4C662B`
- [ ] Address card and relationship manager card same style as personal info
- [ ] "Reassign" trailing `label_medium` `#4C662B` link in RM card
- [ ] FAB "Create Application": `#4C662B` filled, `add` icon, fixed position, elevation 6, 16dp radius
- [ ] "Send Message": outlined `#4C662B`, `message` icon, full-width, 12dp radius
- [ ] Loading: shimmer skeleton blocks replacing all content
- [ ] 80dp bottom spacer ensuring content scrolls clear of FAB
- [ ] All text: Outfit typeface; minimum 12sp label_small
