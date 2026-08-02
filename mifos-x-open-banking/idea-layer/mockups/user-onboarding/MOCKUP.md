# User onboarding — Visual Mockup

> Auto-generated from `screens/user-onboarding/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31

**Implemented** — `onboarding/IntroScreen.kt` inside `feature/login`; it has **no module of its
own**. The app's first screen for an unauthenticated PSU.

---

## Screen: Welcome to Open Banking

**Archetype** `onboarding` · **States** `intro`

**One state, and `state_model: {}`.** `IntroScreen` is a **stateless composable** — no ViewModel,
no actions, no error surface. Nothing is fetched, so there is nothing to load, empty or fail.

> **Reverse-synced 2026-07-28.** The idea-layer previously described a **three-step pager** with
> six sub-screen transitions in `flow.yaml`. Source ships **one stateless screen**. Both the pager
> and the phantom transitions were removed; do not reintroduce them.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **hidden** | `ui.yaml#shell.bottom_navigation_visible: false` |
| Top app bar | **hidden** | `ui.yaml#shell.top_app_bar_visible: false` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

**The only screen in the app with no top app bar and no bottom nav.** There is nothing to
navigate back to — this is the entry point — and no tabs, because tabs live behind authentication.
The screen is edge-to-edge content with a single forward exit.

---

## State: intro

```
┌─────────────────────────────────────────┐
│                                          │
│                                          │
│            ┌──────────────┐              │  hero_illustration
│            │              │              │  OnboardingHeroIllustration
│            │      ⬡       │              │  NOT decorative — has alt text
│            │              │              │
│            └──────────────┘              │
│                                          │
│      See all your accounts               │  intro_headline
│      in one place                        │  headlineMedium, role=heading
│                                          │
│   Connect your HSBC accounts securely    │  intro_body, bodyMedium
│   with Open Banking. No passwords are     │  on-surface-variant
│   ever shared with this app, and you      │
│   stay in control of your data.           │
│                                          │
│   ( FAPI 1.0 Advanced )  ( FCA regulated )│  trust_chips — NON-interactive
│                                          │
│                                          │
│  [           Continue           ]         │  continue_button, filled
│                                          │
└─────────────────────────────────────────┘
   no top app bar · no bottom nav
```

### Component hierarchy

```
user-onboarding/
└── IntroScreen (stateless, edge-to-edge)
    ├── hero_illustration: image (OnboardingHeroIllustration, alt text)
    ├── intro_headline: text (headlineMedium, role: heading)
    ├── intro_body: text (bodyMedium, on-surface-variant)
    ├── trust_chips: chip_group (selection_mode: none)
    │   ├── fapi_chip: "FAPI 1.0 Advanced"
    │   └── fca_chip: "FCA regulated"
    └── continue_button: button (filled)
```

| Element | Token | Notes |
|---|---|---|
| Headline | `headlineMedium` (28sp) | `role: heading` — a real a11y heading, not styled text |
| Body | `bodyMedium` on `onSurfaceVariant` | establishes FCA regulation and password-free access |
| Trust chips | assist chips, `secondaryContainer` | **`selection_mode: none`** — non-interactive badges |
| CTA | `primary`, radius `full`, filled | |
| Background | `surface` | flat; no card, no gradient |

**The hero illustration is `decorative: false` and carries `alt` text.** It is the only
non-decorative image in the app — every other glyph is a Material Symbol marked decorative. It
conveys the product proposition to a screen-reader user, so it is described, not hidden.

**The trust chips are badges, not filters.** `selection_mode: none` — they cannot be tapped,
selected or filtered by. They exist to state the regulatory posture before the PSU is asked to
connect a bank account. Styling them as selectable chips would be a lie about their affordance;
they must not have Pressed or Selected states.

The copy leads with what the customer gets ("See all your accounts in one place") and follows with
why it is safe — not the reverse. Opening on compliance language reads as defensive.

**Interactions**

| Component | Action | Target | Notes |
|---|---|---|---|
| `continue_button` | `navigate_login` | **`login`** | the screen's only interactive element and only outward edge |

`onContinue` calls `navController.navigate(LoginRoute)` inside `authGraph`. The login screen then
stages the account-access-consent and launches the FAPI app-to-app redirect — **this** screen never
touches the network.

There is no "Skip", no "Maybe later", and no back. The app has no unauthenticated content to skip
to; every surface behind this point requires a consent.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| user-onboarding | `login` | `continue_button` |

Entry is the app's launch destination for an unauthenticated PSU — reached from
`RootNavScreen` when `ConsentSession.isActive()` is false, not from any in-app navigation.

---

## Removed in the 2026-07-28 reverse sync

| Removed | Why |
|---|---|
| Three-step pager description | Source ships one stateless screen, not a pager |
| 6 phantom sub-screen transitions in `flow.yaml` | No such transitions exist — there are no sub-screens |
