# MOCKUP — Open Source Licenses

**Archetype:** index_list
**Shell:** Top app bar ("Open Source Licenses") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ←  Open Source Licenses             │  ← M3 TopAppBar, back arrow
├─────────────────────────────────────┤
│                                     │
│  Mifos X Open Banking is built on  │  ← body_medium, #44483D, 24dp padding
│  these outstanding open-source      │
│  libraries.                         │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Compose Multiplatform [Apache]│  │  ← White card, 12dp radius
│  │ v1.8.2 · JetBrains           │  │    Name: body_large #1A1C16 w500
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │    Meta: body_small #44483D
│  │ Ktor                 [Apache]│  │    Badge: #CDEDA3 bg, #4C662B text
│  │ v3.2.0 · JetBrains           │  │    label_small, 6dp radius
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ Koin                 [Apache]│  │
│  │ v4.1.0 · insert-koin.io      │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ Store5               [Apache]│  │
│  │ v5.1.0 · Mobile Kotlin       │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ Room KMP             [Apache]│  │
│  │ v2.7.0 · Google / AndroidX   │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ kotlinx.serialization[Apache]│  │
│  │ v1.8.1 · JetBrains           │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ kotlinx.coroutines   [Apache]│  │
│  │ v1.10.1 · JetBrains          │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │ Material3            [Apache]│  │
│  │ v1.3.2 · Google / Compose    │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen padding: 24dp (`spacing.lg`) on all sides.
- Subtitle 24dp margin-bottom before list card.
- List card: white (#FFFFFF), 12dp radius, no external border, no elevation shadow.
- Each row: 16dp horizontal + 16dp vertical inner padding; two-line layout (name + meta). Badge floats trailing.
- Dividers: `#E1E4D5`, 16dp horizontal margin, 1dp height.
- All rows are tappable (open Apache 2.0 license URL in system browser).
- Scroll: full-page vertical scroll if content exceeds viewport.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Open Source Licenses             │
├─────────────────────────────────────┤
│                                     │
│  ████████████████████████████       │  ← Subtitle shimmer
│  ████████████████████               │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  ████████   │  │  ← Row shimmer (name + badge)
│  │  ██████████████               │  │    (meta line)
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │  ████████████████  ████████   │  │
│  │  ██████████████               │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │  ████████████████  ████████   │  │
│  │  ██████████████               │  │
│  ├ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┤  │
│  │  (4 more rows...)             │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** `trust_horizon` gradient shimmer applied. 8 rows simulated. No interaction.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Open Source Licenses             │
├─────────────────────────────────────┤
│                                     │
│                                     │
│              </›                    │  ← code_off icon 48dp #BA1A1A, centered
│                                     │
│   Unable to load license            │  ← body_medium #44483D centered
│   information. Please restart       │
│   the app.                          │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Icon and message vertically centered in viewport. No retry button (restart required for asset read failure).

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Open Source Licenses             │
├─────────────────────────────────────┤
│                                     │
│  Mifos X Open Banking is built on  │  ← Subtitle remains visible
│  these outstanding open-source      │
│  libraries.                         │
│                                     │
│              </›                    │  ← code_off icon 48dp #75796C centered
│                                     │
│          No licenses found          │  ← headline_small #1A1C16 centered
│   License data could not be parsed. │  ← body_medium #44483D centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Should never occur in production — all 8 licenses are bundled. Shown only if JSON parsing fails without a read error.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon, title "Open Source Licenses"
- [ ] No bottom navigation bar (shell: bottom_nav: false)
- [ ] Subtitle paragraph: body_medium `#44483D`, 24dp spacing below
- [ ] White list card: `#FFFFFF`, 12dp radius, 24dp screen margin
- [ ] 8 two-line list rows: name (body_large `#1A1C16`, weight 500) + meta (body_small `#44483D`)
- [ ] Trailing badge on each row: `#CDEDA3` background, `#4C662B` text, 6dp radius, label_small
- [ ] 7 intra-list dividers: `#E1E4D5`, 16dp horizontal margin
- [ ] All rows tappable → system browser opens Apache 2.0 URL
- [ ] Shimmer loading state: 8 two-line skeleton rows with matching proportions
- [ ] Error icon: code_off 48dp `#BA1A1A`, centered
- [ ] All text uses Outfit typeface; 24dp screen padding
