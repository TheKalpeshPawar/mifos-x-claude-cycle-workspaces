## HSBC source build (step H) — active plan

The Kotlin source migration from OBP → HSBC UK/CE OBIE sandbox (FAPI 1.0 Advanced) is planned in
**`plan-layer/project-plans/mifos-x/mifos-x-open-banking/active/hsbc-source-implementation/PLAN.md`**
(framework repo). Read it before any `source/` work. Highlights: network-layer-FIRST (mTLS +
`private_key_jwt` PS256 + detached-JWS for PISP writes + OAuth2/PKCE), then consent→authorise→callback,
then OBIE DTOs/repos, then features (each gated on a real-HSBC-endpoint smoke probe + a per-screen
**source-phase screenshot-verify** against the idea-layer preview). Verified live 2026-06-15: auth +
`POST /aisp/account-access-consents` → 201/AWAU. New source branch `feat/hsbc-obie-fapi-network` on top of
`feat/kmp-detemplate-app-shell-obp-client`. Certs/keys by path/env-var only (HSBC material at
`/home/kalpesh/OpenBankingProject/HSBC_Sandbox/` + key `/home/kalpesh/OpenBankingProject/mifos-sandbox.key`).

<!-- code-review-graph MCP tools -->
## MCP Tools: code-review-graph

**IMPORTANT: This project has a knowledge graph. ALWAYS use the
code-review-graph MCP tools BEFORE using Grep/Glob/Read to explore
the codebase.** The graph is faster, cheaper (fewer tokens), and gives
you structural context (callers, dependents, test coverage) that file
scanning cannot.

### When to use graph tools FIRST

- **Exploring code**: `semantic_search_nodes` or `query_graph` instead of Grep
- **Understanding impact**: `get_impact_radius` instead of manually tracing imports
- **Code review**: `detect_changes` + `get_review_context` instead of reading entire files
- **Finding relationships**: `query_graph` with callers_of/callees_of/imports_of/tests_for
- **Architecture questions**: `get_architecture_overview` + `list_communities`

Fall back to Grep/Glob/Read **only** when the graph doesn't cover what you need.

### Key Tools

| Tool | Use when |
| ------ | ---------- |
| `detect_changes` | Reviewing code changes — gives risk-scored analysis |
| `get_review_context` | Need source snippets for review — token-efficient |
| `get_impact_radius` | Understanding blast radius of a change |
| `get_affected_flows` | Finding which execution paths are impacted |
| `query_graph` | Tracing callers, callees, imports, tests, dependencies |
| `semantic_search_nodes` | Finding functions/classes by name or keyword |
| `get_architecture_overview` | Understanding high-level codebase structure |
| `refactor_tool` | Planning renames, finding dead code |

### Workflow

1. The graph auto-updates on file changes (via hooks).
2. Use `detect_changes` for code review.
3. Use `get_affected_flows` to understand impact.
4. Use `query_graph` pattern="tests_for" to check coverage.

## Code style: comments (user directive, 2026-06-07 — HARD RULE)

When writing or editing source code in this workspace (all `source/` repos, all languages):

- **NEVER add `//` line comments.** No end-of-line comments, no `// explanation` above statements, no commented-out code.
- **The ONLY permitted comment form is `/** … */` KDoc** on declarations (classes, functions, properties, files). If something inside a function body needs explaining, explain it in the declaration's KDoc instead — or restructure the code so it doesn't need explaining (extract a well-named function/val).
- License headers stay as-is (`/* … */` block at file top).
- Scope: applies to NEW and EDITED code. Do NOT mass-rewrite existing `//` comments in untouched code; remove/convert them only in lines you are already changing.
- **KDoc quality bar**: a KDoc must read as documentation, not a relocated `//` comment. First line = a short summary of WHAT the declaration is/does; body = the behavior contract in terms of its parameters (use `[param]` links). No design-session context ("like the reference design", "per the screenshot"), no narration of internals the caller can't observe.

## Counterparty display names (user directive, 2026-06-07 — HARD RULE)

OBP stamps the LOGIN USERNAME (e.g. `afternooncoffee`) into `other_account.holder.name` whenever the counterparty has no public holder — which covers every transfer between the user's own accounts and most sandbox merchant rows.

- **NEVER render the login username as a counterparty name** anywhere in the app (transaction history, detail, tags, PFM merchant lists, standing orders, any future surface).
- Display precedence: resolved destination **account holder name** (Owner customer-account link legal name, account label fallback) → real non-placeholder holder → transaction description.
- Resolution infrastructure: `core/data/.../transactions/CounterpartyNameResolver.kt` — mirror-joins self-transfers across the user's own accounts (same description + completed timestamp, negated amount) to map the obfuscated `other_account.id` to a real account, persists learned names in the Room cache. Display helper: `counterpartyDisplayName(...)` in `feature/transactions/TransactionsFormat.kt`. New surfaces must reuse these, not re-derive from `holder.name`.

## Idea-layer preview dark-mode — KNOWN ISSUE (2026-06-15)

Preview HTML dark mode is fragile. The render template (`layers/idea/templates/prototype-render/PROMPT_SCREEN.md`) prescribes the `:root[data-theme="dark"]` toggle mechanism, but the shared `idea-layer/preview/_shared/preview-runtime.js` (the byte-identical, SHA-pinned framework runtime) **never sets `data-theme`** — there is no OS-preference sync and no in-app toggle. So a `:root[data-theme="dark"]` block alone is **dead CSS in the preview** — it never activates.

Consequence: a preview only renders dark if its HTML *also* contains an `@media (prefers-color-scheme: dark)` block (auto-follows the OS). The render agents emit this inconsistently, so some screens render dark and some don't, even though all carry the `[data-theme="dark"]` palette.

**When rendering/validating previews:**
- A screen state is dark-capable ONLY if its `preview/{state}.html` contains `@media (prefers-color-scheme: dark)`. Checking for `[data-theme="dark"]` alone is misleading (RV-023 false-passes on it).
- `/idea-render-screen` for this project MUST emit BOTH the `@media (prefers-color-scheme: dark)` block AND the `[data-theme="dark"]` block, and self-verify the `@media` block is present per file before finishing (`design_read.theme = auto` ⇒ dark must auto-follow the OS).
- Proper root-cause fix (deferred, framework-scope): patch `preview-runtime.js` to sync `data-theme` to `matchMedia('(prefers-color-scheme: dark)')` — that would activate the existing `[data-theme]` blocks on every screen at once with no re-renders, but it touches the SHA-pinned framework template (`layers/idea/templates/preview/_shared/preview-runtime.js`) so it needs a framework change + re-propagation. Until then, renders must include `@media`.

**Second pitfall — NEVER hardcode `data-theme` on the root element (2026-06-15).** Some renders emitted `<body data-theme="light">` or `<html data-theme="dark">`. Because the CSS has matching `[data-theme="light"]`/`[data-theme="dark"]` blocks, that attribute PINS one palette on the whole document and **overrides the `@media (prefers-color-scheme: dark)` flip** — the screen is stuck light (or stuck dark) and ignores the OS. This is what made `accounts`/`beneficiaries` render light-only and `direct-debits`/`standing-orders`/`pfm-dashboard`/etc. render dark-only. Fix: the root `<html>`/`<body>` MUST have NO `data-theme` attribute — leave it to `:root` (light default) + `@media` (auto dark). Verify after render: `rg '<(html|body)[^>]*\sdata-theme=' screens/*/preview/*.html` must return ZERO.
