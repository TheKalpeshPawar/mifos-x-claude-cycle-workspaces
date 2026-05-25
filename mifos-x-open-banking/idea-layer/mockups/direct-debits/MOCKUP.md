# Direct Debits — Visual Specification

| Field | Value |
|---|---|
| Feature | direct-debits |
| Flavor | consumer |
| Archetype | index_list |
| Status | designed |

---

## Screen Layout

### State: populated

```
┌──────────────────────────────────────────┐
│ ←  Direct Debits                      ⋮  │  ← TopAppBar: arrow_back | more_vert
├──────────────────────────────────────────┤
│                                          │
│  Direct Debits          [3 active]       │  ← headline_large #1800B1 bold | #E8F5E9 chip #4CAF50
│                                          │
│ ┌────────────────────────────────────┐   │
│ │  Netflix                 [Active]  │   │  ← white card #FFFFFF, elevation 2, r=16dp
│ │  £15.99 / month    Next: 3 Jun 2026│   │  ← #1800B1 semibold | body_small #888888
│ │  Ref: DD-NF-20240301               │   │  ← label_small #AAAAAA
│ └────────────────────────────────────┘   │  ← margin 20dp h, 12dp bottom
│                                          │
│ ┌────────────────────────────────────┐   │
│ │  Spotify                 [Active]  │   │  ← white card #FFFFFF, elevation 2, r=16dp
│ │  £10.99 / month   Next: 12 Jun 2026│   │
│ │  Ref: DD-SP-20231115               │   │
│ └────────────────────────────────────┘   │
│                                          │
│ ┌────────────────────────────────────┐   │
│ │  PureGym             [Cancelled]   │   │  ← muted card #FAFAFA, no elevation, r=16dp
│ │  £29.99 / month                    │   │  ← #AAAAAA normal weight (no next date)
│ │  Ref: DD-GYM-20220601              │   │  ← label_small #CCCCCC
│ └────────────────────────────────────┘   │
│                                          │
│                    [+ Set Up Direct Debit]│  ← FAB bottom-right, #1800B1, r=16dp, elev 6
└──────────────────────────────────────────┘
```

---

### State: loading

```
┌──────────────────────────────────────────┐
│ ←  Direct Debits                      ⋮  │
├──────────────────────────────────────────┤
│                                          │
│  Direct Debits                           │  ← Title visible; no count chip yet
│                                          │
│ ┌────────────────────────────────────┐   │
│ │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │   │  ← Skeleton card 1, h=110dp, shimmer
│ └────────────────────────────────────┘   │
│ ┌────────────────────────────────────┐   │
│ │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │   │  ← Skeleton card 2, h=110dp, shimmer
│ └────────────────────────────────────┘   │
│ ┌────────────────────────────────────┐   │
│ │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │   │  ← Skeleton card 3, h=110dp, shimmer
│ └────────────────────────────────────┘   │
└──────────────────────────────────────────┘
```

---

### State: empty

```
┌──────────────────────────────────────────┐
│ ←  Direct Debits                      ⋮  │
├──────────────────────────────────────────┤
│                                          │
│  Direct Debits                           │
│                                          │
│                                          │
│                                          │
│              [account_balance_wallet]    │  ← icon, large, muted #9E9E9E
│                                          │
│          No direct debits set up         │  ← title_medium, #111111, centered
│                                          │
│  Authorise merchants like Netflix or     │  ← body_medium, #888888, centered
│  your utility providers to collect       │
│  payments automatically on agreed dates  │
│                                          │
│                                          │
│                    [+ Set Up Direct Debit]│  ← FAB always visible
└──────────────────────────────────────────┘
```

---

### State: cancel_confirm (dialog overlay)

```
┌──────────────────────────────────────────┐
│ ←  Direct Debits                      ⋮  │
├──────────────────────────────────────────┤  ← full list visible behind 50% dim overlay
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│  ← scrim alpha 0.5
│░░░░                                 ░░░░│
│░░░░  ┌──────────────────────────┐  ░░░░│
│░░░░  │   Cancel Direct Debit?   │  ░░░░│  ← dialog r=20dp, elev 8, #FFFFFF bg
│░░░░  │                          │  ░░░░│  ← headline_small #111111 bold
│░░░░  │  Netflix (DD-NF-20240301)│  ░░░░│
│░░░░  │  will stop collecting    │  ░░░░│  ← body_medium #555555
│░░░░  │  payments. This cannot   │  ░░░░│
│░░░░  │  be undone.              │  ░░░░│
│░░░░  │                          │  ░░░░│
│░░░░  │  [Yes, Cancel Mandate ]  │  ░░░░│  ← filled #D32F2F white text, full-width, r=12dp
│░░░░  │  [   Keep Mandate     ]  │  ░░░░│  ← outlined #1800B1 border+text, full-width, r=12dp
│░░░░  └──────────────────────────┘  ░░░░│
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│
└──────────────────────────────────────────┘
```

---

### State: error

```
┌──────────────────────────────────────────┐
│ ←  Direct Debits                      ⋮  │
├──────────────────────────────────────────┤
│                                          │
│  Direct Debits                           │
│                                          │
│                                          │
│                 [cloud_off]              │  ← icon, large, #9E9E9E
│                                          │
│       Unable to load direct debits       │  ← title_medium, #111111, centered
│                                          │
│   Check your connection and try again    │  ← body_medium, #888888, centered
│                                          │
│              [    Try Again    ]         │  ← outlined button, #1800B1
│                                          │
│                    [+ Set Up Direct Debit]│  ← FAB always visible
└──────────────────────────────────────────┘
```

---

## Component Detail

### Mandate Card — Active (Netflix, Spotify)

```
┌──────────────────────────────────────────┐
│  {MerchantName}              [Active]    │  ← title_medium #111111 semibold | badge #E8F5E9/#4CAF50
│                                          │  ← header row: space_between, align flex_start
│  £{amount} / month     Next: {date}      │  ← body_large #1800B1 semibold | body_small #888888
│                                          │  ← amount row: space_between, align center, pt=4dp
│  Ref: {mandateReference}                 │  ← label_small #AAAAAA
└──────────────────────────────────────────┘
  Background: #FFFFFF | corner_radius: 16dp | elevation: 2
  Border: #F0F0F0 1dp | margin: 20dp h, 12dp bottom | padding: 16dp
  on_click: view_direct_debit → direct-debit-detail
```

### Mandate Card — Cancelled (PureGym)

```
┌──────────────────────────────────────────┐
│  {MerchantName}          [Cancelled]     │  ← title_medium #888888 semibold | badge #F5F5F5/#9E9E9E
│                                          │
│  £{amount} / month                       │  ← body_large #AAAAAA normal (no next date row)
│                                          │
│  Ref: {mandateReference}                 │  ← label_small #CCCCCC
└──────────────────────────────────────────┘
  Background: #FAFAFA | corner_radius: 16dp | elevation: 0
  Border: #E0E0E0 1dp | margin: 20dp h, 12dp bottom | padding: 16dp
  on_click: view_direct_debit → direct-debit-detail
```

### Active Count Chip

```
 [3 active]
  Background: #E8F5E9 | corner_radius: 12dp
  Padding: 10dp h, 4dp v
  Typography: label_medium | Color: #4CAF50 | font_weight: semibold
  Updates when a mandate is cancelled (3 → 2)
```

### Cancel Confirmation Dialog

```
┌──────────────────────────────────────────┐
│        Cancel Direct Debit?              │  ← headline_small #111111 bold
│                                          │
│  {merchantName} ({mandateRef}) will      │  ← body_medium #555555
│  stop collecting payments. This          │
│  cannot be undone.                       │
│                                          │
│  ┌──────────────────────────────────┐    │  ← filled #D32F2F, white text, r=12dp
│  │       Yes, Cancel Mandate        │    │
│  └──────────────────────────────────┘    │
│                                          │
│  ┌──────────────────────────────────┐    │  ← outlined #1800B1 border/text, r=12dp
│  │          Keep Mandate            │    │
│  └──────────────────────────────────┘    │
└──────────────────────────────────────────┘
  corner_radius: 20dp | background: #FFFFFF | elevation: 8
  padding: 24dp h+v | Overlay scrim: alpha 0.5
```

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap Netflix card | direct_debit_netflix | view_direct_debit → direct-debit-detail sheet |
| Tap Spotify card | direct_debit_spotify | view_direct_debit → direct-debit-detail sheet |
| Tap PureGym card | direct_debit_gym | view_direct_debit → direct-debit-detail sheet (read-only) |
| Tap "Yes, Cancel Mandate" | cancel_confirm_cta | confirm_cancel_direct_debit → DELETE API → reload list |
| Tap "Keep Mandate" | cancel_dismiss_cta | dismiss_cancel_dialog → close dialog, no side effects |
| Tap FAB | setup_direct_debit_fab | setup_direct_debit → new mandate setup sheet |
| Tap back arrow | top bar navigation_icon | navigate_back → accounts screen |
| Tap overflow (⋮) | more_vert | open_direct_debit_options → options menu |
| Pull to refresh | scroll area | RefreshTriggered event → reload mandate list |
| Tap retry (error) | retry_button | RetryLoad event → loading state → API call |

---

## Design Notes

**Mandate reference on every card:** `mandate_reference` (e.g., "DD-NF-20240301") is surfaced in `label_small` muted text on every card — active and cancelled. This supports user support queries and is injected into the cancel confirm dialog body for explicit confirmation.

**Cancelled card visual language:** PureGym card uses a differentiated visual treatment: `#FAFAFA` background (vs `#FFFFFF` active), zero elevation, `#E0E0E0` border (vs `#F0F0F0`), greyed merchant name (`#888888`), muted amount (`#AAAAAA`), and ghost mandate ref (`#CCCCCC`). No next-date row — irrelevant for cancelled mandates.

**Active count chip accuracy:** The "3 active" chip reflects active Netflix + Spotify only — PureGym is cancelled and excluded from the active count. If the user cancels Netflix, the chip should update to "2 active" without a screen reload (optimistic update from ViewModel).

**Destructive action guard:** The cancel flow is a two-step interaction: (1) user must explicitly choose to cancel from the detail view, (2) the `cancel_confirm` dialog then requires a second explicit confirmation with the red "Yes, Cancel Mandate" CTA. This friction is intentional — direct debit cancellation cannot be undone within the app.

**No quick-delete row icons:** Direct debits differ from standing orders (which are user-controlled). Cancellation requires navigating to detail first. No swipe-to-delete or row-level delete icons — this asymmetry is by design.

**FAB always visible:** The "Set Up Direct Debit" FAB is visible in all states (populated, empty, error). Even when viewing cancelled mandates, users should always have a path to set up new mandates. The FAB is hidden only during the loading skeleton state.

**Cancelled mandates in list:** OBP returns both active and cancelled mandates. Cancelled mandates are shown at the bottom of the list in a muted style — they provide audit trail for the user (they can see what was cancelled and when).

*Generated by /idea export | 2026-05-25*
