# MOCKUP — About

**Archetype:** settings
**Shell:** Top app bar ("About") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ←  About                            │  ← TopAppBar, title_large, back arrow
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [Mifos Logo]│            │  ← Image 80×80dp, tinted #4C662B, centred
│         └──────────────┘            │
│       Mifos X Open Banking          │  ← headline_small, #4C662B, centred
│      Open Banking for Everyone      │  ← body_medium, #44483D, centred
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Version         1.0.0        │  │  ← App Info card (white, radius 12dp)
│  │  ─────────────────────────── │  │     body_large "#1A1C16" | body_medium "#44483D"
│  │  Build           2026.05.001  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Legal                        │  │  ← Legal card (white, radius 12dp)
│  │  ─────────────────────────── │  │     title_medium #4C662B header
│  │  Terms of Service      ↗      │  │  ← body_large, #1A1C16 | open_in_new #C5C8BA
│  │  ─────────────────────────── │  │
│  │  Privacy Policy        ↗      │  │  ← body_large, #1A1C16 | open_in_new #C5C8BA
│  │  ─────────────────────────── │  │
│  │  Open Source Licenses  >      │  │  ← body_large, #1A1C16 | chevron_right #C5C8BA
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │      Rate This App            │  │  ← Outlined button, border+text #4C662B
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Logo section: centred column with 32dp top + bottom padding; logo image above app name, tagline below.
- App Info card: full-width, 16dp horizontal margin, 8dp vertical gap below logo section. Row layout: label (flex 1) + value (right-aligned). Hairline `#E1E4D5` divider between rows (4dp top/bottom margin).
- Legal card: full-width, 16dp horizontal margin, 16dp gap below App Info card. Each row is a stack: link text (flex 1) + trailing icon (18–20dp). Hairline `#E1E4D5` dividers between all three rows.
- Rate App button: full-width outlined button, 16dp horizontal margin, 24dp top margin after Legal card.
- Scroll: SingleChildScrollView — content may overflow on small screens.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│         ░░░░░░░░░░░░  (skeleton)    │  ← 80×80dp logo shimmer, centred
│         ░░░░░░░░░░░░░░ (skeleton)   │  ← App name placeholder shimmer
│         ░░░░░░░░░░░░   (skeleton)   │  ← Tagline placeholder shimmer
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ░░░░░░░░░  ░░░░░░░░░░░░░░░  │  │  ← App Info card skeleton (2 rows)
│  │  ░░░░░░░░░  ░░░░░░░░░░░░░░░  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │  ← Legal card skeleton (3 rows)
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer (`#E1E4D5` → `#F0F1E6` animated) applied to all skeleton blocks. No interactive elements visible. Top app bar remains visible.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│                                     │
│              ⓘ                      │  ← info_outline icon, 48dp, #BA1A1A, centred
│                                     │
│    Unable to load app information.  │  ← body_medium, #44483D, centred
│      Please restart the app.        │  ← body_medium, #44483D, centred
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Icon and message centred horizontally and vertically within the viewport. No cards, no button. Top app bar remains visible.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [Mifos Logo]│            │  ← Logo still rendered
│         └──────────────┘            │
│       Mifos X Open Banking          │
│      Open Banking for Everyone      │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Legal                        │  │  ← Legal card always shown
│  │  ─────────────────────────── │  │
│  │  Terms of Service      ↗      │  │
│  │  ─────────────────────────── │  │
│  │  Privacy Policy        ↗      │  │
│  │  ─────────────────────────── │  │
│  │  Open Source Licenses  >      │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** App Info card (version/build) and Rate App button hidden because version data is unavailable. Logo section and Legal card always rendered — legal navigation must remain accessible regardless of build data.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon (`arrow_back`)
- [ ] App logo 80×80dp centred, tinted `#4C662B`
- [ ] App name headline_small (24sp/SemiBold) in `#4C662B`
- [ ] Tagline body_medium (14sp) in `#44483D`
- [ ] App Info card: white `#FFFFFF`, 12dp radius, rows with body_large label + body_medium value
- [ ] Hairline `#E1E4D5` dividers between all card rows
- [ ] Legal card: `title_medium` "Legal" header in `#4C662B`, three link rows with trailing icons
- [ ] `open_in_new` icon (18dp, `#C5C8BA`) for ToS and Privacy Policy rows
- [ ] `chevron_right` icon (20dp, `#C5C8BA`) for Licenses row
- [ ] Outlined button "Rate This App" with `#4C662B` border and text
- [ ] Shimmer skeleton blocks matching content layout proportions for loading state
- [ ] Error state centred with `info_outline` icon in `#BA1A1A` (error color)
- [ ] Empty state: logo + Legal card; App Info + Rate App button hidden
- [ ] All text uses Outfit typeface
- [ ] 16dp horizontal content padding throughout
- [ ] 48dp minimum touch targets on all interactive rows and button
