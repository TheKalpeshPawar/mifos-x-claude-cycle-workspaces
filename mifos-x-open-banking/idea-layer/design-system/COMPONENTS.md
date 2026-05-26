---
name: Mifos X Open Banking — Components
version: "2.0.0"
generated_at: "2026-05-25"
figma_source: "tEEJwW4HkUR75fKhDq73Jz"
category: banking
---

# Mifos X Open Banking — Component Library

> M3 components extracted from Figma design system. Each entry documents the Figma component spec, token references, and Compose implementation target.

## Buttons

### Button / Filled
- **Figma**: `#4C662B` background, white text, 40px height, 20px border-radius (pill), 24px horizontal padding
- **Typography**: Outfit Medium 14px / 20px line-height (Label Large)
- **Compose**: `Button(colors = ButtonDefaults.buttonColors(containerColor = Primary))`
- **Usage**: Primary actions — Login, Send, Confirm, Save

### Button / Outlined
- **Figma**: 1px `#75796C` border, `#4C662B` text, 40px height, 20px border-radius, 24px horizontal padding
- **Typography**: Outfit Medium 14px / 20px line-height
- **Compose**: `OutlinedButton(border = BorderStroke(1.dp, Outline))`
- **Usage**: Secondary actions — Continue with OBP-OIDC, Cancel, Sign Out (with Error color)

### Button / Text
- **Typography**: Outfit Medium 14px, `#4C662B` color
- **Usage**: Tertiary actions — Forgot password, See all, links

## FAB

### FAB / Primary
- **Figma**: 56px square, 16px border-radius, `#4C662B` background, white "+" icon 28px
- **Compose**: `FloatingActionButton(containerColor = Primary, shape = RoundedCornerShape(16.dp))`
- **Usage**: Primary creation — New payment, Add beneficiary, New account

## Badges

### Badge / Success
- **Figma**: `#4C662B` background, white text, 24px height, 8px border-radius, 10px horizontal padding
- **Typography**: Outfit Medium 12px
- **Content**: "COMPLETED"

### Badge / Pending
- **Figma**: `#E8A317` background, white text, same dimensions
- **Content**: "INITIATED"

### Badge / Failed
- **Figma**: `#BA1A1A` background, white text, same dimensions
- **Content**: "FAILED"

## Inputs

### TextField / Default
- **Figma**: White background, 1px `#75796C` border, 56px height, 4px border-radius, 16px horizontal padding, 8px vertical padding
- **Label**: Outfit Medium 11px `#75796C` (Label Small)
- **Value**: Outfit Regular 16px `#1A1C16` (Body Large)
- **Compose**: `OutlinedTextField(shape = RoundedCornerShape(4.dp))`

## Surfaces

### Card / Base
- **Figma**: White background, 1px `#C5C8BA` border, 12px border-radius, 16px padding
- **Title**: Outfit Medium 16px `#1A1C16` (Title Medium)
- **Supporting text**: Outfit Regular 14px `#44483D` (Body Medium)
- **Compose**: `Card(border = BorderStroke(1.dp, OutlineVariant), shape = RoundedCornerShape(12.dp))`

### Balance Card (Banking)
- **Figma**: `#CDEDA3` background, 16px border-radius, 20px padding, no border
- **Label**: Outfit Medium 12-14px `#44483D`
- **Amount**: Outfit SemiBold 32px `#1A1C16` / 40px line-height (Display Small)
- **Subtitle**: Outfit Regular 12px `#44483D`

### Transaction Item (Banking)
- **Container**: White card with `#C5C8BA` border, 12px radius, 16px padding
- **Icon**: 40px circle with `#F9FAEF` background
- **Merchant**: Outfit Medium 16px `#1A1C16`
- **Category**: Outfit Regular 12px `#44483D`
- **Amount**: Outfit Medium 16px — credit `#4C662B`, debit `#BA1A1A`
- **Badge**: inline, right-aligned

## Navigation

### TopBar / Default
- **Figma**: `#F9FAEF` background, 56px height, 16px horizontal padding
- **Back arrow**: 24px, `#1A1C16`
- **Title**: Outfit Regular 22px / 28px line-height (Title Large)
- **Gap**: 16px between arrow and title
- **Compose**: `TopAppBar(colors = TopAppBarDefaults.topAppBarColors(containerColor = Background))`

### BottomNav / Home
- **Figma**: `#F9FAEF` background, 1px `#C5C8BA` border-top, 80px height
- **Layout**: 4 tabs evenly spaced, each 80px wide
- **Active tab**: Icon inside 64×28px pill with `#DCE7C8` background, 14px border-radius. Label Outfit Medium 11px `#1A1C16`
- **Inactive tab**: No pill. Label Outfit Medium 11px `#44483D`
- **Tabs**: Home, Accounts, Payments, Profile
- **Compose**: `NavigationBar(containerColor = Background)`

## Feedback

### Loading States
- **Skeleton shimmer**: Gradient sweep `#E1E4D5` → `#F9FAEF`, 1.5s linear infinite
- **Circular spinner**: 3px border, `#CDEDA3` track, `#4C662B` active arc, 1s linear
- **Pattern**: Chrome (TopBar, BottomNav) stays real during loading. Content replaced by skeletons matching the content layout geometry.

### Empty / Error States
- **Empty**: Centered icon (48px, `#75796C`) + title (Outfit Medium 16px) + description (Outfit Regular 14px `#44483D`) + optional action button
- **Error**: Same layout, icon in `#BA1A1A`, "Retry" filled button

## Design Tokens Quick Reference

| Token | Light | Dark |
|-------|-------|------|
| Primary | `#4C662B` | `#B2D188` |
| Primary Container | `#CDEDA3` | `#354E16` |
| Background | `#F9FAEF` | `#12140E` |
| Surface | `#FFFFFF` | `#12140E` |
| Error | `#BA1A1A` | `#FFB4AB` |
| Outline | `#75796C` | `#8F9285` |
| Outline Variant | `#C5C8BA` | `#44483D` |
| Text Primary | `#1A1C16` | `#E3E3D8` |
| Text Secondary | `#44483D` | `#C5C8BA` |

_Generated by /design-system --full · 2026-05-25 · Figma source: tEEJwW4HkUR75fKhDq73Jz_
