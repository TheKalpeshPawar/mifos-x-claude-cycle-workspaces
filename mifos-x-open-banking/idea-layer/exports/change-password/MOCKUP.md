# MOCKUP — Change Password

**Archetype:** form  
**Shell:** Top app bar ("Change Password") with back arrow. No bottom navigation bar.  
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: idle / content (Primary)

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │  ← Top app bar (M3 TopAppBar, back arrow)
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │  ← titleLarge, Outfit Bold, earth-green
│  Keep your account secure by        │  ← bodyMedium, subdued, Outfit Regular
│  choosing a strong new password.    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Current Password             │  │  ← M3 OutlinedTextField label
│  │  ●●●●●●●●●●●●       👁        │  │  ← Masked input + show/hide toggle
│  ├───────────────────────────────┤  │
│  │  New Password                 │  │  ← M3 OutlinedTextField label
│  │  ●●●●●●●●●●●●       👁        │  │  ← Masked input + show/hide toggle
│  │                               │  │
│  │  [████████████░░░░░░░░░░░░░]  │  │  ← LinearProgressIndicator (0.0–1.0)
│  │  Strength: Fair               │  │  ← bodySmall, dynamic label
│  ├───────────────────────────────┤  │
│  │  Confirm New Password         │  │  ← M3 OutlinedTextField label
│  │  ●●●●●●●●●●●●       👁        │  │  ← Masked input + show/hide toggle
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Update Password         │  │  ← FilledButton, full-width, earth-green
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Header section: 24 dp top padding, 16 dp horizontal padding.
- Form card: M3 ElevatedCard, 16 dp horizontal margin; fields separated by 12 dp vertical gap inside card.
- Password strength progress bar: LinearProgressIndicator, full card width minus 16 dp internal padding; color transitions Weak=error / Fair=warning / Strong=earth-green.
- Strength label: right-aligned bodySmall beneath progress bar.
- Submit button: FilledButton, 16 dp horizontal margin, 16 dp top margin after form card.
- Keyboard: IME action "Done" on confirm field fires OnSubmitClicked.

---

## Screen: submitting

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Keep your account secure by        │
│  choosing a strong new password.    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Current Password   (locked)  │  │  ← Fields disabled (alpha 0.38)
│  │  ●●●●●●●●●●●●       👁        │
│  ├───────────────────────────────┤  │
│  │  New Password       (locked)  │  │
│  │  ●●●●●●●●●●●●       👁        │
│  │  [████████████████░░░░░░░░░]  │  │
│  │  Strength: Strong             │  │
│  ├───────────────────────────────┤  │
│  │  Confirm New Password(locked) │  │
│  │  ●●●●●●●●●●●●       👁        │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │    ◌  Updating…               │  │  ← CircularProgressIndicator inline in button
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** All form fields alpha-reduced and non-interactive. Submit button shows inline spinner replacing label.

---

## Screen: success

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Keep your account secure by        │
│  choosing a strong new password.    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ✓  Password updated          │  │  ← M3 Banner (success tint, earth-green icon)
│  │     Your password has been    │  │
│  │     changed successfully.     │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Form hidden after success. Success banner full-width, earth-green left border accent, checkmark icon.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Keep your account secure by        │
│  choosing a strong new password.    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ✕  Current password is       │  │  ← M3 Banner (error tint, M3 error icon)
│  │     incorrect.                │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Form card re-enabled for correction
│  │  Current Password             │  │
│  │  ●●●●●●●●●●●●       👁        │
│  │  ...                          │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Update Password         │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner appears above the form card (not inside). Banner uses M3 error color scheme with an X icon. Form remains interactive for correction.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  ████████████████████  (skeleton)   │  ← Title placeholder
│  ████████████████████████████████   │  ← Subtitle placeholder
│                                     │
│              ◌                      │  ← CircularProgressIndicator, centred
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Header skeleton + centred spinner. No form or button visible.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Change Password                  │
├─────────────────────────────────────┤
│                                     │
│  Update Your Password               │
│  Password change unavailable        │  ← Subtitle replaced with unavailability message
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Header only. No form, no button. Subtitle updated to explain unavailability.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon
- [ ] M3 OutlinedTextField for all three password fields with show/hide toggle icon
- [ ] LinearProgressIndicator beneath New Password field; color-coded by strength tier
- [ ] Strength label right-aligned bodySmall (Outfit), dynamic text
- [ ] FilledButton "Update Password" (earth-green #4C662B) full-width
- [ ] Inline CircularProgressIndicator inside button during submitting state
- [ ] M3 success Banner (earth-green left accent, ✓ icon)
- [ ] M3 error Banner (M3 error color, ✕ icon)
- [ ] Disabled field appearance (alpha 0.38) during submitting state
- [ ] All text uses Outfit typeface
- [ ] 16 dp horizontal content padding throughout
- [ ] ElevatedCard wrapping form fields
