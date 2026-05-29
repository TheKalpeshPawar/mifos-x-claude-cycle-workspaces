# SPEC — Customer 360 Profile

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | customer-detail          |
| Flavor        | fieldOfficer             |
| Status        | approved                 |
| Quality Score | 93                       |
| ViewModel     | CustomerDetailViewModel  |

---

## Overview

The Customer 360 Profile screen provides Field Officers with a comprehensive, scrollable 360-degree view of a specific customer, accessed by tapping a customer row in the customer-search results. The screen opens with a solid green hero header (`#4C662B`) showing a circular initials avatar (white circle, green text), the customer's full legal name, member-since date, and a KYC Verified badge. Directly below the header a quick-stats row (background `#F9FAEF`) displays three summary metrics arranged horizontally: account count, total balance in KES, and last activity relative timestamp. A 5-tab horizontal tab bar (Overview · KYC · Accounts · Applications · Messages) segments detailed content; Overview is selected by default with a 3dp `#4C662B` underline indicator. The Overview tab renders three white elevation-1 cards: Personal Information (full name, date of birth, national ID, phone, email plus a "View Full Profile →" link), Address, and Relationship Manager (officer name + Reassign link). A KYC status banner appears contextually: green (`#CDEDA3` with `#4C662B` left accent) when verified, amber-accented when pending. A fixed-position FAB ("Create Application", `#4C662B`, `add` icon) sits 88dp above the bottom edge at right-16dp. A full-width outlined "Send Message" button anchors the scrollable content above an 80dp spacer. The screen is mobile-only (390dp baseline). No bottom navigation bar is shown in fieldOfficer flavor; a standard top app bar with back arrow is assumed from the navigation host.

Demo customer: **Wanjiru Kamau** (`cust-ke-001-wanjiru`), Equity Bank Kenya, KYC verified, 2 accounts (Savings KES 187,450 + Current KES 42,800 = KES 230,250 total).

---

## Screens

| ID                    | Name                  | Route                           | Layout | Scroll   |
|-----------------------|-----------------------|---------------------------------|--------|----------|
| customer_detail_main  | Customer 360 Profile  | /customer-detail/{customerId}   | Column | Vertical |

**Shell:** Top app bar (back arrow, customer name as title). No bottom navigation bar for fieldOfficer flavor screens.

---

## Components

| ID                           | Type    | Description                                                                                                          |
|------------------------------|---------|----------------------------------------------------------------------------------------------------------------------|
| customer_header_box          | box     | Solid `#4C662B` hero header; horizontal row; 20dp top padding, `spacing.md` horizontal, `spacing.lg` bottom padding |
| customer_avatar              | box     | Circular 60×60dp; bg `#FFFFFF`; initials in `Outfit/headline_small` bold `#4C662B`; 16dp right margin, flex-shrink 0 |
| customer_full_name           | text    | Customer legal name — `Outfit/headline_small`, `#FFFFFF`, bold; from API `legal_name`                               |
| customer_since_text          | text    | "Customer since Jan 2024" — `Outfit/body_medium`, `#44483D`; derived from account open date                         |
| kyc_verified_badge           | box     | "KYC Verified" — `#4C662B` bg, `#FFFFFF` text, 12dp radius, 10dp horizontal + `spacing.xs` vertical padding, `Outfit/label_small` bold; shown only when `kyc_status == true` |
| quick_stats_row              | stack   | Horizontal; `#F9FAEF` bg; `space_around` justify; `spacing.sm` vertical padding; contains 3 stat texts              |
| stat_accounts_count          | text    | "2 Accounts" — `Outfit/title_small`, `#4C662B`, bold, centered; from accounts API                                   |
| stat_total_balance           | text    | "KES 230,250" — `Outfit/title_small`, `#1A1C16`, bold, centered; summed from accounts response                      |
| stat_last_activity           | text    | "3 days ago" — `Outfit/title_small`, `#44483D`, medium, centered; relative timestamp                                 |
| tab_bar                      | stack   | Horizontal; `#FFFFFF` bg; 1dp `#E1E4D5` bottom border; `role: tablist`                                              |
| tab_overview                 | input   | "Overview" tab — selected by default; active: `#4C662B` text + 3dp `#4C662B` bottom border                          |
| tab_kyc                      | input   | "KYC" tab — shows KYC document list; navigates to kyc-review panel                                                   |
| tab_accounts                 | input   | "Accounts" tab — shows linked customer accounts                                                                       |
| tab_applications             | input   | "Applications" tab — shows account applications                                                                        |
| tab_messages                 | input   | "Messages" tab — navigates to customer-messages                                                                        |
| personal_info_card           | box     | `#FFFFFF`, 12dp radius, elevation 1, 16dp padding; `spacing.md` horizontal margin, `spacing.md` top, `spacing.sm` bottom |
| personal_info_label          | text    | "Personal Information" — `Outfit/title_small`, `#4C662B`, bold; 10dp bottom padding                                  |
| personal_info_name           | text    | "Wanjiru Kamau" (full legal name from API) — `Outfit/body_medium`, `#1A1C16`, medium                                 |
| personal_info_dob            | text    | "DOB: 22 Mar 1988" — `Outfit/body_small`, `#44483D`; from `date_of_birth`                                            |
| personal_info_id             | text    | "National ID: (from KYC doc)" — `Outfit/body_small`, `#44483D`; from KYC records                                     |
| personal_info_phone          | text    | "Phone: +254 712 345 678" — `Outfit/body_small`, `#44483D`; from `mobile_phone_number`                               |
| personal_info_email          | text    | "Email: wanjiru.kamau@gmail.com" — `Outfit/body_small`, `#4C662B`; from `email`                                      |
| view_full_profile_link       | link    | "View Full Profile →" — `Outfit/body_medium`, `#4C662B`; 20dp horizontal, `spacing.sm` top; navigates to customer-profile |
| address_card                 | box     | `#FFFFFF`, 12dp radius, elevation 1, 16dp padding; `spacing.md` horizontal margin, `spacing.sm` bottom               |
| address_label                | text    | "Address" — `Outfit/title_small`, `#4C662B`, bold; `spacing.sm` bottom padding                                       |
| address_value                | text    | "123 Moi Avenue, Nairobi, Kenya" — `Outfit/body_medium`, `#1A1C16`; from address API data                            |
| relationship_manager_card    | box     | `#FFFFFF`, 12dp radius, elevation 1, 16dp padding; horizontal row; space-between; align-center                        |
| relationship_manager_label   | text    | "Assigned to: Priya Sharma" — `Outfit/body_medium`, `#1A1C16`, medium; from staff assignment API                      |
| reassign_link                | link    | "Reassign" — `Outfit/label_medium`, `#4C662B`; opens reassign officer dialog                                          |
| kyc_status_banner_verified   | box     | `#CDEDA3` bg, 10dp radius, 4dp left border `#4C662B`, 14dp padding; row; align-center; conditional on `kyc_verified` |
| kyc_verified_text            | text    | "KYC Verified · Last checked 15 Apr 2026" — `Outfit/body_medium`, `#4C662B`, medium; date from `last_ok_date`         |
| kyc_status_banner_pending    | box     | `#CDEDA3` bg, 10dp radius, 4dp left border `#E8A317`, 14dp padding; `role: alert`; conditional on `kyc_pending`       |
| kyc_pending_text             | text    | "KYC Pending — Action Required" — `Outfit/body_medium`, `#44483D` bold (7.25:1 contrast pass; NOT `#E8A317` which fails WCAG AA) |
| bottom_actions_spacer        | spacer  | 80dp height — scroll clearance below fixed FAB                                                                         |
| create_application_fab       | button  | "Create Application" — filled `#4C662B`, `#FFFFFF` text, `add` icon leading; 16dp radius, 20dp horizontal + 14dp vertical padding; fixed bottom-88dp right-16dp; elevation 6 |
| send_message_button          | button  | "Send Message" — outlined `#4C662B`, `message` icon leading; full-width, 12dp radius; `spacing.md` horizontal margin + bottom |

---

## States

| ID      | Trigger                            | Description                                                                                                       |
|---------|------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry (customerId received) | Hero header always visible; avatar, name, stats, tab bar, cards all shimmer as skeleton blocks (`short4` motion, 200ms) |
| content | Customer data loaded successfully   | Full layout; KYC verified banner shown (pending banner hidden); Overview tab active; all cards populated from API  |
| error   | API failure (non-404)              | Hero header visible; all stats, tabs, cards, FAB, and buttons hidden; error message shown inline with retry prompt  |
| empty   | Customer not found (404)           | Full screen empty — no header; "Customer record not found. The customer may have been archived or the ID is invalid." |

---

## State Model

**ViewModel:** `CustomerDetailViewModel`
**Screen State Type:** `CustomerDetailUiState`

| Name             | Type                  | Default                          |
|------------------|-----------------------|----------------------------------|
| customerId       | String                | `""`                             |
| customer         | Customer?             | `null`                           |
| accounts         | List\<Account\>       | `emptyList()`                    |
| selectedTab      | CustomerDetailTab     | `CustomerDetailTab.OVERVIEW`     |
| kycStatus        | KycStatus             | `KycStatus.UNKNOWN`              |
| totalBalance     | Double                | `0.0`                            |
| isLoading        | Boolean               | `true`                           |
| networkError     | String?               | `null`                           |
| customerNotFound | String?               | `null`                           |

**Events:** `TabSwitchedEvent`, `CreateApplicationEvent`, `SendMessageEvent`, `ReassignOfficerEvent`, `ReviewKycEvent`, `RetryLoadEvent`

**Actions:** `switch_tab`, `navigate`, `reassign_officer`, `retry_load`

**DI Dependencies:** `CustomerRepository`, `AccountRepository`, `NavigationService`

---

## Navigation

| From            | To                    | Trigger                        | Type |
|-----------------|-----------------------|--------------------------------|------|
| customer-detail | kyc-review            | `tab_kyc` tap                  | push |
| customer-detail | account-applications  | `create_application_fab` tap   | push |
| customer-detail | customer-messages     | `send_message_button` tap      | push |
| customer-detail | customer-profile      | `view_full_profile_link` tap   | push |

---

## API Endpoints

| Endpoint                                                                              | Auth        | Tag      | Purpose                                           |
|---------------------------------------------------------------------------------------|-------------|----------|---------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}                                 | DirectLogin | Customers | Fetch full customer record (demographics, KYC)    |
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/accounts                        | DirectLogin | Accounts  | Fetch accounts associated with this customer      |
| GET /obp/v5.0.0/banks/{bankId}/customers/{customerId}/customer-account-links          | DirectLogin | Customer  | Fetch customer-account link records (link IDs)    |

---

## Design Tokens

| Token                          | Value   | Usage                                                                                              |
|--------------------------------|---------|----------------------------------------------------------------------------------------------------|
| colors.light.primary           | #4C662B | Hero header bg, avatar text + left accent on KYC verified banner, KYC badge bg, active tab indicator + underline, section label text (`title_small`), email text, link color, FAB fill, Send Message border + text, Reassign link |
| colors.light.primary_container | #CDEDA3 | KYC verified banner bg, KYC pending banner bg                                                     |
| colors.light.background        | #F9FAEF | Screen background, quick-stats row bg                                                              |
| colors.light.surface           | #FFFFFF | Cards bg (personal info, address, RM card), tab bar bg, avatar fill                               |
| colors.light.on_primary        | #FFFFFF | Hero header text (customer name), KYC badge text, FAB label + icon                               |
| colors.light.on_surface        | #1A1C16 | Personal info values (name, address, RM label), total balance stat                                |
| colors.light.on_surface_variant| #44483D | Customer-since text, DOB / phone body-small fields, last-activity stat, KYC pending text (WCAG AA pass) |
| colors.semantic.pending        | #E8A317 | KYC pending banner 4dp left-accent border ONLY (not used for text — contrast fails)               |
| typography.headline_small      | Outfit 24sp/600 | Customer name in hero header, avatar initials                                               |
| typography.title_small         | Outfit 14sp/500 | Quick stats values, card section labels (Personal Information, Address)                     |
| typography.body_medium         | Outfit 14sp/400 | Customer-since text, personal info primary fields, KYC banner text, RM name                 |
| typography.body_small          | Outfit 12sp/400 | DOB, phone, address detail fields                                                             |
| typography.label_small         | Outfit 11sp/500 | KYC Verified badge text                                                                       |
| typography.label_medium        | Outfit 12sp/500 | Tab labels, Reassign link                                                                     |
| elevation.level1               | 1dp     | Personal info card, address card, relationship manager card                                        |
| elevation.level3               | 6dp     | Create Application FAB                                                                             |
| radius.md                      | 12dp    | All content cards (personal info, address, RM), Send Message button, KYC banners                  |
| radius.lg                      | 16dp    | FAB border-radius                                                                                  |
| radius.pill                    | 999dp   | KYC Verified badge (12dp set directly; pill-style intent)                                          |
| spacing.xs                     | 4dp     | KYC badge vertical padding                                                                         |
| spacing.sm                     | 8dp     | Tab padding vertical, card bottom margin, address label bottom padding                             |
| spacing.md                     | 16dp    | Card horizontal margin, card padding, FAB right offset                                             |
| spacing.lg                     | 24dp    | Hero header bottom padding                                                                         |
| motion.duration.short4         | 200ms   | Skeleton shimmer loop duration                                                                     |

---

_Generated by /idea export | 2026-05-30_
