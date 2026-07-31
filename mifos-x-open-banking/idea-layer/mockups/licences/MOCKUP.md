# Open-Source Licences — Visual Mockup

> Auto-generated from `screens/licences/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30

**Implemented** — `LicencesScreen.kt` lives inside `feature/settings`; it has **no module of its
own**. Reached from Settings → Open-source licences.

---

## Screen: Open-source licences

**Archetype** `detail_screen` · **States** `content`

**One state, and that is correct.** The licence text is a file bundled in the binary
(`composeResources/files/mpl_licence.txt`), read via
`produceState { Res.readBytes(...).decodeToString() }`. A bundled resource cannot 404, cannot be
empty, and cannot fail the network — so there is no loading, empty or error state to render. A
skeleton here would animate for a read that completes in microseconds.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **hidden** | `ui.yaml#shell.bottom_navigation_visible: false` |
| Top app bar | **visible**, title `{strings.licences.screen_title}` | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell` |

Bottom nav is hidden — this is a terminal reference document reached from Settings, and a tab tap
from a legal text is not a journey the app supports.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Open-source licences                │
├─────────────────────────────────────────┤
│  This app is built with open-source      │  licences_intro, bodyMedium
│  software. The full licence text is       │
│  reproduced below.                        │
│                                          │
│  Mozilla Public License Version 2.0      │  licences_body, MONOSPACE
│  ==================================      │
│                                          │
│  1. Definitions                           │
│                                          │
│  1.1. "Contributor" means each individual│
│  or legal entity that creates, contributes│
│  to the creation of, or owns Covered      │
│  Software.                                │
│                                          │
│  1.2. "Contributor Version" means the     │
│  combination of the Contributions of      │
│  others (if any) used by a Contributor…   │
│                          ⋮                │  scrolls
└─────────────────────────────────────────┘
   no bottom nav
```

### Component hierarchy

```
licences/
├── TopAppBar
│   ├── back_button (arrow_back)
│   └── title: "Open-source licences"
└── licences_screen: stack (vertical, scrollable)
    ├── licences_intro: text (bodyMedium)
    └── licences_body: text (MONO, bodySmall)
```

| Element | Token | Notes |
|---|---|---|
| Intro | `bodyMedium` on `onSurfaceVariant` | one short framing paragraph |
| Licence body | `bodySmall`, **`typography.font_family.mono`** | Roboto Mono |
| Screen padding | `spacing.screen_padding` | 16dp |
| Background | `surface` | no card, no container |

**Monospace is deliberate, not stylistic.** The MPL-2.0 text is a legal document with hard-wrapped
lines and ASCII rules (`====`); a proportional font reflows them into ragged nonsense. This is the
same reasoning that binds mono to money and account numbers — fidelity of the original form.

**Rendered flat, with no card.** The text is the entire screen. Wrapping several thousand words of
licence in a `surfaceContainer` card would add a border around content that has no natural end.

**Interactions** — scroll and back. Nothing is tappable; there are no hyperlinks in the rendered
text.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| settings | licences | "Open-source licences" row |
| licences | settings | back |

---

## What this screen deliberately is not

| Not this | Why |
|---|---|
| An AboutLibraries dependency list | AboutLibraries was tried and **removed**. This renders one bundled MPL-2.0 file, not a generated dependency graph |
| A web view | The text is bundled, not fetched — no network, no `LocalUriHandler` |
| A Terms page | There is no Terms page for this project. The only external legal link is Privacy, which opens `https://mifos.org/privacy-policy/` from **Settings**, not here |
