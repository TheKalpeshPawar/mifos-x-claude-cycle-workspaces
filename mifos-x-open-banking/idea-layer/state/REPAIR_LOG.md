# REPAIR_LOG.md — state-repair audit trail

| Timestamp | Check | Action | Details |
|-----------|-------|--------|---------|
| 2026-05-27T17:30:00Z | stale-running | fixed | `idea-preview` running since 2026-05-25T15:35:17Z (>48h) → reconciled to `failure` |
| 2026-05-27T17:30:00Z | legacy-blocks | migrated | Top-level `design_system:` block → merged into `capabilities.design_system` with hashes |
| 2026-05-27T17:30:00Z | legacy-blocks | migrated | Top-level `verify:` block → merged into `capabilities.idea-verify.warning_summary` |
| 2026-05-27T17:30:00Z | duplicate-blocks | removed | Stale `capabilities.idea-sync` (2026-05-22, status: partial) removed; kept latest (2026-05-27, status: complete) |
| 2026-05-27T17:30:00Z | legacy-dashboard-removed | fixed | Deleted `dashboard/DEV_STATUS.md` + `dashboard/dev-status.html` + empty `dashboard/` dir (RULE-DASHBOARD-SINGLETON-001) |
