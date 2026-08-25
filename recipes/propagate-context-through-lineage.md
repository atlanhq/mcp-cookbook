---
name: Propagate context through lineage
slug: propagate-context-through-lineage
number: 14
summary: Push descriptions and tags from a source table to every downstream asset in one pass.
job: Make data understandable
action: Make changes
personas:
- Data/BI Analyst
- Data Engineer
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- documentation
- lineage
- tags
start_here: false
source_url: https://atlan.com/mcp-cookbook/propagate-context-through-lineage/
related:
- propagate-pii-tags-to-parent-assets
- enrich-assets-with-your-context
- warn-downstream-owners-before-a-change-lands
---

# Propagate context through lineage

Push descriptions and tags from a source table to every downstream asset in one pass.

| | |
|---|---|
| **Use case** | Make data understandable |
| **Action** | Make changes |
| **Who it serves** | Data/BI Analyst, Data Engineer, Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

You finally documented customers_raw: a clear description and PII tags on the sensitive columns. Everything built on top of it, the views, the marts, the dashboards, should inherit that context, but it does not happen on its own. You want to walk the lineage once and carry the description and tags forward while the work is fresh.

## What to ask for

- The downstream lineage for customers_raw
- Every view, table, and dashboard it feeds
- The description and PII tags copied onto each

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Take the description and PII tags from the customers_raw table and propagate them outward through its downstream lineage, expanding hop by hop.
```

## Steps

### 1. Trace the downstream lineage from the source.

```text
Trace the downstream lineage from <source table> one hop at a time.
```

### 2. Walk the downstream nodes: views, tables, dashboards.

```text
List the downstream views, tables, and dashboards.
```

### 3. Apply the source's descriptions and tags to each.

```text
Copy the description and <tag> tags from <source table> to all of them.
```

## What you'll need

**Required**

- A source asset with complete metadata (customers_raw)
- Lineage populated for that asset
- Permission to update the downstream assets

**Optional, but it helps**

- Which tags to carry versus leave behind (you may want PII to travel but not a team-specific tag)
- A depth limit, if the lineage runs many hops and you only want the first level

## What you get

- The downstream lineage of customers_raw, listed by asset type
- The source description applied to each downstream asset that lacked one
- The PII tags carried onto every downstream asset that inherits the sensitive columns

Context stops dead-ending at the source. The description and the PII classification now travel with the data, so a governance policy that keys on the PII tag fires downstream too.

**What changed in Atlan:** Changed: descriptions and PII tags on the downstream assets. Left untouched: the source table, and any downstream asset that already carried its own description.

## Follow-ups

**Carry ownership too**

```text
Also set the same owner as customers_raw on any downstream asset that has no owner.
```

**Stop at a boundary**

```text
Propagate only to the analytics schema and stop; do not touch anything in sandbox.
```

**Verify it landed**

```text
Show me every downstream asset that still has no PII tag after the run so I can check why.
```

## Cook's note

> Do this right after you finally document a source table. Push it downstream while it's fresh.

- Match the tool to the work. Lineage propagation touches many assets at once; run it in an AI tool that lists the targets before it writes, so a wrong tag does not spread.
- Automate or chain it. Chain it onto your documentation workflow: whenever a source table gets new PII tags, propagate them the same night.
- Ask what it changed. Add "list every downstream asset you tagged and which tags you added." When classification travels, you want the receipt.

## Related recipes

- [Propagate PII tags to parent assets](./propagate-pii-tags-to-parent-assets.md) — Roll column-level PII classification up to parent tables and schemas so policies fire.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Warn downstream owners before a change lands](./warn-downstream-owners-before-a-change-lands.md) — Find every downstream consumer of a changing asset and warn their owners first.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/propagate-context-through-lineage/
