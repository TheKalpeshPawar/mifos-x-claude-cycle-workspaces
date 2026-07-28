# Journeys Index — mifos-x-open-banking

Schema: `core/schemas/journeys/journey.schema.json` (x-contract-version: 1.0.0)
Reverse-synced: 2026-07-28 by `/gap-analysis-project` against the shipped source.
Flow linkage: run `/idea journey link` to wire `flows[]` bidirectional refs to `idea-layer/flows/*.yaml`.

---

## Journey Inventory

| id | persona | archetype | # screens | tier | release phase | features covered |
|----|---------|-----------|-----------|------|---------------|-----------------|
| [onboarding-consent](onboarding-consent.yaml) | Priya | first-time user | 4 | maximum | P0 | consent-onboarding, accounts |
| [account-browsing](account-browsing.yaml) | Priya | returning account checker | 2 | medium | P0 | accounts, balances |
| [transaction-review](transaction-review.yaml) | Priya | transaction investigator | 2 | medium | P0 | transactions |
| [consent-management](consent-management.yaml) | Priya | consent steward | 2 | maximum | P0 | consent-dashboard |
| [home-overview](home-overview.yaml) | Priya | daily pulse check | 1 | minimal | P0 | home |
| [recurring-and-statements](recurring-and-statements.yaml) | Priya | commitments reviewer | 6 | medium | P1 | standing-orders, direct-debits, scheduled-payments, statements, accounts (account-detail entry) |
| [settings-and-profile](settings-and-profile.yaml) | Priya | personalisation manager | 2 | minimal | P0 | settings, licences |
| [developer-full-surface](developer-full-surface.yaml) | Sam | expert AISP auditor | 5 | maximum | P2 | account-holder, product, beneficiaries, accounts (entry) |

Total: 8 journeys, 24 screen-sequence slots.

**Removed 2026-07-28:** `pfm-review` — all four of its screens (pfm-dashboard,
spending-by-category, budgets, recurring-subscriptions) were spec-only and have been
deleted. `settings-and-profile` lost its profile step and gained licences;
`developer-full-surface` lost its atm-locator step and renamed party → account-holder.

---

## Screen Coverage (20 / 20)

| screen | covered by journey(s) |
|--------|-----------------------|
| user-onboarding | onboarding-consent |
| login | onboarding-consent |
| consent-callback | onboarding-consent |
| accounts | onboarding-consent, account-browsing, developer-full-surface |
| account-detail | account-browsing, recurring-and-statements, developer-full-surface |
| transactions | transaction-review |
| transaction-detail | transaction-review |
| consent-list | consent-management |
| consent-detail | consent-management |
| home | home-overview |
| standing-orders | recurring-and-statements |
| direct-debits | recurring-and-statements |
| scheduled-payments | recurring-and-statements |
| statements | recurring-and-statements |
| statement-detail | recurring-and-statements |
| settings | settings-and-profile |
| licences | settings-and-profile |
| account-holder | developer-full-surface |
| product | developer-full-surface |
| beneficiaries | developer-full-surface |

Coverage: **20 / 20** (100%). All shipped screens covered.

---

## RULE-JOURNEY-001 Compliance

| check | status | notes |
|-------|--------|-------|
| J1 — every journey YAML has required top-level fields | PASS | id, version, persona, goal, success_metric, screen_sequence, expected_outcome present in all 9 |
| J2 — id matches filename stem | PASS | all 9 file stems match their `id:` value |
| J3 — screen_sequence minItems=1 | PASS | minimum 1 screen (home-overview); maximum 6 |
| J4 — success_metric.kind ∈ enum | PASS | all use valid enum values (activation, task_completion, retention, satisfaction, time_to_value) |
| J5 — tier ∈ enum | PASS | maximum / medium / minimal used correctly |
| J6 — preconditions and failure_modes present on high-risk journeys | PASS | all maximum-tier journeys have both; minimal-tier journeys have failure_modes |
| J7 — INDEX.md covers all journey ids | PASS | all 8 journeys listed above |

---

## Known Schema Conflict (report-only, not a RULE-JOURNEY-001 failure)

The schema pattern for `screen_id`, `feature_id`, `recovery_screen`, and `fallback_screen_id`
is `^[a-z][a-zA-Z0-9]*$` (camelCase only, no hyphens). This project uses kebab-case screen
IDs (e.g. `consent-detail`, `user-onboarding`) matching the `screens/` directory structure.
Per the task directive ("screen_id is a free string, kebab is fine"), kebab IDs are used
throughout. **Action required**: update the project's local `journey.schema.json` pattern
to `^[a-z][a-z0-9-]*$` (matching the JourneyId pattern) so validators accept these IDs,
OR add an `x-allow-kebab: true` annotation. Alternatively, run `sed` to convert screen_ids
to camelCase once a canonical mapping is agreed.
