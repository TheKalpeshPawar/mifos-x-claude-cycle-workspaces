---
ui_yaml_sha: 610d54f97461af152d8413cddf97ce826c1911adb639f69fe46a26dba9a5cfcb
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 7785f709dd906df7f8bc0d97d8fb52d8389cab2a79d2944a0fac875fb3620e2e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: meetings
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# meetings — error state

> Auto-generated from screens/meetings/ui.yaml @ SHA 44938563d03647d7
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the meetings screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Title "Meetings" Outfit Medium 18sp #E3E3D8 centered. Background #12140E. Zero elevation.

**Component 2 — Hero** (centered, top margin 64dp): 160dp x 160dp illustration of a calendar with a broken link or missing page rendered in #44483D and #8F9285 on #12140E. error_state archetype.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): Title "Couldn't load meetings" Outfit SemiBold 22sp #E3E3D8 centered.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Check your connection and try again. Upcoming meetings will appear once you reconnect." Outfit Regular 14sp #C5C8BA centered line-height 20sp, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Button** (centered, top margin 16dp): Text button "Go back" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green #B2D188 retry button provides a grounded, calm recovery action for field officers who depend on their schedule staying accessible.

## Archetype: screen

## Layout
- type: column (scrollable)
- padding: 16
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
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

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

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Real content:** every text label, image, and data point reflects the content source manifest above — no numbered generic items, no filler text, no dummy text, no empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "screen" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 6 checkpoints pass.

Anchored by the recovery accent #B2D188, the error layout stays calm and balanced, giving field officers a clear, restrained path back to their schedule.

↑↑↑ MOCKUP PROMPT
