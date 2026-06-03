# MOCKUP — Change Password

**Archetype:** form
**ViewModel:** ChangePasswordViewModel
**Shell:** Top app bar ("Change Password") with back arrow → Profile. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.
**States:** loading, idle, submitting, success, error, content, empty
**Updated:** 2026-06-02 (archetype + states_handled added; ChangePasswordViewModel confirmed)

---

## Screen: idle (Default — empty form)

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │  ← M3 TopAppBar, back arrow → profile
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │  ← headline_small, #4C662B
│  Choose a strong password that      │  ← body_medium, #44483D
│  you don't use elsewhere.           │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Current Password             │  │  ← OutlinedTextField, password variant
│  │  ┌─────────────────────────┐  │  │
│  │  │  ············           │  │  │  ← masked, border #C5C8BA
│  │  └─────────────────────────┘  │  │
│  │  ─────────────────────────── │  │  ← divider #E1E4D5
│  │  New Password                 │  │  ← OutlinedTextField, password variant
│  │  ┌─────────────────────────┐  │  │
│  │  │  ············           │  │  │  ← border #C5C8BA
│  │  └─────────────────────────┘  │  │
│  │  ▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░ │  │  ← strength bar 4dp, color_medium #F4B400
│  │  Password strength: Fair      │  │  ← body_small #44483D
│  │  ─────────────────────────── │  │  ← divider #E1E4D5
│  │  Confirm New Password         │  │  ← OutlinedTextField, password variant
│  │  ┌─────────────────────────┐  │  │
│  │  │  ············           │  │  │  ← border #C5C8BA
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Update Password         │  │  ← FilledButton, bg #4C662B, white text
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background `#F9FAEF`. 24dp horizontal padding throughout.
- Form card: white `#FFFFFF`, 12dp radius, 16dp internal padding, 1dp `#C5C8BA` border.
- All three password fields use 56dp height, 4dp radius. Focused border switches to `#4C662B`.
- Dividers `#E1E4D5` between fields. Strength bar fills progressively left-to-right.
- Submit button: full-width FilledButton, 40dp height, pill radius, `#4C662B`.

---

## Screen: submitting

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Choose a strong password that      │
│  you don't use elsewhere.           │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Current Password (disabled)  │  │  ← fields disabled, opacity 0.5
│  │  ┌─────────────────────────┐  │  │
│  │  │  ·············          │  │  │
│  │  └─────────────────────────┘  │  │
│  │  ─────────────────────────── │  │
│  │  New Password (disabled)      │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  ·············          │  │  │
│  │  └─────────────────────────┘  │  │
│  │  ▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░ │  │  ← strength bar, color_high #4C662B
│  │  Password strength: Good      │  │
│  │  ─────────────────────────── │  │
│  │  Confirm New Password (dis.)  │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  ·············          │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       ○ Updating...           │  │  ← CircularProgressIndicator inline, white
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** All form fields have `enabled = false`. Submit button shows inline loading spinner replacing label text.

---

## Screen: success

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Choose a strong password that      │
│  you don't use elsewhere.           │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ✓  Your password has been    │  │  ← success banner, bg #D8EED0
│  │     changed successfully.     │  │     text #4C662B, 8dp radius
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Update Password         │  │  ← button disabled in success
│  └───────────────────────────────┘  │
│                                     │
│  (Navigating back to profile…)      │  ← auto-pop after 2 seconds
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Form card hidden. Success banner full-width. Auto-pop fires after 2000ms delay via coroutine in ViewModel.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Choose a strong password that      │
│  you don't use elsewhere.           │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ⚠  Password change failed.   │  │  ← error banner, bg #FFDAD6
│  │     Please check your current │  │     text #BA1A1A, 8dp radius
│  │     password and try again.   │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Current Password             │  │  ← form re-enabled; current password field
│  │  ┌─────────────────────────┐  │  │     highlighted in error red #BA1A1A
│  │  │  ············           │  │  │
│  │  └─────────────────────────┘  │  │
│  │  ─────────────────────────── │  │
│  │  New Password                 │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  ·············          │  │  │
│  │  └─────────────────────────┘  │  │
│  │  ─────────────────────────── │  │
│  │  Confirm New Password         │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  ·············          │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Update Password         │  │  ← enabled again for retry
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner appears above form card. Current password field border switches to `#BA1A1A`. All fields re-enabled.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Choose a strong password that      │
│  you don't use elsewhere.           │
│                                     │
│              🔄                     │  ← lock_reset icon, 48dp, #C5C8BA
│                                     │
│     Password change unavailable.    │  ← body_medium, center, #44483D
│      Please try again later.        │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Header text retained for context. Form card and button hidden. Empty state icon + message centered.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Choose a strong password that      │
│  you don't use elsewhere.           │
│                                     │
│  ████████████████████████████████   │  ← skeleton card shimmer ~200dp height
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Brief shimmer block replacing form card. Transitions to `idle` in <100ms once auth session resolves.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon, "Change Password" title
- [ ] Form card: white `#FFFFFF` background, 12dp radius, 1dp `#C5C8BA` border
- [ ] Three OutlinedTextFields — password variant with toggle-visibility eye icon
- [ ] Focused border changes to `#4C662B` (primary)
- [ ] Linear strength bar (4dp, 2dp radius) with three-colour progression: red → amber → green
- [ ] Dividers `#E1E4D5` between field groups inside card
- [ ] Error banner: `#FFDAD6` background, `#BA1A1A` text, warning icon, 8dp radius
- [ ] Success banner: `#D8EED0` background, `#4C662B` text, check icon, 8dp radius
- [ ] FilledButton "Update Password": `#4C662B`, full-width, 40dp height, pill radius
- [ ] Submitting state: button shows inline `CircularProgressIndicator`, fields disabled
- [ ] Success state: banner only, button disabled, auto-pop after 2s
- [ ] Empty state: `lock_reset` icon 48dp tinted `#C5C8BA`, body_medium message
- [ ] All text: Outfit typeface; minimum 14sp for body
- [ ] 24dp horizontal content padding throughout
- [ ] Touch targets ≥ 48dp for all interactive elements
