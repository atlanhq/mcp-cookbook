---
name: Sync metadata across environments
slug: sync-metadata-across-environments
number: 19
summary: Keep descriptions, tags, and custom metadata aligned across dev, staging, and prod.
job: Govern & keep trusted
action: Make changes
personas:
- Data Governance Lead
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- documentation
- tags
start_here: false
source_url: https://atlan.com/mcp-cookbook/sync-metadata-across-environments/
related:
- keep-asset-metadata-fresh
- enrich-assets-with-your-context
- triage-assets-for-migration
---

# Sync metadata across environments

Keep descriptions, tags, and custom metadata aligned across dev, staging, and prod.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Make changes |
| **Who it serves** | Data Governance Lead, Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

orders_fact exists in both production and staging, and their metadata has drifted apart: production has a good description and tags, staging is half-blank, and nobody remembers which is right. You want them aligned, with one environment clearly the one that wins.

## What to ask for

- orders_fact in both production and staging
- A side-by-side of their descriptions, tags, and custom metadata
- The production metadata synced onto staging where staging is missing fields

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Find the orders_fact table in both production and staging. Compare their descriptions, tags, and custom metadata, then sync the production metadata to staging where staging is missing fields.
```

## Steps

### 1. Find the asset and its counterpart in the other environment.

```text
Find <table> in both <prod> and <staging>.
```

### 2. Compare the metadata fields side by side.

```text
Compare their descriptions, tags, and custom metadata.
```

### 3. Apply the more complete metadata to the environment that's missing it.

```text
Sync the <prod> metadata to <staging> where <staging> is missing fields.
```

## What you'll need

**Required**

- The asset and its two environments (orders_fact in prod and staging)
- Which environment wins (production, here)
- Permission to update metadata in the target environment

**Optional, but it helps**

- Which fields to sync and which to leave environment-specific (a staging-only note, say)
- A direction rule, if some fields should flow staging to prod instead

## What you get

- The two copies of orders_fact, matched across environments
- A field-by-field comparison of descriptions, tags, and custom metadata
- The production values written onto staging wherever staging was missing them

The same asset now reads the same way in both places, so a developer in staging sees the context production already has, and governance does not depend on which environment you opened.

**What changed in Atlan:** Changed: the missing fields on the staging copy. Left untouched: the production copy, and any staging field that already had a value; nothing is overwritten.

## Follow-ups

**Do the whole schema**

```text
Run the same comparison for every table in the orders schema and sync the gaps.
```

**Show the conflicts**

```text
Where prod and staging both have a value but they disagree, list them for me instead of syncing.
```

**Check dev too**

```text
Add dev to the comparison and show which environment is furthest behind.
```

## Cook's note

> Decide which environment wins before you run it, or you'll ping-pong edits.

- Match the tool to the work. Run it where you can see the comparison before the sync, so you can catch a field that should stay environment-specific.
- Automate or chain it. Once the winning environment is fixed, schedule the sync so staging never drifts far from production again.
- Ask what it changed. Add "list every staging field you wrote and its new value." That is your diff for the sync.

## Related recipes

- [Keep asset metadata fresh](./keep-asset-metadata-fresh.md) — Catch stale certifications, missing owners, and outdated descriptions early.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Triage assets for migration](./triage-assets-for-migration.md) — Classify every asset by consumer count, ownership, and certification before migrating.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/sync-metadata-across-environments/
