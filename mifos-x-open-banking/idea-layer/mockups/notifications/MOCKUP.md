# Visual Specification — Notifications

| Field | Value |
|---|---|
| Feature | notifications |
| Flavor | consumer |
| Archetype | index_list |
| States | loading, populated, empty, error |

---

## Screen Layout (Populated State)

Top app bar: "Notifications" title, arrow_back navigation icon, done_all action ("Mark all as read"), tune action ("Notification settings"). No bottom navigation bar. Scrollable single-column list on background #FCF8FF (soft off-white).

```
┌─────────────────────────────────────────────┐
│  ← Notifications                  ✓✓  ⚙    │  ← Top app bar
├─────────────────────────────────────────────┤
│                                             │
│  Notifications                Mark All Read │  ← Header row
│                                             │
│  TODAY                                      │  ← Section header
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ ●  [↓]  Payment received           ● ● │ │  ← Unread card
│ │         Payment of £50.00 received      │ │     (purple bg)
│ │         from James Wilson               │ │
│ │         10 min ago                      │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ ●  [✓]  KYC verification approved  ● ● │ │  ← Unread card
│ │         Your identity has been verified. │ │     (purple bg)
│ │         You now have full access.        │ │
│ │         1 hr ago                         │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│  EARLIER                                    │  ← Section header
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │    [↻]  Direct debit mandate created    │ │  ← Read card
│ │         Direct debit mandate created for│ │     (white bg)
│ │         Netflix — £15.99/month from     │ │
│ │         your Current Account. 3 hr ago  │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │    [↓]  Salary credited                 │ │  ← Read card
│ │         £3,200.00 from Acme Ltd has     │ │     (white bg)
│ │         been credited to your Current   │ │
│ │         Account. Yesterday              │ │
│ └─────────────────────────────────────────┘ │
│                                             │  ← 24dp bottom spacer
└─────────────────────────────────────────────┘
```

Legend: `● ●` = unread dot (10x10, #1800B1) | `[↓]` = payment icon (green circle) | `[✓]` = verified_user icon (blue circle) | `[↻]` = autorenew icon (teal circle)

---

## Components

### Header Row
- **Layout:** Horizontal, space-between, center-aligned
- **Padding:** horizontal 20dp, top 16dp, bottom 8dp
- **Title:** "Notifications" — headline_large, #1800B1, bold
- **Button:** "Mark All Read" — text variant, #008B8B teal, label_medium, no horizontal padding

### Section Headers

**Today**
- typography: label_medium, #888888, semi-bold
- padding: horizontal 20dp, top 8dp, bottom 4dp

**Earlier**
- typography: label_medium, #888888, semi-bold
- padding: horizontal 20dp, top 12dp, bottom 4dp

---

### Notification Card — Payment of £50.00 from James Wilson (Unread, payment)

**Container**
- Background: #F0EDFF (soft purple — unread signal)
- Border: #D4C8FF, 1dp
- Corner radius: 16dp
- Padding: horizontal 16dp, vertical 14dp
- Margin: horizontal 20dp, bottom 8dp
- Tap action: open_notification → transaction-detail

**Internal row (horizontal, spacing 12dp, align: flex_start)**

Icon circle
- Size: 44x44dp, radius 22dp
- Background: #4CAF50 (green — incoming money)
- Icon: arrow_downward, 22dp, #FFFFFF

Text column (flex: 1)
- Title: "Payment received" — body_medium, #111111, semi-bold (maximum contrast = unread)
- Body: "Payment of £50.00 received from James Wilson" — body_small, #444444, top 2dp, bottom 4dp
- Timestamp: "10 min ago" — label_small, #888888

Unread dot
- Size: 10x10dp, radius 5dp
- Color: #1800B1 (primary)
- Align: flex_start, margin_top 4dp
- Accessibility role: status, content_description: "Unread notification"

---

### Notification Card — KYC Verification Approved (Unread, security)

**Container**
- Background: #F0EDFF, border #D4C8FF — same unread style
- Tap action: open_notification → kyc-review (cross-persona deep link)

**Internal row**

Icon circle
- Background: #1800B1 (primary blue — identity/trust)
- Icon: verified_user, 22dp, #FFFFFF

Text column
- Title: "KYC verification approved" — body_medium, #111111, semi-bold
- Body: "Your identity has been verified. You now have full access to all account features." — body_small, #444444
- Timestamp: "1 hr ago" — label_small, #888888

Unread dot: same as above

---

### Notification Card — Netflix Direct Debit Mandate (Read, system)

**Container**
- Background: #FFFFFF (white — read signal)
- Border: #F0F0F0, 1dp
- Corner radius: 16dp
- Padding: horizontal 16dp, vertical 14dp
- Margin: horizontal 20dp, bottom 8dp
- Tap action: open_notification → accounts

**Internal row**

Icon circle
- Background: #008B8B (teal — recurring/scheduled action)
- Icon: autorenew, 22dp, #FFFFFF

Text column
- Title: "Direct debit mandate created" — body_medium, #555555, semi-bold (reduced contrast = read)
- Body: "Direct debit mandate created for Netflix — £15.99/month from your Current Account." — body_small, #777777
- Timestamp: "3 hr ago" — label_small, #AAAAAA
- No unread dot

---

### Notification Card — Acme Ltd Salary Credited (Read, payment)

**Container**
- Same read card style as Netflix card
- Tap action: open_notification → transaction-detail

**Internal row**

Icon circle
- Background: #4CAF50 (green — incoming money)
- Icon: arrow_downward, 22dp, #FFFFFF

Text column
- Title: "Salary credited" — body_medium, #555555, semi-bold
- Body: "£3,200.00 from Acme Ltd has been credited to your Current Account." — body_small, #777777
- Timestamp: "Yesterday" — label_small, #AAAAAA
- No unread dot

---

## State Variants

### Loading State

Top app bar visible. Header row (title only, no "Mark All Read" button). Four shimmer skeleton cards stacked vertically, each with:
- Gray rectangle (44x44dp) for icon circle
- Two gray rounded rectangles for title + body lines
- One short gray line for timestamp

### Empty State

Top app bar visible. Header row (title only). Centered column:
- Icon: notifications_none_outlined, 64dp, #AAAAAA
- Title: "You're all caught up" — headline_small, #333333
- Message: "No new notifications. We'll let you know about payments, alerts and updates." — body_medium, #777777, centered, max_width 280dp

### Error State

Top app bar visible. Header row (title only). Centered column:
- Icon: cloud_off, 64dp, #AAAAAA
- Title: "Unable to load notifications" — headline_small, #333333
- Message: "Check your connection and try again" — body_medium, #777777
- Retry button: "Try again" — outlined, #1800B1, margin_top 16dp, tap → RetryLoad

---

## Interaction Patterns

| Target | Gesture | Action | Navigation |
|---|---|---|---|
| notification_payment_james | Tap | open_notification | → transaction-detail |
| notification_kyc_approved | Tap | open_notification | → kyc-review (cross-persona) |
| notification_netflix_mandate | Tap | open_notification | → accounts |
| notification_salary_credited | Tap | open_notification | → transaction-detail |
| mark_all_read_button | Tap | mark_all_read | All unread dots removed; card backgrounds → white |
| Top app bar done_all | Tap | mark_all_read | Same as button |
| Top app bar tune | Tap | open_notification_settings | → settings |
| Top app bar back arrow | Tap | navigate_back | → home |

---

## Content Data

| # | Category | Icon | Icon Colour | Title | Body | Time | State |
|---|---|---|---|---|---|---|---|
| 1 | payment | arrow_downward | #4CAF50 green | "Payment received" | "Payment of £50.00 received from James Wilson" | 10 min ago | Unread |
| 2 | security | verified_user | #1800B1 blue | "KYC verification approved" | "Your identity has been verified. You now have full access to all account features." | 1 hr ago | Unread |
| 3 | system | autorenew | #008B8B teal | "Direct debit mandate created" | "Direct debit mandate created for Netflix — £15.99/month from your Current Account." | 3 hr ago | Read |
| 4 | payment | arrow_downward | #4CAF50 green | "Salary credited" | "£3,200.00 from Acme Ltd has been credited to your Current Account." | Yesterday | Read |

---

## Design Notes

**Unread vs Read Visual System — triple signal for accessibility:**
- Unread: #F0EDFF background + #D4C8FF border + #1800B1 unread dot + #111111 text
- Read: #FFFFFF background + #F0F0F0 border + no dot + #555555 text
- Three simultaneous signals ensure the read/unread distinction is perceived even when one channel (colour alone) is unavailable

**Section grouping rationale:**
- "Today" = notifications received since midnight — drives urgency; user expects to act on these
- "Earlier" = older read notifications — reference only; lower visual weight confirms no action needed

**Category icon colour semantics:**
- Green (#4CAF50): money in — payment received, salary credited — positive financial event
- Primary blue (#1800B1): trust/identity — KYC, security events — importance signal
- Teal (#008B8B): scheduled/system — direct debit mandates, recurring actions — informational

**Typography hierarchy:**
- Unread title: body_medium semi-bold #111111 — maximum contrast, priority reading
- Read title: body_medium semi-bold #555555 — same weight, lower contrast = consumed state
- All body text: body_small — compact to show full notification message without truncation
- All timestamps: label_small at right-aligned bottom — minimal visual weight

**"Mark All Read" placement:**
- Inline text button (teal, not primary) to signal utility rather than primary CTA
- Mirrored in top app bar done_all icon for thumb-reach accessibility on large screens

**Accessibility:**
- Each card has a comprehensive a11y content_description including read state, title, message, and relative age
- Unread dot: role="status" with "Unread notification" description
- All card tap targets span full card width for thumb reach
- Minimum touch target: 48x48dp (card padding ensures this)

---

*Generated by /idea export | 2026-05-25*
