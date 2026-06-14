# Figma Prompts — Review & Grant Access (Consent Request)

**Feature:** consent-request
**Archetype:** form
**States:** content, submitting, error, empty

---

## State: content

Design a full-screen consent-grant screen for an HSBC Open Banking account connection on Android (390dp baseline width). No Top App Bar. No bottom navigation bar. Background `#F9FAEF`.

**Title and subtitle:** Title (Outfit 28sp, `#1A1C16`): "Review what you'll share". Below it, body text (Outfit 14sp, `#44483D`, `spacing.lg` bottom padding): "This app is asking to read the following information from your HSBC account. Tap Grant access to continue to HSBC's secure sign-in."

**Scope summary card:** `#F0F1E6` fill, 12dp corner radius, `spacing.md` padding, `spacing.md` bottom margin, full width. Two rows each: Material icon 20dp `#386663` leading + body_medium (Outfit 14sp, `#1A1C16`, weight 600) text:
- Row 1: `account_balance` icon + "Shared with: all your HSBC accounts"
- Row 2: `schedule` icon + "Access until: 11 September 2026 (90 days)"

**Clusters card:** `#FFFFFF` fill, 1dp `#C5C8BA` border, 12dp corner radius, `spacing.md` padding, `spacing.md` bottom margin, full width. Heading (Outfit 16sp, weight 700, `#1A1C16`): "Read-only data clusters". Then 10 rows separated by 1dp `#E1E4D5` horizontal dividers. Each row: Material icon 20dp `#4C662B` leading (8dp start padding), body_medium (Outfit 14sp, `#1A1C16`) description (flex:1, 8dp start padding from icon), badge trailing.

Row 1: `account_balance_wallet` + "Account details — your account names, numbers, sort codes and currency" + **Required badge** (outlined, `#44483D` text, 1dp `#C5C8BA` border, 8dp radius, Outfit 11sp)
Row 2: `savings` + "Balances — your current and available balance on each account" + **Required badge**
Row 3: `receipt_long` + "Transactions — incoming and outgoing payments, dates, amounts and merchant details" + **Required badge**
Row 4: `group` + "Payees — the saved payees you can send money to" + **Optional badge** (`#CDEDA3` fill, `#102000` text, 8dp radius, Outfit 11sp)
Row 5: `event_repeat` + "Standing orders — your scheduled recurring payments and their next due dates" + **Optional badge**
Row 6: `sync_alt` + "Direct debits — the mandates set up on your account and their recent payments" + **Optional badge**
Row 7: `event_upcoming` + "Scheduled payments — one-off future-dated payments and their dates" + **Optional badge**
Row 8: `contact_page` + "Account-holder info — the account holder's name and contact details" + **Optional badge**
Row 9: `inventory_2` + "Product details — the account type, rates and features of your HSBC product" + **Optional badge**
Row 10: `description` + "Statements — your account statements and the periods they cover" + **Optional badge**

**Expiry note:** body_small (Outfit 12sp, `#44483D`, `spacing.md` bottom padding): "This access expires automatically after 90 days. You can disconnect sooner at any time from Settings."

**Buttons:** M3 FilledButton full-width, `#4C662B` fill, `#FFFFFF` label (Outfit 14sp, weight 500): "Grant access". 8dp radius. `spacing.sm` top margin. Below it, M3 OutlinedButton full-width, `#4C662B` border + text: "Cancel". 8dp radius. `spacing.sm` top margin.

**Footer:** body_small (Outfit 12sp, `#44483D`, center, `spacing.xl` bottom padding): "You'll approve this at HSBC. We never see your password."

**DON'Ts:**
- Do not truncate or abbreviate any cluster description — show the full text for all 10 rows.
- Do not make the permission badges checkboxes or toggles — they are display-only read-only badges.
- Do not show a TopAppBar or bottom navigation.
- Do not use amber or red for "Optional" badges — `#CDEDA3` fill only.

---

## State: submitting

Full-screen centred loading state. `#F9FAEF` background. No TopAppBar. Centre a 32dp circular indeterminate spinner (`#4C662B`). Below it (Outfit 14sp, `#44483D`, center): "Creating your consent…". All other content hidden — no scope card, no clusters card, no buttons.

**DON'Ts:**
- Do not show any content from the `content` state — this is a full-screen takeover.
- Do not add a cancel button during submission — the in-flight POST cannot be interrupted.

---

## State: error

Same layout as `content` — scope card + clusters card + expiry note + buttons all visible. Insert an error banner **between the expiry note and the Grant access button**: `#FFDAD6` fill, 8dp corner radius, `spacing.md` padding, horizontal row — Material `error` icon 20dp `#BA1A1A` on the left, then body_small (Outfit 12sp, `#410002`, `spacing.sm` start padding): "We couldn't start your connection. Please check your network and try again."

**DON'Ts:**
- Do not hide the clusters card or Grant button — the PSU must be able to retry from the error state.

---

## State: empty

Full-screen centred empty state. `#F9FAEF` background. No TopAppBar. Centre vertically:
- Material `account_balance` icon 48dp, `#75796C`, centered
- Title (Outfit 16sp, weight 700, `#1A1C16`, center, `spacing.md` top padding): "No accounts to share"
- Body (Outfit 14sp, `#44483D`, center, `spacing.sm` top / `spacing.md` bottom padding): "We couldn't find any HSBC accounts to connect. Check that your accounts are open and eligible for Open Banking, then try again."
- M3 OutlinedButton full-width `#4C662B`: "Cancel" (only button — no Grant access in empty state)

---
