# CLAUDE.md - Sentinel

**Workflow:** Full AssemblyZero workflow. Read `C:\Users\mcwiz\Projects\AssemblyZero\WORKFLOW.md`.

---

## Project Identifiers

- **Repository:** `martymcenroe/sentinel`

---

## Project Overview

PR Issue-Reference Enforcer — GitHub App on Cloudflare Workers. Ensures every PR references a GitHub issue (`Closes #N`) or explicitly opts out (`No-Issue: <reason>`).

### Architecture

| Component | Tech | Location |
|-----------|------|----------|
| CF Worker | JS (ES Modules) | `src/` |
| Tests | Vitest | `tests/` |
| Scripts | Bash | `scripts/` |

### Key Files

- `wrangler.toml` — CF Worker config
- `src/index.js` — Request router (/webhook, /health)
- `src/webhook.js` — HMAC signature verification + event dispatch
- `src/auth.js` — GitHub App JWT signing + installation tokens
- `src/checks.js` — Check Run creation via Checks API
- `src/validate.js` — PR body regex validation

---

## Development

```bash
npm test
npm run deploy
```

### Secrets (CF Worker)

- `WEBHOOK_SECRET` — GitHub webhook HMAC secret
- `APP_ID` — GitHub App ID
- `PRIVATE_KEY_B64` — PKCS#8 PEM private key, base64-encoded
