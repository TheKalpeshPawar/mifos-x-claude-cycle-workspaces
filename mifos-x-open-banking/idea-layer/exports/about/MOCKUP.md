# MOCKUP — About

**Archetype:** settings  
**Shell:** Top app bar ("About") with back arrow. No bottom navigation bar.  
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ←  About                            │  ← Top app bar (M3 TopAppBar, back arrow)
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [App Logo]  │            │  ← Centered app logo (image, ~72×72 dp)
│         └──────────────┘            │
│         Mifos X Open Banking        │  ← App name, titleLarge, earth-green
│                                     │
│  ┌───────────────────────────────┐  │
│  │  App Information              │  │  ← Card (M3 ElevatedCard)
│  │  ─────────────────────────── │  │
│  │  Version          1.0.0       │  │
│  │  Build            2026.05.001 │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Legal                        │  │  ← Card (M3 ElevatedCard)
│  │  ─────────────────────────── │  │
│  │  Terms of Service          >  │  │  ← Tappable row, opens external URL
│  │  Privacy Policy            >  │  │  ← Tappable row, opens external URL
│  │  Open Source Licenses      >  │  │  ← Tappable row, opens external URL
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       ★  Rate This App        │  │  ← Filled tonal button, earth-green
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Logo section: vertically centred in top ~30% of scrollable area; logo above app name.
- App info card and Legal card: full-width with 16 dp horizontal padding, 8 dp vertical gap between cards.
- Each Legal row: ListItem with trailing chevron icon; divider between rows.
- Rate app button: full-width FilledTonalButton, 16 dp horizontal margin, 24 dp top margin after Legal card.
- Scroll: SingleChildScrollView — content may overflow on small screens.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│  ████████████████  (skeleton)       │  ← Logo placeholder ~72×72 dp
│  ████████████      (skeleton)       │  ← App name placeholder
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Card skeleton (App info)
│  │  ████████████  ██████████████ │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Card skeleton (Legal)
│  │  ████████████████████████████ │  │
│  │  ████████████████████████████ │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation applied to all skeleton blocks. No interactive elements.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│              ⚠                      │  ← Error icon, large (48 dp), M3 error color
│                                     │
│     Unable to load app info         │  ← bodyLarge, center-aligned
│  Check your device and try again.   │  ← bodyMedium, subdued, center-aligned
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Icon + messages centred vertically in the viewport.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  About                            │
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [App Logo]  │            │
│         └──────────────┘            │
│         Mifos X Open Banking        │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Legal                        │  │
│  │  ─────────────────────────── │  │
│  │  Terms of Service          >  │  │
│  │  Privacy Policy            >  │  │
│  │  Open Source Licenses      >  │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** App info card absent (version unavailable). Legal card and logo remain. No Rate App button.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon
- [ ] ElevatedCard for App Information and Legal sections
- [ ] ListItem rows with chevron trailing icon for all legal links
- [ ] FilledTonalButton for Rate App (earth-green #4C662B container)
- [ ] Shimmer skeleton blocks matching content layout proportions
- [ ] Error state centred with M3 error color icon
- [ ] All text uses Outfit typeface
- [ ] 16 dp horizontal content padding throughout
