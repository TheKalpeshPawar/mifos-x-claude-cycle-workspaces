# idea-layer — Layer Status

> Refreshed 2026-07-30 by `/idea-sync`. 23 screens · 18 features · 15 FRs · 9 flows.

| Artifact | Status |
|---|---|
| CAPABILITY_STATE.yaml | ✅ initialized via /idea init (2026-06-29) — 0 capabilities backfilled (bootstrap mode) |
| app-shell.yaml | ✅ scaffolded via /idea init (2026-06-29); Pay tab retargeted to send-money 2026-07-30 |
| STITCH_STATUS.yaml | ⚠️ scaffolded via /idea init (2026-06-29) — stitch artifacts deleted 2026-07-28; generation deferred, decision still open |
| idea-plan.yaml | ✅ current — PISP scope reversal + P3 phase (2026-07-30) |
| screens/ | ✅ 23 screens — 19 approved, 1 implemented, 3 enriched (PISP, awaiting `/idea approve`) |
| flows/ | ✅ 9 flows — send-money-payment added 2026-07-30 |
| journeys/ | ✅ 8 journeys — not yet extended for the PISP flow |
| _strings/strings.yaml | ✅ 554 keys — 554 referenced, 0 missing, 0 orphans (parity restored 2026-07-30) |
| _list.json | ✅ regenerated 2026-07-30 — 23 screens, 3 flagged idea-layer-ahead-of-source |
| APP_FLOW.mmd | ✅ regenerated 2026-07-30 — 23 nodes, 86 edges, 0 stale endpoints (was absent since 2026-07-28) |
| TAG_REGISTRY.yaml | ✅ 82 tags — 68 source-backed, 14 specification-only (PISP) |
| EXPORT_MATRIX.yaml | ⚠️ roster refreshed to 23; ledger empty by design — exports/ absent |
| components.yaml · design-system/ | ✅ Trust Blue 1.1.0 / tokens 2.1.0 — payment semantics, form validation, irreversible-action contract |
| design-system/components/ | ✅ 27 registry entries + 4 per-component specs (section_header registered 2026-07-30) |
| state/DESIGN_VALIDATION.yaml | ✅ score 89.5, pass — 0 critical, 3 warning, 3 info (partial corpus: 14 rules non-executable) |
| state/DESIGN_SYSTEM_STATE.yaml | ✅ created 2026-07-30 — 15 WCAG pairs measured, 0 failures |
| state/CAPABILITY_GAPS.yaml | ✅ 0 open findings (reset 2026-07-28) |
| exports/ | ❌ absent — `/idea-feature-export --all` (23 features) |
| mockups/ · screens/*/preview/ | ❌ absent — deferred project-wide since 2026-07-28 |
| _cache/data-flow-views/ | ❌ absent — `/idea-data-flow` |

## Known gaps

1. **Derived artifacts absent project-wide.** The 2026-07-28 reverse sync deleted exports,
   mockups, previews, stitch prompts and `_cache/`. Regeneration is deferred, and the stitch
   decision is explicitly still open. This is why `/idea-sync` reports `partial` — its
   7-artifact-group existence gate fails by design, not by defect.
2. **3 features are idea-layer-ahead-of-source.** `send-money`, `payment-consent` and
   `payment-status` are specified but unimplemented (P3). The Pay tab still renders
   `PlaceholderScreen("Pay")`.
3. **P3 has four blocking prerequisites** before any of it can be device-verified: no
   `Pisp.kt` client, no detached-JWS signer, no idempotency-key handling, no payments-scope
   token path. Recorded in `state/FLYWHEEL_STATE.yaml#open_risks`.
4. **Journeys not extended for PISP.** `journeys/` still describes the 8 AIS journeys; the
   send-money-payment flow has no journey counterpart yet.
