# MOCKUP — KYC Document Review

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow ("KYC Review"). No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │  ← Top app bar
├─────────────────────────────────────┤
│ ████████████████████████████████████│  ← Header band skeleton (56dp, shimmer)
│                                     │
│  ████████  ████████  (skeleton)     │  ← Status badge row skeleton
│                                     │
│  ██████████████  (skeleton)         │  ← "Documents" heading skeleton
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████  ██████████████████ │  │  ← Document card skeleton
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████  ██████████████████ │  │  ← Document card skeleton
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████  ██████████████████ │  │  ← Document card skeleton
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████  ██████████████████ │  │  ← Document card skeleton
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│                                     │
│  ██████████████  (skeleton)         │  ← Risk section heading
│  ████████████████████  (skeleton)   │  ← Risk dropdown skeleton
│                                     │
│  ████████████████████  (skeleton)   │  ← Approve button skeleton
│  ████████████████████  (skeleton)   │  ← Reject button skeleton
└─────────────────────────────────────┘
```

**Layout notes:** All shimmer blocks use `trust_horizon` gradient. No interactive elements during loading.

---

## Screen: reviewing

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │  ← M3 TopAppBar, back arrow
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │ ●JM  John Mwangi              │  │  ← #4C662B header band
│  │      KYC Review Required      │  │    Avatar: white circle, "JM" #4C662B
└──┤                               ├──┘    Name: title_medium #FFFFFF bold
   └───────────────────────────────┘       Label: body_small #CDEDA3
│                                     │
│  KYC Status:  [In Progress]         │  ← body_medium + #CDEDA3 chip, #E8A317 border
│                                     │
│  Documents                          │  ← title_medium #1A1C16 heading
│                                     │
│  ┌───────────────────────────────┐  │
│  │ [img] National ID — Front     │  │  ← White card, 1dp #E1E4D5 border
│  │       Uploaded ✓ · 22 May 2026│  │    Status: body_small #4C662B
│  │                          View │  │    "View": label_medium #4C662B underline
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ [□]  National ID — Back       │  │  ← Placeholder: image_not_supported #44483D
│  │      Pending Upload           │  │    Status: body_small #44483D
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ (●)  Selfie / Liveness Check  │  │  ← Circular thumbnail, 2dp #4C662B border
│  │      Passed ✓ · 22 May 2026   │  │    Status: body_small #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ [⌂]  Proof of Address (Opt.)  │  │  ← home icon placeholder #44483D
│  │      Not uploaded    [Upload] │  │    Upload: outlined #386663
│  └───────────────────────────────┘  │
│                                     │
│  Risk Assessment                    │  ← title_medium #1A1C16 heading
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Risk Level              ▼    │  │  ← Outlined dropdown: Low/Medium/High/Declined
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │         Approve KYC           │  │  ← Filled, #4C662B bg, #FFFFFF text, full-width
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │         Reject KYC            │  │  ← Outlined, #BA1A1A border/text, full-width
│  └───────────────────────────────┘  │
│                                     │
│       Request More Documents        │  ← Text button, #4C662B, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Header band: full-width, 0dp radius, 16dp horizontal + vertical padding.
- Each document card: 16dp horizontal margin, 8dp margin-bottom, 14dp internal padding, 10dp radius.
- Approve/Reject buttons: full-width with 16dp horizontal margin, 8dp gap between buttons.
- Scroll: vertical, starts at 0 padding below header band.

---

## Screen: verifying

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  [... reviewing layout beneath ...]  │
│                                     │
│  ╔═════════════════════════════════╗ │
│  ║                                 ║ │
│  ║    ○  Verifying documents…      ║ │  ← Progress overlay (scrim + spinner)
│  ║                                 ║ │    Circular indeterminate #4C662B
│  ╚═════════════════════════════════╝ │
└─────────────────────────────────────┘
```

**Layout notes:** Semi-transparent scrim (50% opacity) over reviewing layout. Spinner centered. Taps blocked.

---

## Screen: approved

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  ✓  KYC Approved              │  │  ← Success banner: #CDEDA3 bg, #4C662B text
│  │     John Mwangi's identity has│  │    Checkmark icon 24dp
│  │     been verified.            │  │
│  └───────────────────────────────┘  │
│                                     │
│  [... reviewing layout below ...]   │  ← Approve button disabled (muted)
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Success banner inlined at top of scrollable area, 16dp horizontal margin, 12dp radius.

---

## Screen: rejected

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  ✗  KYC Rejected              │  │  ← Error banner: #FFDAD6 bg, #BA1A1A text
│  │     National ID back not      │  │    Error icon 24dp
│  │     uploaded. Selfie mismatch.│  │
│  └───────────────────────────────┘  │
│                                     │
│  [... reviewing layout below ...]   │
└─────────────────────────────────────┘
```

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │ ●JM  John Mwangi              │  │  ← Header band unchanged
│  │      KYC Review Required      │  │
│  └───────────────────────────────┘  │
│                                     │
│              [description]          │  ← description icon 48dp #75796C
│                                     │
│       No KYC documents to review    │  ← headline_small #1A1C16 centered
│   Upload documents via the customer │
│   onboarding screen to continue.   │  ← body_medium #44483D centered
│                                     │
└─────────────────────────────────────┘
```

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│                                     │
│              ⚠                      │  ← Error icon 48dp #BA1A1A
│                                     │
│    Could not load KYC documents     │  ← body_large centered
│    Check your connection and        │
│    try again.                       │  ← body_medium #44483D centered
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Retry              │  │  ← Filled button #4C662B
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon, no bottom nav
- [ ] Full-width green header band (`#4C662B`) with 40×40 white avatar circle + initials "JM"
- [ ] KYC status chip: `#CDEDA3` background, 1dp `#E8A317` border, 16dp radius
- [ ] 4 document cards: white surface, 1dp `#E1E4D5` border, 10dp radius, elevation 1
- [ ] National ID Front: thumbnail + green "Uploaded ✓" status text + "View" underline link
- [ ] National ID Back: placeholder icon + "Pending Upload" subdued text
- [ ] Selfie: circular thumbnail with 2dp `#4C662B` border ring
- [ ] Proof of Address: home icon + "Upload" outlined button in `#386663`
- [ ] Risk level dropdown: 4 options (Low / Medium / High / Declined)
- [ ] Rejection reason textarea: conditionally shown when risk = Declined
- [ ] Approve button: full-width filled `#4C662B`
- [ ] Reject button: full-width outlined `#BA1A1A`
- [ ] Request More Documents: text button `#4C662B`
- [ ] Verifying state: progress overlay with spinner over reviewing layout
- [ ] Success / rejection banners use primary_container / error_container tokens
- [ ] All text uses Outfit typeface; 16dp horizontal content padding throughout
