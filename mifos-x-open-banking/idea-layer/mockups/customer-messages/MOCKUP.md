# Mockup Specification: Customer Messages

| Field | Value |
|---|---|
| Feature | customer-messages |
| Flavor | fieldOfficer |
| Archetype | index_list |

---

## Screen Layout

```
[ Status Bar ]
[ "Messages"      [5 unread] ]         ← headline_large #1800B1 w700 + red pill badge
  ph:16 pt:20 pb:8                       badge: bg:#FF5252 br:12, "5 unread" label_medium white
[ Search messages... ] ← filled pill, bg:#F0F0F0 br:28, prefix 🔍, mh:16 mb:12
──────────────────────────────────────────────────
  === THREAD LIST (content state) ===

┌─ UNREAD THREAD ─────────────────────────────────┐  bg:#EEF0FF, border:#C5CAF5, br:12
│ [JM]  John Mwangi               2 min ago ●1800B1│  avatar bg:#1800B1 44px
│  ●    "Please send me the account..."  ● [dot]  │  unread dot: 10px circle #1800B1
└──────────────────────────────────────────────────┘  elevation:1, mh:16 mb:8
┌─ READ THREAD ───────────────────────────────────┐  bg:#FFFFFF, border:#E0E0E0, br:12
│ [SO]  Sarah Odhiambo            1 hr ago #999   │  avatar bg:#008B8B 44px
│       "Thank you for approving my application!" │
└──────────────────────────────────────────────────┘  elevation:1, mh:16 mb:8
┌─ READ THREAD ───────────────────────────────────┐  bg:#FFFFFF, border:#E0E0E0, br:12
│ [PK]  Peter Kamau               Yesterday #999  │  avatar bg:#607D8B 44px
│       "When can I expect my card to arrive?"    │
└──────────────────────────────────────────────────┘  elevation:1, mh:16 mb:8
──────────────────────────────────────────────────
[ FAB: [edit] New Message ] ← extended FAB, bg:#1800B1, white, bottom-right, mb:24 mr:16

  === COMPOSE BOTTOM SHEET (when FAB tapped) ===
┌─────────────────────────────────────────────────┐
│  ── (drag handle) ──                            │
│  New Message                   title_medium 700 │
│  ┌─ Customer ────────────────────────────────┐  │
│  │  Search customers...       autocomplete   │  │
│  └───────────────────────────────────────────┘  │
│  ┌─ Subject ─────────────────────────────────┐  │
│  │  Account query, Document request...       │  │
│  └───────────────────────────────────────────┘  │
│  ┌─ Message ─────────────────────────────────┐  │
│  │  Type your message to the customer...     │  │
│  │  (minLines:4, maxLines:8 textarea)        │  │
│  └───────────────────────────────────────────┘  │
│  [ Send Message ] ← filled #1800B1 full-width   │
└─────────────────────────────────────────────────┘
  bg:#FFFFFF, br:20, p:20
```

---

## Components

### Title Row
- **"Messages" text:** headline_large (32sp), color #1800B1, weight 700
- **Unread badge:** Positioned end of row — background #FF5252, border_radius:12, padding 10px/4px; text "5 unread" label_medium white weight 700; role: status

### Search Bar
- **Style:** Filled variant, border_radius:28 (pill), bg:#F0F0F0, padding_horizontal:16, prefix search icon
- **Behavior:** Filters `filteredThreads` from the ViewModel; does not make new API calls

### Thread Cards

**Unread thread (John Mwangi):**
- Background: #EEF0FF (blue tint), border: #C5CAF5 1px, border_radius:12, elevation:1
- Avatar: 44px circle, bg:#1800B1, initials "JM" label_large white weight 700
- Name: title_small #1A1A1A weight 700
- Time: body_small #1800B1 weight 600 (colored for unread emphasis)
- Preview: body_medium #333333, maxLines:1, ellipsis
- Unread dot: 10px circle bg:#1800B1, positioned end of preview row

**Read thread (Sarah Odhiambo):**
- Background: #FFFFFF, border: #E0E0E0 1px
- Avatar: 44px circle, bg:#008B8B, initials "SO"
- Name: title_small #1A1A1A weight 600
- Time: body_small #999999 (muted)
- Preview: body_medium #666666

**Read thread (Peter Kamau):**
- Same as Sarah; avatar bg:#607D8B, initials "PK"

### Compose Bottom Sheet
- Modal bottom sheet, bg:#FFFFFF, border_radius top:20, padding:20
- Drag handle implied at top
- Customer field: autocomplete variant — search as you type from CustomerSearchService
- Subject field: standard text outlined input, placeholder "Account query, Document request..."
- Message textarea: outlined, minLines:4, maxLines:8, placeholder "Type your message to the customer..."
- Send button: filled #1800B1, full width

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Thread row (any) | Tap | Opens thread detail / conversation view |
| Search bar | Tap + type | Filters thread list by customer name or message content |
| New Message FAB | Tap | Opens compose bottom sheet (isComposeOpen = true) |
| Customer autocomplete | Tap + type | Searches via CustomerSearchService |
| Send Message button | Tap | Calls POST API; closes sheet on success; refreshes thread list |
| Swipe down on sheet | Gesture | Dismisses compose sheet (ComposeDismissed event) |

**Loading state:** Thread card placeholders show shimmer with avatar circle, name line, and preview line as rounded grey rectangles.

**Empty state:** Centered layout with `message` icon, "No Messages" in title_large, "Start a conversation by composing a new message to a customer" in body_medium #757575.

---

## Content Data

| Thread | Customer | Preview | Time | Status |
|---|---|---|---|---|
| thread_1 | John Mwangi (JM) | "Please send me the account statement for..." | 2 min ago | Unread |
| thread_2 | Sarah Odhiambo (SO) | "Thank you for approving my application!" | 1 hr ago | Read |
| thread_3 | Peter Kamau (PK) | "When can I expect my card to arrive?" | Yesterday | Read |

---

## Design Notes

**Unread distinction:** Unread threads use a perceptible blue-tinted background (#EEF0FF) and blue border (#C5CAF5) rather than just a dot, ensuring officers with color vision differences can detect unread status via multiple cues (background shift + dot).

**Thread avatar colors:** Each customer has a persistent avatar color (John = brand purple, Sarah = teal, Peter = blue-grey). These colors are derived from customer data at render time using a hash-to-color function, consistent across all screens.

**Time formatting:** Unread thread time rendered in #1800B1 (attention-grabbing); read thread time in #999999 (receded). Both use relative format: "2 min ago", "1 hr ago", "Yesterday".

**Extended FAB:** Uses extended form (icon + "New Message" label) rather than a mini icon-only FAB, because the compose action benefits from the explicit label on a screen where the icon alone may be ambiguous.

**Compose transport:** The `transport` field in the API must be `sms`, `email`, `ftp`, or `post`. The compose sheet should auto-select `sms` as the default transport for field officer use cases, with an optional selector for email.

**Accessibility:** Thread cards have role: button with a full-sentence contentDescription including the preview text and time (e.g. "Unread message from John Mwangi: Please send me the account statement for... 2 minutes ago"). Unread badge has role: status.

---
_Generated by /idea export | 2026-05-25_
