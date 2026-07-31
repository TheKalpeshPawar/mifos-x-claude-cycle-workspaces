# Design Layer Context

> Auto-generated summary. Last updated: 2026-07-30T13:00:00Z
> Source: `workspaces/mifos-x/mifos-x-open-banking/idea-layer/` (`screens/` + `design-system/`)

---

## Summary

The design layer for a UK Open Banking **AISP + PISP** reference app: 23 screens specified as
sibling YAML, rendered against the **Trust Blue 1.1.0** Material 3 system. Twenty screens ship in
source; three (`send-money`, `payment-consent`, `payment-status`) are P3 specifications added by
the 2026-07-30 scope reversal that made the app move money for the first time.

Current focus is design-record completeness: mockup and Figma hand-off artifacts now exist for all
23 features, and per-state prompts for all 95 declared states. Rendered previews and Stitch-SDK
visuals are deferred by explicit decision.

---

## Quick Stats

| Metric | Value |
|--------|-------|
| Total Items | 23 screens |
| Completed | 20 (87%) — ship in source |
| In Progress | 3 — P3 specifications, no feature module |
| Gaps | 5 open findings |
| Categories | 7 |
| Last Updated | 2026-07-30T13:00:00Z |

---

## Key Components

- **`design-system/design-tokens.yaml` (2.1.0)** — rendering source of truth. 29 M3 colour roles per
  mode, verbatim from the Material Theme Builder export (seed `#266489`).
- **`design-system/DESIGN.md` (Trust Blue 1.1.0)** — agent-facing brand spec derived from the tokens.
- **`semantic.payment_disposition`** — the three-way in-progress / settled / rejected triad. Added
  in 2.1.0 because a submitted payment is not a boolean.
- **`semantic.money`** — credit `primary`, debit `error`, neutral `onSurfaceVariant`. Deliberately
  not green/red, for calm-finance and colour-blind safety.
- **`form.*`** — field outline states, amount field, on-change-after-first-blur validation. The app
  had no forms before PISP.
- **`irreversible_action`** — review surface, CTA names action + amount, same-weight escape,
  lock-on-tap. Governs `send-money` confirm and `consent-detail` revoke.
- **`app-shell.yaml`** — four bottom-nav tabs: Home · Accounts · Pay · More.
- **`mockups/{feature}/`** — MOCKUP.md + PROMPTS_FIGMA.md, 23/23 complete.

---

## Categories

| Category | Items | Status |
|----------|:-----:|--------|
| Screen specs (`screens/*/ui.yaml`) | 23 | complete |
| Mockups (`mockups/*/MOCKUP.md`) | 23 | complete |
| Figma hand-off (`PROMPTS_FIGMA.md`) | 23 | complete |
| Per-state prompts (`screens/*/prompts/`) | 95 | complete |
| Design system (tokens + DESIGN.md) | 2 | complete |
| Rendered previews (`screens/*/preview/`) | 0 | **deferred** |
| Stitch visuals (`mockups/*/stitch/`) | 0 | **deferred** |

---

## Recent Changes

| Date | Change |
|------|--------|
| 2026-07-30 | Mockup + Figma hand-off generated for all 23 features (46 files) |
| 2026-07-30 | 95 per-state prompts built via `stitch-prompt-build.ts`; prompts confirmed **not** deferred |
| 2026-07-30 | `home` corrected — hero card opens `AccountSelectorSheet` (was: navigate to account-detail); `connect_bank_button` removed |
| 2026-07-30 | `scheduled-payments` gained the `unsupported` state its two gated siblings already declared |
| 2026-07-30 | Design system → Trust Blue 1.1.0 / tokens 2.1.0 — payment disposition, form validation, irreversible-action contract |

---

## Dependencies

- **Depends On**: idea-layer screens · design-system tokens · `app-shell.yaml` · `_strings/`
- **Depended By**: feature layer (Compose implementation) · `/idea-feature-render` · `/idea-feature-stitch` · exports

---

## Current Gaps

- [ ] `scheduled-payments` `unsupported` declared in idea-layer but **not in source** — a `U000` still routes to a retryable error path
- [ ] `U000` modelled in no `api.yaml` for any of the three gated features — the state exists, the condition producing it does not
- [ ] `flow_ref` declared on 9 of 23 `docs.yaml` — per-flow views cover 3 of 9 flows
- [ ] 2 components lack `accessibility_label`: `settings/app_version_row`, `transactions/tx_category_tag`
- [ ] `account-detail` — 14 test scenarios with empty descriptions
- [ ] Rendered previews and Stitch visuals deferred by decision (not a defect)

---

## Context for Claude

```yaml
layer: design
source: workspaces/mifos-x/mifos-x-open-banking/idea-layer
last_updated: 2026-07-30T13:00:00Z

stats:
  total: 23
  completed: 20
  in_progress: 3
  gaps: 5

categories:
  screen_specs: 23
  mockups: 23
  prompts_figma: 23
  per_state_prompts: 95
  previews: 0
  stitch_visuals: 0

high_priority:
  - scheduled-payments unsupported state missing in source
  - U000 condition unmodelled in api.yaml across three gated features
  - PISP regulatory ADR unwritten (adr_required on 3 features)

blockers:
  - prototype/index.html absent — blocks /idea-sync STEP 4.VERIFY
  - dashboard/DEV_STATUS.md + dev-status.html absent — blocks STEP 4.VERIFY

recommended_actions:
  - /implement scheduled-payments  # close the idea<->source unsupported gap
  - /project-dashboard             # generate the missing dashboard pair
  - hand-write ADR 0002            # PISP regulatory position

recent_focus: >-
  Design-record completeness. Mockups and Figma hand-off now exist for all 23 features and
  per-state prompts for all 95 states; previews and Stitch visuals remain deferred by decision.
  Two stale home surfaces were corrected against source during the same pass.
```
