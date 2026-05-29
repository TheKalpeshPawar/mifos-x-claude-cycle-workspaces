# MOCKUP — Forgot Password

**Archetype:** form
**Shell:** Top app bar ("Reset Password") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: idle

```
┌─────────────────────────────────────┐
│ ←  Reset Password                   │  ← M3 TopAppBar, back arrow
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [🔒 reset]  │            │  ← ic_lock_reset, 72×72dp, #4C662B tint
│         └──────────────┘            │
│                                     │
│     Forgot your password?           │  ← headline_small, #4C662B, center
│                                     │
│  Enter your username or email       │  ← body_medium, #44483D, center
│  address and we'll send a link      │
│  to reset your password.            │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Username or Email             │  │  ← TextField, 56dp height
│  │ e.g. john.doe or john@…       │  │  ← placeholder, body_medium
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Send Reset Link         │  │  ← Filled button, #4C662B, 12dp radius
│  └───────────────────────────────┘  │
│                                     │
│          Back to Login              │  ← body_medium link, #386663, center
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- All content centered horizontally within 16dp horizontal padding.
- Illustration 72×72dp centred, 24dp bottom padding before headline.
- Submit button: full content width, 12dp radius, 40dp height minimum.
- "Back to Login": text link, no underline by default, #386663.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Reset Password                   │
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [🔒 reset]  │            │
│         └──────────────┘            │
│                                     │
│     Forgot your password?           │
│                                     │
│  Enter your username or email…      │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ john.doe                      │  │  ← Input populated (disabled state)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │    ◌  Send Reset Link         │  │  ← Loading spinner inside button
│  └───────────────────────────────┘  │
│                                     │
│          Back to Login              │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Input field disabled (greyed border, no cursor). Submit button shows M3 CircularProgressIndicator (white, 20dp) inline. Button not interactive.

---

## Screen: success

```
┌─────────────────────────────────────┐
│ ←  Reset Password                   │
├─────────────────────────────────────┤
│                                     │
│                                     │
│         ┌──────────────┐            │
│         │ [✉️ check]   │            │  ← mark_email_read, 48dp, #4C662B
│         └──────────────┘            │
│                                     │
│         Check your inbox            │  ← title_large, #4C662B, center
│                                     │
│  If an account exists for that      │  ← body_medium, #44483D, center
│  email, you'll receive a password   │
│  reset link within a few minutes.   │
│                                     │
│                                     │
│          Back to Login              │  ← body_medium link, #386663
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Form section (input + submit button) hidden. Success section vertically centred with xl padding top. Non-enumeration copy: does not confirm whether account exists.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Reset Password                   │
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [🔒 reset]  │            │
│         └──────────────┘            │
│                                     │
│     Forgot your password?           │
│                                     │
│  Enter your username or email…      │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ johnxyz                       │  │  ← Input with red border (error_border)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ⚠ We couldn't find an account │  │  ← Error banner: #FFDAD6 fill, #BA1A1A text
│  │   with that username or email.│  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Send Reset Link         │  │
│  └───────────────────────────────┘  │
│                                     │
│          Back to Login              │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner (#FFDAD6, 8dp radius) between input and submit button. Input border changes to #BA1A1A. Error message deliberately same for 404 (user not found) and 400 (invalid input) — prevents enumeration.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Reset Password                   │
├─────────────────────────────────────┤
│                                     │
│         ┌──────────────┐            │
│         │  [🔒 reset]  │            │
│         └──────────────┘            │
│                                     │
│     Forgot your password?           │
│                                     │
│  Password reset unavailable.        │  ← body_medium, #44483D, center
│  Contact your bank for assistance.  │
│                                     │
│          Back to Login              │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Service-unavailable fallback — form hidden, only illustration + title + message + back link.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon, title "Reset Password"
- [ ] Lock reset illustration 72×72dp, #4C662B tint, horizontally centered
- [ ] Headline "Forgot your password?" — headline_small (Outfit 24sp/600), #4C662B, center
- [ ] Subtitle — body_medium (Outfit 14sp/400), #44483D, center
- [ ] Single TextField: 56dp height, 4dp radius, default border #C5C8BA, focus border #4C662B, error border #BA1A1A
- [ ] Submit button: filled, #4C662B fill, white text, label_large (14sp/500), 12dp radius, full content width
- [ ] Loading state: CircularProgressIndicator inside button, input disabled
- [ ] Success: mark_email_read icon 48dp #4C662B; title_large "Check your inbox"; non-enumeration body copy
- [ ] Error banner: #FFDAD6 fill, #BA1A1A text, 8dp radius, between input and submit
- [ ] "Back to Login" text link: body_medium, #386663, centered, always visible
- [ ] No bottom navigation bar (shared flavor screen)
- [ ] All text: Outfit typeface. 16dp horizontal padding throughout.
