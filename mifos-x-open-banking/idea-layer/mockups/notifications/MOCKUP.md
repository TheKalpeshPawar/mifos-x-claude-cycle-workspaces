# Visual Specification — Notifications

| Field | Value |
|---|---|
| Feature | notifications |
| Flavor | consumer |
| Archetype | index_list |

---

## Screen Layout

Top app bar: "Notifications" title, back arrow, done_all "Mark all as read" icon, tune "Notification settings" icon. No bottom navigation. Scrollable single-column content (background #FCF8FF):

1. **Header row** — "Notifications" title (headline_large #1800B1) + "Mark All Read" text button (#008B8B teal), space-between, padding horizontal 20, top 16
2. **Payment received card** — Unread, #F0EDFF background, #D4C8FF border (radius 16, margin horizontal 20, bottom 8)
3. **Direct debit reminder card** — Read, white background, #F0F0F0 border (radius 16, margin horizontal 20, bottom 8)
4. **Budget alert card** — Read, white background, #F0F0F0 border (radius 16, margin horizontal 20, bottom 8)
5. **Bottom spacer** — 24dp

---

## Components

### Header Row
- **Layout:** Horizontal, space-between, center-aligned, padding horizontal 20, top 16, bottom 8
- **Title:** "Notifications" headline_large, #1800B1, bold
- **"Mark All Read" button:** Text variant, #008B8B, label_medium, no padding horizontal

### Payment Received Notification Card (Unread)
- **Container:** Background #F0EDFF (purple-tinted unread), border #D4C8FF 1dp, corner_radius 16, padding 16, margin horizontal 20, bottom 8
- **Internal layout (horizontal row, spacing 12, align flex_start):**
  - **Icon circle:** 44x44, background #4CAF50 (green), radius 22, centered; arrow_downward icon 22dp white
  - **Text column (flex 1):**
    - "Payment received" — body_medium, #111111, semi-bold
    - "Your salary of £3,200.00 from Acme Ltd has been credited to your account." — body_small, #444444, top 2, bottom 4
    - "2 min ago" — label_small, #888888
  - **Unread dot:** 10x10 circle, #1800B1, align_self flex_start, margin_top 4
- **Visual cue:** The purple-tinted background is the primary unread indicator at the card level

### Direct Debit Reminder Card (Read)
- **Container:** Background #FFFFFF, border #F0F0F0 1dp, corner_radius 16, padding 16
- **Internal layout:**
  - **Icon circle:** 44x44, background #008B8B (teal), radius 22; schedule icon 22dp white
  - **Text column:**
    - "Direct debit reminder" — body_medium, **#555555** (dimmed vs unread), semi-bold
    - "Your Council Tax direct debit of £148.00 will be collected on 1 June 2026." — body_small, #777777
    - "3 hr ago" — label_small, #AAAAAA
  - No unread dot

### Budget Alert Card (Read)
- **Container:** Same style as direct debit card
- **Internal layout:**
  - **Icon circle:** 44x44, background #FF9800 (orange/amber), radius 22; warning_amber_outlined icon 22dp white
  - **Text column:**
    - "Budget alert" — body_medium, #555555, semi-bold
    - "Your Dining Out budget is 97% used. Only £5.00 remaining this month." — body_small, #777777
    - "Yesterday" — label_small, #AAAAAA
  - No unread dot

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| notification_payment_received | Tap | open_notification → navigates to transactions screen |
| notification_direct_debit | Tap | open_notification → navigates to direct-debits screen |
| notification_budget_alert | Tap | open_notification → navigates to pfm-dashboard screen |
| mark_all_read_button | Tap | mark_all_read action — all unread dots removed; card backgrounds normalise to white |
| top app bar done_all icon | Tap | mark_all_read action — same as inline button |
| top app bar tune icon | Tap | open_notification_settings action — notification preferences screen |
| top app bar back arrow | Tap | navigate_back to home |

---

## Content Data

| Notification | Icon Color | Title | Message | Time | Read State |
|---|---|---|---|---|---|
| Payment received | #4CAF50 green | "Payment received" | "Your salary of £3,200.00 from Acme Ltd has been credited to your account." | 2 min ago | Unread |
| Direct debit reminder | #008B8B teal | "Direct debit reminder" | "Your Council Tax direct debit of £148.00 will be collected on 1 June 2026." | 3 hr ago | Read |
| Budget alert | #FF9800 orange | "Budget alert" | "Your Dining Out budget is 97% used. Only £5.00 remaining this month." | Yesterday | Read |

---

## Design Notes

**Unread vs Read Visual System:**
- Unread cards: #F0EDFF background + #D4C8FF border + #1800B1 unread dot + #111111 text — three simultaneous signals ensure no ambiguity for colour-blind users
- Read cards: #FFFFFF background + #F0F0F0 border + no dot + #555555 text — lower visual weight to indicate consumed state
- This dual-signal approach (background AND dot AND text colour) ensures accessibility even when one channel is not perceived

**Icon Circle Colour Semantics:**
- Green (#4CAF50): money in — salary, credits, received funds — positive financial event
- Teal (#008B8B): upcoming action needed — direct debits, reminders, things to watch
- Orange (#FF9800): warning — budget alerts, approaching limits — same colour as the PFM budget warning bar

**Typography:**
- Unread notification title: body_medium semi-bold **#111111** — maximum contrast
- Read notification title: body_medium semi-bold **#555555** — same weight but lower contrast signals "already seen"
- All timestamps: label_small — smallest readable text size, positioned bottom to not compete with message

**"Mark All Read" button:**
- Uses teal #008B8B rather than primary #1800B1 — distinct from destructive actions and from the primary CTA, appropriate for a helpful utility action

**Accessibility:**
- Each notification card has a comprehensive a11y label including read state, title, message, and age
- Unread dot has role="status" with content_description "Unread notification"
- Card tap targets are full-width for easy thumb reach

*Generated by /idea export | 2026-05-25*
