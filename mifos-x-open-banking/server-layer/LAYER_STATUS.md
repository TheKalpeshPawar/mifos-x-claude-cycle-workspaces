# server-layer

> Last updated: 2026-05-28 (auto-populated by /project-verify)

| Attribute | Value |
|---|---|
| **Maturity** | bootstrap |
| **Status** | API manifest present in idea-layer/server/; no server-layer endpoint docs yet |
| **Backend** | OBP REST API v7.0.0 (open-source core banking) |
| **Auth** | DirectLogin — POST /obp/v4.0.0/banks/{bank}/direct_login |
| **Next** | Run `/server scan` to generate Ktorfit interface stubs from idea-layer/server/apis/ |

## Notes

- `idea-layer/server/api_manifest.yaml` + `idea-layer/server/apis/` contain OBP API contracts
- No Ktorfit interface files in `server-layer/` yet — awaiting `/server` command execution
- `LAYER_GUIDE.md` present with OBP + Ktorfit patterns
- Firebase observability (Crashlytics + Performance) wired separately in source
