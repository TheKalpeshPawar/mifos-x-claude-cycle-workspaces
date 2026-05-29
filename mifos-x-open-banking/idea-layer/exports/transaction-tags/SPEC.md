# SPEC — Transaction Tags & Notes

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | transaction-tags               |
| Flavor        | consumer                       |
| Status        | approved                       |
| Quality Score | 99                             |
| ViewModel     | TransactionTagsViewModel       |

---

## Overview

Transaction Tags & Notes is a detail-screen feature accessible from the transaction detail view. It allows a Consumer persona user to annotate any transaction with free-form hashtag tags (#groceries, #work-expense, #rent, #holiday, #gym), a private text note, and a receipt image attachment. The top app bar shows "Tags & Notes" with a back arrow (navigate_back → transaction-detail) and a "Clear all" delete icon action. A green transaction header card (#4C662B) shows the merchant name ("Whole Foods Market"), debit amount ("−£67.84"), and timestamp ("23 May 2026 · 14:32"). Below that, horizontally scrollable tag chips allow removing existing tags with a single tap; an outlined text input + filled "Add" button lets the user append new tags. A multiline notes text area captures a private annotation (e.g. "Weekly shop — bought extra for bank holiday"). A dashed receipt attachment area with a camera button lets users attach an image from gallery or take a photo. A full-width green "Save" button persists tags, notes, and images via OBP Transaction Metadata endpoints and navigates back to transaction-detail. On successful save a green banner ("Tags and notes saved") briefly appears before auto-navigation (1800 ms delay). Data is loaded via the OBP v1.2.1 Transaction Metadata API: GET tags, POST tag, DELETE tag, POST comment, POST image. Demo data is Kenyan persona (user: amina.wanjiru) with tags #groceries, #transport, #utilities.

---

## Screens

| ID                | Name                      | Route                                  | Layout | Scroll   |
|-------------------|---------------------------|----------------------------------------|--------|----------|
| transaction-tags  | Transaction Tags & Notes  | /transaction-tags/{transactionId}      | Column | Vertical |

**Shell:** Top app bar with back arrow (navigate_back). No bottom navigation.

| App Bar Element  | Value                                       |
|------------------|---------------------------------------------|
| Title            | "Tags & Notes"                              |
| Navigation Icon  | arrow_back → navigate_back                  |
| Action Icon      | delete_outlined → clear_all_metadata "Clear all" |

---

## Components

| ID                        | Type    | Description                                                                                              |
|---------------------------|---------|----------------------------------------------------------------------------------------------------------|
| transaction_header_card   | box     | #4C662B fill, 20dp radius, 20dp H + 20dp V padding, 20dp H margin, 16dp top margin, 20dp bottom margin; tappable → navigate_to_transaction_detail |
| txn_merchant              | text    | "Whole Foods Market" — Outfit/title_large, #FFFFFF, semibold, 8dp bottom padding                        |
| txn_amount                | text    | "−£67.84" — Outfit/display_small, #FFFFFF, bold, 4dp bottom padding                                     |
| txn_date                  | text    | "23 May 2026 · 14:32" — Outfit/body_medium, #CDEDA3                                                     |
| tags_section_label        | text    | "Tags" — Outfit/title_medium, #1A1C16, semibold, 20dp H + 10dp bottom padding; heading role             |
| tags_hint_text            | text    | "Tap a tag to remove it" — Outfit/body_small, #44483D, 20dp H + 8dp bottom padding                      |
| tags_chips_row            | stack   | Horizontal scroll, 8dp spacing, 20dp H + 12dp bottom padding; API → obp_transaction_tags_get; loading: skeleton×3, error: banner + retry, empty: box + label_outlined icon |
| tag_chip_groceries        | box     | "#groceries" — #CDEDA3 fill, 20dp radius, 12dp H + 6dp V padding, Outfit/label_medium, #4C662B text; tap → remove_tag |
| tag_chip_work_expense     | box     | "#work-expense" — #DCE7C8 fill, 20dp radius, same padding, Outfit/label_medium, #386663 text; tap → remove_tag |
| tag_chip_rent             | box     | "#rent" — #CDEDA3 fill, 20dp radius, same padding, Outfit/label_medium, #44483D text (WCAG AA: 7.25:1 on #CDEDA3); tap → remove_tag |
| tag_chip_holiday          | box     | "#holiday" — #CDEDA3 fill, 20dp radius, same padding, Outfit/label_medium, #4C662B text; tap → remove_tag |
| tag_chip_gym              | box     | "#gym" — #CDEDA3 fill, 20dp radius, same padding, Outfit/label_medium, #BA1A1A text; tap → remove_tag   |
| add_tag_row               | stack   | Horizontal, 8dp spacing, 20dp H + 20dp bottom padding, center-aligned                                    |
| add_tag_input             | input   | Outlined, #E1E4D5 border, 12dp radius, 14dp H + 12dp V padding, Outfit/body_medium, flex: 1; label_outlined leading icon; placeholder "#groceries, #holiday…"; tap → focus_tag_input |
| add_tag_button            | button  | "Add" — filled, #4C662B fill, #FFFFFF text, 12dp radius, 16dp H + 12dp V padding, Outfit/label_medium; tap → add_tag |
| notes_divider             | divider | #F9FAEF, 1dp, 20dp H + 20dp bottom margin; decorative                                                   |
| notes_section_label       | text    | "Notes" — Outfit/title_medium, #1A1C16, semibold, 20dp H + 10dp bottom padding; heading role            |
| notes_text_area           | input   | Outlined, #E1E4D5 border, 12dp radius, 14dp H + 12dp V padding, Outfit/body_medium, min 100dp height, 20dp H + 20dp bottom margin; placeholder "e.g. Weekly shop — bought extra for bank holiday"; multiline; API → obp_transaction_comment_add; loading: skeleton×2, error: banner + retry, empty: box + edit_note icon |
| receipt_divider           | divider | #F9FAEF, 1dp, 20dp H + 20dp bottom margin; decorative                                                   |
| receipt_section_label     | text    | "Receipt" — Outfit/title_medium, #1A1C16, semibold, 20dp H + 10dp bottom padding; heading role          |
| receipt_attachment_area   | box     | #F9FAEF fill, 16dp radius, dashed 1dp #E1E4D5 border, 24dp padding, 20dp H + 12dp bottom margin, center-aligned; tap → pick_image_from_gallery; API → obp_transaction_image_add; loading: skeleton×1, error: banner + retry, empty: box + receipt_long_outlined icon |
| receipt_placeholder_icon  | icon    | receipt_long_outlined, 36dp, #44483D, center-aligned, 8dp bottom margin; decorative (role: none)        |
| receipt_placeholder_text  | text    | "Tap to attach a receipt image" — Outfit/body_medium, #44483D, center-aligned                            |
| camera_button             | button  | "Take Photo" — outlined, #386663 border + text, 12dp radius, camera_alt leading icon, 20dp H + 12dp V padding, Outfit/label_medium; tap → open_camera |
| save_button               | button  | "Save" — filled, #4C662B fill, #FFFFFF text, 14dp radius, 24dp H + 16dp V padding, Outfit/label_large, full width, 20dp H + 32dp bottom margin; tap → save_metadata → transaction-detail |
| save_success_banner       | box     | "Tags and notes saved" — #CDEDA3 fill, 12dp radius, 16dp H + 12dp V padding, 20dp H + 16dp bottom margin; role: status; visible in save_success state only |
| save_success_icon         | icon    | check_circle_outlined, 20dp, #4C662B, 8dp right margin; decorative                                      |

---

## States

| ID           | Trigger                                    | Description                                                                                          |
|--------------|--------------------------------------------|------------------------------------------------------------------------------------------------------|
| loading      | Screen entry / RetryLoad event             | Transaction header visible; skeleton shimmer (short4 = 200ms) for tags, notes, receipt; save button hidden |
| view_tags    | MetadataLoaded (2 existing tags)           | Full layout: header + 2 chips (groceries, work-expense) + add-tag row + notes area + receipt area + save |
| content      | Alias for view_tags (default loaded state) | Identical layout to view_tags                                                                        |
| edit_mode    | add_tag_input focused / note editing       | All 5 chips visible; add_tag_input border → #4C662B 2dp; keyboard visible                           |
| save_success | save_metadata action succeeds              | Success banner + check icon visible; auto-navigates to transaction-detail after 1800 ms              |
| empty        | No tags on this transaction                | Header + add-tag row + notes + save; empty guidance in tags_chips_row; no chips                      |
| error        | OBP API call failed                        | Transaction header only; cloud_off icon + "Unable to load metadata" + retry; save button hidden      |

---

## State Model

**ViewModel:** `TransactionTagsViewModel`
**Screen State Type:** `TransactionTagsUiState`

| Name           | Type                        | Default       |
|----------------|-----------------------------|---------------|
| transaction    | TransactionDetail?          | null          |
| tags           | List\<TransactionTag\>      | emptyList()   |
| noteText       | String                      | ""            |
| tagInputText   | String                      | ""            |
| attachedImages | List\<TransactionImage\>    | emptyList()   |
| isSaving       | Boolean                     | false         |
| uiState        | TransactionTagsUiState      | Loading       |
| error          | UiError?                    | null          |

**Events:** `MetadataLoaded`, `TagAdded(value: String)`, `TagRemoved(value: String)`, `NoteChanged(text: String)`, `ImagePicked(uri: String)`, `CameraCaptured(uri: String)`, `SaveClicked`, `SaveComplete`, `RetryLoad`, `InputFocused(field: String)`, `InputBlurred`

**Actions:** `add_tag`, `remove_tag`, `focus_tag_input`, `focus_notes`, `pick_image_from_gallery`, `open_camera`, `save_metadata`, `clear_all_metadata`, `navigate_to_transaction_detail`

**DI Dependencies:** `TransactionMetadataRepository`, `ImageRepository`

**Errors:**

| Field          | Code               | Message                                                              |
|----------------|--------------------|----------------------------------------------------------------------|
| global         | LOAD_FAILED        | "Unable to load transaction metadata. Please try again."             |
| save_tag       | TAG_SAVE_FAILED    | "Could not add tag. Please try again."                               |
| save_note      | NOTE_SAVE_FAILED   | "Could not save note. Please try again."                             |
| save_image     | IMAGE_SAVE_FAILED  | "Could not attach image. Please try again."                          |
| tag_validation | TAG_EMPTY          | "Tag cannot be empty. Type a tag name like #groceries."              |
| tag_validation | TAG_DUPLICATE      | "That tag is already added to this transaction."                     |

---

## Navigation

| From              | To                 | Trigger                                     | Type  |
|-------------------|--------------------|---------------------------------------------|-------|
| transaction-tags  | transaction-detail | navigate_back (top app bar arrow)           | pop   |
| transaction-tags  | transaction-detail | save_metadata (Save button) after 1800 ms   | pop   |
| transaction-tags  | transaction-detail | navigate_to_transaction_detail (header tap) | push  |
| transaction-tags  | transactions       | go_to_transactions (deep-link shortcut)     | push  |
| transaction-tags  | home               | go_to_home (deep-link shortcut)             | push  |

---

## API Endpoints

| Endpoint                                                                                                                    | Auth        | Tag                  | Purpose                              |
|-----------------------------------------------------------------------------------------------------------------------------|-------------|----------------------|--------------------------------------|
| GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                       | DirectLogin | Transaction-Metadata | Load existing tags for transaction   |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                      | DirectLogin | Transaction-Metadata | Add a new tag to the transaction     |
| DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}            | DirectLogin | Transaction-Metadata | Remove a tag from the transaction    |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments                  | DirectLogin | Transaction-Metadata | Add/update a private note (comment)  |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images                    | DirectLogin | Transaction-Metadata | Attach a receipt image by URL        |

---

## Design Tokens

| Token                              | Value           | Usage                                                                                       |
|------------------------------------|-----------------|---------------------------------------------------------------------------------------------|
| colors.light.primary               | #4C662B         | Transaction header card fill, Add button fill, Save button fill, tag chip text, success icon |
| colors.light.primary_container     | #CDEDA3         | Tag chips (#groceries, #rent, #holiday, #gym) fill, success banner fill, txn date text     |
| colors.light.nav_active_indicator  | #DCE7C8         | Tag chip (#work-expense) fill                                                               |
| colors.light.secondary             | #386663         | camera_button border + text, #work-expense chip text                                        |
| colors.light.error                 | #BA1A1A         | #gym tag chip text                                                                          |
| colors.light.background            | #F9FAEF         | Screen base, receipt attachment area fill, divider color                                    |
| colors.light.surface_variant       | #E1E4D5         | Input border color, receipt dashed border                                                   |
| colors.light.on_surface            | #1A1C16         | Section labels ("Tags", "Notes", "Receipt")                                                 |
| colors.light.on_surface_variant    | #44483D         | Hint text, receipt icon, #rent chip text (7.25:1 WCAG AA on #CDEDA3)                       |
| colors.light.on_primary            | #FFFFFF         | Transaction header text, Add button text, Save button text                                  |
| typography.display_small           | Outfit 32sp/600 | Transaction amount "−£67.84"                                                                |
| typography.title_large             | Outfit 22sp     | Merchant name "Whole Foods Market"                                                          |
| typography.title_medium            | Outfit 16sp/500 | Section labels "Tags", "Notes", "Receipt"                                                   |
| typography.body_medium             | Outfit 14sp/400 | Transaction date, input text, notes area, receipt placeholder                               |
| typography.body_small              | Outfit 12sp/400 | Hint text "Tap a tag to remove it"                                                          |
| typography.label_large             | Outfit 14sp/500 | Save button label                                                                           |
| typography.label_medium            | Outfit 12sp/500 | Tag chip labels, Add button label, camera button label                                      |
| radius.xl (20dp)                   | 20dp            | Transaction header card, tag chips                                                          |
| radius.lg (16dp)                   | 16dp            | Receipt attachment area                                                                     |
| radius.md (12dp)                   | 12dp            | Input fields, Add button, notes area, camera button; Save button uses 14dp                 |
| motion.duration.short4             | 200ms           | Skeleton shimmer duration in loading state                                                  |
| touchTargets.min_touch_target      | 48dp            | All interactive elements (chips, buttons, inputs)                                           |
| touchTargets.spacing_between_targets | 8dp           | Gap between tag chips, add-tag row element spacing                                          |

---

_Generated by /idea export | 2026-05-30_
