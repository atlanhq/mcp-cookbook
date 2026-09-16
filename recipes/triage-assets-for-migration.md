---
name: Triage assets for migration
slug: triage-assets-for-migration
number: 11
summary: Classify every asset by consumer count, ownership, and certification before migrating.
job: Retire & migrate
action: Make changes
personas:
- Data Engineer
effort: Involved
runs_in: any AI tool
requires:
- lineage
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/triage-assets-for-migration/
related:
- safely-deprecate-unused-assets
- sync-metadata-across-environments
- score-assets-for-ai-readiness
---

# Triage assets for migration

Classify every asset by consumer count, ownership, and certification before migrating.

| | |
|---|---|
| **Use case** | Retire & migrate |
| **Action** | Make changes |
| **Who it serves** | Data Engineer |
| **Effort** | Involved |
| **Runs in** | any AI tool |

## The problem

You are moving the legacy_dwh schema to a new warehouse, and the fastest way to stall is to migrate in the wrong order: a table you called low-priority turns out to feed forty dashboards, or has no owner to answer questions. You want every asset scored up front so you move the high-traffic, well-owned tables first.

## What to ask for

- All tables in the legacy_dwh schema
- Each one's downstream consumer count, owner, and certification
- A high, medium, or low migration priority written to custom metadata

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
We're migrating all tables in the legacy_dwh schema to the new warehouse. For each table, show me how many downstream consumers it has, who owns it, and whether it's certified. Then classify each one as high, medium, or low migration priority and write that to the Migration Priority custom metadata field.
```

## Steps

### 1. Search for all assets in the source environment.

```text
List all tables in the <legacy_dwh> schema.
```

### 2. Check downstream consumers, owner, and certification.

```text
For each, trace its downstream consumers outward (expand as needed), and show its owner and certification status.
```

### 3. Score each by migration priority and write it to custom metadata.

```text
Classify each as high, medium, or low priority and write it to <Migration Priority> custom metadata.
```

## What you'll need

**Required**

- The source scope (legacy_dwh)
- The priority rubric (what makes a table high versus low)
- A Migration Priority custom metadata field, and permission to write it (if it doesn't exist yet, create it once first — a one-time setup step)

**Optional, but it helps**

- A usage window for "active" consumers, so dormant dependencies do not inflate priority
- A cap, if you want only the top tier scored this round

## What you get

- Every legacy_dwh table with its consumer count, owner, and certification
- A high, medium, or low priority per table, against your rubric
- The priority written to the Migration Priority custom metadata field

The migration gets a running order instead of a guess. Sort by the field, and the high-traffic, well-owned tables move first, with the orphans flagged before they surprise you.

**What changed in Atlan:** Changed: the Migration Priority custom metadata field on each table. Left untouched: the tables, their lineage, and the data, all read to compute priority, not edited.

## Follow-ups

**Give me the wave plan**

```text
Group the tables into three migration waves by priority and show the owner for each wave.
```

**Surface the risks**

```text
List the high-priority tables that have no owner or are not certified; those need attention first.
```

**Track progress**

```text
As tables get migrated, show what share of high-priority tables remain.
```

## Cook's note

> Sort by consumer count. Migrate the high-traffic, well-owned tables first.

- Match the tool to the work. This scores a whole schema; use a more capable model so the rubric holds across every table, and review before it writes.
- Automate or chain it. Re-run it weekly through the migration, so the priority field reflects what is already moved and what remains.
- Ask what it changed. Add "list every table you wrote a priority to and the value." That is the record of the triage run.

## Related recipes

- [Safely deprecate unused assets](./safely-deprecate-unused-assets.md) — Verify no active consumers exist, notify owners, then mark assets as deprecated.
- [Sync metadata across environments](./sync-metadata-across-environments.md) — Keep descriptions, tags, and custom metadata aligned across dev, staging, and prod.
- [Score assets for AI readiness](./score-assets-for-ai-readiness.md) — Rate assets on documentation, ownership, and quality before they enter AI pipelines.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/triage-assets-for-migration/
