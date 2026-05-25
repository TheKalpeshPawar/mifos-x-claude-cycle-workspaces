# Visual Specification — Transaction Tags & Notes

| Field | Value |
|---|---|
| Feature | transaction-tags |
| Flavor | consumer |
| Archetype | detail_screen |

---

## Screen Layout

Top app bar: "Tags & Notes" title, back arrow, delete_outlined "Clear All" icon (destructive). No bottom navigation. Scrollable single-column content:

1. **Transaction header card** — Deep purple #1800B1 card (radius 20, padding 20, margin horizontal 20, top 16, bottom 20) with merchant, amount, date
2. **"Tags" section heading** — title_medium, semi-bold, #111111
3. **Tag chips row** — Horizontal scrollable row of green chips; each chip is tappable to remove
4. **Add tag row** — Outlined input + "Add" button side by side
5. **Divider** — #F0F0F0, 1dp
6. **"Notes" section heading** — title_medium, semi-bold
7. **Notes text area** — Outlined multi-line input (min height 100, margin horizontal 20)
8. **Divider** — #F0F0F0, 1dp
9. **"Receipt" section heading** — title_medium, semi-bold
10. **Receipt drop zone** — Dashed-border box (radius 16, center-aligned receipt icon + placeholder text)
11. **"Take Photo" button** — Outlined teal (#008B8B) with camera icon
12. **"Save" button** — Full-width filled #1800B1, bottom of screen, large tap target

---

## Components

### Transaction Header Card
- **Style:** Background #1800B1, corner_radius 20, padding horizontal/vertical 20, margin horizontal 20
- **Merchant:** "Whole Foods Market" — title_large, white, semi-bold, bottom 8
- **Amount:** "-£67.84" — display_small, white, bold, bottom 4
- **Date:** "23 May 2026 · 14:32" — body_medium, #C5B8FF (soft lavender on dark)
- **Note:** The purple header creates a strong visual anchor tying this screen to the originating transaction

### Tag Chips
- **Style:** Each chip has background #E8F5E9, corner_radius 20, padding horizontal 12 vertical 6, text #2E7D32, typography label_medium
- **Current tags:** "Groceries", "Organic"
- **Interaction:** Tap to remove; chip disappears with confirmation
- **Row:** Horizontal scrollable with spacing 8, padding horizontal 20

### Add Tag Row
- **Input:** Outlined, border #CCCCCC, radius 12, leading label_outlined icon, placeholder "Add a tag...", flex 1, padding horizontal 14 vertical 12
- **Button:** "Add" filled #1800B1, white text, radius 12, padding horizontal 16 vertical 12, label_medium
- **Layout:** Horizontal row with spacing 8, padding horizontal 20

### Notes Text Area
- **Style:** Outlined, border #CCCCCC, radius 12, padding 14/12, min_height 100, margin horizontal 20, bottom 20
- **Placeholder:** "Add a private note about this transaction..."
- **Typography:** body_medium
- **Role:** multiline textbox

### Receipt Attachment Area
- **Style:** Background #F8F8F8, radius 16, dashed border #DDDDDD 1dp, padding 24, margin horizontal 20, bottom 12, items centered
- **Contents:**
  - receipt_long_outlined icon, 36dp, #BBBBBB, centered, bottom 8
  - "Tap to attach a receipt image" body_medium, #AAAAAA, centered
- **Interaction:** Tap triggers pick_image_from_gallery

### Camera Button
- **Style:** Outlined, border #008B8B, text #008B8B, radius 12, leading camera_alt icon, padding horizontal 20 vertical 12, centered (align_self center), margin horizontal 20, bottom 24

### Save Button
- **Style:** Filled #1800B1, white text, corner_radius 14, padding horizontal 24 vertical 16, label_large, full width, margin horizontal 20, bottom 32

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| tag_chip_groceries / tag_chip_organic | Tap | remove_tag action — chip animates out; API DELETE call |
| add_tag_input | Tap | focus_tag_input action — keyboard opens |
| add_tag_button | Tap | add_tag action — tag added to chips row; input cleared; API POST |
| notes_text_area | Tap | focus_notes action — multi-line keyboard opens |
| receipt_attachment_area | Tap | pick_image_from_gallery action — system file picker opens |
| camera_button | Tap | open_camera action — camera intent opens |
| save_button | Tap | save_metadata action — all changes posted to OBP; screen pops on success |
| top app bar delete icon | Tap | clear_all_metadata action — confirmation dialog before clearing |

---

## Content Data

| Element | Sample Value |
|---|---|
| Merchant | Whole Foods Market |
| Amount | -£67.84 |
| Date and time | 23 May 2026 · 14:32 |
| Existing tag 1 | Groceries |
| Existing tag 2 | Organic |
| Notes placeholder | Add a private note about this transaction... |
| Receipt placeholder | Tap to attach a receipt image |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 header card creates a strong branded identity that ties the metadata screen to the specific transaction
- #C5B8FF for the date on the dark header — a desaturated lavender that reads clearly on deep purple without harsh white
- Green (#E8F5E9 / #2E7D32) tag chips — distinct from the purple palette; signals "label" not "action"
- Teal #008B8B for the camera button — deliberate differentiation from the primary purple CTA colour to avoid confusion with Save

**Typography:**
- Transaction amount: display_small — the largest visible number, anchors the user in context of which transaction they're editing
- Section headings: title_medium semi-bold — creates visual chapters in a single scrolling form

**Spacing:**
- Sections are divided by 1dp #F0F0F0 dividers with 20dp horizontal margins — subtle separation without heavy visual weight
- The Save button sits at the very bottom with 32dp bottom margin and 16dp vertical padding — generous tap target to avoid accidental other taps

**Accessibility:**
- Tag chips read out "Tag: [name]. Tap to remove." — action intent is explicit in the a11y label
- Notes textarea has hint "Type a tag name and tap Add" via a11y hint; multiline declared
- Receipt area reads "No receipt attached. Tap to choose from gallery." — current state described

*Generated by /idea export | 2026-05-25*
