# MOCKUP — Field Officer Dashboard

**Archetype:** dashboard
**Shell:** M3 bottom navigation bar (80dp height, #F9FAEF background, #C5C8BA border-top, #DCE7C8 active-indicator pill). Top-right: profile icon (account_circle 32dp #4C662B, absolute top:20 right:16) + settings icon (settings 24dp #44483D, absolute top:24 right:56).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────────┐
│                              ⚙    👤    │  ← settings 24dp #44483D (right:56) · account_circle 32dp #4C662B (right:16)
│  Good morning, Priya 👋                 │  ← headline_medium (28sp/400), #4C662B · pt:20 ph:16
│  Monday, 25 May 2026 · Mifos Nairobi   │  ← body_medium (14sp/400), #44483D · pt:4 pb:16
│                                         │
│  ┌────────────────────┐ ┌────────────┐  │  ← stats_grid: 2-col 12dp gap ph:16 pb:16
│  │ ░░░░░░░░░░░░░░░░░░ │ │ ░░░░░░░░░ │  │  ← skeleton (×4): #E1E4D5, 12dp radius, 80dp height
│  │ ░░░░░░░░░░░░░░░░░░ │ │ ░░░░░░░░░ │  │    shimmer 200ms (short4), static_placeholder reduced-motion
│  └────────────────────┘ └────────────┘  │
│  ┌────────────────────┐ ┌────────────┐  │
│  │ ░░░░░░░░░░░░░░░░░░ │ │ ░░░░░░░░░ │  │
│  │ ░░░░░░░░░░░░░░░░░░ │ │ ░░░░░░░░░ │  │
│  └────────────────────┘ └────────────┘  │
│                                         │
│  Action Needed                          │  ← title_large (22sp), #1A1C16 · visible label during skeleton
│  ┌─────────────────────────────────┐    │  ← skeleton alert rows (×3): #E1E4D5 12dp radius 52dp height
│  │ ░░░░░░░░░░░░░░░░░░░░  [░░░░░░] │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │
│  │ ░░░░░░░░░░░░░░░░░░░░  [░░░░░░] │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← skeleton corporate + agent cards (×2)
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │
│  │ ░░░░░░░░░░░░░░░░░░░░  [░░░░░░] │    │
│  └─────────────────────────────────┘    │
│                                         │
│  Today's Schedule                       │  ← title_medium (16sp/500), #1A1C16
│  ┌─────────────────────────────────┐    │  ← skeleton meeting rows (×2): #E1E4D5 52dp height
│  │ ░░░░░░  ░░░░░░░░░░░░░░░░░░░░░░ │    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │
│  │ ░░░░░░  ░░░░░░░░░░░░░░░░░░░░░░ │    │
│  └─────────────────────────────────┘    │
│                                         │
├─────────────────────────────────────────┤
│  [Home] [Customers] [Apps] [Messages] [More] │  ← M3 bottom nav 80dp, Home active (DCE7C8 pill)
└─────────────────────────────────────────┘
```

**Layout notes:** Greeting + date/branch always visible during loading. All KPI cards, alert rows, corporate/agent cards, and meeting rows render as skeleton blocks (#E1E4D5, matching card dimensions). shimmer_duration: short4 (200ms). Reduced-motion device: static grey placeholder with no animation.

---

## Screen: content

```
┌─────────────────────────────────────────┐
│                              ⚙    👤    │  ← absolute: settings right:56, profile right:16
│  Good morning, Priya 👋                 │  ← headline_medium (28sp/600w), #4C662B · pt:20 ph:16
│  Monday, 25 May 2026 · Mifos Nairobi   │  ← body_medium (14sp/400), #44483D · pt:4 pb:16
│                                         │
│  ┌──────────────────┐ ┌──────────────┐  │  ← stats_grid 2-col 12dp gap ph:16 pb:16
│  │║ 124             │ │║ 5           │  │  ← ║ = 4dp left border
│  │  Active          │ │  Pending     │  │    Left border: #4C662B · #E8A317
│  │  Customers       │ │  Applications│  │    Fill: #CDEDA3 · 12dp radius · 16dp pad
│  │  display_small   │ │  #44483D*    │  │    * a11y fix: was #E8A317 (1.68:1 fail → #44483D 7.26:1)
│  └──────────────────┘ └──────────────┘  │
│  ┌──────────────────┐ ┌──────────────┐  │
│  │║ 3               │ │║ 2           │  │    Left border: #BA1A1A · #386663
│  │  KYC             │ │  Meetings    │  │    Fill: #CDEDA3 · #DCE7C8
│  │  Pending         │ │  Today       │  │    Values: #BA1A1A · #386663
│  └──────────────────┘ └──────────────┘  │
│                                         │
│  Action Needed                          │  ← title_large (22sp/400), #1A1C16, w700, heading-2
│                                         │
│  ┌─────────────────────────────────┐    │  ← alert_kyc_expiry_john: #CDEDA3, 12dp r, 4dp border #E8A317
│  │║ John Mwangi — KYC expires      │    │    role=alert · row align_items=center · ph:16 mb:8
│  │  in 3 days        [Review KYC] │    │    button: outlined #44483D (a11y), label_small
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← alert_application_pending_sarah: border #BA1A1A
│  │║ Sarah Odhiambo — Application   │    │
│  │  pending 7 days [View Application]│  │    button: outlined #BA1A1A, label_small
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← alert_new_lead_peter: border #4C662B, mb:16
│  │║ New lead: Peter Kamau —        │    │
│  │  Retail account request          │    │    button: outlined #4C662B, label_small
│  │                [Start Onboarding]│    │
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← action_corporate_onboard: #CDEDA3, 12dp r, 16dp pad
│  │ Acme Trading Ltd —             │    │    children stacked vertically
│  │ New business account inquiry   │    │
│  │         [Start Corporate Onboarding] │  ← text btn, #386663, label_medium
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← action_register_as_agent: #CDEDA3, 12dp r, row
│  │ Complete Agent Registration     │    │    children: title (flex:1) + Register button
│  │                        [Register]│   │    text btn, #386663, label_medium
│  └─────────────────────────────────┘    │
│                                         │
│  Today's Schedule                       │  ← title_medium (16sp/500), #1A1C16, w600, heading-2 · ph:16 pb:8
│                                         │
│  ┌─────────────────────────────────┐    │  ← meeting_row_1: #FFFFFF, 10dp radius, elev:1
│  │ 10:00 AM  │  Mary Wanjiku       │    │    time: 72dp fixed, label_large (14sp/600) #4C662B
│  │           │  Loan Review        │    │    details: body_medium #1A1C16, flex:1
│  └─────────────────────────────────┘    │
│  ┌─────────────────────────────────┐    │  ← meeting_row_2: #FFFFFF, 10dp radius, elev:1 · mb:24
│  │  2:30 PM  │  James Otieno       │    │
│  │           │  New Account Discussion│  │
│  └─────────────────────────────────┘    │
│                                         │
├─────────────────────────────────────────┤
│  [Home*] [Customers] [Apps] [Messages] [More] │  ← M3 bottom nav, Home active (#DCE7C8 pill indicator)
└─────────────────────────────────────────┘
```

**Layout notes:**
- **KPI grid**: 2-column, 12dp gap, 16dp horizontal pad. Cards: #CDEDA3 fill (Active Customers, Pending Apps, KYC Pending) and #DCE7C8 (Meetings Today). 12dp radius, 16dp pad, 4dp left border.
- **KPI border accents**: Active Customers = #4C662B · Pending Apps = #E8A317 · KYC Pending = #BA1A1A · Meetings Today = #386663.
- **KPI values**: display_small (32sp/600). Colours: 124 = #4C662B · 5 = #44483D (a11y override — original #E8A317 failed 1.68:1 contrast on #CDEDA3) · 3 = #BA1A1A · 2 = #386663.
- **Alert rows**: #CDEDA3 fill, 12dp radius, 4dp coloured left border, row align_items=center, 14dp pad, 16dp h-margin. Action buttons outlined, 8dp radius, label_small: KYC = #44483D border/text (a11y-safe on #CDEDA3) · Application = #BA1A1A · Lead = #4C662B.
- **Corporate card**: children stacked — title body_medium + "Start Corporate Onboarding" text btn (#386663, label_medium).
- **Agent card**: row — title flex:1 + "Register" text btn (#386663, label_medium).
- **Meeting rows**: #FFFFFF fill, 10dp radius, 1dp elevation. Time column: 72dp fixed width, label_large (14sp/500) #4C662B w600. Detail: body_medium (14sp/400) #1A1C16 flex:1.

---

## Screen: error

```
┌─────────────────────────────────────────┐
│                              ⚙    👤    │
│  Good morning, Priya 👋                 │  ← always visible
│  Monday, 25 May 2026 · Mifos Nairobi   │  ← always visible
│                                         │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │  ⚠  Unable to load             │    │  ← error banner, error_outline icon
│  │     dashboard data.             │    │
│  │     Check your connection       │    │
│  │     and try again.              │    │
│  │                                 │    │
│  │        [ Try Again ]            │    │  ← outlined, #4C662B, pill radius
│  └─────────────────────────────────┘    │  ← id=error_retry_button, action=retry_load
│                                         │
├─────────────────────────────────────────┤
│  [Home] [Customers] [Apps] [Messages] [More] │
└─────────────────────────────────────────┘
```

**Layout notes:** Stats grid, "Action Needed" section, and "Today's Schedule" section are hidden (hide_components per states.error definition). Error banner centred. "Try Again" button: outlined, #4C662B border+text, pill radius, min 48dp touch target.

---

## Screen: empty

```
┌─────────────────────────────────────────┐
│                              ⚙    👤    │
│  Good morning, Priya 👋                 │  ← always visible
│  Monday, 25 May 2026 · Mifos Nairobi   │  ← always visible
│                                         │
│                                         │
│       ┌─ dashboard_customize ─┐         │  ← icon 48dp (icon-2xl token), #44483D
│       └───────────────────────┘         │
│                                         │
│  No dashboard data available yet.      │  ← title_medium (16sp/500), center, #1A1C16
│  Start by onboarding a customer.       │  ← body_medium (14sp/400), center, #44483D
│                                         │
│    ┌────────────────────────────────┐   │
│    │     Onboard a Customer         │   │  ← filled, #4C662B, pill radius · action=navigate target=customer-search
│    └────────────────────────────────┘   │
│                                         │
├─────────────────────────────────────────┤
│  [Home] [Customers] [Apps] [Messages] [More] │
└─────────────────────────────────────────┘
```

**Layout notes:** Stats grid, Action Needed, and Schedule sections hidden. Empty icon dashboard_customize centred. CTA navigates to customer-search. Empty state uses `empty_icon`, `empty_message`, `empty_action_label`, `empty_action_target` from states.empty definition.

---

## Design Checklist (Figma / Stitch)

- [ ] Greeting "Good morning, Priya 👋" — headline_medium (Outfit 28sp/400), #4C662B; pt:20 ph:16 w600
- [ ] Date/branch "Monday, 25 May 2026 · Mifos Nairobi Branch" — body_medium (14sp/400), #44483D; pt:4 pb:16
- [ ] Profile icon account_circle 32dp #4C662B absolute top:20 right:16; settings icon 24dp #44483D absolute top:24 right:56
- [ ] 2-column KPI grid: 12dp gap, 16dp horizontal padding, 16dp bottom padding
- [ ] KPI cards: #CDEDA3 fill (Active Customers, Pending Apps, KYC Pending); #DCE7C8 fill (Meetings Today); 12dp radius; 16dp padding; 4dp left border
- [ ] KPI left border colours: #4C662B (customers) · #E8A317 (pending apps) · #BA1A1A (KYC) · #386663 (meetings)
- [ ] KPI values display_small (32sp/600): 124 = #4C662B · 5 = #44483D (a11y override — NOT #E8A317) · 3 = #BA1A1A · 2 = #386663
- [ ] "Action Needed" header: title_large (Outfit 22sp/400) #1A1C16 w700; heading-2; ph:16 pt:8 pb:8
- [ ] KYC expiry alert: #CDEDA3 fill, 12dp radius, 4dp border #E8A317, row, 14dp pad. Text: "John Mwangi — KYC expires in 3 days" body_medium #1A1C16. Button: "Review KYC" outlined #44483D (7.26:1), label_small, 8dp radius
- [ ] Application alert: 4dp border #BA1A1A. Text: "Sarah Odhiambo — Application pending 7 days". Button: "View Application" outlined #BA1A1A, label_small
- [ ] Lead alert: 4dp border #4C662B, mb:16. Text: "New lead: Peter Kamau — Retail account request". Button: "Start Onboarding" outlined #4C662B, label_small
- [ ] Corporate card: #CDEDA3, 12dp r, 16dp pad. Title: "Acme Trading Ltd — New business account inquiry" body_medium #1A1C16. Btn: "Start Corporate Onboarding" text #386663 label_medium
- [ ] Agent card: #CDEDA3, 12dp r, 16dp pad, row. Title: "Complete Agent Registration" flex:1. Btn: "Register" text #386663 label_medium
- [ ] "Today's Schedule" header: title_medium (Outfit 16sp/500) #1A1C16 w600; ph:16 pb:8
- [ ] Meeting rows: #FFFFFF fill, 10dp radius, 1dp elevation; row align_items=center; 14dp pad; ph:16
- [ ] Meeting time: label_large (14sp/500) #4C662B w600, 72dp fixed width. Details: body_medium (14sp/400) #1A1C16 flex:1
- [ ] Meeting 1: "10:00 AM" | "Mary Wanjiku · Loan Review"
- [ ] Meeting 2: "2:30 PM" | "James Otieno · New Account Discussion"; mb:24
- [ ] Bottom nav M3: 80dp height, #F9FAEF background, #C5C8BA border-top, #DCE7C8 active-indicator pill
- [ ] Loading: skeleton #E1E4D5 on all KPI + alert + meeting sections; shimmer short4 (200ms); greeting+date always visible
- [ ] Error: banner with "Unable to load dashboard data. Check your connection and try again." + "Try Again" button
- [ ] Empty: dashboard_customize icon 48dp + "No dashboard data available yet." + "Onboard a Customer" filled btn
- [ ] All text: Outfit typeface only. Touch targets ≥ 48dp. 16dp horizontal content padding throughout.

---

_Generated by /idea export | 2026-05-30_
