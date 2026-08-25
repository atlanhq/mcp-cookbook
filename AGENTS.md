# AGENTS.md — Atlan AI Agent Guidelines

> **Version:** 6.1 | **Updated:** 2026-03-26  
> **Applies To:** All AI agents (Claude, GPT, Copilot, Cursor, Cline, etc.)  
> **Companion:** See `CLAUDE.md` for a lean quick-reference optimized for Claude Code.  
> **Security Contact:** Slack `#bu-security-and-it`

---

## Project Overview

The **Atlan MCP Cookbook** — 33 tested recipes for putting a company's own context to work through
the [Atlan MCP](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview),
from inside whatever AI tool the reader already builds in. Each recipe is a real workflow someone
runs: the problem it solves, the prompts to type, what to hand it, and what comes back.

This repo is a **read-only published mirror** of [atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/).
Every recipe is written and tested against a live Atlan tenant on the website, then refreshed into
here. That provenance is the point: a prompt that has not been through that testing would be
untested advice sitting next to tested advice, with no way for a reader to tell them apart.

There is no application code, no runtime, no build, no dependencies and no secrets in this repo —
Markdown, one JSON index, two SVGs, and a single GitHub Actions workflow.

| Path | What it is |
|---|---|
| `recipes/` | 33 recipes, one Markdown file each — YAML front matter + numbered steps |
| `recipes.json` | machine index: facets, summaries, hero prompts, `start_here`, `prerequisite_index` |
| `.claude/skills/find-a-recipe/` | routing skill — reads the index, picks the recipe for a job and role, hands over the prompt with placeholders intact |
| `images/` | Atlan brand assets (`atlan-logo-blue.svg`, `atlan-logo-white.svg`) |
| `.github/workflows/close-recipe-prs.yml` | closes PRs against generated content — the only executable surface here |
| `CONTRIBUTING.md` | why recipes are not edited in this repo, and how to report a broken one |

**Reading a recipe is not enough to run one.** Every recipe needs the Atlan MCP connected to the
reader's AI tool, and can only surface context that already exists in their tenant. If an asset is
undocumented, no prompt will invent its meaning — that absence is usually the finding, not a failure.

## Project Commands

There is nothing to build, test, lint or deploy. Commands that matter are validation and use:

```bash
jq -e . recipes.json >/dev/null              # index parses
jq -r '.recipes[].slug' recipes.json         # list every recipe slug
jq -r '.start_here[]' recipes.json           # the 6 day-one recipes
jq -r '.recipes[] | select(.action=="Make changes") | .slug' recipes.json   # the 14 that write back
claude                                        # then describe a problem — the skill routes you
cp -r .claude/skills/find-a-recipe ~/.claude/skills/   # use the skill outside this repo
```

After any refresh from the website, three checks catch a bad sync:

```bash
# 1. declared count matches files on disk
[ "$(jq -r .recipe_count recipes.json)" = "$(ls recipes/*.md | wc -l | tr -d ' ')" ] && echo ok

# 2. every indexed slug has a file
jq -r '.recipes[].slug' recipes.json | while read s; do [ -f "recipes/$s.md" ] || echo "no file: $s"; done

# 3. every relative link resolves from its own file's directory
find . -name '*.md' -not -path './.git/*' | while read f; do d=$(dirname "$f"); \
  grep -oE '\]\([^)#][^)]*\)' "$f" | sed -E 's/^\]\(//; s/\)$//' | grep -vE '^(https?|mailto):' | \
  while read l; do [ -e "$d/${l%%#*}" ] || echo "BROKEN $f -> $l"; done; done
```

## Coding Conventions

**Generated content is off limits.** Everything under `recipes/` and all of `recipes.json` is
produced from atlan.com. A change made here is overwritten on the next refresh and never reaches the
website or its readers. Do not hand-edit either, and do not offer to — route the fix to the website.
The one exception is repo-level metadata that the generator does not own (for example the `_comment`
provenance string).

**Handing over a prompt.** Keep `<placeholders>` intact. A prompt still containing `<schema>` is the
intended state — substitute only what the user has actually told you, and leave the rest for them to
fill. Never present an improvised prompt as one from the cookbook; if a prompt is your own, say so.

**Routing.** Only route to recipes that exist in `recipes.json`. Never invent a recipe. Offer every
recipe that fits, and state what it assumes rather than silently withholding it — a recipe someone
cannot run today still tells them what is worth building toward.

**Links.** Relative only (`./recipes/…`, `images/…`), so they resolve on GitHub and in a local clone
alike. Recipe-to-recipe links are bare filenames resolved from `recipes/`.

**Front matter** is a fixed set, in this order: `name, slug, number, summary, job, action, personas,
effort, runs_in, requires, start_here, source_url, related`.

**Voice.** Second person, plain English, no hype, no padding. Lead with the thing the reader wants.
Recipes are written to be pasted, not admired.

**Workflow.** Changes land as direct commits to `main`; this repo does not take pull requests, and
any PR touching generated content is closed automatically.

## Architecture Notes

Content flows one way:

```
atlan.com/mcp-cookbook  ──sync──▶  recipes/ + recipes.json  ──read──▶  find-a-recipe skill  ──▶  user
   (source of truth)                  (this repo, generated)              (routing only)
```

There is deliberately no write path back. This repo is a distribution copy — that is what makes the
"do not edit here" rule structural rather than a matter of etiquette.

**The index is the interface.** `recipes.json` carries `source`, `mcp_setup_url`, `recipe_count`,
`facets`, `start_here`, `prerequisite_index`, and a `recipes[]` array whose objects hold
`name, slug, number, summary, job, action, personas, effort, runs_in, requires, start_here,
step_count, hero_prompt, path, url, related`. Anything building on the cookbook should parse that
file rather than scraping the Markdown.

**Facets are the routing keys:**

| Facet | Values |
|---|---|
| `job` | Find & understand data (13) · Govern & keep trusted (7) · Make data understandable (6) · Change & fix data safely (4) · Retire & migrate (3) |
| `action` | Look up (19, read-only) · Make changes (14, writes back to Atlan) |
| `persona` | Data Engineer · Data/BI Analyst · AI Builder · Data Governance Lead · Data/Business User |
| `effort` | Quick (14) · Moderate (18) · Involved (1) |

`action` is the one worth checking before running anything: 14 recipes write back to Atlan.
Personas are a hint, not a gate — most recipes serve several.

**Readiness is modelled explicitly.** 27 of the 33 recipes declare a `requires`, keyed to
`prerequisite_index`: `glossary`, `lineage`, `owners`, `tags`, `documentation`, `domains`,
`data_quality`. Running a recipe in a tenant that has not built the thing it leans on returns a thin
answer, and a reader could reasonably conclude the whole cookbook does not work — hence `start_here`,
the 6 read-only recipes that assume nothing and work on day one in any tenant.

**Security posture.** No secrets, no credentials, no customer data, no code execution paths. The only
executable surface is `.github/workflows/close-recipe-prs.yml`, and it carries one hard invariant:
it triggers on `pull_request_target` — required, because a fork PR's default token is read-only and
cannot comment or close — which means it runs with base-repo privileges and access to secrets.
It therefore **must never gain an `actions/checkout` step**, and never fetches or executes anything
from the PR; it only asks the API which filenames changed. Permissions are scoped to
`contents: read` / `pull-requests: write`. If you touch that file, keep both the invariant and the
comment that explains it.

---

## Security

### How to Use This Section

1. **Every change:** Apply the 5 Always-Check Invariants.
2. **Based on what you're changing:** Apply the relevant Conditional Checks.
3. **When you find issues:** Use the Severity & Response rules.

**Tags:** `[MUST]` = required | `[REDLINE]` = forbidden | `[SHOULD]` = best practice

---

### Always-Check Invariants (Every Change)

1. **[MUST] No secrets** in code, config, logs, CI output, or `.env` files in version control.
2. **[MUST] Authentication & authorization must be real** — every protected endpoint must verify identity (JWT, OAuth, API key, session token, OIDC, or whatever mechanism the service uses) and enforce permissions. No "phantom auth" (imported but unused middleware).
3. **[MUST] No wildcards** — no `CORS: *`, `Action:"*"`, RBAC `resources:["*"]`, or GitHub `write-all`.
4. **[MUST] No untrusted execution** — no `eval`, unsafe deserialization, command injection, or untrusted input in CI `run:` blocks.
5. **[MUST] Pin supply chain** — actions→full SHA, images→version/SHA, no `latest`, verify deps exist and are reputable.

---

### Conditional Checks

Apply when the described pattern is present in the change:

| When you see... | Check |
|-----------------|-------|
| **DB queries** | **[MUST]** Parameterized only; scope to tenant/org if multi-tenant. **[REDLINE]** String concatenation with user input. |
| **Auth/session code** | **[MUST]** Validate credentials properly (JWT signature + claims, API key lookup, OAuth token introspection, session validity — whatever the service uses). **[MUST]** Tokens/sessions must expire. **[SHOULD]** httpOnly + secure + sameSite cookies for browser sessions. **[SHOULD]** Use established auth libraries, not hand-rolled crypto. |
| **New API endpoint** | **[MUST]** Must ship with authentication, authorization, input validation, and rate limiting. Not a follow-up. Add tenant scoping if the service is multi-tenant. |
| **Error responses** | **[MUST]** Generic to clients. **[REDLINE]** Stack traces, SQL, file paths, internal IPs in client responses. |
| **Outbound HTTP with user input** | **[MUST]** Allowlist hosts; block internal/metadata IPs (10.x, 172.16-31.x, 192.168.x, 169.254.169.254, localhost). |
| **Logging code** | **[REDLINE]** Never log tokens, cookies, secrets, Authorization headers, full request/response bodies. **[SHOULD]** Include contextual identifiers (tenant, user, request ID) in structured logs for audit. |
| **Dependency changes** | **[MUST]** Block CRITICAL/HIGH CVEs; flag MEDIUM. Check for typosquatting (new pkg, low downloads, similar name). Verify lockfile matches manifest. |
| **`.env` files** | **[MUST]** In `.gitignore`; `.env.example` has placeholders only. Block real secrets. |
| **CI/CD workflows** | **[MUST]** Pin actions to SHA. Minimum permissions. **[REDLINE]** PR metadata in `run:` blocks; `pull_request_target` with secrets + PR checkout; `write-all` permissions. |
| **Helm/K8s manifests** | **[MUST]** `runAsNonRoot`, `readOnlyRootFilesystem`, `allowPrivilegeEscalation: false`, `drop: ["ALL"]`. Least-privilege RBAC (Role over ClusterRole, no wildcards). **[REDLINE]** Secrets in `values.yaml`; `privileged: true`; `latest` tags. |
| **Shell scripts** | **[MUST]** `set -euo pipefail`. Quote variables. `mktemp` + cleanup trap. **[REDLINE]** `eval` with user input; `curl \| bash`; secrets in CLI args. |
| **Frontend code** | **[REDLINE]** `dangerouslySetInnerHTML`/`v-html`/`innerHTML` with user-controlled data. **[MUST]** No tokens/secrets in localStorage or sessionStorage. **[MUST]** Validate redirect targets against allowlist (prevent open redirects). **[MUST]** CSRF protection on state-changing requests if cookie-based auth. **[MUST]** Sanitize rich text with DOMPurify or equivalent before rendering. **[SHOULD]** Set strict CSP headers; avoid `unsafe-inline`/`unsafe-eval`. **[SHOULD]** No source maps in production. **[SHOULD]** Avoid exposing PII, internal IDs, or debug data in client state/URLs. **[SHOULD]** Use `rel="noopener noreferrer"` on external links with `target="_blank"`. |
| **IaC (Terraform/CF)** | **[MUST]** No public buckets. Encrypt at rest. Least-privilege IAM (no `Action:"*"`). **[SHOULD]** Minimize `0.0.0.0/0` ingress. |
| **AI/LLM code** | **[MUST]** No raw user input in system/privileged prompts — use clear delimiters between instructions and user content. **[MUST]** Mask PII/secrets/tenant data before sending to any LLM. **[MUST]** Sanitize model output before rendering in UI (XSS risk). **[MUST]** Do not use LLM output for auth/authz decisions. **[MUST]** Do not send customer data to external LLMs without explicit approval/DPA. **[REDLINE]** Passing LLM output directly to `eval`, SQL, shell commands, or `innerHTML` — leads to code injection, command injection, SQLi, and XSS. **[SHOULD]** Validate/filter model outputs before any downstream use. **[SHOULD]** Log categories of data sent to LLMs (not raw content). **[SHOULD]** Rate limit LLM API calls to prevent abuse/cost overrun. |
| **Docker** | **[MUST]** Non-root user. Pin base image versions. **[REDLINE]** Secrets in build layers; `privileged: true`. |
| **Code references/imports** | **[MUST]** All code in approved GitHub org (AtlanHQ). Flag personal repos or non-org imports. |

---

### Severity & Response

| Severity | Criteria | Action |
|----------|----------|--------|
| **CRITICAL** | RCE, data breach, cross-tenant access, credential exposure, full auth bypass, CRITICAL CVEs | **Block.** Fix immediately. No opt-out. |
| **HIGH** | Endpoint auth bypass, privilege escalation, tenant isolation gap, HIGH CVEs | **Block.** Fix before merge. No opt-out. |
| **MEDIUM** | Info disclosure via errors, weak config, CORS issues, missing controls | **Flag** with fix. Can be follow-up. |
| **LOW** | Best practice gaps, defense-in-depth | **Note** briefly. |

**Review format (MEDIUM+):**
```txt
🔒 SECURITY REVIEW
Issue: [description]
Severity: CRITICAL | HIGH | MEDIUM
Location: [file:line]
Risk: [what attacker gains, Atlan-specific impact]
Fix: [concrete fix — implement immediately for CRITICAL/HIGH]
```

**Quick format (LOW):** `⚡ Security note: [risk] → [fix]`

---

### Handling Existing Violations

- **In your diff:** Fix or flag with 🔒 format.
- **Outside your diff:** Note briefly. Don't refactor without explicit approval.
- **Never** use existing violations to justify new ones.

---

### Multi-Tenant Security (When Applicable)

> **Note:** Not all services are multi-tenant. If your service is single-tenant or internal-only, this section may not apply. Check your Architecture Notes above.

For multi-tenant services, every data path must enforce tenant/org isolation.

**The rule:** Tenant/org identifier from authenticated session → enforced in every data access → return 404 on miss (not 403).

```txt
✅ tenantId = extractTenantId(authenticatedSession)
✅ resource = query(filters={ id: resourceId, tenant_id: tenantId })
✅ if not resource: return 404

❌ tenant_id = request.params["tenant_id"]     // attacker swaps tenant
❌ SELECT * FROM resources WHERE id = ?        // missing tenant/org filter
❌ /api/tenants/{tenant_id}/resources          // who verifies ownership?
```

**Enforce in:** DB queries, cache keys (`tenant:{id}:…`), file storage paths, search filters, queue messages, webhook destinations.

---

### New API Endpoint Checklist

Every new endpoint **[MUST]** have before merging:
- [ ] Authentication (verify identity via JWT, API key, OAuth, session, or service-appropriate mechanism)
- [ ] Authorization (user/role permissions verified; tenant scoping if multi-tenant)
- [ ] Input validation (schema, allowlists, length limits)
- [ ] Rate limiting (keyed by user/tenant/IP as appropriate, return 429 + Retry-After)

---

### Security Review Checklist

**Universal:**
- [ ] No secrets in code/config/logs/CI output
- [ ] Client errors don't expose internals
- [ ] Existing security patterns reused (no new auth flows without review)

**Data Access:**
- [ ] Tenant/org scoping enforced from auth context (if multi-tenant)
- [ ] Input validated; parameterized queries only
- [ ] Auth + authz enforced; rate limiting on sensitive endpoints

**Infrastructure:**
- [ ] Containers non-root; minimal capabilities; images pinned
- [ ] RBAC least privilege; secrets managed externally
- [ ] TLS enforced; network exposure minimized

**CI/CD:**
- [ ] Actions pinned to SHAs; minimum permissions; no injection patterns

**Frontend:**
- [ ] No unsafe HTML rendering; tokens not in localStorage/sessionStorage
- [ ] Redirects validated against allowlist; CSP headers configured
- [ ] CSRF protection on state-changing requests (if cookie-based auth)

---

### When to Request Manual Security Review

Reach out to `#bu-security-and-it` before merging when changes touch:
- Auth/authz flows or multi-tenant isolation logic
- Secrets management or new external integrations
- New public-facing endpoints or services
- Any change where you're unsure about security impact

---

### Appendix: References

- [OWASP Top 10](https://owasp.org/www-project-top-ten/) | [API Security Top 10](https://owasp.org/www-project-api-security/)
- [STRIDE Threat Model](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats)
- [GitHub Actions Hardening](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-for-github-actions)
- [Kubernetes Security](https://kubernetes.io/docs/concepts/security/) | [SLSA](https://slsa.dev/) | [OpenSSF Scorecard](https://securityscorecards.dev/)