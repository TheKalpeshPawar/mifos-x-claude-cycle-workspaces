# Visual Specification — Transaction Tags & Notes

| Field | Value |
|---|---|
| Feature | transaction-tags |
| Flavor | consumer |
| Archetype | detail_screen |
| Status | designed |

---

## Screen Layout

**Top app bar:** "Tags & Notes" title, back arrow (navigate_back → transaction-detail), delete_outlined "Clear All" icon (clear_all_metadata). No bottom navigation. Single-column vertical scroll:

1. **Transaction summary card** — branded header anchoring the screen to its transaction context
2. **Tags section** — heading, hint, colour-coded chip row, add-tag input row
3. **Divider**
4. **Notes section** — heading + multi-line text area
5. **Divider**
6. **Receipt section** — heading, dashed drop zone, camera button
7. **Save button** — full-width primary CTA, bottom of scroll
8. **Save-success banner** — overlaid green strip; visible only in save_success state

---

## Component Detail

### 1. Transaction Summary Card

```
┌─────────────────────────────────────┐  bg: #1800B1, radius: 20
│  Whole Foods Market                 │  title_large  white  semi-bold
│  -£67.84                            │  display_small  white  bold
│  23 May 2026 · 14:32                │  body_medium  #C5B8FF (lavender)
└─────────────────────────────────────┘
  margin: 20dp h, 16dp top, 20dp bottom
  a11y: "Transaction: Whole Foods Market, debit £67.84, 23 May 2026"
  on_click: navigate_to_transaction_detail
```

The deep purple header creates a strong visual anchor — the user always knows which transaction they are annotating.

---

### 2. Tags Section

**Heading row**
- "Tags" — title_medium, #111111, semi-bold, padding_h 20, bottom 10
- "Tap a tag to remove it" — body_small, #888888, padding_h 20, bottom 8 (hidden in loading/error)

**Chip colours — five distinct hues, one per category:**

| Chip | Label | Background | Text |
|---|---|---|---|
| tag_chip_groceries | #groceries | #E8F5E9 | #2E7D32 (green) |
| tag_chip_work_expense | #work-expense | #E3F2FD | #1565C0 (blue) |
| tag_chip_rent | #rent | #FFF3E0 | #E65100 (orange) |
| tag_chip_holiday | #holiday | #F3E5F5 | #6A1B9A (purple) |
| tag_chip_gym | #gym | #FCE4EC | #AD1457 (pink) |

Chip common style: corner_radius 20, padding 12h / 6v, label_medium. Chips sit in a horizontal scrollable row (spacing 8, overflow scroll_horizontal, padding_h 20).

- **view_tags state:** #groceries and #work-expense shown (2 chips)
- **edit_mode state:** all five chips shown (5 chips)

Each chip tap fires `remove_tag`; chip animates out and API DELETE is called.

**Add-tag row** (below chip row, visible in view_tags and edit_mode):

```
[ 🏷  #groceries, #holiday…         ] [ Add ]
  outlined  border #CCCCCC  flex 1      filled #1800B1
  border #1800B1 2dp in edit_mode
```

- Input: outlined, radius 12, padding 14h/12v, leading label_outlined icon, placeholder "#groceries, #holiday…"
- Button: "Add" filled #1800B1, white, radius 12, padding 16h/12v, label_medium

---

### 3. Notes Section

Separated from Tags by a 1dp #F0F0F0 divider (margin_h 20).

- "Notes" — title_medium, semi-bold, padding_h 20, bottom 10
- Multi-line text area: outlined, border #CCCCCC, radius 12, padding 14h/12v, min_height 100, margin_h 20, bottom 20
- Placeholder: "e.g. Weekly shop — bought extra for bank holiday"
- Role: multiline textbox; a11y: "Notes text area. Enter a private note for this transaction. Only you can see this."

---

### 4. Receipt Section

Separated from Notes by a 1dp #F0F0F0 divider (margin_h 20).

- "Receipt" — title_medium, semi-bold, padding_h 20, bottom 10
- **Drop zone:** bg #F8F8F8, radius 16, dashed border #DDDDDD 1dp, padding 24, margin_h 20, bottom 12, items centred
  - receipt_long_outlined icon — 36dp, #BBBBBB, bottom 8
  - "Tap to attach a receipt image" — body_medium, #AAAAAA, centred
  - Tap fires: `pick_image_from_gallery`
- **"Take Photo" button:** outlined #008B8B border + text, radius 12, leading camera_alt icon, padding 20h/12v, align_self centre, margin_h 20, bottom 24
  - Tap fires: `open_camera`

---

### 5. Save Button

```
┌─────────────────────────────────────┐
│              Save                   │
└─────────────────────────────────────┘
  filled #1800B1  white text  corner_radius 14
  padding: 24h / 16v  width: full  margin: 20h / 32dp bottom
  label_large
  on_click: save_metadata → transaction-detail
```

---

### 6. Save-Success Banner (save_success state only)

```
  ✅  Tags and notes saved
  bg #E8F5E9  radius 12  padding 16h/12v  margin 20h/16dp bottom
  check_circle_outlined 20dp #2E7D32 (margin_right 8)
  role: status
```

Banner appears immediately after save completes. Screen auto-navigates to transaction-detail after **1 800 ms**.

---

## State Layouts

| State | Visible sections |
|---|---|
| loading | Transaction summary card only + skeleton (3 rows) |
| view_tags | Full screen — 2 tag chips (#groceries, #work-expense) shown |
| edit_mode | Full screen — all 5 tag chips shown; add_tag_input border = #1800B1 2dp; keyboard up |
| save_success | Transaction card + success banner + tags + notes (receipt hidden); auto-nav after 1 800 ms |
| error | Transaction card only + cloud_off icon + "Unable to load metadata" + retry button; save button hidden |

---

## Interaction Map

| Component | Gesture | Action | Result |
|---|---|---|---|
| top app bar back | Tap | navigate_back | Pop to transaction-detail |
| top app bar delete | Tap | clear_all_metadata | Confirmation dialog → all metadata cleared |
| transaction_header_card | Tap | navigate_to_transaction_detail | Push transaction-detail |
| tag chip (any) | Tap | remove_tag | Chip animates out; DELETE API call |
| add_tag_input | Tap | focus_tag_input | Transition to edit_mode; keyboard opens; border turns #1800B1 |
| add_tag_button | Tap | add_tag | New chip appears; input cleared; POST tags API |
| notes_text_area | Tap | focus_notes | Multi-line keyboard opens |
| receipt_attachment_area | Tap | pick_image_from_gallery | System file picker opens |
| camera_button | Tap | open_camera | Camera intent opens |
| save_button | Tap | save_metadata | Sequential API calls; → save_success → auto-nav transaction-detail |

---

## Content Data

| Element | Value |
|---|---|
| Merchant | Whole Foods Market |
| Amount | -£67.84 |
| Date and time | 23 May 2026 · 14:32 |
| Tag 1 | #groceries (green) |
| Tag 2 | #work-expense (blue) |
| Tag 3 | #rent (orange) |
| Tag 4 | #holiday (purple) |
| Tag 5 | #gym (pink) |
| Tag input placeholder | #groceries, #holiday… |
| Notes placeholder | e.g. Weekly shop — bought extra for bank holiday |
| Receipt placeholder | Tap to attach a receipt image |
| Success banner | Tags and notes saved |

---

## Design Notes

**Colour strategy:**
- Primary #1800B1 header creates strong branded identity and spatial anchoring — the user never loses context of which transaction they're editing.
- #C5B8FF (lavender) for the date on the dark card — high legibility without harsh white on deep purple.
- Five distinct chip hues (green/blue/orange/purple/pink) provide at-a-glance category recognition even before reading the label text.
- Teal #008B8B for the camera button deliberately differentiates it from the primary purple CTA, preventing confusion with the Save action.

**Typography rhythm:**
- display_small for the transaction amount — the largest numeric element anchors the user spatially.
- title_medium semi-bold section headings divide the single scrollable form into scannable chapters.
- label_medium on chips — compact and readable at small radii.

**Spacing:**
- 1dp #F0F0F0 dividers with 20dp horizontal margins provide subtle section boundaries without visual weight.
- Save button: 16dp vertical padding + 32dp bottom margin = generous tap target with clear visual breathing room.
- Horizontal chip row: 8dp spacing prevents visual crowding across five chips.

**Accessibility:**
- Tag chips: "Tag: #groceries. Tap to remove." — action intent explicit.
- Add-tag input hint: "Type a tag name like #groceries and tap Add."
- Notes textarea: declared multiline; hint text describes privacy context.
- Success banner: role=status ensures screen-reader announcement without refocus.
- Transaction card: region role summarises context for screen-reader users navigating by landmark.

*Generated by /idea export | 2026-05-25*
