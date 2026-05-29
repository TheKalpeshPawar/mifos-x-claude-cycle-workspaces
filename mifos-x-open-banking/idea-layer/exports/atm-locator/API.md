# API Reference — ATM & Branch Locator

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | atm-locator                            |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v5.1.0/banks/{bankId}/atms

**Auth:** DirectLogin
**Tag:** ATM
**Trigger:** Screen entry — `AtmLocatorViewModel` calls `loadAtms()` with resolved user latitude/longitude on `ScreenOpened`; re-triggered on `SearchLocationEvent` with new coordinates.

Fetches ATMs near the user's location. The ViewModel applies client-side `AtmFilter` (ALL / ATMs / 24/7) to the response before updating `atmList`. Results are sorted by proximity. Up to `limit` (default 10) entries are returned; the UI renders the nearest 3 in the content state.

### Path Parameters

| Name   | Type   | Required | Value              | Description                   |
|--------|--------|----------|--------------------|-------------------------------|
| bankId | String | Yes      | (from session)     | OBP bank identifier           |

### Query Parameters

| Name      | Type   | Required | Example            | Description                               |
|-----------|--------|----------|--------------------|-------------------------------------------|
| latitude  | Double | Yes      | -1.2674            | User's device latitude coordinate         |
| longitude | Double | Yes      | 36.8069            | User's device longitude coordinate        |
| limit     | Int    | No       | 10                 | Max ATMs to return (default 10)           |

### Response Fields

| Field                           | Type           | Description                                                     |
|---------------------------------|----------------|-----------------------------------------------------------------|
| id                              | String         | Unique ATM identifier (e.g. "atm-kcb-westlands-001")           |
| name                            | String         | ATM display name (e.g. "KCB Westlands ATM")                    |
| address                         | Address        | Structured address: line_1, line_2, city, county, country, postcode |
| address.line_1                  | String         | Street address line 1 (e.g. "Westlands Commercial Centre")     |
| address.city                    | String         | City name (e.g. "Nairobi")                                      |
| address.country                 | String         | ISO 2-char country code (e.g. "KE")                             |
| address.postcode                | String         | Postal code (e.g. "00100")                                      |
| location                        | LatLng         | ATM coordinates for map pin placement                           |
| location.latitude               | Double         | e.g. -1.2674                                                    |
| location.longitude              | Double         | e.g. 36.8069                                                    |
| open_24_hours                   | Boolean        | `true` when ATM operates around the clock                       |
| cash_withdrawal_national_amount | String         | Max national withdrawal amount (e.g. "40000" in local currency) |
| supported_languages             | List\<String\> | ISO language codes (e.g. ["en", "sw"])                          |
| services                        | List\<String\> | Capability keys: "cash_withdrawal", "balance_enquiry", "mini_statement", "pin_change", "cash_deposit", "fund_transfer" |

### Demo Data (from demo-data.yaml)

| id                         | name                  | city    | open_24_hours | cash_withdrawal_national_amount | services                                           |
|----------------------------|-----------------------|---------|---------------|---------------------------------|----------------------------------------------------|
| atm-kcb-westlands-001      | KCB Westlands ATM     | Nairobi | true          | 40000                           | cash_withdrawal, balance_enquiry, mini_statement, pin_change |
| atm-equity-cbd-002         | Equity Bank CBD ATM   | Nairobi | true          | 40000                           | cash_withdrawal, cash_deposit, balance_enquiry, fund_transfer |
| atm-coop-karen-003         | Co-op Bank Karen ATM  | Nairobi | false         | 30000                           | cash_withdrawal, balance_enquiry, mini_statement   |
| atm-ncba-mombasa-road-004  | NCBA Mombasa Road ATM | Nairobi | true          | 40000                           | cash_withdrawal, balance_enquiry, pin_change       |

### Error Codes

| Code | Message                                  | UI Handling                                             |
|------|------------------------------------------|---------------------------------------------------------|
| 401  | Unauthorized — missing or invalid token  | Clear session, navigate to login screen                 |
| 404  | Bank not found                           | Show error state with "Unable to load ATMs" message     |
| 500  | Internal server error                    | Show error state; offer retry via `RetryLoad` event     |

---

## GET /obp/v5.1.0/banks/{bankId}/branches

**Auth:** DirectLogin
**Tag:** Branch
**Trigger:** Screen entry — called in parallel with ATM fetch; results merged into `atmList` when `selectedFilter` is ALL or Branches.

Fetches bank branches near the user's location. Lobby hours are used to determine open/closed status and rendered as the hours line in each result card (e.g. "Mon–Fri 9am–5pm" for lobby.monday opens_at="08:30", closes_at="17:00"). `drive_up` is present in the schema but not currently surfaced in the UI card. `branch_routings` provides sort codes for potential deep-link use.

### Path Parameters

| Name   | Type   | Required | Value          | Description         |
|--------|--------|----------|----------------|---------------------|
| bankId | String | Yes      | (from session) | OBP bank identifier |

### Query Parameters

| Name      | Type   | Required | Example | Description                          |
|-----------|--------|----------|---------|--------------------------------------|
| latitude  | Double | Yes      | -1.2674 | User's device latitude coordinate    |
| longitude | Double | Yes      | 36.8069 | User's device longitude coordinate   |

### Response Fields

| Field                        | Type                  | Description                                                        |
|------------------------------|-----------------------|--------------------------------------------------------------------|
| id                           | String                | Unique branch identifier (e.g. "branch-kcb-westlands-001")        |
| name                         | String                | Branch display name (e.g. "KCB Westlands Branch")                 |
| address                      | Address               | Structured address (same schema as ATM)                            |
| location                     | LatLng                | Branch coordinates for map pin                                     |
| lobby                        | LobbyHours            | Per-day opening hours map; null opens_at/closes_at = closed        |
| lobby.monday.opens_at        | String?               | Opening time ISO HH:MM (e.g. "08:30"); null = closed              |
| lobby.monday.closes_at       | String?               | Closing time ISO HH:MM (e.g. "17:00"); null = closed              |
| lobby.saturday.opens_at      | String?               | Saturday open time (e.g. "09:00"); null = closed                  |
| drive_up                     | DriveUpHours          | Drive-through hours; null values = no drive-through service        |
| branch_routings              | List\<BranchRouting\> | Routing records; scheme "OBP" or "SORT_CODE"                       |
| branch_routings[].scheme     | String                | e.g. "OBP", "SORT_CODE"                                           |
| branch_routings[].address    | String                | Routing value (e.g. "09-76-13")                                   |

### Demo Data (from demo-data.yaml)

| id                       | name                     | city    | lobby.monday (opens–closes) | lobby.saturday (opens–closes) | sort_code  |
|--------------------------|--------------------------|---------|-----------------------------|-------------------------------|------------|
| branch-kcb-westlands-001 | KCB Westlands Branch     | Nairobi | 08:30–17:00                 | 09:00–13:00                   | 09-76-13   |
| branch-equity-cbd-001    | Equity Bank CBD Branch   | Nairobi | 08:00–17:00                 | 08:30–14:00                   | 07-89-21   |
| branch-coop-karen-001    | Co-op Bank Karen Branch  | Nairobi | 08:30–16:30                 | 09:00–12:00                   | 11-22-33   |

### Error Codes

| Code | Message                                  | UI Handling                                             |
|------|------------------------------------------|---------------------------------------------------------|
| 401  | Unauthorized — missing or invalid token  | Clear session, navigate to login screen                 |
| 404  | Bank not found                           | Show error state with "Unable to load ATMs" message     |
| 500  | Internal server error                    | Show error state; offer retry via `RetryLoad` event     |

---

_Generated by /idea export | 2026-05-30_
