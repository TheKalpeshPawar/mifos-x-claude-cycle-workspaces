# MOCKUP — Transaction Tags & Notes

**Archetype:** detail_screen
**Shell:** Top app bar ("Tags & Notes", back arrow, delete/clear action). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │  ← TopAppBar, arrow_back + delete_outlined
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │  ← Transaction header card, bg #4C662B
│  │  Whole Foods Market           │  │    title_large SemiBold, white
│  │  -£67.84                      │  │    display_small Bold, white
│  │  23 May 2026 · 14:32          │  │    body_medium, #CDEDA3
│  └───────────────────────────────┘  │    radius 20, padding 20, margin H 20
│                                     │
│  ████████████████████  (skeleton)   │  ← Tags section skeleton
│  ████  ██████  ████    (skeleton)   │  ← 3 chip skeletons
│                                     │
│  ████████████████████  (skeleton)   │  ← Notes section skeleton (2 lines)
│  ████████████████████               │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Hero card always visible in loading state. Tag chips and notes text area replaced by shimmer skeletons (radius matching component shapes). Save button hidden.

---

## Screen: view_tags (content)

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market           │  │  ← Hero card, bg #4C662B
│  │  -£67.84                      │  │  ← display_small Bold, white
│  │  23 May 2026 · 14:32          │  │  ← body_medium, #CDEDA3
│  └───────────────────────────────┘  │
│                                     │
│  Tags                               │  ← title_medium SemiBold, #1A1C16
│  Tap a tag to remove it             │  ← body_small, #44483D
│                                     │
│  [#groceries] [#work-expense]       │  ← Chips row; horizontal scroll
│                                     │    #groceries: #CDEDA3 bg/#4C662B text
│                                     │    #work-expense: #DCE7C8 bg/#386663 text
│  ┌────────────────────┐  [ Add ]    │
│  │ [label] #holiday…  │  [button]   │  ← add_tag_input (flex:1) + Add button
│  └────────────────────┘             │    outlined `#E1E4D5` | filled `#4C662B`
│                                     │
│  ─────────────────────────────────  │  ← Divider #F9FAEF
│                                     │
│  Notes                              │  ← title_medium SemiBold, #1A1C16
│  ┌───────────────────────────────┐  │
│  │ e.g. Weekly shop — bought     │  │  ← Outlined multiline, #E1E4D5 border
│  │ extra for bank holiday        │  │    body_medium, min 100dp height
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Receipt                            │  ← title_medium SemiBold, #1A1C16
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐  │  ← Dashed border box #F9FAEF bg
│  │        [receipt_long]         │  │    #E1E4D5 1dp dashed border
│  │   Tap to attach a receipt     │  │    radius 16dp, padding 24dp
│   ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  │
│                                     │
│    ┌────────────────────────────┐   │
│    │ [camera] Take Photo        │   │  ← OutlinedButton, #386663, radius 12
│    └────────────────────────────┘   │
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Save               │  │  ← FilledButton, #4C662B, full-width
│  └───────────────────────────────┘  │    label_large, radius 14dp
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Hero card: `#4C662B` bg, radius 20dp, padding 20dp, margin H 20dp, margin_top 16dp. Merchant title_large/SemiBold white. Amount display_small/Bold white. Date body_medium `#CDEDA3`.
- Tags section: section label title_medium/SemiBold `#1A1C16`. Hint body_small `#44483D`. Chip row horizontally scrollable, padding H 20dp.
- Chips: radius 20dp, padding H 12/V 6. `#groceries`/`#holiday`/`#gym`: `#CDEDA3` bg; `#work-expense`: `#DCE7C8` bg/`#386663` text; `#rent`: `#CDEDA3` bg/`#44483D` text (A11Y fix).
- Add-tag row: outlined input flex:1, `#E1E4D5` border, radius 12dp, label_outlined icon; "Add" FilledButton `#4C662B`, radius 12dp, label_medium.
- Notes: outlined multiline TextArea, `#E1E4D5` border, radius 12dp, min 100dp.
- Receipt area: dashed `#E1E4D5` border, `#F9FAEF` bg, radius 16dp; receipt_long_outlined 36dp `#44483D`.
- Camera button: OutlinedButton, `#386663` text + border, camera_alt icon, radius 12dp, centred.
- Save: FilledButton `#4C662B`, full-width (margin H 20dp), radius 14dp, label_large white.

---

## Screen: edit_mode

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market -£67.84   │  │  ← Hero (same)
│  └───────────────────────────────┘  │
│                                     │
│  Tags                               │
│  Tap a tag to remove it             │
│                                     │
│  [#groceries] [#work-expense]       │
│  [#rent] [#holiday] [#gym]          │  ← All 5 chips visible in edit_mode
│                                     │
│  ┌────────────────────────────┐     │  ← Input: active #4C662B 2dp border
│  │ [label] #holiday           │[Add]│  ← Keyboard visible below
│  └────────────────────────────┘     │
│                                     │
│  ■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■ │  ← Soft keyboard (bottom ~40% of screen)
└─────────────────────────────────────┘
```

**Layout notes:** 5 chips shown. add_tag_input has `#4C662B` 2dp border (focused state). Soft keyboard pushes content up. Scroll continues to work.

---

## Screen: save_success

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market -£67.84   │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ✓  Tags and notes saved       │  │  ← Success banner: #CDEDA3 bg
│  └───────────────────────────────┘  │    check_circle_outlined 20dp #4C662B
│                                     │    body_medium #1A1C16
│  Tags                               │
│  [#groceries] [#work-expense]       │
│  [#rent]                            │
│                                     │
│  Notes                              │
│  ┌───────────────────────────────┐  │
│  │ (saved note text)             │  │
│  └───────────────────────────────┘  │
│                                     │
│  (auto-navigating in 1.8s…)         │
└─────────────────────────────────────┘
```

**Layout notes:** Success banner slides in at top of content (below hero). `#CDEDA3` bg, radius 12dp. Saved tag subset visible. Auto-navigate to transaction-detail after 1.8 seconds.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market -£67.84   │  │
│  └───────────────────────────────┘  │
│                                     │
│  Tags                               │
│                                     │
│  ┌───────────────────────────────┐  │  ← Empty state inline box (box type)
│  │ [label_outlined]              │  │    icon label_outlined 24dp #44483D
│  │  No tags added yet.           │  │    body_medium #44483D
│  │  Type a tag above and tap Add │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌────────────────────┐  [ Add ]    │
│  │ [label] #holiday…  │  [button]   │
│  └────────────────────┘             │
│                                     │
│  Notes                              │
│  ┌────────────────────────────────┐ │
│  │ No note added yet. Write a    │  │  ← Empty box: edit_note icon + body text
│  │ private note only you can see │  │
│  └────────────────────────────────┘ │
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Save               │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Tags & Notes            [clear]  │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  Whole Foods Market -£67.84   │  │
│  └───────────────────────────────┘  │
│                                     │
│          [cloud_off]                │  ← 48dp, #BA1A1A, centered
│                                     │
│     Unable to load metadata         │  ← titleMedium, #1A1C16, center
│  Could not load tags and notes.     │  ← bodyMedium, #44483D, center
│  Check your connection and retry.   │
│                                     │
│         ┌──────────────┐            │
│         │    Retry     │            │  ← OutlinedButton, #4C662B
│         └──────────────┘            │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Hero always visible. Error centred below hero. Save button hidden.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar back arrow + delete_outlined clear action
- [ ] Transaction header card: `#4C662B` bg, radius 20dp, margin H 20dp
- [ ] Amount in display_small/Bold white; date in body_medium `#CDEDA3`
- [ ] Tag chips: radius 20dp, label_medium; each variant correct bg/text token
- [ ] #work-expense: `#DCE7C8` bg / `#386663` text (secondary family)
- [ ] #rent: `#CDEDA3` bg / `#44483D` text (accessibility fix — not yellow)
- [ ] add_tag_input: outlined `#E1E4D5` border, label_outlined icon, flex:1
- [ ] add_tag_button: FilledButton `#4C662B`, radius 12dp
- [ ] edit_mode: input border becomes `#4C662B` 2dp when focused
- [ ] Notes textarea: outlined, `#E1E4D5` border, radius 12dp, min 100dp, multiline
- [ ] Receipt area: `#F9FAEF` bg, `#E1E4D5` dashed border, radius 16dp
- [ ] Camera button: OutlinedButton `#386663`, camera_alt icon
- [ ] Save button: FilledButton `#4C662B`, full-width, radius 14dp, label_large
- [ ] Success banner: `#CDEDA3` bg, check_circle_outlined 20dp `#4C662B`
- [ ] Auto-navigate to transaction-detail at 1.8s after save_success
- [ ] 5 chips visible in edit_mode; 2 chips in view_tags/content
- [ ] All text Outfit typeface
