---
ui_yaml_sha: 610d54f97461af152d8413cddf97ce826c1911adb639f69fe46a26dba9a5cfcb
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 97f32ef5b1ec02a922f3d26380672efcbae464251195062632222c8a09ca3deb

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: meetings
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# meetings — empty state

> Auto-generated from screens/meetings/ui.yaml @ SHA c812df4226dd1d68
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the meetings screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Meetings - May 2026" Outfit Medium 18sp #E3E3D8 left-aligned 16dp padding. Background #12140E.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 16dp): 7 day chips all unselected outlined 1dp #44483D background #1E201A. Sun 25 selected filled #354E16. Button "Today" Outfit Medium 12sp #B2D188 right-aligned.

**Component 3 — Hero** (centered, top margin 64dp, horizontal padding 48dp): Illustration of an empty calendar page rendered in #1E201A tones on #12140E. empty_state archetype.

**Component 4 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): Title "No meetings scheduled" Outfit SemiBold 22sp #E3E3D8 centered.

**Component 5 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Schedule a meeting with a customer to get started." Outfit Regular 14sp #C5C8BA centered line-height 20sp, max 25 words.

**Component 6 — FAB** (bottom-right, extended FAB 56dp tall 999dp radius, background #B2D188): Label "Schedule Meeting" Outfit SemiBold 14sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green #B2D188 FAB invites first action with calm, balanced restraint, calibrated to the proactive field officer workflow.

## Archetype: screen

## Layout
- type: column (scrollable)
- padding: 32
- alignment: start

## Composition (top → bottom)
1. **text** (#meetings_title) — content: "Meetings · May 2026"
2. **stack** (#week_strip_calendar) — "week_strip_calendar"
   - **box** (#day_mon) — "day_mon"
      - **text** (#day_mon_label) — content: "Mon"
      - **text** (#day_mon_date) — content: "19"
   - **box** (#day_tue) — "day_tue"
      - **text** (#day_tue_label) — content: "Tue"
      - **text** (#day_tue_date) — content: "20"
   - **box** (#day_wed) — "day_wed"
      - **text** (#day_wed_label) — content: "Wed"
      - **text** (#day_wed_date) — content: "21"
   - **box** (#day_thu) — "day_thu"
      - **text** (#day_thu_label) — content: "Thu"
      - **text** (#day_thu_date) — content: "22"
   - **box** (#day_fri) — "day_fri"
      - **text** (#day_fri_label) — content: "Fri"
      - **text** (#day_fri_date) — content: "23"
   - **box** (#day_sat) — "day_sat"
      - **text** (#day_sat_label) — content: "Sat"
      - **text** (#day_sat_date) — content: "24"
   - **box** (#day_sun) — "day_sun"
      - **text** (#day_sun_label) — content: "Sun"
      - **text** (#day_sun_date) — content: "25"
3. **button** (#today_button) — label: "Today"
4. **text** (#upcoming_section_header) — content: "3 meetings this week"
5. **box** (#meeting_card_1) — "meeting_card_1"
   - **stack** (#meeting_1_header) — "meeting_1_header"
      - **text** (#meeting_1_time) — content: "10:00 AM"
      - **box** (#meeting_1_type_chip) — "meeting_1_type_chip"
         - **text** (#meeting_1_type_text) — content: "Online"
   - **text** (#meeting_1_title) — content: "Account Opening Meeting"
   - **text** (#meeting_1_customer) — content: "John Mwangi · 1 hr · Google Meet"
   - **stack** (#meeting_1_actions) — "meeting_1_actions"
      - **button** (#meeting_1_join_button) — label: "Join"
      - **button** (#meeting_1_notes_button) — label: "Notes"
6. **box** (#meeting_card_2) — "meeting_card_2"
   - **stack** (#meeting_2_header) — "meeting_2_header"
      - **text** (#meeting_2_time) — content: "2:00 PM"
      - **box** (#meeting_2_type_chip) — "meeting_2_type_chip"
         - **text** (#meeting_2_type_text) — content: "In-Person"
   - **text** (#meeting_2_title) — content: "KYC Review"
   - **text** (#meeting_2_customer) — content: "Sarah Odhiambo · 30 min · Nairobi Branch, Kimathi St"
7. **box** (#meeting_card_3) — "meeting_card_3"
   - **stack** (#meeting_3_header) — "meeting_3_header"
      - **text** (#meeting_3_time) — content: "Tomorrow · 11:00 AM"
      - **box** (#meeting_3_type_chip) — "meeting_3_type_chip"
         - **text** (#meeting_3_type_text) — content: "Phone"
   - **text** (#meeting_3_title) — content: "New Prospect — Introductory Call"
   - **text** (#meeting_3_customer) — content: "Peter Kamau · Referral from Equity Bank"
8. **button** (#schedule_meeting_fab) — label: "Schedule Meeting"
9. **box** (#create_meeting_sheet) — "create_meeting_sheet"
   - **text** (#create_sheet_heading) — content: "Schedule Meeting"
   - **input** (#meeting_customer_autocomplete) — label: "Customer"
   - **input** (#meeting_date_picker) — label: "Date & Time"
   - **input** (#meeting_duration_select) — label: "Duration"
   - **input** (#meeting_type_select) — label: "Meeting Type"
   - **input** (#meeting_notes_input) — label: "Notes"
   - **button** (#confirm_meeting_button) — label: "Confirm Meeting"

## State-specific behavior
- Show an empty-state illustration, a friendly message, and one primary call-to-action button.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- (no named components extracted — see composition)

## Shell (app-shell resolved for this state)
- App-shell rules are defined per project; per-screen overrides are merged in.
- Render MUST keep nav/bar elements consistent with the resolved shell — present or absent, never partial.

## Tokens (design-tokens roles consumed)
- Colors: primary / secondary / surface / on-surface / on-surface-variant / error (M3 standard roles).
- Typography: body-large / title-large (M3 standard roles).
- Spacing: gap.sm / gap.md / gap.lg.
- ALL token references are by name from the uploaded design system — no hex literals, no inline size values.

## Self-Validation Checklist (MANDATORY)

Before returning the rendered mockup, verify ALL of these are true. If any fails, FIX the output and re-render.

- [ ] **Per-state shape:** the render shows ONLY this state ("empty"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the primary #B2D188 on the FAB, the empty layout stays calm and balanced, ready to transition into content.

↑↑↑ MOCKUP PROMPT
