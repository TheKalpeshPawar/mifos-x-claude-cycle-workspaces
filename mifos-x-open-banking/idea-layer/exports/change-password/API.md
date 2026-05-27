# API — Change Password

## Endpoint

| Field | Value |
|---|---|
| Method | PUT |
| Path | `/obp/v7.0.0/users/current/password` |
| Auth | Bearer token (authenticated user required) |
| Module | obp-auth / AuthRepository |

## Request

```json
{
  "current_password": "string",
  "new_password": "string"
}
```

| Field | Type | Required | Notes |
|---|---|---|---|
| current_password | String | Yes | User's current account password |
| new_password | String | Yes | Desired new password; validated against strength policy server-side |

## Response — Success (200)

```json
{
  "success": true,
  "message": "Password updated successfully."
}
```

| Field | Type | Notes |
|---|---|---|
| success | Boolean | `true` on successful update |
| message | String | Human-readable confirmation |

## Error Responses

| HTTP Status | Error Code | UI Handling |
|---|---|---|
| 400 | `WRONG_CURRENT_PASSWORD` | Error banner: "Current password is incorrect." |
| 400 | `WEAK_PASSWORD` | Error banner: "New password does not meet strength requirements." |
| 401 | `USER_NOT_LOGGED_IN` | Redirect to login screen |
| 500 | `INTERNAL_SERVER_ERROR` | Error banner: "Something went wrong. Please try again." |

## Client Behaviour

- Request fires only when all three fields are non-empty and `newPassword == confirmPassword`.
- Form is disabled (`isSubmitting = true`) during the in-flight request.
- On 200: `isSuccess = true`, error banner cleared, form reset.
- On 4xx/5xx: `errorMessage` populated, `isSubmitting = false`, form re-enabled.
- `PasswordStrengthEvaluator` runs client-side on every `OnNewPasswordChanged` event — independent of the API call.
