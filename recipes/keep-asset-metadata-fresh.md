---
name: Keep asset metadata fresh
slug: keep-asset-metadata-fresh
number: 18
summary: Catch stale certifications, missing owners, and outdated descriptions early.
job: Govern & keep trusted
action: Make changes
personas:
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- documentation
- domains
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/keep-asset-metadata-fresh/
related:
- score-assets-for-ai-readiness
- gamify-your-context
- sync-metadata-across-environments
---

# Keep asset metadata fresh

Catch stale certifications, missing owners, and outdated descriptions early.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Make changes |
| **Who it serves** | Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

Metadata drifts. In the analytics schema, certifications from last year are still marked current, a few owners have since left, and some descriptions describe a table that has since been reshaped. You want to surface what needs attention before the drift confuses someone downstream.

## What to ask for

- Tables in analytics certified more than 6 months ago
- A review of which descriptions and owners look out of date
- A warning announcement on the ones that need recertification

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Find all tables in the analytics schema certified more than 6 months ago. Review their current descriptions and owners, and flag any that need recertification with a warning announcement.
```

## Steps

### 1. Search for assets with stale or incomplete metadata.

```text
Find tables in the <schema> schema certified more than <6 months> ago.
```

### 2. Compare what's changed against what's documented.

```text
Show which descriptions or owners look out of date.
```

### 3. Update the fields, and announce it if the asset is in active use.

```text
Flag the ones needing recertification with a warning announcement.
```

## What you'll need

**Required**

- The scope to check (a schema, a domain, or the whole estate)
- Your staleness threshold (certified more than 6 months ago)
- Permission to post announcements and update metadata

**Optional, but it helps**

- A definition of "in active use" (queried in the last 30 days, say), so announcements go only where they matter
- The recertification owner to route flags to

## What you get

- A list of analytics tables certified more than 6 months ago
- A read on which descriptions and owners look out of date
- A warning announcement on the tables that need recertification

Drift becomes a short, ranked worklist instead of a surprise. Anyone who opens a flagged table sees the recertification notice in context.

**What changed in Atlan:** Changed: a warning announcement on the flagged tables (and any field you approved). Left untouched: certifications themselves, which stay as they are until a human recertifies.

## Follow-ups

**Narrow to what matters**

```text
Of the flagged tables, show only the ones queried in the last 30 days (where usage data exists); ignore the dormant ones.
```

**Draft the recert checklist**

```text
For each flagged table, list what a reviewer should confirm before recertifying it.
```

**Route it**

```text
Group the flags by owning team so I can send each team its own list.
```

## Cook's note

> Schedule this monthly. Drift is easier to fix a little at a time than all at once.

- Match the tool to the work. This posts announcements; run it where you can see the flagged list before anything is posted, and confirm the scope.
- Automate or chain it. This is the recipe most worth putting on a schedule: a monthly sweep keeps the estate honest without anyone remembering to run it.
- Ask what it changed. Add "list every asset you posted an announcement on." That is your monthly drift log.

## Related recipes

- [Score assets for AI readiness](./score-assets-for-ai-readiness.md) — Rate assets on documentation, ownership, and quality before they enter AI pipelines.
- [Gamify your context](./gamify-your-context.md) — Generate per-domain enrichment scorecards to motivate metadata contributions.
- [Sync metadata across environments](./sync-metadata-across-environments.md) — Keep descriptions, tags, and custom metadata aligned across dev, staging, and prod.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/keep-asset-metadata-fresh/
