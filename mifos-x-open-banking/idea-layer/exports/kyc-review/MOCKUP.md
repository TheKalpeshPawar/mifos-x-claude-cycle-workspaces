# MOCKUP — KYC Document Review

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow ("KYC Review"). No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │  ← M3 TopAppBar, back arrow
├─────────────────────────────────────┤
│ ████████████████████████████████████│  ← Header band skeleton (56dp, shimmer, trust_horizon gradient)
│                                     │
│  ████████  ████████  (skeleton)     │  ← Status badge row skeleton
│                                     │
│  ██████████████  (skeleton)         │  ← "Documents" heading skeleton
│                                     │
│  ┌───────────────────────────────┐  │  ← Document card skeleton 1 (#E1E4D5, 10dp radius)
│  │  ████████  ██████████████████ │  │
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Document card skeleton 2
│  │  ████████  ██████████████████ │  │
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Document card skeleton 3
│  │  ████████  ██████████████████ │  │
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Document card skeleton 4
│  │  ████████  ██████████████████ │  │
│  │            ████████           │  │
│  └───────────────────────────────┘  │
│                                     │
│  ██████████████  (skeleton)         │  ← Risk section heading skeleton
│  ████████████████████  (skeleton)   │  ← Risk dropdown skeleton
│                                     │
│  ████████████████████  (skeleton)   │  ← Approve button skeleton (disabled)
│  ████████████████████  (skeleton)   │  ← Reject button skeleton (disabled)
└─────────────────────────────────────┘
```

**Layout notes:** All shimmer blocks use `trust_horizon` gradient (`#F0F1E6` → `#E1E4D5`). No interactive elements during loading. Vertical scroll with 0dp padding.

---

## Screen: reviewing (= content)

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │  ← M3 TopAppBar, back arrow, #F9FAEF bg
├─────────────────────────────────────┤
│ ┌─────────────────────────────────┐ │  ← #4C662B header band, full-width, 0dp radius
│ │ ◉JM  John Mwangi               │ │     Avatar: 40×40 white circle, "JM" label_large #4C662B bold
│ │      KYC Review Required       │ │     Name: title_medium #FFFFFF weight 700
│ └─────────────────────────────────┘ │     "KYC Review Required": body_small #CDEDA3
│                                     │
│  KYC Status:  [In Progress]         │  ← body_medium #44483D + chip: #CDEDA3 bg, 1dp #E8A317 border
│               ─────────────         │    "In Progress": label_medium #44483D weight 600, 16dp radius
│                                     │
│  Documents                          │  ← title_medium #1A1C16, heading level 2, 16dp horiz pad
│                                     │
│  ┌───────────────────────────────┐  │  ← doc_national_id_front card
│  │ [img] National ID — Front     │  │    #FFFFFF, 10dp radius, 1dp #E1E4D5 border, elev 1
│  │  56×40 thumbnail (6dp radius) │  │    Thumbnail: 56×40, 6dp radius, cover fit
│  │       body_large #1A1C16 bold │  │    Title: body_large #1A1C16, weight 600
│  │  Uploaded ✓ · 22 May 2026     │  │    Status: body_small #4C662B (green = verified)
│  │                          View │  │    "View": label_medium #4C662B, underline, action: view_document
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← doc_national_id_back card
│  │ [□]  National ID — Back       │  │    Placeholder: #F9FAEF, image_not_supported icon #44483D 20dp
│  │  56×40 placeholder box        │  │
│  │       body_large #1A1C16 bold │  │    Title: body_large #1A1C16, weight 600
│  │  Pending Upload               │  │    Status: body_small #44483D (subdued = not uploaded)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← doc_selfie card
│  │ (●)  Selfie / Liveness Check  │  │    Circular thumbnail: 56×40 (28dp radius), 2dp #4C662B border
│  │  circular, 2dp #4C662B border │  │
│  │       body_large #1A1C16 bold │  │    Title: body_large #1A1C16, weight 600
│  │  Passed ✓ · 22 May 2026       │  │    Status: body_small #4C662B (green = passed)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← doc_proof_of_address card
│  │ [⌂]  Proof of Address (Opt.)  │  │    Placeholder: home icon #44483D 20dp
│  │  56×40 placeholder box        │  │
│  │       body_large #1A1C16 bold │  │    Title: body_large #1A1C16, weight 600
│  │  Not uploaded    [ Upload ]   │  │    Status: body_small #44483D
│  └───────────────────────────────┘  │    "Upload": outlined, #386663 border/text, label_small
│                                     │
│  Risk Assessment                    │  ← title_medium #1A1C16, heading level 2
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Risk Level              ▼    │  │  ← Outlined select, options: Low / Medium / High / Declined
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │         Approve KYC           │  │  ← Filled, #4C662B bg, #FFFFFF text, full-width
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │         Reject KYC            │  │  ← Outlined, #BA1A1A border/text, full-width
│  └───────────────────────────────┘  │
│                                     │
│      Request More Documents         │  ← Text button, #4C662B, 24dp bottom margin
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background: `#F9FAEF` (background token). Vertical scroll starting at 0dp.
- Header band: full-width, 0dp border-radius, 16dp horizontal + vertical padding. Horizontal stack: 40×40 avatar (24dp radius) + vertical text group. Gap: 12dp.
- Status chip: 16dp border-radius, 8dp horizontal / 4dp vertical padding, 1dp `#E8A317` border on `#CDEDA3` fill.
- Document cards: 16dp horizontal margin, 8dp bottom margin, 14dp internal padding, 10dp radius, 1dp `#E1E4D5` border, elevation 1.
- Card rows: horizontal stack, 12dp gap, center-aligned. Thumbnail area: 56×40dp.
- Approve/Reject buttons: full-width with 16dp horizontal margin, 8dp gap. Pill shape (button height 40dp).
- Request More Docs: 16dp horizontal margin, 24dp bottom margin.

---

## Screen: reviewing — Declined risk (rejection reason textarea visible)

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│ [... header band + doc cards ...]   │
│                                     │
│  Risk Assessment                    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Risk Level: Declined    ▼    │  │  ← Dropdown: Declined selected
│  └───────────────────────────────┘  │
│                                     │
│  Reason for Rejection               │  ← rejection_reason_input (conditionally visible)
│  ┌───────────────────────────────┐  │
│  │ Explain why KYC cannot be     │  │  ← Outlined textarea, 3–6 lines
│  │ approved — e.g. National ID   │  │    Placeholder in #44483D, body_medium
│  │ does not match selfie, blurry │  │    Min 3 lines, max 6 lines
│  │ documents, suspected fraud... │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │         Approve KYC           │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │         Reject KYC            │  │
│  └───────────────────────────────┘  │
│      Request More Documents         │
└─────────────────────────────────────┘
```

**Layout notes:** Rejection reason textarea appears between risk dropdown and action buttons when `riskLevel == DECLINED`. Textarea: 16dp horizontal margin, 16dp bottom margin, 3 min lines, 6 max lines.

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
│  ║      ◌  Verifying documents…    ║ │  ← Progress overlay: scrim (50% #000000) + circular
│  ║                                 ║ │    indeterminate spinner #4C662B, body_medium text
│  ╚═════════════════════════════════╝ │
└─────────────────────────────────────┘
```

**Layout notes:** Semi-transparent scrim (`#000000` 50%) over reviewing layout. Spinner centered at mid-screen. All taps intercepted/blocked. `showProgressOverlay: true`, `overlayMessage: "Verifying documents..."`.

---

## Screen: approved

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │  ← Success banner: #CDEDA3 bg, 12dp radius, 16dp margin
│  │  ✓  KYC Approved              │  │    check_circle icon 24dp #4C662B
│  │     John Mwangi's identity has│  │    body_large #4C662B bold
│  │     been verified.            │  │    body_medium #44483D
│  └───────────────────────────────┘  │
│                                     │
│  [... reviewing layout below ...]   │  ← Approve button shown as disabled/muted
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** `showSuccessBanner: true`. Success banner inlined at top of scrollable content area, below customer header band. 16dp horizontal margin, 12dp border-radius. Approve button disabled state. Auto-navigate to customer-detail triggered by `KycApproved` event.

---

## Screen: rejected

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │  ← Rejection banner: #FFDAD6 bg, 12dp radius, 16dp margin
│  │  ✗  KYC Rejected              │  │    cancel icon 24dp #BA1A1A
│  │     National ID back not      │  │    body_large #BA1A1A bold
│  │     uploaded. Selfie does not │  │    Rejection reason from officer textarea
│  │     match ID photo.           │  │    body_medium #44483D
│  └───────────────────────────────┘  │
│                                     │
│  [... reviewing layout below ...]   │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** `showRejectionBanner: true`. Rejection banner inlined at top of scrollable area. `#FFDAD6` = `colors.light.error_container`. Officer-entered `rejectionReason` text shown in banner body.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│ ┌─────────────────────────────────┐ │  ← Customer header band unchanged
│ │ ◉JM  John Mwangi               │ │
│ │      KYC Review Required       │ │
│ └─────────────────────────────────┘ │
│                                     │
│                                     │
│         [description icon]          │  ← description icon 48dp #75796C (outline variant)
│                                     │
│    No KYC documents to review       │  ← headline_small #1A1C16, center-aligned
│                                     │
│  Upload documents via the customer  │  ← body_medium #44483D, center-aligned
│  onboarding screen to continue.     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** `showEmptyState: true`, `emptyMessage: "No KYC documents to review"`. 16dp padding. No document cards, no action buttons. Customer header band still shown for context.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  KYC Review                       │
├─────────────────────────────────────┤
│                                     │
│              ⚠                      │  ← error_outline icon 48dp #BA1A1A
│                                     │
│    Could not load KYC documents     │  ← body_large #1A1C16, center-aligned
│                                     │
│    Check your connection and        │  ← body_medium #44483D, center-aligned
│    try again.                       │
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Retry              │  │  ← Outlined button, #4C662B border/text
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** `showErrorBanner: true`. 16dp padding throughout. Error icon at top (48dp), then body copy, then Retry button. Maps to `DOCUMENT_LOAD_FAILED` or `NETWORK_UNAVAILABLE` error.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon — no bottom navigation bar on this detail screen
- [ ] Full-width green header band (`#4C662B`, 0dp radius) — 40×40 white avatar circle (24dp radius) with initials "JM" (label_large `#4C662B`, weight 700), name in title_medium `#FFFFFF` weight 700, subhead in body_small `#CDEDA3`
- [ ] KYC status row: "KYC Status:" body_medium `#44483D` + chip `#CDEDA3` bg, 1dp `#E8A317` border, 16dp radius, "In Progress" label_medium `#44483D` weight 600
- [ ] "Documents" section heading: title_medium `#1A1C16`, heading level 2, 16dp horiz + 8dp vert padding
- [ ] 4 document cards: `#FFFFFF` surface, 10dp radius, 1dp `#E1E4D5` border, elevation 1, 16dp horizontal margin, 8dp bottom margin, 14dp internal padding
- [ ] National ID Front: 56×40 thumbnail (6dp radius, cover) + body_large `#1A1C16` title + body_small `#4C662B` "Uploaded ✓ · 22 May 2026" + "View" label_medium `#4C662B` underline
- [ ] National ID Back: 56×40 `#F9FAEF` placeholder (image_not_supported icon `#44483D` 20dp) + body_large `#1A1C16` title + body_small `#44483D` "Pending Upload"
- [ ] Selfie: 56×40 circular thumbnail (28dp radius) with 2dp `#4C662B` border ring + body_large title + body_small `#4C662B` "Passed ✓ · 22 May 2026"
- [ ] Proof of Address: 56×40 `#F9FAEF` placeholder (home icon `#44483D` 20dp) + body_large title + body_small `#44483D` "Not uploaded" + "Upload" outlined button `#386663` border/text label_small
- [ ] "Risk Assessment" heading: title_medium `#1A1C16`, heading level 2, 16dp horizontal padding, 8dp bottom padding
- [ ] Risk level dropdown: outlined select, 4 options (Low / Medium / High / Declined), 16dp horizontal margin
- [ ] Rejection reason textarea: conditionally visible when risk = Declined; outlined, 3–6 lines, 16dp margin, placeholder text in `#44483D`
- [ ] Approve KYC button: filled `#4C662B` bg `#FFFFFF` text, full-width, 16dp horizontal margin, 40dp height
- [ ] Reject KYC button: outlined `#BA1A1A` border/text, full-width, 16dp horizontal margin, 40dp height
- [ ] Request More Documents: text button `#4C662B`, 16dp horizontal margin, 24dp bottom margin
- [ ] Verifying overlay: semi-transparent `#000000` 50% scrim + circular indeterminate spinner `#4C662B` + "Verifying documents…" body_medium
- [ ] Approved state: success banner `#CDEDA3` bg, 12dp radius, check_circle `#4C662B` icon + body text; approve button disabled
- [ ] Rejected state: rejection banner `#FFDAD6` bg, 12dp radius, cancel `#BA1A1A` icon + officer rejection reason text
- [ ] Empty state: description icon 48dp `#75796C` + headline_small `#1A1C16` + body_medium `#44483D` (centered)
- [ ] Error state: error_outline icon 48dp `#BA1A1A` + body copy + Retry outlined button `#4C662B`
- [ ] All text uses Outfit typeface throughout. 48dp minimum touch targets on interactive elements. 16dp horizontal content padding.
- [ ] Screen background `#F9FAEF` (background token). Skeleton shimmer uses `trust_horizon` gradient.

---

_Generated by /idea export | 2026-05-30_
