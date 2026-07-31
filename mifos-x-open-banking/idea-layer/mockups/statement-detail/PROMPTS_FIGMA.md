# Statement detail — Figma Design Prompt

> Generated from `screens/statement-detail/ui.yaml` by `/idea-feature-mockup`
> Design System: Material Design 3 — Trust Blue 1.1.0 · tokens `design-tokens.yaml` 2.1.0
> Generated: 2026-07-30

---

## 1. Frame Setup

- **Frame**: iPhone 14 Pro (393 × 852) / Android (412 × 892)
- **Grid**: 4-column, 16dp gutter, 16dp margin
- **Status bar**: 54dp · **Bottom nav**: 80dp · **Safe area**: top 54 / bottom 34
- **Top app bar**: 56dp **with leading back arrow**

---

## 2. Design Token Variables

Shared collection from `design-tokens.yaml` 2.1.0 — full tables in
`mockups/send-money/PROMPTS_FIGMA.md §2`. Subset bound here:

| Variable | Light | Dark | Usage |
|---|---|---|---|
| `color/surfaceContainer` | `#EBEEF3` | `#1C2024` | Summary card, transaction group |
| `color/surfaceContainerHigh` | `#E5E8ED` | `#262A2E` | Row pressed |
| `color/onSurface` | `#181C20` | `#E0E3E8` | Period, merchant names |
| `color/onSurfaceVariant` | `#41474D` | `#C1C7CE` | Labels, statement id, **summary balances (neutral)** |
| `color/secondaryContainer` | `#D3E5F5` | `#384956` | **Download PDF** CTA |
| `color/onSecondaryContainer` | `#384956` | `#D3E5F5` | Download label |
| `color/primary` | `#266489` | `#95CDF7` | Back icon, **credit amounts** |
| `color/error` | `#BA1A1A` | `#FFB4AB` | **Debit amounts**, error glyph |
| `color/inverseSurface` | `#2D3135` | `#E0E3E8` | Snackbar |

All figures → **Roboto Mono**. Radius: cards `radius/md`, button `radius/full`. Theme **auto**.

---

## 3. Auto Layout Structure

### Loading

```
Frame: statement-detail_loading (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (Fill × 56dp, Horizontal, padding 4/16, gap 16dp)
  │   ├─ back_button: IconButton (48dp, arrow_back 24dp, color/primary)
  │   └─ Title: "Statement" (titleLarge, color/onSurface, Fill)
  ├─ progress_indicator (48dp circular, color/primary, centered)
  └─ BottomNav (Fill × 80dp)
```

**One spinner for both streams** — `combineScreenStates` holds Loading until statement metadata
*and* its transactions resolve. Do not design two independent loading regions.

### Content

```
Frame: statement-detail_content (Fill, Auto Layout Vertical)
  ├─ TopAppBar (same)
  ├─ ScrollContent (Fill, Auto Layout Vertical, padding 12dp, gap 16dp)
  │   ├─ summary_card (Fill × Hug, padding 16dp, radius/md, gap 12dp)
  │   │   Fill: color/surfaceContainer · Elevation: level1
  │   │   ├─ period: "1 Jun – 30 Jun 2026" (titleLarge, color/onSurface)
  │   │   ├─ statementId: "Statement 0042" (bodyMedium, Roboto Mono,
  │   │   │     color/onSurfaceVariant)
  │   │   └─ BalanceRows (Fill, Vertical, gap 4dp)
  │   │       ├─ "Opening balance" / "£1,042.18"
  │   │       ├─ "Closing balance" / "£1,204.55"
  │   │       ├─ "Payments in"     / "£3,120.00"
  │   │       └─ "Payments out"    / "£2,957.63"
  │   │           Label bodyMedium color/onSurfaceVariant ·
  │   │           Value bodyLarge ROBOTO MONO color/onSurfaceVariant, align end
  │   ├─ download_button (Fill × 48dp, radius/full, TONAL)
  │   │   Fill: color/secondaryContainer ·
  │   │   ├─ Icon: download (18dp, color/onSecondaryContainer)
  │   │   └─ Label: "Download PDF" (labelLarge, color/onSecondaryContainer)
  │   ├─ transactions_header → "TRANSACTIONS"
  │   │     (labelMedium, UPPERCASE, color/onSurfaceVariant)
  │   └─ statement_transactions_list (Fill, Vertical, gap 0dp, radius/md, clip,
  │                                   Fill: color/surfaceContainer)
  │       └─ transaction_row (Fill × 64dp, padding 12/16, space-between)
  │           ├─ TextColumn (Fill, gap 2dp)
  │           │   ├─ Merchant (bodyLarge, color/onSurface)
  │           │   └─ Date (bodySmall, color/onSurfaceVariant)
  │           └─ Amount (bodyLarge, ROBOTO MONO, align end)
  │                 Variant: Credit → color/primary | Debit → color/error
  └─ BottomNav
```

**Two money treatments on one screen — both are correct:**

| Figure | Colour | Signed? |
|---|---|:---:|
| Summary balances (opening, closing, in, out) | `color/onSurfaceVariant` | **No** |
| Transaction amounts | `color/primary` credit / `color/error` debit | **Yes** |

A closing balance is a *position*; a transaction is a *movement*. Same split `home` makes between
its hero card and its recent-transaction rows. Do not unify them.

**Reuse the `transaction_row` component from `transactions`** — same model, same formatting, same
target. Do not fork a statement-specific variant.

`download_button` is **tonal**, not filled: the screen's primary content is the statement itself,
and a filled CTA would outrank it.

### Empty — list only, card and CTA remain

```
Frame: statement-detail_empty
  Identical to Content, EXCEPT statement_transactions_list is replaced by:
  └─ EmptyBlock (Fill, Hug, padding 24dp, center, gap 8dp)
      ├─ Icon: receipt_long (48dp, color/onSurfaceVariant)
      ├─ Title: "No transactions in this period" (titleMedium, center)
      └─ Body: "This statement covers a period with no activity."
               (bodyMedium, center, color/onSurfaceVariant)
```

**The summary card and Download PDF stay visible.** A statement with no activity is still a real
statement with real balances and a downloadable PDF — replacing the whole screen would hide both.
Do not build a full-screen empty frame.

### Error

```
Frame: statement-detail_error (Fill, Auto Layout Vertical, center)
  ├─ TopAppBar (same)
  ├─ ErrorContent (Hug, Vertical, center, gap 16dp, padding 24dp)
  │   ├─ Icon: error_outline (64dp, color/error)
  │   ├─ Title: "Couldn't load this statement" (headlineMedium, center)
  │   └─ retry_button (Fill × 48dp, radius/full, Fill: color/primary)
  └─ BottomNav
```

Retry refreshes **both** streams.

### Download failure — snackbar over intact content

```
Overlay: statement-detail_download_error (on the CONTENT frame)
  └─ Snackbar (Fill − 32dp, Hug, padding 14/16, radius/xs,
               anchored above BottomNav + 16dp)
      Fill: color/inverseSurface ·
      Label: "Couldn't download that statement" (bodyMedium,
             color/inverseOnSurface)
```

Same rule as `statements`: a failed download never replaces the screen, and a **successful**
download shows nothing — the platform's save/share sheet is the feedback.

---

## 4. Component Variants

### card: `summary_card`

Fill × Hug · Padding 16dp · Radius `radius/md` · Gap 12dp · Fill `color/surfaceContainer` ·
Elevation `level1` · **No interactive states**.

### button: `download_button`

| Property | Values |
|---|---|
| State | Default, Pressed, Focused, **Downloading** |

Fill × 48dp · Radius `radius/full` · Fill `color/secondaryContainer` · Icon 18dp + labelLarge
`color/onSecondaryContainer`.

**Downloading**: swap the icon for a 20dp indeterminate indicator, label to "Downloading…", tap
disabled. **No progress bar** — HSBC returns the PDF as a single `ByteArray` with no streamed
progress.

### list_item: `transaction_row`

| Property | Values |
|---|---|
| Direction | **Debit** (default), Credit |
| State | Default, Pressed, Focused |

Fill × 64dp · Padding 12/16 · space-between. Debit `−` + `color/error`; credit `+` +
`color/primary`. Tappable → `transaction-detail`.

### icon_button: `back_button` / button: `retry_button`

48dp × 48dp, 24dp `arrow_back`, `color/primary`. Retry: Fill × 48dp, `radius/full`,
`color/primary`, labelLarge `color/onPrimary`.

---

## 5. Assets Required

### Icons (Material Symbols, Outlined)

| Icon | Size | Usage |
|---|:---:|---|
| `arrow_back` | 24dp | Top app bar leading |
| `download` | 18dp | Download PDF CTA |
| `receipt_long` | 48dp | Empty-list block |
| `error_outline` | 64dp | Error illustration |
| `home`, `account_balance`, `payments`, `more_horiz` | 24dp | Bottom nav |

### Images

None.

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:---:|---|
| Compact (< 600dp) | Single column. Primary target. |
| Medium (600–840dp) | Content column capped 600dp, centred; side margins 24dp |
| Expanded (> 840dp) | Content column capped 600dp, centred. Do **not** place the summary card and transaction list side by side — the summary is context *for* the list, and reading order matters |

---

## Mood Palette Usage

| Mood Color | Hex | Component(s) | If Unused — Reason |
|---|---|---|---|
| `mood_gradients.hero.light` | `#C9E6FF → #F7F9FF` | — | **Unused.** The summary card is a candidate hero surface, but it sits above a transaction list that must read as equal-weight; a wash on the card would visually detach it from the data it summarises. |
| `mood_gradients.accent.light` | `#266489 → #50606E` | — | **Unused.** Transaction amounts carry the only colour semantics and must stay flat `primary`/`error`. `tertiary` unused project-wide. |

---

## WCAG Contrast Audit

| Text Token | Bg Token | Ratio | Required | Pass? |
|---|---|:---:|:---:|:---:|
| `onSurface` `#181C20` | `surfaceContainer` `#EBEEF3` | 14.6:1 | 4.5 | ✅ |
| `onSurfaceVariant` `#41474D` | `surfaceContainer` `#EBEEF3` | 8.2:1 | 4.5 | ✅ |
| `primary` `#266489` (credit) | `surfaceContainer` `#EBEEF3` | 5.6:1 | 4.5 | ✅ |
| `error` `#BA1A1A` (debit) | `surfaceContainer` `#EBEEF3` | 5.7:1 | 4.5 | ✅ |
| `onSecondaryContainer` `#384956` | `secondaryContainer` `#D3E5F5` | 7.22:1 | 4.5 | ✅ |
| `inverseOnSurface` `#EEF1F6` | `inverseSurface` `#2D3135` | 12.1:1 | 4.5 | ✅ |
| `onPrimary` `#FFFFFF` | `primary` `#266489` | 6.11:1 | 4.5 | ✅ |
| `primary` `#266489` (back icon) | `surface` `#F7F9FF` | 6.11:1 | 3.0 | ✅ |

All pass WCAG AA. Credit/debit amounts clear 4.5:1 **and** carry a `+`/`−` sign, so direction never
rests on colour alone (WCAG 1.4.1).

---

## Platform Easing

| Property | Value |
|---|---|
| Emphasis curve | `cubic-bezier(0.2, 0.0, 0, 1.0)` |
| iOS | `CAMediaTimingFunction(controlPoints: 0.2, 0.0, 0.0, 1.0)` |
| Android | `PathInterpolator(0.2f, 0.0f, 0.0f, 1.0f)` |
| Durations | short 150ms · medium 300ms · long 450ms |
| Intensity | **low** — honour OS reduce-motion |

Loading → content cross-fades at `medium` (300ms) — **both streams resolve into one transition**,
never two staggered reveals. Snackbar enters at `short` (150ms), auto-dismisses after 4s.
