# CLAUDE.md - sentinel Project

You are a team member on the sentinel project, not a tool.

## Project Identifiers

- **Repository:** `martymcenroe/sentinel`
- **Project Root (Windows):** `C:\Users\mcwiz\Projects\sentinel`
- **Project Root (Unix):** `/c/Users/mcwiz/Projects/sentinel`
- **Worktree Pattern:** `sentinel-{IssueID}` (e.g., `sentinel-22`)

## Project-Specific Context

**Stack:** Cloudflare Worker (JavaScript, ES Modules), entry point `src/index.js`. Tests via Vitest. Scripts in `scripts/` (bash). Deploy via `wrangler` (config in `wrangler.toml`).

PR Issue-Reference Enforcer — GitHub App on Cloudflare Workers. Ensures every PR references a GitHub issue (`Closes #N`) or explicitly opts out (`No-Issue: <reason>`).

### Architecture

| Component | Tech | Location |
|-----------|------|----------|
| CF Worker | JS (ES Modules) | `src/` |
| Tests | Vitest | `tests/` |
| Scripts | Bash | `scripts/` |

### Key Files

- `wrangler.toml` — CF Worker config
- `src/index.js` — Request router (`/webhook`, `/health`)
- `src/webhook.js` — HMAC signature verification + event dispatch
- `src/auth.js` — GitHub App JWT signing + installation tokens
- `src/checks.js` — Check Run creation via Checks API
- `src/validate.js` — PR body regex validation

### Development

```bash
npm test
npm run deploy
```

### Secrets (CF Worker)

- `WEBHOOK_SECRET` — GitHub webhook HMAC secret
- `APP_ID` — GitHub App ID
- `PRIVATE_KEY_B64` — PKCS#8 PEM private key, base64-encoded

## Workflow Overrides

_None yet. If this project needs to override any universal CLAUDE.md rule (e.g., a custom merge tool, a special test convention), document the override here with explicit language ("override") per ADR 0219._
