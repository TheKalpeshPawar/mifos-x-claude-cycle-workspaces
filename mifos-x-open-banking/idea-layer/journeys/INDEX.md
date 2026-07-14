# Journeys Index — mifos-x-open-banking

Schema: `core/schemas/journeys/journey.schema.json` (x-contract-version: 1.0.0)
Authored: 2026-07-14 via `/idea journey --all` batch scaffold.
Flow linkage: omitted from initial authoring. Run `/idea journey link` to wire `flows[]` bidirectional refs to `idea-layer/flows/*.yaml`.

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
| [settings-and-profile](settings-and-profile.yaml) | Priya | personalisation manager | 2 | minimal | P0 | settings, profile |
| [pfm-review](pfm-review.yaml) | Priya | personal finance analyst | 4 | medium | P2 | pfm |
| [developer-full-surface](developer-full-surface.yaml) | Sam | expert AISP auditor | 6 | maximum | P2 | party, product, atm-locator, beneficiaries, accounts (entry) |

Total: 9 journeys, 29 screen-sequence slots across 25 unique screens.

---

## Screen Coverage (25 / 25)

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
| profile | settings-and-profile |
| pfm-dashboard | pfm-review |
| spending-by-category | pfm-review |
| budgets | pfm-review |
| recurring-subscriptions | pfm-review |
| party | developer-full-surface |
| product | developer-full-surface |
| atm-locator | developer-full-surface |
| beneficiaries | developer-full-surface |

Coverage: **25 / 25** (100%). All `has_ui` features covered.

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
| J7 — INDEX.md covers all journey ids | PASS | all 9 journeys listed above |

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
