# CLAUDE.md — Atlan AI Agent Quick Reference (Claude Code Edition)

> **Version:** 6.1 | **Updated:** 2026-03-26  
> **Full Policy:** See `AGENTS.md` for all domain-specific rules and checklists.  
> **Security Contact:** Slack `#bu-security-and-it`

---

## Project Overview

The **Atlan MCP Cookbook** — 33 tested recipes for putting your company's context to work through
the [Atlan MCP](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview),
from inside whatever AI tool you already build in.

This repo is a **read-only published mirror** of [atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/).
Recipes are written and tested against a live Atlan tenant on the website, then refreshed into here.
There is no application code, no runtime, no dependencies and no secrets — Markdown plus one JSON index.

| Path | What it is |
|---|---|
| `recipes/` | 33 recipes, one Markdown file each — YAML front matter + numbered steps |
| `recipes.json` | machine index: facets, summaries, hero prompts, `start_here`, `prerequisite_index` |
| `.claude/skills/find-a-recipe/` | routing skill — reads the index, picks the recipe for a job and role, hands over the prompt |
| `images/` | Atlan brand assets (light/dark logo) |
| `.github/workflows/` | the recipe auto-close workflow (the only executable surface in the repo) |

## Project Commands

Nothing here builds, tests, lints or deploys. The useful commands are validation and use:

```bash
jq -e . recipes.json >/dev/null              # index parses
jq -r '.recipes[].slug' recipes.json         # list every recipe slug
claude                                        # then describe a problem — the skill routes you
cp -r .claude/skills/find-a-recipe ~/.claude/skills/   # use the skill outside this repo
```

Consistency checks worth running after a refresh from the website:

```bash
[ "$(jq -r .recipe_count recipes.json)" = "$(ls recipes/*.md | wc -l | tr -d ' ')" ]  # counts agree
jq -r '.recipes[].slug' recipes.json | while read s; do [ -f "recipes/$s.md" ] || echo "no file: $s"; done
```

## Coding Conventions

- **Never hand-edit `recipes/` or `recipes.json`.** Both are generated from the website and are
  overwritten on the next refresh. Real fixes are made on atlan.com.
- **Keep `<placeholders>` intact** when handing a prompt to someone. A prompt still containing
  `<schema>` is the intended state — substitute only what the user has actually told you.
- **Relative links only** (`./recipes/…`, `images/…`) so they resolve both on GitHub and in a clone.
- Recipe front matter is a fixed set: `name, slug, number, summary, job, action, personas, effort,
  runs_in, requires, start_here, source_url, related`.
- Prose voice: second person, plain English, no hype. Recipes are written to be pasted, not admired.
- Changes land as **direct commits to `main`**. PRs touching generated content are closed automatically.

## Architecture Notes

Content flows one way — **atlan.com → sync → this repo**. The website is the source of truth and this
repo is a distribution copy, so there is deliberately no write path back.

The facets in `recipes.json` are the routing keys the skill uses: `job` (5 values), `action`
(Look up 19 / Make changes 14), `persona` (5), `effort` (Quick 14 / Moderate 18 / Involved 1).
`requires` — declared by 27 of the 33 recipes — plus `prerequisite_index`
(`glossary, lineage, owners, tags, documentation, domains, data_quality`) tell a reader what must
already exist in their tenant; `start_here` lists the 6 recipes that assume nothing and work on day one.

The only executable surface is `.github/workflows/close-recipe-prs.yml`. It runs on
`pull_request_target` — required, because a fork PR's default token is read-only and cannot comment
or close — and therefore **must never gain an `actions/checkout` step**: it reads changed filenames
from the API and never fetches or executes PR code. Permissions are scoped to `contents: read` /
`pull-requests: write`.

---

## Security Quick Reference

### Tags

`[MUST]` = required | `[REDLINE]` = forbidden | `[SHOULD]` = best practice

### Always-Check Invariants (Every Change)

1. **[MUST] No secrets** in code, config, logs, CI output, or `.env` files in version control.
2. **[MUST] Auth & authz must be real** — every protected endpoint must verify identity (JWT, OAuth, API key, session, OIDC, etc.) and enforce permissions. No phantom middleware.
3. **[MUST] No wildcards** — no `CORS: *`, `Action:"*"`, RBAC `resources:["*"]`, or `write-all`.
4. **[MUST] No untrusted execution** — no `eval`, unsafe deserialization, command injection, or CI `run:` injection.
5. **[MUST] Pin supply chain** — actions→SHA, images→version/SHA, no `latest`, verify deps exist.

### Conditional Checks (When Relevant)

| When you see... | Check |
|-----------------|-------|
| DB queries | **[MUST]** Parameterized only; tenant/org scoping if multi-tenant |
| New API endpoint | **[MUST]** Auth, authz, input validation, rate limiting — all before merge |
| Auth/session code | **[MUST]** Validate credentials properly (JWT, API key, OAuth, session — whatever the service uses). Tokens must expire. **[SHOULD]** Use established auth libraries. |
| Error responses | **[MUST]** Generic to clients; no internals leaked |
| Outbound HTTP with user input | **[MUST]** Allowlist hosts; block internal/metadata IPs |
| Logging | **[REDLINE]** Never log tokens, cookies, secrets, Authorization headers |
| Dependencies | **[MUST]** Block CRITICAL/HIGH CVEs; check typosquatting |
| CI/CD workflows | **[MUST]** Pin actions to SHA; minimum permissions; no injection |
| Helm/K8s | **[MUST]** Non-root, read-only FS, drop all caps; least-privilege RBAC |
| Frontend | **[REDLINE]** No `dangerouslySetInnerHTML`/`v-html`/`innerHTML` with user data. **[MUST]** No tokens in localStorage/sessionStorage. Validate redirects. CSRF if cookie auth. Sanitize rich text (DOMPurify). **[SHOULD]** Strict CSP; no source maps in prod; no PII in client state/URLs. |
| AI/LLM | **[MUST]** No raw user input in system prompts. Mask PII/secrets before LLM calls. Sanitize output before UI rendering. No LLM output for auth decisions. No customer data to external LLMs without approval. **[REDLINE]** LLM output to `eval`, SQL, shell, or `innerHTML`. **[SHOULD]** Rate limit LLM API calls. |

> For full details on each domain, see `AGENTS.md § Conditional Checks`.

### Severity & Response

| Severity | Action |
|----------|--------|
| **CRITICAL** | **Block.** Fix immediately. No opt-out. |
| **HIGH** | **Block.** Fix before merge. No opt-out. |
| **MEDIUM** | Flag with recommended fix. Can be follow-up. |
| **LOW** | Note briefly. |

### Review Output (MEDIUM+)

```txt
🔒 SECURITY REVIEW
Issue: [description]
Severity: CRITICAL | HIGH | MEDIUM
Location: [file:line]
Risk: [what attacker gains]
Fix: [concrete fix — implement immediately for CRITICAL/HIGH]
```

### Existing Violations

- **In your diff:** Fix or flag with 🔒 format.
- **Outside your diff:** Note briefly. Don't refactor without approval.
- **Never** use existing violations to justify new ones.

### Manual Security Review

Reach out to `#bu-security-and-it` before merging when changes touch auth/authz, multi-tenant isolation, secrets management, new public endpoints, or anything you're unsure about.