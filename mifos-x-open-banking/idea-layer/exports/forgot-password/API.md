# API — Forgot Password

## Endpoints

### POST `/obp/v7.0.0/users/forgot-password/reset-emails`

**Tag:** User
**Trigger:** OnSubmitClicked
**Description:** Request a password reset email for the specified user account.

#### Request

| Field    | Type   | Required | Description                      |
|----------|--------|----------|----------------------------------|
| username | String | Yes      | Account username                 |
| email    | String | Yes      | Email address associated with account |

```json
{
  "username": "alex.consumer",
  "email": "alex@example.com"
}
```

#### Response (200 OK)

| Field   | Type    | Description                         |
|---------|---------|-------------------------------------|
| success | Boolean | Whether the reset email was queued   |
| message | String  | Human-readable confirmation message  |

```json
{
  "success": true,
  "message": "Password reset email sent successfully."
}
```

#### Errors

| Code | Key                    | UI Handling                                                |
|------|------------------------|------------------------------------------------------------|
| 404  | ACCOUNT_NOT_FOUND      | Show error banner: "No account found with those details."  |
| 429  | RATE_LIMITED           | Show error banner: "Too many attempts. Please wait."       |
| 500  | INTERNAL_SERVER_ERROR  | Show error banner: "Something went wrong. Please try again." |

#### Client Behaviour

- Disable submit button during request (isSubmitting = true)
- On 200: transition to success state, show confirmation
- On 404: show error banner, keep form editable for correction
- On 429: show rate-limit message, disable submit for cooldown period
- On 500: show generic error, allow retry
- Validate email format client-side before submission
