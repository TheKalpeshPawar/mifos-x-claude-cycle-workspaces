# MOCKUP — Transaction Tags & Notes

**Archetype:** detail_screen
**Shell:** Top app bar ("Tags & Notes", arrow_back navigation icon, delete_outlined "Clear all" action). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: Material Design 3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │  ← TopAppBar: title_large #1A1C16; back arrow;
│                                     │    delete_outlined icon (clear_all_metadata)
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │  ← transaction_header_card
│  │  Whole Foods Market           │  │    bg #4C662B, radius 20dp
│  │  −£67.84                      │  │    padding H 20dp / V 20dp
│  │  23 May 2026 · 14:32          │  │    txn_merchant: title_large, #FFFFFF, semibold
│  └───────────────────────────────┘  │    txn_amount: display_small, #FFFFFF, bold
│                                     │    txn_date: body_medium, #CDEDA3
│  Tags                               │  ← tags_section_label visible (title_medium, #1A1C16)
│                                     │
│  ████████  ████████  ████████       │  ← skeleton shimmer chips ×3
│  (chip shimmer 20dp radius)         │    motion: short4 = 200ms
│                                     │
│  Notes                              │  ← notes_section_label visible
│                                     │
│  █████████████████████████████████  │  ← skeleton note area line 1
│  ██████████████████████             │  ← skeleton note area line 2
│                                     │
│  Receipt                            │  ← receipt_section_label visible
│                                     │
│  ████████████████████████████████   │  ← skeleton receipt block (1 block)
│                                     │
│  (Save button hidden)               │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Transaction header card always visible in loading state. skeleton shimmer uses `#E1E4D5` base. Save button not rendered. Skeleton shapes match component radii: chips 20dp, text areas 12dp, receipt block 16dp.

---

## Screen: view_tags (content)

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │  ← transaction_header_card, bg #4C662B
│  │  Whole Foods Market           │  │    title_large, semibold, #FFFFFF
│  │  −£67.84                      │  │    display_small, bold, #FFFFFF
│  │  23 May 2026 · 14:32          │  │    body_medium, #CDEDA3
│  └───────────────────────────────┘  │    radius 20dp, margin top 16dp
│                                     │
│  Tags                               │  ← title_medium, semibold, #1A1C16
│  Tap a tag to remove it             │  ← body_small, #44483D
│                                     │
│  ╔══════════╗ ╔══════════════════╗  │  ← tags_chips_row (horizontal scroll)
│  ║#groceries║ ║  #work-expense   ║  │    #groceries: #CDEDA3 bg / #4C662B text
│  ╚══════════╝ ╚══════════════════╝  │    #work-expense: #DCE7C8 bg / #386663 text
│                                     │    chips: radius 20dp, label_medium, 12dp H pad
│  ┌──────────────────────┐  ┌─────┐  │  ← add_tag_row
│  │ [🏷] #groceries, …   │  │ Add │  │    add_tag_input: outlined, #E1E4D5 border
│  └──────────────────────┘  └─────┘  │    radius 12dp, flex:1, body_medium
│                                     │    add_tag_button: filled #4C662B, radius 12dp
│  ─────────────────────────────────  │  ← notes_divider (#F9FAEF, 1dp)
│                                     │
│  Notes                              │  ← title_medium, semibold, #1A1C16
│  ┌───────────────────────────────┐  │
│  │ e.g. Weekly shop — bought     │  │  ← notes_text_area: outlined, #E1E4D5 border
│  │ extra for bank holiday        │  │    radius 12dp, min 100dp, body_medium, multiline
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← receipt_divider (#F9FAEF, 1dp)
│                                     │
│  Receipt                            │  ← title_medium, semibold, #1A1C16
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐  │  ← receipt_attachment_area
│  │      [receipt_long_outlined]  │  │    #F9FAEF bg, dashed #E1E4D5 border 1dp
│  │  Tap to attach a receipt      │  │    radius 16dp, padding 24dp
│   ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  │    icon 36dp #44483D, body_medium #44483D
│                                     │
│     ┌─────────────────────────┐     │  ← camera_button
│     │ [📷] Take Photo         │     │    outlined, #386663 border + text, radius 12dp
│     └─────────────────────────┘     │    camera_alt leading icon, label_medium
│                                     │
│  ┌───────────────────────────────┐  │  ← save_button
│  │             Save              │  │    filled #4C662B, full-width, radius 14dp
│  └───────────────────────────────┘  │    label_large #FFFFFF
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Hero card: `#4C662B` bg, radius 20dp, padding H/V 20dp, margin H 20dp, top 16dp.
- Tag chips: horizontally scrollable row (overflow: scroll_horizontal), 8dp between chips.
- `#groceries`/`#holiday`/`#rent`/`#gym`: `#CDEDA3` bg. `#work-expense`: `#DCE7C8` bg / `#386663` text. `#rent`: `#44483D` text (WCAG AA contrast fix — not yellow).
- Add-tag row: label_outlined 🏷 icon inside input, placeholder "#groceries, #holiday…", flex:1.
- Notes min-height 100dp; multiline; auto-expands.
- Receipt area: dashed border, receipt_long_outlined icon 36dp centered.
- Save: full-width, margin H 20dp, 32dp bottom margin.

---

## Screen: edit_mode

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market           │  │  ← Hero (always visible)
│  │  −£67.84                      │  │
│  │  23 May 2026 · 14:32          │  │
│  └───────────────────────────────┘  │
│                                     │
│  Tags                               │
│  Tap a tag to remove it             │
│                                     │
│  ╔══════════╗ ╔══════════════════╗  │  ← All 5 chips visible in edit_mode
│  ║#groceries║ ║  #work-expense   ║  │
│  ╚══════════╝ ╚══════════════════╝  │
│  ╔══════╗ ╔═════════╗ ╔═════╗       │
│  ║ #rent║ ║ #holiday║ ║ #gym║       │
│  ╚══════╝ ╚═════════╝ ╚═════╝       │
│                                     │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐  │  ← add_tag_input: focused state
│  │ [🏷] #holiday                │  │    border: #4C662B 2dp (component_override)
│   ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  │
│                          [ Add ] │  │
│                                     │
│  ──────────── (content above) ───── │
│  ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■ ■  │  ← Soft keyboard (occupies bottom ~40%)
└─────────────────────────────────────┘
```

**Layout notes:** All 5 tag chips visible in edit_mode (groceries, work-expense, rent, holiday, gym). Focused add_tag_input shows `#4C662B` 2dp border. Soft keyboard pushes content up; vertical scroll remains active.

---

## Screen: save_success

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market           │  │  ← Hero card
│  │  −£67.84                      │  │
│  │  23 May 2026 · 14:32          │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← save_success_banner
│  │ ✓  Tags and notes saved       │  │    bg #CDEDA3, radius 12dp, padding H 16/V 12
│  └───────────────────────────────┘  │    check_circle_outlined 20dp #4C662B
│                                     │    role: status
│  Tags                               │
│  Tap a tag to remove it             │
│                                     │
│  ╔══════════╗ ╔══════════════════╗  │  ← Retained tags from save_success state
│  ║#groceries║ ║  #work-expense   ║  │    (groceries, work-expense, rent)
│  ╚══════════╝ ╚══════════════════╝  │
│  ╔══════╗                           │
│  ║ #rent║                           │
│  ╚══════╝                           │
│                                     │
│  Notes                              │
│  ┌───────────────────────────────┐  │
│  │ Paid via Equity mobile —      │  │  ← Saved note content (demo data)
│  │ confirmed by SMS KES 3,420    │  │
│  └───────────────────────────────┘  │
│                                     │
│  (Auto-navigating to transaction-   │
│   detail in 1.8 seconds…)           │
└─────────────────────────────────────┘
```

**Layout notes:** Success banner appears immediately after save (role: status for screen reader). Auto-navigate to `transaction-detail` fires after 1800 ms delay. Retained subset of 3 tags shown. Save button not shown in save_success layout.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market           │  │  ← Hero card
│  │  −£67.84                      │  │
│  │  23 May 2026 · 14:32          │  │
│  └───────────────────────────────┘  │
│                                     │
│  Tags                               │  ← tags_section_label
│                                     │
│  ┌───────────────────────────────┐  │  ← tags_chips_row empty component
│  │  [🏷]                         │  │    type: box, icon: label_outlined 24dp #44483D
│  │  No tags added yet.           │  │    body_medium, #44483D
│  │  Type a tag above and tap Add │  │
│  │  to categorise this txn.      │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌──────────────────────┐  ┌─────┐  │  ← add_tag_row
│  │ [🏷] #groceries, …   │  │ Add │  │
│  └──────────────────────┘  └─────┘  │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Notes                              │
│                                     │
│  ┌───────────────────────────────┐  │  ← notes_text_area empty component
│  │  [✏]                          │  │    type: box, icon: edit_note 24dp #44483D
│  │  No note added yet.           │  │    body_medium, #44483D
│  │  Write a private note only    │  │
│  │  you can see.                 │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← save_button
│  │             Save              │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:** No tag chips rendered. Empty state boxes shown inline within respective sections (tags and notes). Receipt section also shows empty box with receipt_long_outlined icon per component_states.empty spec.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [🗑]     │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market           │  │  ← Hero card always visible in error state
│  │  −£67.84                      │  │
│  │  23 May 2026 · 14:32          │  │
│  └───────────────────────────────┘  │
│                                     │
│           [☁ cloud_off]             │  ← error_icon: cloud_off, centered
│                                     │    ~48dp, #BA1A1A (error color)
│     Unable to load metadata         │  ← error_title: title_medium, #1A1C16, center
│                                     │
│  Could not load tags and notes.     │  ← error_message: body_medium, #44483D, center
│  Check your connection and          │
│  try again.                         │
│                                     │
│        ┌─────────────────┐          │
│        │      Retry      │          │  ← show_retry_button: outlined, #4C662B
│        └─────────────────┘          │    fires RetryLoad event
│                                     │
│  (Save button hidden)               │
└─────────────────────────────────────┘
```

**Layout notes:** Hero always visible in error state. Error icon, title, message, and retry button are centered in the remaining space. Save button not rendered. Tags, notes, and receipt sections not rendered.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar: "Tags & Notes" title, arrow_back navigation icon, delete_outlined action ("Clear all")
- [ ] No bottom navigation bar (shell: bottom_nav: false)
- [ ] Transaction header card: `#4C662B` bg, radius 20dp, margin H 20dp, top 16dp
- [ ] Merchant "Whole Foods Market": title_large, semibold, `#FFFFFF`
- [ ] Amount "−£67.84": display_small (32sp/600), bold, `#FFFFFF`
- [ ] Date "23 May 2026 · 14:32": body_medium (14sp/400), `#CDEDA3`
- [ ] Tags section label: title_medium (16sp/500), semibold, `#1A1C16`, heading role
- [ ] Hint "Tap a tag to remove it": body_small (12sp/400), `#44483D`
- [ ] Tag chips: radius 20dp, padding H 12dp/V 6dp, label_medium (12sp/500)
- [ ] #groceries, #holiday, #gym: `#CDEDA3` bg / `#4C662B` text
- [ ] #work-expense: `#DCE7C8` bg / `#386663` text (secondary family)
- [ ] #rent: `#CDEDA3` bg / `#44483D` text (WCAG AA fix — 7.25:1 contrast; NOT yellow)
- [ ] add_tag_input: outlined `#E1E4D5` border, label_outlined leading icon, radius 12dp, flex:1
- [ ] add_tag_button: filled `#4C662B`, `#FFFFFF` text, radius 12dp, label_medium
- [ ] edit_mode: add_tag_input border → `#4C662B` 2dp; all 5 chips visible
- [ ] Notes textarea: outlined `#E1E4D5` border, radius 12dp, min 100dp, multiline
- [ ] Placeholder: "e.g. Weekly shop — bought extra for bank holiday"
- [ ] Receipt attachment area: `#F9FAEF` bg, dashed `#E1E4D5` border 1dp, radius 16dp, 24dp padding
- [ ] receipt_long_outlined icon: 36dp, `#44483D`, centered
- [ ] camera_button: outlined `#386663` border + text, camera_alt icon, radius 12dp, centered
- [ ] save_button: filled `#4C662B`, full-width (margin H 20dp), radius 14dp, label_large
- [ ] save_success_banner: `#CDEDA3` bg, check_circle_outlined 20dp `#4C662B`, radius 12dp; role: status
- [ ] Auto-navigate to transaction-detail at 1800 ms after save_success
- [ ] loading state: skeleton×3 chips, skeleton×2 note lines, skeleton×1 receipt block; save button hidden
- [ ] error state: cloud_off icon centered, retry button outlined `#4C662B`; save button hidden
- [ ] All text: Outfit typeface. Minimum touch target 48dp. Screen baseline 390px.

---

_Generated by /idea export | 2026-05-30_