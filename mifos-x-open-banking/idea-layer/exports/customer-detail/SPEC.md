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

The Customer 360 Profile screen provides Field Officers with a comprehensive view of a specific customer's data, accessible by tapping any customer in the customer-search results. The screen opens with a green hero header (`#4C662B`) displaying the customer's initials avatar, full name, member-since date, and KYC status badge. Below the hero, a quick-stats row shows 3 summary metrics: account count, total balance, and last activity date. A 5-tab horizontal tab bar (Overview, KYC, Accounts, Applications, Messages) segments the detailed content. The Overview tab — shown by default — contains a Personal Information card (full name, DOB, national ID, phone, email), an Address card, and a Relationship Manager assignment card with reassign capability. A KYC status banner (green "Verified" or amber "Pending") appears contextually based on `kycStatus`. A fixed-position FAB ("Create Application") sits above the bottom nav, and a full-width "Send Message" outlined button anchors the bottom of the scrollable content. The Field Officer can navigate from this screen to KYC Review, Account Applications, Customer Messages, and the full Customer Profile.

---

## Screens

| ID                    | Name                  | Route                           | Layout | Scroll   |
|-----------------------|-----------------------|---------------------------------|--------|----------|
| customer_detail_main  | Customer 360 Profile  | /customer-detail/{customerId}   | Column | Vertical |

**Shell:** Top app bar (back arrow, customer name as title). No bottom navigation bar for Field Officer screens.

---

## Components

| ID                           | Type    | Description                                                                                           |
|------------------------------|---------|-------------------------------------------------------------------------------------------------------|
| customer_header_box          | box     | Green hero header `#4C662B`; horizontal row containing avatar + name stack; 20dp top padding         |
| customer_avatar              | box     | Circular 60×60dp; bg `#FFFFFF`; initials "JM" in `headline_small` `#4C662B`, bold; 16dp margin-right |
| customer_full_name           | text    | "John Mwangi" — `headline_small`, `#FFFFFF`, bold; data from API `legal_name`                        |
| customer_since_text          | text    | "Customer since Jan 2024" — `body_medium`, `#44483D`; derived from `last_ok_date`                    |
| kyc_verified_badge           | box     | "KYC Verified" — `#4C662B` bg, `#FFFFFF` text, 12dp radius, `label_small`, bold; shown when `kyc_status == true` |
| quick_stats_row              | stack   | Horizontal row; `#F9FAEF` bg; `space_around` justify; 3 stats                                        |
| stat_accounts_count          | text    | "2 Accounts" — `title_small`, `#4C662B`, bold, centered                                              |
| stat_total_balance           | text    | "KES 145,200" — `title_small`, `#1A1C16`, bold, centered                                             |
| stat_last_activity           | text    | "3 days ago" — `title_small`, `#44483D`, medium, centered                                            |
| tab_bar                      | stack   | Horizontal tab bar; white bg, 1dp `#E1E4D5` border-bottom                                            |
| tab_overview                 | input   | "Overview" tab; selected by default; active: `#4C662B` text + 3dp border-bottom                      |
| tab_kyc                      | input   | "KYC" tab; navigates to kyc-review content panel                                                      |
| tab_accounts                 | input   | "Accounts" tab; shows linked accounts                                                                  |
| tab_applications             | input   | "Applications" tab; shows account applications                                                         |
| tab_messages                 | input   | "Messages" tab; navigates to customer-messages                                                         |
| personal_info_card           | box     | White card, 12dp radius, elevation 1, 16dp padding; visible in Overview tab                           |
| personal_info_label          | text    | "Personal Information" — `title_small`, `#4C662B`, bold, 10dp bottom padding                         |
| personal_info_name           | text    | "John Kamau Mwangi" — `body_medium`, `#1A1C16`, medium; from `legal_name`                            |
| personal_info_dob            | text    | "DOB: 14 Mar 1985" — `body_small`, `#44483D`; from `date_of_birth`                                   |
| personal_info_id             | text    | "National ID: KE12345678" — `body_small`, `#44483D`                                                  |
| personal_info_phone          | text    | "Phone: +254 722 123 456" — `body_small`, `#44483D`; from `mobile_phone_number`                      |
| personal_info_email          | text    | "Email: john.mwangi@gmail.com" — `body_small`, `#4C662B`; from `email`                               |
| view_full_profile_link       | link    | "View Full Profile →" — `body_medium`, `#4C662B`; navigates to customer-profile                      |
| address_card                 | box     | White card, 12dp radius, elevation 1; address detail                                                  |
| address_label                | text    | "Address" — `title_small`, `#4C662B`, bold                                                            |
| address_value                | text    | "123 Moi Avenue, Nairobi, Kenya" — `body_medium`, `#1A1C16`                                          |
| relationship_manager_card    | box     | White card, 12dp radius, elevation 1; horizontal row: assigned officer + Reassign link                |
| relationship_manager_label   | text    | "Assigned to: Priya Sharma" — `body_medium`, `#1A1C16`, medium                                       |
| reassign_link                | link    | "Reassign" — `label_medium`, `#4C662B`; opens reassign officer dialog                                |
| kyc_status_banner_verified   | box     | `#CDEDA3` bg, 4dp left border `#4C662B`, 10dp radius; "KYC Verified · Last checked 15 Apr 2026"      |
| kyc_verified_text            | text    | "KYC Verified · Last checked 15 Apr 2026" — `body_medium`, `#4C662B`, medium                        |
| kyc_status_banner_pending    | box     | `#CDEDA3` bg, 4dp left border `#E8A317`; "KYC Pending — Action Required"; role: alert                |
| kyc_pending_text             | text    | "KYC Pending — Action Required" — `body_medium`, `#44483D` (7.25:1 pass), bold                      |
| bottom_actions_spacer        | spacer  | 80dp height — scroll clearance for fixed FAB                                                          |
| create_application_fab       | button  | "Create Application" — filled `#4C662B`, `add` icon, fixed bottom-right (88dp from bottom, 16dp right), elevation 6 |
| send_message_button          | button  | "Send Message" — outlined `#4C662B`, `message` icon, full-width, 12dp radius                         |

---

## States

| ID      | Trigger                            | Description                                                                                    |
|---------|------------------------------------|------------------------------------------------------------------------------------------------|
| loading | Screen entry                       | Green hero header visible; all content areas replaced by shimmer skeleton blocks               |
| content | Customer data loaded successfully   | All components visible; KYC banner shows based on `kycStatus`; Overview tab active by default  |
| error   | API failure                        | Hero header visible; content area shows error message; no tabs, no cards, no FAB               |
| empty   | Customer record not found (404)    | No header; empty message "Customer record not found. The customer may have been archived or the ID is invalid." |

---

## State Model

**ViewModel:** `CustomerDetailViewModel`
**Screen State Type:** `CustomerDetailUiState`

| Name          | Type                  | Default                         |
|---------------|-----------------------|---------------------------------|
| customerId    | String                | `""`                            |
| customer      | Customer?             | `null`                          |
| accounts      | List\<Account\>       | `emptyList()`                   |
| selectedTab   | CustomerDetailTab     | `CustomerDetailTab.OVERVIEW`    |
| kycStatus     | KycStatus             | `KycStatus.UNKNOWN`             |
| totalBalance  | Double                | `0.0`                           |
| isLoading     | Boolean               | `true`                          |
| networkError  | String?               | `null`                          |
| customerNotFound | String?            | `null`                          |

**Events:** `TabSwitchedEvent`, `CreateApplicationEvent`, `SendMessageEvent`, `ReassignOfficerEvent`, `ReviewKycEvent`, `RetryLoadEvent`

**Actions:** `switch_tab`, `navigate`, `reassign_officer`, `retry_load`

**DI Dependencies:** `CustomerRepository`, `AccountRepository`, `NavigationService`

---

## Navigation

| From            | To                    | Trigger                       | Type  |
|-----------------|-----------------------|-------------------------------|-------|
| customer-detail | kyc-review            | `tab_kyc` tap                 | push  |
| customer-detail | account-applications  | `create_application_fab` tap  | push  |
| customer-detail | customer-messages     | `send_message_button` tap     | push  |
| customer-detail | customer-profile      | `view_full_profile_link` tap  | push  |

---

## API Endpoints

| Endpoint                                                              | Auth        | Tag       | Purpose                                          |
|-----------------------------------------------------------------------|-------------|-----------|--------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}                 | DirectLogin | Customers | Fetch full customer record (demographics, KYC)   |
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/accounts        | DirectLogin | Accounts  | Fetch accounts linked to this customer           |
| GET /obp/v5.0.0/banks/{bankId}/customers/{customerId}/customer-account-links | DirectLogin | Customer | Fetch customer-account link records         |

---

## Design Tokens

| Token                          | Value   | Usage                                                                   |
|--------------------------------|---------|-------------------------------------------------------------------------|
| color.light.primary            | #4C662B | Hero header bg, avatar text + border, KYC verified badge bg, tab active indicator, section label text, email text, link text, FAB + send message button, Reassign link |
| color.light.primary_container  | #CDEDA3 | KYC verified banner bg, KYC pending banner bg                           |
| color.light.background         | #F9FAEF | Screen background, quick-stats row bg                                   |
| color.light.surface            | #FFFFFF | Cards background, tab bar background, avatar bg                         |
| color.light.on_primary         | #FFFFFF | Hero text (full name), KYC badge text, FAB icon                        |
| color.light.on_surface         | #1A1C16 | Personal info values, address, relationship manager name                |
| color.light.on_surface_variant | #44483D | Customer-since text, DOB/ID/phone, last-activity stat, KYC pending text |
| color.semantic.pending         | #E8A317 | KYC pending banner left-accent border                                   |
| typography.headline_small      | —       | Customer full name in header (24sp/SemiBold)                            |
| typography.title_small         | —       | Quick stats values (14sp/Medium), section labels in cards               |
| typography.body_medium         | —       | Customer-since, personal info primary values, KYC banner text           |
| typography.body_small          | —       | DOB, national ID, phone, address detail                                 |
| typography.label_small         | —       | KYC verified badge text                                                 |
| typography.label_medium        | —       | Tab labels, Reassign link                                               |
| elevation.level1               | 1dp     | Personal info, address, relationship manager cards                      |
| elevation.level2               | 2dp     | (reserved)                                                              |
| elevation.level3               | 6dp     | Create Application FAB                                                  |
| radius.md                      | 12dp    | All detail cards, send message button                                   |
| radius.lg                      | 16dp    | FAB border-radius                                                       |
| spacing.md                     | 16dp    | Card padding, content horizontal margin                                 |

---

_Generated by /idea export | 2026-05-29_
