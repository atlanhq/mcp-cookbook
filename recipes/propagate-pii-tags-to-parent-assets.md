---
name: Propagate PII tags to parent assets
slug: propagate-pii-tags-to-parent-assets
number: 20
summary: Roll column-level PII classification up to parent tables and schemas so policies
  fire.
job: Govern & keep trusted
action: Make changes
personas:
- Data Engineer
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- tags
start_here: false
source_url: https://atlan.com/mcp-cookbook/propagate-pii-tags-to-parent-assets/
related:
- propagate-context-through-lineage
- score-assets-for-ai-readiness
- keep-asset-metadata-fresh
---

# Propagate PII tags to parent assets

Roll column-level PII classification up to parent tables and schemas so policies fire.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Make changes |
| **Who it serves** | Data Engineer, Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

In the customers database, individual columns are tagged PII, but the tables and schemas above them are not. So table-level and schema-level policies never fire, and a control you think is on is quietly off. You want the classification rolled up to every level.

## What to ask for

- Every column tagged PII in customers
- Their parent tables and schemas
- The PII tag applied to any parent that is not already tagged

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Find all columns tagged as PII in the customers database. For each one, apply the PII tag to its parent table and schema if those aren't already tagged.
```

## Steps

### 1. Find columns tagged PII.

```text
Find all columns tagged <PII> in the <customers> database.
```

### 2. Walk up to their parent table and schema.

```text
For each, find its parent table and schema.
```

### 3. Apply the same classification to parents where it's missing.

```text
Apply the <PII> tag to any parent that isn't already tagged.
```

## What you'll need

**Required**

- The database or scope to check (customers)
- The classification to roll up (PII, and any aliases like Confidential or Sensitive)
- Permission to apply tags

**Optional, but it helps**

- Whether to stop at the table or continue to the schema and database
- Any parent to exclude, such as a reference table that should not inherit the tag

## What you get

- Every PII-tagged column in customers, with its parent table and schema
- The PII tag applied to each parent that was missing it
- A consistent classification from column up to schema

The classification now holds at every level, so table-level and schema-level policies actually fire. A column tag alone never triggered them; now the controls apply where you expected.

**What changed in Atlan:** Changed: PII tags added to parent tables and schemas that lacked them. Left untouched: the column tags, the data, and any parent already correctly tagged.

## Follow-ups

**Prove the coverage**

```text
List any table with a PII column whose schema is still untagged, so I can confirm the roll-up is complete.
```

**Extend the classes**

```text
Do the same for Confidential and Sensitive tags, not just PII.
```

**Extend the roll-up**

```text
Continue up to the database level: if any schema under customers now carries PII, tag the database too.
```

## Cook's note

> Do this before you rely on table-level policies. A column tag alone won't trigger them.

- Match the tool to the work. Classification changes are high-stakes; run it where you can review the parents to be tagged before it writes.
- Automate or chain it. Schedule it so newly tagged PII columns get their parents classified within a day, before a policy gap can open.
- Ask what it changed. Add "list every parent asset you tagged." For a compliance control, that record matters.

## Related recipes

- [Propagate context through lineage](./propagate-context-through-lineage.md) — Push descriptions and tags from a source table to every downstream asset in one pass.
- [Score assets for AI readiness](./score-assets-for-ai-readiness.md) — Rate assets on documentation, ownership, and quality before they enter AI pipelines.
- [Keep asset metadata fresh](./keep-asset-metadata-fresh.md) — Catch stale certifications, missing owners, and outdated descriptions early.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/propagate-pii-tags-to-parent-assets/
