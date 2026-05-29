# API Reference — Login

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | login                                       |
| Base URL | https://apisandbox.openbankproject.com      |

---

## POST /my/logins/direct

**Auth:** DirectLogin (credentials in Authorization header)
**Tag:** Authentication
**Trigger:** `onDirectLoginClicked()`

### Request Headers

| Header        | Value                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------|
| Authorization | `DirectLogin username="{username}", password="{password}", consumer_key="{consumer_key}"` |

No request body — all credential data is in the Authorization header.

### Response Fields

| Field | Type   | Stored As     |
|-------|--------|---------------|
| token | String | session_token |

### Error Codes

| Code | Name                | UI Message                                                                     |
|------|---------------------|--------------------------------------------------------------------------------|
| 400  | INVALID_CREDENTIALS | "Invalid username or password. Please check your credentials and try again."  |
| 401  | UNAUTHORIZED        | "You are not authorized to access this account."                               |
| 500  | SERVER_ERROR        | "Something went wrong on our end. Please try again in a moment."               |

---

## GET /obp/v5.1.0/well-known

**Auth:** None
**Tag:** Authentication
**Trigger:** App startup (once, result cached for session)

### Response Fields

| Field          | Type   | Example                                                                                  |
|----------------|--------|------------------------------------------------------------------------------------------|
| provider_id    | String | "obp-oidc"                                                                               |
| well_known_url | String | "https://apisandbox-oidc.openbankproject.com/obp-oidc/.well-known/openid-configuration" |

---

## GET https://apisandbox-oidc.openbankproject.com/obp-oidc/auth

**Auth:** None (opens system browser)
**Tag:** Authentication
**Trigger:** `onOAuthLoginClicked()` — opens system browser with authorization URL

### Query Parameters

| Parameter             | Type   | Value                                              |
|-----------------------|--------|----------------------------------------------------|
| response_type         | String | "code"                                             |
| client_id             | String | {consumer_key}                                     |
| redirect_uri          | String | "org.mifos.openbanking://oauth/callback"           |
| scope                 | String | "openid profile email"                             |
| state                 | String | {csrf_state} (generated per request)               |
| code_challenge        | String | {pkce_code_challenge} — SHA-256 of code_verifier   |
| code_challenge_method | String | "S256"                                             |

### Redirect Response Parameters

| Field | Type   | Description            |
|-------|--------|------------------------|
| code  | String | Authorization code     |
| state | String | CSRF state (must match)|

### Error Codes

| Code | Name            | UI Message                                                        |
|------|-----------------|-------------------------------------------------------------------|
| 302  | OAUTH_CANCELLED | "Sign-in was cancelled. You can try again or use DirectLogin."   |

---

## POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token

**Auth:** None
**Tag:** Authentication
**Trigger:** `onOAuthCallback(code, state)` — token exchange after browser redirect
**Content-Type:** application/x-www-form-urlencoded

### Request Body

| Field         | Type   | Value / Source                              |
|---------------|--------|---------------------------------------------|
| grant_type    | String | "authorization_code"                        |
| code          | String | oauth_callback_code                         |
| redirect_uri  | String | "org.mifos.openbanking://oauth/callback"    |
| client_id     | String | OBP_CONSUMER_KEY                            |
| code_verifier | String | pkce_code_verifier                          |

### Response Fields

| Field         | Type   | Stored As     | Notes                                                  |
|---------------|--------|---------------|--------------------------------------------------------|
| access_token  | String | session_token |                                                        |
| id_token      | String | —             | JWT RS256; contains sub, name, email, email_verified   |
| refresh_token | String | refresh_token |                                                        |
| token_type    | String | —             | "Bearer"                                               |
| expires_in    | Int    | —             | 3600 (seconds)                                         |

### Error Codes

| Code | Name                      | UI Message                                              |
|------|---------------------------|---------------------------------------------------------|
| 400  | OAUTH_TOKEN_EXCHANGE_FAILED| "Authentication failed. Please try signing in again." |
| 401  | UNAUTHORIZED              | "Invalid authorization. Please try again."              |

---

## GET https://apisandbox-oidc.openbankproject.com/obp-oidc/userinfo

**Auth:** Bearer {access_token}
**Tag:** Authentication
**Trigger:** After successful token exchange

### Request Headers

| Header        | Value                  |
|---------------|------------------------|
| Authorization | Bearer {access_token}  |

### Response Fields

| Field          | Type    | Description              |
|----------------|---------|--------------------------|
| sub            | String  | User subject identifier  |
| name           | String  | Display name             |
| email          | String  | Email address            |
| email_verified | Boolean | Email verification status|

---

## POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token (refresh)

**Auth:** None
**Tag:** Authentication
**Trigger:** `token_expired` — silent background refresh
**Content-Type:** application/x-www-form-urlencoded

### Request Body

| Field         | Type   | Value / Source       |
|---------------|--------|----------------------|
| grant_type    | String | "refresh_token"      |
| refresh_token | String | stored_refresh_token |
| client_id     | String | OBP_CONSUMER_KEY     |

### Response Fields

| Field         | Type   | Description              |
|---------------|--------|--------------------------|
| access_token  | String | New access token         |
| refresh_token | String | New refresh token        |
| expires_in    | Int    | Expiry in seconds (3600) |

---

## POST https://apisandbox-oidc.openbankproject.com/obp-oidc/revoke

**Auth:** None
**Tag:** Authentication
**Trigger:** `on_logout`
**Content-Type:** application/x-www-form-urlencoded

### Request Body

| Field     | Type   | Source           |
|-----------|--------|------------------|
| token     | String | session_token    |
| client_id | String | OBP_CONSUMER_KEY |

---

_Generated by /idea export | 2026-05-29_
