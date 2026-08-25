---
name: Document SQL with business context
slug: document-sql-with-business-context
number: 16
summary: Generate business-readable descriptions for SQL models from the context already in
  Atlan.
job: Make data understandable
action: Make changes
personas:
- AI Builder
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- documentation
- glossary
start_here: false
source_url: https://atlan.com/mcp-cookbook/document-sql-with-business-context/
related:
- grow-your-business-glossary
- enrich-assets-with-your-context
- trace-a-broken-dashboard-to-its-root-cause
---

# Document SQL with business context

Generate business-readable descriptions for SQL models from the context already in Atlan.

| | |
|---|---|
| **Use case** | Make data understandable |
| **Action** | Make changes |
| **Who it serves** | AI Builder, Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

Your monthly_revenue_summary dbt model is documented in the way models usually are: a note about the SQL, nothing about what it means to the business. You want a description a stakeholder can read, built from the glossary terms and descriptions its source tables already carry in Atlan.

## What to ask for

- The Atlan descriptions and glossary terms for the model's source tables
- A business-friendly description of what the model calculates and who it is for
- The description saved back to the model in Atlan

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
For the monthly_revenue_summary model in dbt, look up the Atlan descriptions and glossary terms for its source tables and write a business-friendly description explaining what it calculates and who it's for.
```

## Steps

### 1. Retrieve glossary terms and descriptions for the source assets.

```text
Look up the Atlan descriptions and glossary terms for <model>'s source tables.
```

### 2. Generate a business-readable description for the model.

```text
Write a business-friendly description of what <model> calculates and who it's for.
```

### 3. Write the description back to the asset in Atlan.

```text
Save it to the <model> asset in Atlan.
```

## What you'll need

**Required**

- The model to document (monthly_revenue_summary)
- Glossary terms that exist for its source assets
- Permission to write the description back

**Optional, but it helps**

- The audience for the description (an exec reader versus an analyst)
- A house format, such as description plus "used by" plus grain

## What you get

- The descriptions and glossary terms of the model's source tables, pulled together
- A business-readable description of what the model calculates and who uses it
- The description saved to the model in Atlan

The model gets documentation a stakeholder can actually read, built from context you already curated, so the description writes itself once the glossary is in place.

**What changed in Atlan:** Changed: the description on the monthly_revenue_summary model. Left untouched: the source tables and their terms, which are read to write the description, and the model's SQL.

## Follow-ups

**Do the layer**

```text
Do the same for every model in the revenue folder that has no business description.
```

**Add the grain**

```text
Extend the description with the model's grain and refresh cadence.
```

**Flag the gaps**

```text
If a source table has no glossary term, tell me, so I can define it before documenting the model.
```

## Cook's note

> Start from the source tables' terms. The description writes itself once the glossary is there.

- Match the tool to the work. Writing readable prose is close-reading work; use a more capable model, review the draft, then save.
- Automate or chain it. Chain it to your dbt build: on a new or changed model, draft the business description for review before it ships.
- Ask what it changed. Add "confirm which model you wrote the description to." A one-line check that the write landed on the right asset.

## Related recipes

- [Grow your business glossary](./grow-your-business-glossary.md) — Bootstrap glossary terms from how your assets already use business concepts.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/document-sql-with-business-context/
