# RESUME — mifos-x/mifos-x-open-banking (HSBC migration, post-migration pipeline)

Updated: 2026-06-15. Branch: `feat/hsbc-open-banking-migration` (workspace, local only, NOT pushed).

## ⭐ CURRENT STATE (2026-06-15) — idea-layer pipeline DONE + COMMITTED
- **39/39 screens approved**; contract migration **COMPLETE** (all 39 at 2.0.0); dark-mode **FIXED** (0/188 preview files lack the `@media (prefers-color-scheme: dark)` block).
- **Two commits on the branch:** `0f2aad2a` (binding + steps A/B/C) and `7b643965` (steps D–F: data-flow/DTOs/demo-data, exports, full render + dark-mode fix, schema migration, approvals, + the dark-mode KNOWN ISSUE doc in workspaces/mifos-x/CLAUDE.md). Working tree clean except `.cache/` (excluded).
- **NOT pushed.** Next actions: (a) push the workspace branch + open PR when ready; (b) **Step G** — goal track for the 5 unbound OBIE groups (VRP / International-Scheduled / International-Standing-Order / File / Multi-Bill); (c) **Step H** — `/kmp-implement` Kotlin client/auth rebuild (OBP DirectLogin → HSBC FAPI/mTLS/JWS/DCR), wiring certs from /home/kalpesh/OpenBankingProject/HSBC_Sandbox/.
- Minor leftover polish (non-blocking): Roboto Mono in direct-debit-detail (RV-015); RV-014 --space-*/--sp-* + --r-*/--radius-* token-name fragmentation; consent-request canonical prompts can't build (STN2 form-budget framework issue — previews use ui.yaml fallback); proper dark-mode root-cause fix (patch framework preview-runtime.js to sync data-theme) still deferred (framework-scope).

---
## (historical handoff below — superseded by CURRENT STATE above)

## ✅ IDEA-LAYER PIPELINE COMPLETE — 39/39 screens APPROVED
Steps A–F all done this multi-session run:
- **A sync/verify + auto-fix** — verify PASS; REQUIREMENTS re-synced to §9; field-officer debt purged.
- **B design-system** — earth-green confirmed (indigo was stale); `design.icon_library` added; dead nav targets fixed; DESIGN.md prose de-personalized.
- **C enrich** — 8 consent/redirect screens enriched (~95); consent-manager "Data & Consent" settings row restored. 0 drafts.
- **D data-flow + DTOs + demo-data** — data-flow 13 new + 7 updated; DTO registry refreshed + OBTokenResponse registered (72 DTOs); demo-data 25 features → OBIE shapes; ALL DTO-name drift reconciled (0 unresolved DTO-position refs).
- **E render + validate** — all 39 screens rendered (fresh, postdate inputs); render-validate ran (polish gaps noted below).
- **F export + verify + approve** — 9 exported (9/9 roundtrip PASS); `/idea verify` = **84/84 PASS, 0 fail**; `/idea approve` = **39/39 approved**.

## ⚠️ COMMIT PENDING (biggest immediate action)
EVERYTHING from steps D–F + the schema migration + the 3 idle-state fixes is UNCOMMITTED — large working tree. Only commit `0f2aad2a` (binding + A+B+C) is in. **Commit the D–F batch next**: workspace-scoped (`workspaces/mifos-x/mifos-x-open-banking/` idea-layer + PROJECT_CONFIG), human prose, `--no-verify`, EXCLUDE root CLAUDE.md + `.cache/`. (NO autonomous commit — do on explicit instruction.)

## 🔴 REMAINING WORK (in priority order)
1. **Commit the D–F batch** (above).
2. **Contract migration INCOMPLETE — 31 of 39 screens still at contract_version 1.1.0** (only the 8 consent/redirect screens were migrated to 2.0.0; current = 2.0.0 per VERSION_MANIFEST). The migration agent got cut off after 8. The 31 are approved-at-1.1.0 — **`/implement` STEP 0.2.CONTRACT will BLOCK them at step H** until migrated. Finish: `/idea-migrate-schema --confirm` for the remaining 31 (run in 2-3 sequential batches — it's heavy, ~40 tool-uses/screen; user is limit-sensitive, NEVER run >1 migration agent in parallel). The migration agent also flagged 3 screens with post-2.0.0 required-field GAPS to fill: **payment-result, send-money-amount, standing-order-create** (do NOT fabricate — enrich the missing 2.0.0 fields).
3. **Render polish (RV-023): 13 screens miss the dark-mode `@media` block** — re-render with `/idea-render-screen {id} --force` (theme is `auto`). Screens: account-detail, auth-callback, bank-authorize-handoff, beneficiaries, consent-declined, consent-expired, consent-intro, consent-request, pfm-dashboard, standing-order-detail, standing-order-edit, transactions. Also minor: RV-001 (3 hex in consent-manager/populated.html), RV-014 (--space-*/--sp-* + --r-*/--radius-* naming fragmentation), RV-015 (Roboto Mono in direct-debit-detail), RV-032 (7 dangling data-nav-to → OBP-removed cards/login/change-password in some previews).
4. **CFC-9**: payment-result, send-money-amount, standing-order-create lack `exports/` dir — re-run `/idea export --force {feature}` for these 3.
5. **Step G** — goal track for the 5 unbound OBIE capability groups (no screens yet): VRP, International-Scheduled, International-Standing-Order, File/bulk, Multi-Bill. Use `/goal-analysis-project → /goal-planning-project → /goal-implement-project`.
6. **Step H** — `/kmp-implement`: the Kotlin client/auth rebuild (OBP DirectLogin → HSBC FAPI/mTLS/JWS/DCR). Wire cert material from /home/kalpesh/OpenBankingProject/HSBC_Sandbox/ into local.properties (env-var names only, never values). Requires #2 done first (contract migration) so implement's gate passes.

## KNOWN FRAMEWORK ISSUES (not project bugs)
- **consent-request canonical prompts ABSENT**: form archetype overshoots the STN2 8000-char per-state budget (~8034-8048, ~48 over); shrink ladder can't reduce a no-item-list form. Its previews/exports came from the ui.yaml fallback (fine). Framework fix needed: raise STN2 cap for `form` archetype OR teach splitIntoSections to split forms. Until then, stitch prompt build for consent-request keeps failing.
- **STEP 3.0 deno auditor** (test-renderer.js --full-audit) broken (retired screens/renderers/ dep) — skip.
- **APPROVE_LOG.yaml** has a pre-existing (2026-05-25) non-strict-YAML quirk (interleaved bulk_summary mappings under entries[] list) — cosmetic; optional cleanup.

## STANDING CONVENTIONS (strict)
- Commits: human prose only, no AI/Claude/framework/slash-command mentions, no footer/emoji, `--no-verify`.
- Workspace commits scope to workspaces/mifos-x/mifos-x-open-banking/; stage explicit paths; EXCLUDE root CLAUDE.md + .cache/.
- idea-layer = Claude Intelligence ONLY; NO python/jq/sed/awk/grep on idea-layer content (rg/Read ok; deno OK for framework scripts like stitch-prompt-build).
- backend.owned=false → server/owned-DB checks skip by policy.
- NO autonomous commit/push; user is LIMIT-SENSITIVE — run heavy agents ONE AT A TIME (sequential), never parallel batches.
- Source = read-only unless told; KDoc /** */ only (no // comments); counterparty rule (never render login username as counterparty name).
- Secrets: never paste values; reference by env-var name + file path only.

## GIT STATE
- Workspace branch feat/hsbc-open-banking-migration; HEAD = 0f2aad2a (A+B+C). D–F uncommitted.
- Source app: feat/kmp-detemplate-app-shell-obp-client, PR #4 OPEN (openMF/mifos-x-open-banking). Binding (.claude-sessions/bindings/nosession.json) is correct.
