# MOCKUP — Exchange Rates

**Archetype:** dashboard
**Shell:** No top app bar. Accessed via Home services tile; no dedicated bottom-nav tab. Screen-level title used.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: Material Design 3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← headline_large (32sp), #4C662B, 24dp top pad
│  ██████████████████████████         │  ← skeleton: last_updated_text (single-line shimmer)
│                                     │
│  ┌───────────────────────────────┐  │  ← skeleton: converter_card (#E1E4D5, 16dp radius)
│  │  ████████████████████████████ │  │    shimmer: send_amount_input
│  │                               │  │
│  │  ████████████████████████     │  │    shimmer: from_currency_select
│  │                               │  │
│  │           ⊕                   │  │    shimmer: swap_currencies_icon
│  │                               │  │
│  │  ████████████████████████     │  │    shimmer: to_currency_select
│  │                               │  │
│  │  ███████████████████████████  │  │    shimmer: converted_result_display (large)
│  │  ██████████████████████       │  │    shimmer: rate_info_text
│  │                               │  │
│  │  ██████████████████████████   │  │    shimmer: send_money_cta
│  └───────────────────────────────┘  │
│                                     │
│  ████████████████                   │  ← skeleton: popular_pairs_header
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │  ← skeleton rate rows ×6 (shimmer, 8dp radius)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████    ██████    ████   │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Only fx_rates_title is visible (non-skeleton) during loading. All other components shimmer. Shimmer duration: short4 = 200ms (easing: standard); reduced-motion fallback: static placeholder blocks. Skeleton colour: #E1E4D5 (surface_variant).

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← headline_large (32sp/400), #4C662B
│  Rates updated: 14 May 2026, 15:42  │  ← body_small (12sp), #44483D; UTC suffix
│  UTC                                │
│                                     │
│  ┌───────────────────────────────┐  │  ← converter_card: #FFFFFF, 16dp radius, elev 4
│  │                               │  │    20dp padding, 16dp h-margin
│  │  I want to send               │  │  ← send_amount_input label
│  │  ┌─────────────────────────┐  │  │
│  │  │  1,000                  │  │  │  ← title_large (22sp/700), #4C662B, #F9FAEF bg
│  │  └─────────────────────────┘  │  │    8dp radius, decimal keyboard
│  │                               │  │
│  │  From                         │  │  ← from_currency_select label
│  │  ┌─────────────────────────┐  │  │
│  │  │  GBP              ▼    │  │  │  ← select input, #F9FAEF bg, 8dp radius
│  │  └─────────────────────────┘  │  │
│  │                               │  │
│  │         ╔═══╗                 │  │  ← swap_currencies_icon: swap_vert 32dp, #4C662B
│  │         ║ ⇅ ║                 │  │    on #CDEDA3 circle (16dp radius, 8dp pad)
│  │         ╚═══╝                 │  │    align_self: center
│  │                               │  │
│  │  To                           │  │  ← to_currency_select label
│  │  ┌─────────────────────────┐  │  │
│  │  │  EUR              ▼    │  │  │  ← select input, #F9FAEF bg, 8dp radius
│  │  └─────────────────────────┘  │  │
│  │                               │  │
│  │      = 1,167.20 EUR           │  │  ← display_medium (45sp/700), #4C662B, centred
│  │   Rate: 1 GBP = 1.1672 EUR    │  │  ← body_small (12sp), #44483D, centred
│  │                               │  │
│  │  ┌─────────────────────────┐  │  │  ← send_money_cta: filled, #4C662B bg
│  │  │     Send this amount    │  │  │    #FFFFFF text, label_large (14sp/500)
│  │  └─────────────────────────┘  │  │    12dp radius, full-width, 14dp v-padding
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← section_divider: #E1E4D5, 16dp h-margin
│                                     │
│  Popular Pairs                      │  ← popular_pairs_header: title_medium (16sp/600), #1A1C16
│                                     │
│  ┌───────────────────────────────┐  │  ← rate_row_gbp_eur: #FFFFFF, 8dp radius
│  │  GBP / EUR    1.1672   ↑+0.2% │  │    body_large 500w · 600w · body_small 500w #4C662B
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← rate_row_gbp_usd
│  │  GBP / USD    1.2834  ↓-0.1%  │  │    body_small #BA1A1A + arrow_downward icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← rate_row_gbp_jpy
│  │  GBP / JPY   193.45   ↑+0.4%  │  │    body_small #4C662B + arrow_upward icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← rate_row_eur_usd
│  │  EUR / USD    1.0993  ↓-0.3%  │  │    body_small #BA1A1A + arrow_downward icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← rate_row_usd_inr
│  │  USD / INR    83.22     — 0.0% │  │    body_small #44483D + remove icon (neutral)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← rate_row_eur_gbp: 16dp bottom margin (last)
│  │  EUR / GBP    0.8568  ↓-0.2%  │  │    body_small #BA1A1A + arrow_downward icon
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Converter card: #FFFFFF fill, 16dp radius, elevation 4 (≈level2=3dp in M3 tokens), 20dp internal padding, 16dp horizontal margin, 16dp bottom margin.
- Amount input (send_amount_input): title_large 22sp/700, #4C662B text, #F9FAEF background, 8dp radius, 12dp h-pad, 10dp v-pad, 12dp bottom margin; decimal keyboard.
- Currency selectors (from/to): select variant, #F9FAEF, 8dp radius, arrow_drop_down trailing, 12dp h-pad, 10dp v-pad; 8dp margin-bottom (from), 8dp margin-top / 16dp margin-bottom (to).
- Swap button: swap_vert 32dp icon in #CDEDA3 circular container (16dp radius, 8dp padding); align_self center; 4dp vertical margin.
- Converted result (converted_result_display): display_medium 45sp/700, #4C662B, centred, 8dp vertical padding.
- Rate info (rate_info_text): body_small 12sp, #44483D, centred, 16dp bottom padding.
- CTA (send_money_cta): filled #4C662B, #FFFFFF label_large, 12dp radius, 14dp vertical padding, full content width.
- Rate rows: #FFFFFF fill, 8dp radius, row direction, space-between, align-centre, 16dp h-padding, 14dp v-padding, 16dp h-margin, 2dp bottom-margin (all except last which has 16dp).
- Delta colouring: positive = #4C662B + arrow_upward; negative = #BA1A1A + arrow_downward; zero = #44483D + remove icon.
- Tapping any rate row triggers select_pair action, pre-populating the converter with that pair.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← fx_rates_title visible, headline_large, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │  ← error container (white card, 12dp radius)
│  │                               │  │
│  │  ⚠                           │  │  ← error_outline icon, 32dp, #BA1A1A
│  │  Unable to load exchange      │  │  ← title_medium, #1A1C16, centred
│  │  rates.                       │  │
│  │                               │  │
│  │  Check your connection and    │  │  ← body_medium, #44483D, centred
│  │  try again.                   │  │
│  │                               │  │
│  │      ┌──────────────────┐     │  │  ← outlined button, #4C662B border + text
│  │      │      Retry       │     │  │    12dp radius
│  │      └──────────────────┘     │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** converter_card and all rate rows hidden. Per-component banners (last_updated_text: "Could not retrieve rate timestamp."; converter_card: "Could not load exchange rate. Please try again." with retry) may also appear if partial data loaded before failure.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← fx_rates_title visible
│                                     │
│  ┌───────────────────────────────┐  │  ← empty state container (white card, 12dp radius)
│  │                               │  │
│  │     [currency_exchange]       │  │  ← icon-2xl (48dp), #44483D (on_surface_variant)
│  │                               │  │
│  │  No exchange rates available  │  │  ← title_medium (16sp/500), #1A1C16, centred
│  │  for the selected currencies. │  │
│  │                               │  │
│  │  Try a different currency     │  │  ← body_medium (14sp), #44483D, centred
│  │  pair.                        │  │
│  │                               │  │
│  │  ┌───────────────────────┐    │  │  ← text/outlined button, #4C662B
│  │  │  Reset to GBP / EUR   │    │  │    triggers reset_currency_pair action
│  │  └───────────────────────┘    │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** converter_card and all rate rows hidden. empty_icon: currency_exchange (48dp). "Reset to GBP / EUR" action resets fromCurrency/toCurrency to defaults and triggers RetryLoadEvent.

---

## Design Checklist (Figma / Stitch)

- [ ] Screen title "Exchange Rates" — headline_large (Outfit 32sp/400), #4C662B, 24dp top padding, 16dp horizontal
- [ ] Timestamp "Rates updated: 14 May 2026, 15:42 UTC" — body_small (12sp/400), #44483D; driven by obp_get_fx_rate.effective_date
- [ ] Converter card: #FFFFFF fill, 16dp radius, elevation 4 (M3 level2), 20dp padding, 16dp horizontal margin
- [ ] Amount input: title_large (22sp/700), #4C662B text, #F9FAEF background, 8dp radius, decimal keyboard
- [ ] Currency selectors: select variant, #F9FAEF fill, 8dp radius, arrow_drop_down trailing icon, 48dp minimum touch target
- [ ] Swap icon: swap_vert 32dp, #4C662B on #CDEDA3 circular container (16dp radius, 8dp padding), align_self centre
- [ ] Converted result: display_medium (45sp/700), #4C662B, centred, 8dp vertical padding
- [ ] Rate info: "Rate: 1 GBP = 1.1672 EUR" — body_small (12sp), #44483D, centred
- [ ] "Send this amount" CTA: filled #4C662B, #FFFFFF text, label_large (14sp/500), 12dp radius, 14dp v-padding, full content width
- [ ] Section divider: #E1E4D5, 16dp horizontal margin, 8dp vertical margin
- [ ] "Popular Pairs" header: title_medium (16sp/600), #1A1C16, 16dp horizontal, 8dp top/bottom
- [ ] Rate rows: #FFFFFF fill, 8dp radius, space-between row layout, 16dp h-pad, 14dp v-pad, 16dp h-margin
- [ ] Pair labels: body_large (16sp/500), #1A1C16; Rate values: body_large (16sp/600), #1A1C16
- [ ] Delta indicator positive: body_small (12sp/500), #4C662B, arrow_upward icon leading
- [ ] Delta indicator negative: body_small (12sp/500), #BA1A1A, arrow_downward icon leading
- [ ] Delta indicator neutral (0.0%): body_small (12sp/500), #44483D, remove icon leading
- [ ] All 6 rate rows tappable (48dp touch target) — select_pair action populates converter
- [ ] Loading skeletons: shimmer colour #E1E4D5, 200ms (short4), reduced-motion: static placeholder
- [ ] Error state: converter card + rate rows hidden; error message centred; outlined Retry button
- [ ] Empty state: currency_exchange icon 48dp, "Reset to GBP / EUR" action, converter + rate rows hidden
- [ ] All text: Outfit typeface throughout. 16dp horizontal content padding. Touch targets 48dp minimum.

---

_Generated by /idea export | 2026-05-30_
