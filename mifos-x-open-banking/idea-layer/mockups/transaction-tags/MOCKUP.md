# Mockup: Transaction Tags & Notes

| Field     | Value                      |
|-----------|----------------------------|
| Feature   | transaction-tags           |
| Flavor    | consumer                   |
| Archetype | detail_screen              |
| ViewModel | TransactionTagsViewModel   |
| Route     | /transaction-tags/{transactionId} |
| States    | loading, view_tags, edit_mode, save_success, content, empty, error |

---

## Screen Layout

**Top app bar:** "Tags & Notes" Outfit Medium 18sp, back arrow `arrow_back` (navigate_back → transaction-detail), `delete_outlined` icon right (clear_all_metadata). No bottom navigation. Single-column vertical scroll.

---

## State: loading

```
┌────────────────────────────────────────┐
│ ← Tags & Notes           [🗑 AppBar]  │
├────────────────────────────────────────┤
│                                        │
│ ┌────────────────────────────────────┐ │
│ │ Whole Foods Market      [shimmer]  │ │  ← #4C662B header card
│ │ -£67.84                            │ │
│ │ 23 May 2026 · 14:32                │ │
│ └────────────────────────────────────┘ │
│                                        │
│  Tags                     [heading]    │
│ [⬜⬜⬜⬜] skeleton chips (3x)          │  ← shimmer_duration: short4
│                                        │
│  [ Add tag... ] [Add]                  │
│  ──────────────────────────────────    │
│  Notes                    [heading]    │
│ [⬜⬜⬜⬜⬜⬜⬜⬜] skeleton note         │
│  ──────────────────────────────────    │
│  Receipt                  [heading]    │
│ [⬜⬜⬜⬜⬜⬜⬜⬜] skeleton receipt      │
└────────────────────────────────────────┘
```

Save button hidden in loading state.

---

## State: view_tags / content

```
┌────────────────────────────────────────┐
│ ← Tags & Notes           [🗑 AppBar]  │
├────────────────────────────────────────┤
│ ┌────────────────────────────────────┐ │
│ │ Whole Foods Market                 │ │  ← #4C662B, role: region
│ │ -£67.84                [display_sm]│ │  ← #FFFFFF
│ │ 23 May 2026 · 14:32                │ │  ← #CDEDA3 body_medium
│ └────────────────────────────────────┘ │
│                                        │
│  Tags                     [heading]    │  ← title_medium #1A1C16
│  Tap a tag to remove it    [hint]      │  ← body_small #44483D
│ ╔════════════════════════════════════╗ │
│ ║ #groceries  #work-expense          ║ │  ← horizontal scroll chips
│ ╚════════════════════════════════════╝ │
│  ┌──────────────────────┐  ┌───────┐   │
│  │ 🏷 #groceries, #hol…│  │  Add  │   │  ← add_tag_input + button
│  └──────────────────────┘  └───────┘   │
│  ─────────────────────────────────     │
│  Notes                    [heading]    │
│ ┌────────────────────────────────────┐ │
│ │ e.g. Weekly shop — bought extra…   │ │  ← multiline, min 100dp
│ └────────────────────────────────────┘ │
│  ─────────────────────────────────     │
│  Receipt                  [heading]    │
│ ┌─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐   │
│ │         🧾                       │   │  ← dashed area, receipt icon
│ │   Tap to attach a receipt image  │   │
│ └─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘   │
│  ┌─────────────────┐                  │
│  │ 📷 Take Photo   │ [outlined]        │  ← #386663 border+text
│  └─────────────────┘                  │
│ ┌──────────────────────────────────┐  │
│ │           Save           [filled]│  │  ← #4C662B, full width
│ └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

---

## State: edit_mode

Same as view_tags/content, plus:
- `add_tag_input` border: `#4C662B`, border_width 2dp
- 5 chips shown: #groceries, #work-expense, #rent, #holiday, #gym
- Keyboard visible
- `assert_input_focused: add_tag_input`

---

## State: save_success

Success banner briefly shown; auto-navigate to transaction-detail after 1800ms.

```
│ ┌──────────────────────────────────┐  │
│ │ ✓ Tags and notes saved  [status] │  │  ← #CDEDA3 bg, check_circle_outlined
│ └──────────────────────────────────┘  │
│                                        │
│  Tags / Notes sections visible        │
│  (3 chips: #groceries, #work-expense, #rent)
│  (auto-navigate target: transaction-detail, delay: 1800ms)
```

---

## State: empty

No tags on this transaction yet.

```
│  Tags                     [heading]    │
│                                        │
│  ┌──────────────────────┐  ┌───────┐   │
│  │ 🏷 #groceries, #hol…│  │  Add  │   │
│  └──────────────────────┘  └───────┘   │
│                                        │
│  [empty state]                         │
│  No tags created yet.                  │
│  Add a tag to categorize your          │
│  transactions.                         │
│                                        │
│  Notes + Receipt sections below        │
│ ┌──────────────────────────────────┐  │
│ │           Save           [filled]│  │
│ └──────────────────────────────────┘  │
```

---

## State: error

OBP API failed.

```
│ ┌────────────────────────────────────┐ │
│ │ Whole Foods Market                 │ │  ← header card still visible
│ │ -£67.84                            │ │
│ └────────────────────────────────────┘ │
│                                        │
│    ☁ (cloud_off icon)                  │
│    Unable to load metadata             │  ← title_medium #1A1C16
│    Could not load tags and notes.      │  ← body_medium #44483D
│    Check your connection and try       │
│    again.                              │
│ ┌──────────────┐                       │
│ │    Retry     │ [outlined]             │
│ └──────────────┘                       │
│                                        │
│  (Save button hidden)                  │
```

---

## Design Token Reference

| Token           | Value     | Applied to                                          |
|-----------------|-----------|-----------------------------------------------------|
| primary         | `#4C662B` | Header card bg, save button, check_circle icon      |
| primary_container | `#CDEDA3` | Tag chip backgrounds, success banner              |
| secondary       | `#386663` | Camera button border+text                           |
| on_surface      | `#1A1C16` | Section headings                                    |
| on_surface_variant | `#44483D` | Hint text, receipt placeholder, #rent chip      |
| error           | `#BA1A1A` | #gym chip label                                     |
| surface_variant | `#E1E4D5` | Input borders, dividers                             |
| background      | `#F9FAEF` | Screen bg, dividers                                 |

---

_Generated by /idea export | 2026-06-02_
