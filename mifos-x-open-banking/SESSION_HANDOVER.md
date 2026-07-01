# SESSION HANDOVER — mifos-x-open-banking (UK Open Banking AISP)

> Written 2026-06-29. Paste this to a fresh session to resume, or read top-to-bottom.
> Bind first: `/context-start mifos-x-mifos-x-open-banking`.

---

## 0. Mission

Build the **best-possible UK Open Banking AISP (Account Information) reference app** — a
Kotlin Multiplatform (Compose) client that consumes the **HSBC UK sandbox** strictly to the
**OBIE Read/Write v4.0** standard, demonstrating the **full AISP capability set**. Read-only:
**no payment initiation (PISP), no CBPII**. Built on the de-templated openMF KMP shell.

The framework project was **scrapped and rebuilt from scratch** this session (the user wanted a
clean slate). The real source repo was preserved throughout.

---

## 1. Where things stand (pipeline status)

| Stage | Status |
|---|---|
| Clean-slate scrap of old framework workspace/plans/bindings | ✅ done (backed up) |
| Project recreated + bound (`PROJECT_CONFIG`, `PROJECT.md`, source symlink, MATRIX, binding) | ✅ done |
| Research (HSBC AIS, source state, OB standards) | ✅ done |
| `idea-plan.yaml` authored | ✅ done — **18 features · 25 screens · 8 flows · 19 API endpoints** |
| Branding from Material theme (`#266489`) | ✅ done |
| `/idea-init` (CAPABILITY_STATE, Stitch infra, app-shell) | ✅ done |
| `/idea-import-api` (HSBC AIS v4.0 → REQUIREMENTS + api_manifest + apis) | ✅ done |
| `/design-system` (DESIGN.md + design-tokens + COMPONENTS + Stitch DS upload) | ✅ done |
| `/design-validate` | ✅ design system PASSES WCAG AA + M3; findings only on partial drafts |
| **Screen scaffolding** (`screens/{id}/`) | ⚠️ **NOT done** — only 2 partial drafts (`accounts`, `account-detail`) from interrupted subagents |
| `/idea-enrich`, render, mockups, approve, implement | ⛔ pending (need screens first) |

**The single biggest TODO: scaffold the 25 screens.** Nothing downstream (enrich/render/
export/sync) can run until `screens/{id}/` exist.

---

## 2. The product (final feature set — source of truth: `idea-layer/idea-plan.yaml`)

18 features, grouped by release phase:
- **P0 (MVP):** consent-onboarding (user-onboarding → login OAuth → consent), consent-dashboard,
  accounts, balances, transactions, settings, profile.
- **P1:** beneficiaries, standing-orders, direct-debits, scheduled-payments.
- **P2:** statements, product, party, multi-currency, atm-locator, offers, **pfm**.

25 screens, 8 flows (`onboarding-consent`, `account-browsing`, `transaction-review`,
`consent-management`, `recurring-and-statements`, `settings-and-profile`, `consent-expired`,
`pfm-review`).

**Key user corrections to honor:**
- **No bank-select screen** (HSBC only). Onboarding = `user-onboarding` → `login` (OAuth with HSBC).
- **Permission approval happens on HSBC's portal**, not in-app (the app sends a `Permissions[]`
  array in the consent; the PSU approves the set + selects accounts at the bank; reject → no token).
- **PFM feature** added (modelled on Tink's expense/income/categorization concepts — client-side,
  computed from transactions, no extra endpoint). TrueLayer demo was PISP-only (nothing to import);
  Tink Link is a consent orchestrator (PFM is in its backend reports). Screens: pfm-dashboard,
  spending-by-category, budgets, recurring-subscriptions.

---

## 3. HSBC AIS API (the backend we consume — external, not owned)

- **Resource base:** `https://sandbox.ob.hsbc.co.uk/mock/obie/open-banking/v4.0/aisp`
- **OAuth2 (v1.1):** `…/v1.1/oauth2/{token,authorize}` · **DCR (v3.2.1):** `…/v3.2/oauth2/register`
- **Auth:** FAPI 1.0 Advanced — mTLS + `private_key_jwt` + OAuth2 `authorization_code`+PKCE+signed
  request object, app-to-app SCA. **AIS is read-only → no detached `x-jws-signature`.**
- **19 endpoints** captured in `idea-layer/server/api_manifest.yaml` + `apis/account-information.yaml`
  + `idea-layer/REQUIREMENTS.md` (SFR-AIS-01..19), each mapped to its OBIE DTO + permission + consumer screens.
- DTOs (full Kotlin via `/idea-generate-dtos` later): OBReadConsentResponse1, OBReadAccount6,
  OBReadBalance1, OBReadTransaction6, OBReadBeneficiary5, OBReadStandingOrder6, OBReadDirectDebit2,
  OBReadScheduledPayment3, OBReadStatement2, OBReadProduct2, OBReadParty2/3, OBReadOffer1.

**Sandbox material on disk** (certs/keys by path/env-var only — NEVER inline values):
`/home/kalpesh/OpenBankingProject/HSBC_Sandbox/` — Transport.crt, Signing.crt, pubkeyQseal.pem,
`mifos-sandbox.key` (private), client_id.txt, KID.txt, software_statement.txt (SSA), Postman bundle.
Start docs: `docs/00-HOW-TO-USE-THE-SANDBOX.md`, `docs/01-account-information-sharing.md`.
Swagger: `/home/kalpesh/OpenBankingProject/specs/hsbc-sandbox/openapi/account-info-4.0-personal.yaml`
(+ `dcr-uk.yaml`). Sandbox accounts: CurrentAccount/Savings/CreditCard/Global Money/Global Wallet
(no loans/FD). Offers IS in the personal spec (not M&S-only).

---

## 4. Design system (done — full fidelity to the user's theme)

- **Source:** the user's exact Material Theme Builder export at
  `/home/kalpesh/OpenBankingProject/material-theme/ui/theme/` (Color.kt/Theme.kt/Type.kt), seed
  primary **#266489** (dark #95CDF7), Roboto, theme auto. Type.kt = default `Typography()`.
- **Generated:** `idea-layer/design-system/DESIGN.md` (@google/design.md spec, "Open Banking —
  Trust Blue", minimalist-ui, accessibility-first), `design-tokens.yaml` (29 light + 29 dark M3
  roles VERBATIM), `COMPONENTS.md`, `components/_index.yaml`.
- **Stitch DS uploaded:** project `mifos-x-open-banking-stitch-2026-06-29`
  (id 5458150709735075451), asset_id **8085591672064527850**.
- **Money semantics:** credit = primary, debit = error (no green/red). Amounts in Roboto Mono.
- `/design-validate`: WCAG AA 8/8 + M3 29+29 PASS. Other findings are on the 2 partial drafts only.

---

## 5. Git state (IMPORTANT)

- **Framework repo** (`/home/kalpesh/MobileByteSensai/claude-product-cycle`): on session branch
  **`claude-session-mifos-x-20260629154509571`** (off `development`). Many uncommitted changes
  (idea-layer, MATRIX.md, bindings, PROJECT_CONFIG, workspace CLAUDE.md edit, project-plans removal).
- **Workspace submodule** (`workspaces/mifos-x`): same session branch, idea-layer content uncommitted.
- **Source** (`/home/kalpesh/OpenSource/Mifos/mifos-x-open-banking`, branch `migration/hsbc-sandbox`):
  **fieldOfficer flavor removal COMMITTED** as `2f097c0 refactor(flavors): remove fieldOfficer
  flavor, consumer-only app` (compiles — `:cmp-navigation` built green). Otherwise untouched.
  **USER DIRECTIVE: do NOT touch the source or its branches** unless explicitly asked.
- **Branch hygiene:** old local feat branches `feat/hsbc-open-banking-migration` +
  `feat/sync-workspace-with-template-post-sync` were deleted locally (still on `origin/feat/*`).
- **Nothing pushed, no PRs.** Hard Rule #1 — NO autonomous commits/pushes; wait for explicit "commit".
- The write-tool hook (`check-git-session.sh`) blocks Write/Edit when the framework is on a
  protected branch with no `git_session` in the binding — currently fine (on the session branch;
  binding has `git_session.branch_name` set). If it ever re-blocks: stay on the session branch.

**Backups (this session, reversible):**
`/tmp/claude-1000/-home-kalpesh-MobileByteSensai-claude-product-cycle/eb44f7bd-…/scratchpad/scrap-backup-20260629/`
(scrapped workspace + project-plans + framework session-state tarballs).

---

## 6. Known issues / gotchas

1. **`idea-graph-audit.ts` is broken in this env** — `error: Could not find a matching package
   for 'npm:js-yaml@4.1.0'`. The whole matrix-driven `/idea sync` depends on it. **Fix needed**
   (`deno install` / add `"nodeModulesDir": "auto"` to the relevant deno.json) before `/idea sync`.
2. **No bulk "scaffold from plan" command works cleanly:** `/idea sync` STEP 2 scaffold is
   deprecated and presupposes existing screens; `/idea-add` HALTs on plan-duplicate names. The
   practical path used: dispatch `sonnet-router` subagents to emit the 8-file scaffold per screen
   (idea-add STEP 2.SCAFFOLD template) from the plan + api_manifest + design_read. **2 were
   interrupted mid-run** → `screens/accounts/` (8 files) + `screens/account-detail/` (5 files,
   partial) exist as drafts; the other 23 screens are not scaffolded.
3. **Stitch upload needs the key in env:** `design-md-upload.ts` reads `STITCH_API_KEY` from the
   process env, not `.env.stitch`. Load it inline:
   `STITCH_API_KEY="$(grep '^STITCH_API_KEY=' .../.env.stitch | cut -d= -f2- | tr -d '\r\n')" deno run …`
4. **RULE-CI-001:** NEVER use python/jq/sed/awk/bash to write/scan idea-layer files — Write/Edit
   tools (or Agent subagents) ONLY. (External files — swagger, theme, reference apps — are fine to grep.)
5. The bash **secrets-output guard** trips on the literal word `set` and on env-dumps — avoid `set -e`.

---

## 7. Reference material (audited / used this session)

- HSBC sandbox + specs: see §3.
- Material theme: `/home/kalpesh/OpenBankingProject/material-theme/ui/theme/`.
- Reference apps audited: `/home/kalpesh/OpenBankingProject/OSDemoApps/truelayer-android-sdk-demo/`
  (PISP-only — nothing imported) and `/home/kalpesh/OpenBankingProject/OSDemoApps/tink-link-android/`
  (consent orchestrator + PFM concepts → informed the PFM feature).
- Project source: `/home/kalpesh/OpenSource/Mifos/mifos-x-open-banking` — de-templated KMP shell
  (Kotlin 2.3.20, Compose MP 1.10.3, Ktor 3.3.3/Ktorfit, Koin, Room, androidx-nav; strong reusable
  `core-base/security` + `core-base/network` + `cmp-navigation` 44-route skeleton). **Zero Open
  Banking network/auth/data exists yet — all greenfield.** Comment style: KDoc-only, no `//` (user HARD RULE).
- Separate deliverable made this session: `/home/kalpesh/MobileByteSensei/next-commands.html`
  (full 361-command phased reference — unrelated to this project).

---

## 8. Next steps (recommended order)

1. **Fix the Deno dep** so `idea-graph-audit.ts` runs (unblocks the matrix + `/idea sync`).
2. **Scaffold all 25 screens** cleanly — fan out `sonnet-router` subagents by cluster (consent,
   accounts/txns, payments-context, statements/extras, settings/profile/pfm), each emitting the
   8-file set per screen from idea-plan + `server/api_manifest.yaml` consumers + design_read brand
   + realistic HSBC demo data (RULE-PROTO-CONTENT-001, canonical `on_click` object form). Overwrite
   the 2 partial drafts.
3. `/idea-generate-dtos` (full Kotlin DTOs from the swagger), `/idea-enrich` per feature (fixes the
   design-validate findings), `/idea-generate-data-flow`, `/idea-generate-demo-data`.
4. `/idea-render-screen --all` + `/idea-export-stitch` (mockups against the uploaded design system).
5. `/idea verify` → `/idea approve` (human gate) → `/implement` (FAPI network layer FIRST — mTLS +
   private_key_jwt + OAuth2/PKCE + account-access-consents — then AISP feature screens on the source).
6. When ready to commit: `/git-session-commit` (workspace + framework). Source commits stay on
   `migration/hsbc-sandbox` and only when the user says so.

---

## 9. One-line resume

> Bound project `mifos-x/mifos-x-open-banking`. Plan + API + design system are DONE and validated;
> the 25 screens are NOT scaffolded yet (2 partial drafts). Next: fix the deno `js-yaml` dep, then
> scaffold all 25 screens via subagent fan-out, then enrich → render/mockup → approve → implement.
> Source is at `migration/hsbc-sandbox` (fieldOfficer removed + committed); don't touch it without asking.
