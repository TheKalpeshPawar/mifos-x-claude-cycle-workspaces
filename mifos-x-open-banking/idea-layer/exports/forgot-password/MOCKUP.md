# MOCKUP — Forgot Password

## Layout Overview

Single-column form layout with top app bar, instruction header, input card, and action button. Designed for quick password recovery flow.

---

## State: idle / content

```
┌─────────────────────────────────┐
│ ← Forgot Password               │  ← Top App Bar
├─────────────────────────────────┤
│                                  │
│  Reset Your Password             │  ← headline_small, #4C662B
│  Enter your username and email   │  ← body_medium, #44483D
│  to receive a reset link.        │
│                                  │
│  ┌─────────────────────────────┐ │
│  │ Username                     │ │  ← outlined input
│  │ [________________________]   │ │
│  │                              │ │
│  │ Email                        │ │  ← outlined input, email keyboard
│  │ [________________________]   │ │
│  └─────────────────────────────┘ │  ← filled card, #FFFFFF, r12
│                                  │
│  ┌─────────────────────────────┐ │
│  │      Send Reset Link         │ │  ← filled button, #4C662B
│  └─────────────────────────────┘ │
│                                  │
│        Back to Login →           │  ← inline link → login
│                                  │
└─────────────────────────────────┘
```

## State: submitting

Same as idle but:
- Submit button shows circular loading indicator
- Input fields are disabled (greyed out)
- Back to Login link remains active

## State: success

```
┌─────────────────────────────────┐
│ ← Forgot Password               │
├─────────────────────────────────┤
│                                  │
│  Reset Your Password             │
│                                  │
│  ┌─────────────────────────────┐ │
│  │  ✓  Check Your Inbox        │ │  ← success section
│  │                              │ │
│  │  We've sent a password       │ │  ← body_medium, #44483D
│  │  reset link to your email.   │ │
│  │  Please check your inbox     │ │
│  │  and follow the link.        │ │
│  └─────────────────────────────┘ │  ← #D8EED0 bg, r12
│                                  │
│        Back to Login →           │  ← inline link → login
│                                  │
└─────────────────────────────────┘
```

## State: error

Same as idle but with error banner above form card:

```
│  ┌─────────────────────────────┐ │
│  │ ⚠ No account found with     │ │  ← banner, #FFDAD6 bg
│  │   those details.             │ │     #BA1A1A text
│  └─────────────────────────────┘ │
```

## State: loading

Brief skeleton shimmer replacing form card content. Header remains visible.

## State: empty

```
┌─────────────────────────────────┐
│ ← Forgot Password               │
├─────────────────────────────────┤
│                                  │
│         🔒                       │  ← lock_reset icon, 48dp
│                                  │
│  Password reset unavailable.     │  ← body_medium, centered
│  Please try again later.         │
│                                  │
│        Back to Login →           │
│                                  │
└─────────────────────────────────┘
```

---

## Design Checklist

- [ ] Outfit typography throughout
- [ ] Earth-green accent #4C662B on headline and primary button
- [ ] Input fields: outlined variant, #C5C8BA border, #4C662B focused
- [ ] Error banner: #FFDAD6 background, #BA1A1A text, r8
- [ ] Success section: #D8EED0 background, #4C662B accent, r12
- [ ] Card: #FFFFFF surface, r12 border radius
- [ ] Background: #F9FAEF
- [ ] Back arrow in top app bar navigates back
- [ ] "Back to Login" link navigates to login screen
- [ ] Submit button disabled during submitting state
- [ ] Email input uses email keyboard type
- [ ] Touch targets minimum 48dp
