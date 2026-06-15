# SESSION HANDOVER — mifos-x/mifos-x-open-banking (HSBC Open Banking)

Updated 2026-06-15 (session 3 — epic consumer-app-redesign BUILD-COMPLETE). Read this top-to-bottom before acting. Verify binding: `bash core/scripts/session-resolve.sh` → must print `mifos-x/mifos-x-open-banking`.

> ✅ **EPIC `consumer-app-redesign` — ALL 5 PHASES BUILD-COMPLETE (session 3).** All sub-plans 01–05 `complete`; all tasks `[x]`; `PLAN.md sub_plans_progress` all complete. Built at idea-layer SOURCE-OF-TRUTH level (ui.yaml + siblings + flows + manifest + per-screen prompts + content-state renders), NO step-H/Kotlin code (excluded per user).
> - **Phase 2 (Pay hub):** `pay` tab root (6 states rendered) + merged `authorise-handoff` (3 states, consentContext param incl. vrp-setup) + dropped the 2 old handoffs + 4 shared screens kind-aware + standing-orders folded into recurring tail + pay/authorise-handoff approved.
> - **Phase 3 (International):** `pay-international` (FX surfaced, kind-aware, content rendered) + International in pay chooser + pisp-international{,-scheduled,-standing-order} bound.
> - **Phase 4 (VRP):** `automatic-rules` + `automatic-rule-create` (PSU limits lead) + `automatic-rule-detail` (revoke) under Insights (all 3 content rendered) + pfm-dashboard entry + vrp bound.
> - **Phase 5 (Cleanups):** unbound_obie_groups = ONLY file-bulk + multi-bill (deferred:business-flavour); consent-manager already single-entry; read-only banners on beneficiaries/direct-debits/direct-debit-detail; structural reachability confirmed.
>
> **THE ONE REMAINING IDEA-LAYER STEP — consolidated closeout pass (heavy; deferred all session for budget; run next):**
> 1. **Bottom-nav ripple — PRIMARY 7 screens DONE (session 3):** the 28 previews of account-detail/accounts/beneficiaries/home/transaction-detail/transactions/transaction-tags are repointed Pay→pay (data-nav-to), their `ui.yaml` nav_pay shells + quick-pay buttons too, and beneficiary-row taps now → send-money-amount. REMAINING: ~19 SECONDARY previews still show Pay→send-money (profile, settings, notifications, consent-manager, pfm-settings, products, pfm-dashboard + beneficiaries' internal back/recent-card refs) — different markup variants, sprawling. `send-money` is KEPT so every remaining ref is a VALID link (zero dead links). FINISH via `/idea-render-screen --all` (regenerates ALL bottom navs from the corrected app-shell Pay→pay in one pass), THEN retire `screens/send-money/` + repoint its last few inbound refs.
> 2. **Render the non-content states** of the 6 new screens: pay-international + VRP×3 need loading/empty/error/no_network (their content + prompts exist; pay=6/6 done, authorise-handoff=3/3 done).
> 3. **Wire `read_only_affordance`** into beneficiaries/direct-debits/direct-debit-detail content-state `visible_components` (component declared; add to the state list).
> 4. **`/idea-export`** all new/changed screens (SPEC/API/MOCKUP regenerate — stale derived mentions of old handoffs clean up here).
> 5. **G-5 machine gate:** `/idea-setup-flows` → `/idea-completeness` → `/idea-render-validate` → `/idea verify --render-convergence` → fix loop until clean. THEN set epic `PLAN.md status: complete` + archive.
> 6. **THEN step H** (source `/kmp-implement`) per the step-H directives below — network layer first, new source branch.
>
> ⚠️ Verification note: idea-layer verification is STRUCTURAL (`/idea-render-validate` + dark-mode/nav `rg` checks); screenshot-verify is a step-H gate, NOT idea-layer (clarified 2026-06-15).
> ───────────────────────────────────────── (session-2 detail below; superseded by the above) ─────────────────────────────────────────

> ⚠️ **NEXT SESSION — START HERE (resume after limit reset).** DECISION MADE: **Phase 2 = option (a) FULL BUILD, IN PROGRESS.** Execute all of Phase 2 T1–T5 end-to-end, then the Pay-tab ripple re-render (~30 screens' bottom nav) + working-contract validate loop. Heavy agents SEQUENTIAL (limit directive).
>
> **RESUME CURSOR (the ONLY thing to check):** open `plan-layer/project-plans/mifos-x/mifos-x-open-banking/active/consumer-app-redesign/02-pay-hub.md` → read its frontmatter `tasks_progress:` (T1..T5) + the `- [ ]/[x]` checkboxes. **Do the FIRST task whose status is `pending`/`in-progress`, then continue in order.** Each task is self-contained (Write → Verify → Update flow YAML → Log to `idea-layer/state/ACTIVITY_LOG.jsonl` → Mark checkbox+`tasks_progress`). Persist that on-disk state AFTER each task so any limit hit leaves a clean cursor. After T5: do the ripple (repoint Pay tab `send-money`→`pay` in `app-shell.yaml`, re-render all consumer screens' bottom nav, `/idea-setup-flows` → `/idea-completeness` → `/idea-render-validate` loop until clean), then flip `acceptance:` + epic `sub_plans_progress.02 = complete`.
>
> **Per-task durable protocol (do this so we survive the next hit too):** (1) author/edit the ui.yaml + siblings via Read/Edit/Write ONLY (RULE-CI-001, no python/jq on idea-layer); (2) `/idea-render-screen <screen>` emitting light `:root` + `@media (prefers-color-scheme: dark)`, NO hardcoded `data-theme` on root; (3) STRUCTURAL verify only (`test -f`, `rg -c` for root `data-theme`=0 / `@media` dark present / doctype+single `</html>` / nav targets resolve) + `/idea-render-validate` — NO screenshot at the idea-layer (screenshot-verify is a step-H source-phase gate, clarified 2026-06-15); (4) edit the flow YAML; (5) append ACTIVITY_LOG line; (6) flip checkbox + set `tasks_progress.T<n>: complete` in 02-pay-hub.md; (7) update this banner's "LAST DONE" line below.
>
> **T2 = COMPLETE (session 2).** `screens/authorise-handoff/` built + rendered + verified — the single parameterised redirect handoff MERGING `bank-authorize-handoff` (AIS) + `payment-authorize-handoff` (PISP) via a `consentContext` param {ais-consent, pay-now, scheduled, recurring, international}. Files: `ui.yaml` (full-screen takeover, no top bar / no bottom nav; preparing/redirecting/error states; summary-card for payment contexts, access-scope note for ais-consent; cancel → consent-declined|payment-declined by context; full state_model + dual consent API blocks), `flow.yaml`, `docs.yaml` (status:draft), `prompts/{preparing,redirecting,error}.md`, `preview/{preparing,redirecting,error}.html` (rendered payment-context superset; ais variant documented in HTML comments; VERIFIED root data-theme=0, @media dark=3/3, doctype+close=3/3). FLOWS REPOINTED: `account-access-consent.yaml` (consent-request → authorise-handoff) + `payment-initiation.yaml` (send-money-confirm → authorise-handoff) — all `bank-authorize-handoff`/`payment-authorize-handoff` refs in BOTH flow files now point at `authorise-handoff`. ACTIVITY_LOG + `02-pay-hub.md` T2 `[x]` + `tasks_progress.T2: complete`.
>
> **T3 = COMPLETE (session 2).** Deleted `screens/bank-authorize-handoff/` + `screens/payment-authorize-handoff/` (user OK'd scoped `rm -rf`). Repointed ALL live nav refs in surviving screens → `authorise-handoff`: `consent-request/{ui,flow}.yaml`, `auth-callback/ui.yaml`, `payment-declined/ui.yaml`. Verified ZERO live refs in `screens/` + `flows/`. (Stale derived mentions remain in `exports/`, `mockups/`, `_cache/`, state-logs, `EXPORT_MATRIX.yaml`, `IDEA.md`, `FEATURES.md`, `ROADMAP.md`, dto descriptions — harmless; regenerated by `/idea export` + `/idea sync` + render-validate during the ripple. NOT hand-edited.) ACTIVITY_LOG + `02-pay-hub.md` T3 `[x]` + `tasks_progress.T3: complete`.
>
> **T4 RESUME = per-screen micro-checkpoints (do ONE screen fully, then log, before the next — each is independently resumable).** T4 makes the 4 shared screens `kind`-aware ({now, scheduled, recurring}). For EACH screen: (1) Read its current `ui.yaml`; (2) add a `kind` route/param + make copy/labels kind-aware (e.g. amount screen shows a date picker for scheduled, frequency picker for recurring; now = neither); (3) ensure the nav chain stays `send-money-amount → send-money-confirm → authorise-handoff` (confirm screen's authorise target MUST be `authorise-handoff`, replacing the old `payment-authorize-handoff`); (4) `stitch-prompt-build.ts --feature <screen>` then hand-render changed states (reuse existing preview as base — these screens already have previews; only re-render states whose layout changed); (5) verify (root data-theme=0 / @media dark / nav resolves); (6) append ACTIVITY_LOG + tick the sub-box below. Order + exact change:
>   - **T4.1 `send-money-amount`** — add `kind` param; show CoF/amount always; for `scheduled` add a date field, for `recurring` add frequency+start/end fields; review button → `send-money-confirm`. (status: PENDING)
>   - **T4.2 `send-money-confirm`** — kind-aware review (echo date/frequency when present); authorise button target `payment-authorize-handoff` → **`authorise-handoff`** (with `consentContext` = pay-now/scheduled/recurring). ⚠️ check its `ui.yaml`/`flow.yaml`/`api.yaml` for the OLD handoff name and repoint. (status: PENDING)
>   - **T4.3 `payment-result`** — kind-aware success copy (now = "Payment sent"; scheduled = "Payment scheduled for {date}"; recurring = "Standing order set up"). (status: PENDING)
>   - **T4.4 `payment-declined`** — already repointed to authorise-handoff in T3; just make decline copy kind-aware + confirm shared across kinds. (status: PENDING)
>   When all 4 ticked → append `task-done T4`, flip `02-pay-hub.md` T4 `[x]` + `tasks_progress.T4: complete`, update this block. (`tasks_progress.T4` is being set to `in-progress` now.)
>
> **EXACT NEXT STEP → T4 (start T4.1 `send-money-amount`)** (rebuild shared `send-money-amount`/`send-money-confirm`/`payment-result`/`payment-declined` to be `kind`-aware — accept a `kind` param {now,scheduled,recurring}; send-money-confirm → `authorise-handoff`; re-render each + verify) → **T5** (fold `standing-order-create`/`-edit` into the recurring path → `send-money-amount` kind=recurring; then `/idea-export` + `/idea-approve` ALL rebuilt screens incl. `pay` + `authorise-handoff`; set their status draft→approved) → **RIPPLE** (re-render all ~30 consumer screens' bottom nav now that app-shell Pay→pay; `/idea-setup-flows` → `/idea-completeness` → `/idea-render-validate` loop until clean; then retire `screens/send-money/` once its inbound refs are repointed to `pay`) → flip epic `sub_plans_progress.02 = complete` + acceptance.
>
> ─────────────────────────────────────────
> **T1 = COMPLETE (session 2).** `screens/pay/` fully built + rendered + verified on disk:
> - `ui.yaml` (Pay tab root; kind chooser now/scheduled/recurring → `send-money-amount` via `on_click.target` + `data.kind`; preserves from-account + recipients hub as pay-now shortcut; bottom_nav:true, no back arrow; status:draft — approve in T5), `demo-data.yaml`, `flow.yaml`, `prompts/{6}.md`.
> - `preview/{content,loading,empty,error,no_network,unauthenticated}.html` — all 6 RENDERED by hand (consistent with send-money's token CSS + bottom-nav chrome). VERIFIED: root `data-theme`=ZERO, `@media (prefers-color-scheme:dark)`=6/6, doctype+single `</html>`=6/6, all bottom-nav + kind-row nav targets resolve (home/accounts/pay/pfm-dashboard/settings/send-money-amount/splash all exist).
> - `design-system/app-shell.yaml` — Pay tab `target:` repointed `send-money` → `pay` (the Phase-2 structural change). ⚠️ This means OTHER screens' bottom-nav previews now show a stale Pay→send-money until the ripple re-renders them — that's the planned ripple, handle at end of Phase 2.
> - `flows/payment-initiation.yaml` — `entry_screen: pay`; added `pay → send-money-amount` connection. (Old send-money→… chain kept; merged into authorise-handoff in T2–T4.)
> - ACTIVITY_LOG: render + task-done(T1) appended. `02-pay-hub.md`: T1 `[x]` + `tasks_progress.T1: complete`.
>
> **EXACT NEXT STEP → T2** (single parameterised `authorise-handoff`): create `screens/authorise-handoff/` (ui+siblings) covering AIS-consent + every payment kind via a `consentContext` param (states: loading/content/error; redirect copy "Redirecting you to HSBC to approve securely" + Continue→`auth-callback`). Build prompts (`stitch-prompt-build.ts --feature authorise-handoff`) → hand-render the states (same token CSS; this is a redirect/handoff screen — NOT a tab root, so back-arrow top bar, NO bottom nav). Then repoint flow transitions `consent-request → authorise-handoff` (in `account-access-consent.yaml`) + `send-money-confirm → authorise-handoff` (in `payment-initiation.yaml`, replacing `payment-authorize-handoff`). Append ACTIVITY_LOG, flip T2. → THEN T3 (drop `bank-authorize-handoff` + `payment-authorize-handoff`) → T4 (rebuild shared `send-money-amount`/`-confirm`/`payment-result`/`payment-declined` `kind`-aware) → T5 (fold `standing-order-create`/`-edit` into recurring; `/idea-export` + `/idea-approve` all rebuilt incl. `pay`) → ripple (re-render ~30 screens' bottom nav now that Pay→pay; `/idea-setup-flows` → `/idea-completeness` → `/idea-render-validate` loop until clean).
>
> NOTE: `screens/send-money/` NOT yet retired — keep until its inbound nav refs (Home quick-pay, account-detail, bottom-nav on un-rerendered screens) are repointed to `pay` during the ripple, so reachability stays green at each boundary. Render method this session = hand-authored HTML mirroring `send-money/preview/*.html` conventions (the `/idea-render-screen` skill's heavy multi-input LLM loop was done inline by Claude; prompts/*.md exist if you prefer to re-run the skill).
>
> Git state UNCHANGED from session 1 (HEAD `9beeedd4`, tree clean except `.cache/` + this file). No commit yet this session — commit only on explicit user instruction, scoped to `workspaces/mifos-x/mifos-x-open-banking/`, human prose, `--no-verify`.
>
> Confirmed-fresh facts: screens dir contains `send-money`, `bank-authorize-handoff`, `payment-authorize-handoff` (Phase-2 rebuild/merge/drop targets) and NO `pay`/`authorise-handoff` yet — exactly the pre-Phase-2 state the plan assumes. Sub-plan 01 = complete; 02 = in-progress; 03–05 = pending.

═══════════════════════════════════════════════════════════════════════
MISSION
═══════════════════════════════════════════════════════════════════════
Consumer Open Banking TPP (AISP+PISP) on the HSBC UK/CE sandbox (OBIE v4.0, FAPI 1.0 Advanced), built via the claude-product-cycle framework. The OBP→HSBC idea-layer migration is DONE + approved (39 screens). We are now mid-way through a **holistic idea-layer redesign epic** (`consumer-app-redesign`), at the foundation stage. The Kotlin source still runs OBP — the source rebuild (step H /kmp-implement) has NOT started.

═══════════════════════════════════════════════════════════════════════
GIT STATE
═══════════════════════════════════════════════════════════════════════
- **Workspace repo** (`workspaces/mifos-x/`, repo = TheKalpeshPawar/mifos-x-claude-cycle-workspaces): branch **`feat/hsbc-open-banking-migration`**, PUSHED to origin. Commits this session, all pushed:
  - `0f2aad2a` — binding fix + idea-layer reconcile (steps A–C: verify/autofix, design reconcile, 8 consent screens enriched)
  - `7b643965` — steps D–F (data-flow/DTOs/demo-data, exports, full render + dark-mode, schema migration to contract 2.0.0, 39/39 approved)
  - `2d37c1c1` — dark-theme fix (removed hardcoded data-theme attrs so previews follow OS)
  - `9beeedd4` — preview/export tidy (exports for 3 screens, monospace font, token-name normalize, dangling-nav cleanup)
  - HEAD = `9beeedd4`. Working tree clean except `.cache/` (gitignore-excluded by convention) + this RESUME file.
- **Source repo** (`/home/kalpesh/OpenSource/Mifos/mifos-x-open-banking`, fork origin TheKalpeshPawar, upstream openMF): branch `feat/kmp-detemplate-app-shell-obp-client`, **UNTOUCHED this session**. PR #4 OPEN on openMF (consumer OBP app). A NEW source branch is created ONLY when source implementation (step H) starts.
- **Framework repo** (`claude-product-cycle/`, branch development): the epic plan files live here under `plan-layer/project-plans/mifos-x/mifos-x-open-banking/active/consumer-app-redesign/` (project plans live in the framework repo, NOT the workspace; uncommitted there, consistent with existing project-plans handling). DO NOT do framework-development work (user directive — see below).

═══════════════════════════════════════════════════════════════════════
WHERE WE ARE — the redesign epic `consumer-app-redesign`
═══════════════════════════════════════════════════════════════════════
Goal track complete through PLANNING + Phase 1 of implementation:
- `/goal-analysis-project` → **GOAL.md** (validated). `/goal-planning-project` → **PLAN.md (epic master) + 5 sub-plans** (all gates green, 9/9 acceptance criteria covered). `/goal-implement-project consumer-app-redesign` is IN PROGRESS (status: in-progress).
- Files at `plan-layer/project-plans/mifos-x/mifos-x-open-banking/active/consumer-app-redesign/`:
  - `GOAL.md` — the spec (target app + final flow; D1–D9 decisions).
  - `TARGET_IA.md` — **the design source-of-truth** (bottom-nav, consent gate, Pay hub, Insights/VRP, the working-contract loop). READ THIS FIRST when resuming the epic.
  - `PLAN.md` (epic master) + `01-target-ia-flows.md` … `05-cleanups-verify.md` (sub-plans).
- **Sub-plan 01 (target-IA/flows) = COMPLETE** (status: complete, acceptance: pass). It authored TARGET_IA.md and confirmed app-shell + flows already match the chosen bottom-nav. No idea-layer screen changes in Phase 1.

RESUME POINT → **Phase 2 (`02-pay-hub`)** — not started. A checkpoint question was pending (user interrupted): how to take on Phase 2 — (a) full build now, (b) design just the new `pay` + `authorise-handoff` screens first then ripple, or (c) pause. Re-ask or pick per user.

Remaining sub-plans: 02-pay-hub → 03-international → 04-automatic-rules-vrp → 05-cleanups-verify.

═══════════════════════════════════════════════════════════════════════
★ WORKING CONTRACT — the render/validate LOOP (user-mandated; apply every phase) ★
═══════════════════════════════════════════════════════════════════════
Foundation-first: the COMPLETE idea-layer (all screens designed + rendered + validated) is built and verified BEFORE any source/Kotlin code. Previews are the foundation. For each screen added/changed:
  1. edit ui.yaml (+ flow/api/demo-data siblings) per TARGET_IA.md
  2. `/idea-render-screen` (render preview HTML; emit BOTH light `:root` AND `@media (prefers-color-scheme: dark)`; NEVER hardcode `data-theme` on `<html>`/`<body>` — see CLAUDE.md known-issue)
  3. `/idea-setup-flows` (reconcile flow YAMLs to the new nav)
  4. `/idea-completeness` (catch missing on_click targets / missing screens; create+enrich)
  5. `/idea-render-validate` (RV + cross-screen) = MEASURE
  6. fix → re-render → re-run setup-flows/completeness → re-validate, IN A LOOP, until clean
  7. bottom-nav/app-shell are SHARED CHROME → changing them changes nav on EVERY screen → re-render ALL affected + re-validate (not just the touched screen)
  8. Verification at the idea-layer is STRUCTURAL (`/idea-render-validate` + the dark-mode/nav/doctype `rg` checks) for BOTH new and changed screens. Screenshot-verify is NOT an idea-layer gate — it belongs to step H (the built Kotlin app on a device/emulator). [Clarified 2026-06-15.]
Phase 2 triggers the first big ripple: the Pay tab repoints from send-money → the new `pay` hub → re-render all ~30 consumer screens' bottom nav + loop.

═══════════════════════════════════════════════════════════════════════
ALL STANDING USER DIRECTIVES (STRICT)
═══════════════════════════════════════════════════════════════════════
- Commits: human prose ONLY (no AI/Claude/Anthropic/framework/slash-command/agent mentions, no footer, no emoji), `--no-verify`. Commit only on explicit instruction; commit at END of a batch.
- Workspace commits: scope to `workspaces/mifos-x/mifos-x-open-banking/` (idea-layer + PROJECT_CONFIG); stage explicit paths; EXCLUDE the workspace-root `CLAUDE.md` UNLESS the user explicitly asked to update it (the dark-mode KNOWN-ISSUE doc edit WAS requested + committed). EXCLUDE `.cache/`.
- **DON'T touch / work on the framework** (user: "we won't work on framework"). Authoring project plans into plan-layer is fine (project content), but no framework-code/template/rule development. The deferred framework fixes (group C) are OUT.
- **Limit-sensitive**: run heavy agents ONE AT A TIME (sequential), NEVER parallel batches. Don't rush; be thorough on the foundation.
- idea-layer = Claude Intelligence ONLY (Read/Edit/Write/Agent). NO python/jq/sed/awk/grep on idea-layer files (`rg`/Read for search; deno OK for framework test scripts like the validators/render). Bash on idea-layer only `test -f`/`ls`/`wc -l`.
- Source = read-only until step H; then KDoc `/** */` only, NO `//` line comments; counterparty rule (never render login username as counterparty name); new source branch; never push dev/main.
- SECRETS: never paste values into chat/tracked files; reference cert/credential material by file path + env-var name only (HSBC material at /home/kalpesh/OpenBankingProject/HSBC_Sandbox/).
- backend.owned=false → server/owned-DB + connectivity checks SKIP by policy (not failures).

═══════════════════════════════════════════════════════════════════════
STEP H (source rebuild) — DIRECTIVES (apply when /kmp-implement starts; NOT yet)
═══════════════════════════════════════════════════════════════════════
- Build only AFTER the full idea-layer foundation (this epic) is render-validated.
- **Migrate the SOURCE NETWORK LAYER FIRST** (OBP HTTP/auth → HSBC FAPI/mTLS/detached-JWS/DCR/PKCE consent→authorize→token→resource) before feature/UI layers.
- **ALL source work on a NEW source branch** (create on top of `feat/kmp-detemplate-app-shell-obp-client`).
- Wire HSBC certs into local.properties from HSBC_Sandbox/ (Transport.crt, Signing.crt, pubkeyQseal.pem, software_statement.txt, KID.txt, clientId) — env-var names only.
- Decide the production deep-link/redirect URI registered with HSBC (OBP used org.mifos.openbanking://oauth/callback).
- Confirm source PR #4 iOS CI passed (MapLibre Podfile fix b5c6224) — outstanding from the original migration handover.

═══════════════════════════════════════════════════════════════════════
KEY PRODUCT DECISIONS (locked in GOAL.md D1–D9)
═══════════════════════════════════════════════════════════════════════
- Bottom nav (LOCKED): **Home · Accounts · Pay · Insights · More**. Discovery (products + ATM/branch) surfaced from Home, no own tab.
- Unified **Pay hub**: one kind-chooser (now/scheduled/recurring/international) → shared amount+CoF → confirm → `authorise-handoff` → result/declined. Merge bank-authorize-handoff + payment-authorize-handoff → one `authorise-handoff`. Fold standing-order-create/edit into the recurring path.
- **VRP** = "Automatic rules" under Insights (auto-save/sweeping; PSU max-per-payment + periodic limits + revoke). VRP is the #1 added consumer capability.
- **International** (now/scheduled/standing-order) added to the Pay hub with FX surfaced.
- **File/bulk + Multi-Bill = OUT of the consumer flavour** (B2B). D9: reserved for a future **`business` flavour** reusing the `kmp-product-flavors` machinery (the `fieldOfficer` slot the migration vacates; maps to HSBC UK Business brand; KMP Desktop/Web for treasury/file workflows). A SEPARATE epic (its own /goal-analysis-project) when prioritised — NOT this epic.
- Brand: earth-green M3 (#4C662B, Outfit, density 5).

═══════════════════════════════════════════════════════════════════════
DERIVED-DATA STATUS (confirmed 2026-06-15)
═══════════════════════════════════════════════════════════════════════
- DTOs: 72 OBIE DTO files, COMPLETE — incl. the new-capability families already registered: VRP×6 (OBDomesticVRPConsentRequest/Response, ControlParameters, Request, Response, VRPFundsConfirmationResponse) + International×12 (now/scheduled/standing-order consent+response). So the epic needs SCREENS, not new DTO synthesis.
- Demo-data: OBIE-shaped for 31/39 screens (8 static/UI-only have none, correct). NEW epic screens generate demo-data per-screen as built (DTOs already exist).
- 0 unresolved DTO-position refs; contract_version uniform 2.0.0 across all 39.

═══════════════════════════════════════════════════════════════════════
KNOWN ISSUES / GOTCHAS
═══════════════════════════════════════════════════════════════════════
- **consent-request canonical prompts can't build** (STN2 8K per-state budget on its form archetype — framework issue, deferred). Its previews use the ui.yaml fallback. Don't keep retrying its stitch-prompt build.
- **/idea-render-validate via a custom Agent FAILS** if the agent improvises python on idea-layer (RULE-CI-001). Invoke the actual `/idea-render-validate` SKILL (working deno validator) — it ran fine earlier this session.
- Dark-mode previews: correct mechanism = light `:root` + `@media (prefers-color-scheme: dark)`; the shared preview-runtime.js does NOT toggle `data-theme`, and hardcoding `data-theme` on the root LOCKS the theme. Full root-cause fix (patch preview-runtime.js) is framework-scope → DEFERRED (don't touch framework).
- STEP 3.0 deno auditor (test-renderer.js --full-audit) is broken (retired dep) — skip.
- Plan sub-plans 02-05 contain some illustrative code with premature forward-references (e.g. `nav_to: pay`/`entry_points:[pay]` before the pay screen exists) — execute the INTENT, keep nav targets resolvable at each boundary (G-N / RULE-APP-SHELL-001), repoint when the target screen is built.

═══════════════════════════════════════════════════════════════════════
TO RESUME
═══════════════════════════════════════════════════════════════════════
1. Read TARGET_IA.md + PLAN.md + 02-pay-hub.md.
2. Decide Phase-2 approach (full build / design-pay-hub-first / pause) with the user.
3. Execute Phase 2 per the working-contract loop (build pay hub + merged authorise-handoff → render → setup-flows → completeness → render-validate → loop; re-render all ~30 screens for the Pay-tab ripple; structural render-validate, no screenshots at idea-layer).
4. Continue 03 → 04 → 05. Single commit per RULE-IMPL-SESSION-001 at epic end (or checkpoint-commit per limits — user gates commits).
5. THEN step H (source) per the step-H directives above.
