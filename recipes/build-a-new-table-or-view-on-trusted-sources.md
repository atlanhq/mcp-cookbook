---
name: Build a new table or view on trusted sources
slug: build-a-new-table-or-view-on-trusted-sources
number: 5
summary: Before you write the DDL, use Atlan to pick the right sources, confirm the grain
  and definitions, and avoid rebuilding something that already exists.
job: Find & understand data
action: Look up
personas:
- AI Builder
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- lineage
start_here: false
source_url: https://atlan.com/mcp-cookbook/build-a-new-table-or-view-on-trusted-sources/
related:
- reuse-before-you-rebuild
- get-build-ready-for-a-new-dashboard
- see-what-a-sql-change-will-break-before-you-merge
---

# Build a new table or view on trusted sources

Before you write the DDL, use Atlan to pick the right sources, confirm the grain and definitions, and avoid rebuilding something that already exists.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | AI Builder, Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

You've been asked to build a new customer_360 view. The risk isn't the SQL, it's building on the wrong sources, at the wrong grain, or re-deriving a metric the company already has. Before you write a line of DDL, use Atlan to find the certified sources to build on, confirm what the key fields mean, and check that nothing equivalent already exists.

## What to ask for

- The certified source tables to build on
- The governed definitions and grain of the key fields
- Whether an equivalent table or view already exists

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
I'm about to build a customer_360 view. Which certified tables should I build on, what are the governed definitions of the key fields, and does an equivalent view already exist?
```

## Steps

### 1. Find the certified sources to build on, and flag lookalikes to avoid.

```text
I'm building a <new table/view> for <purpose> — which certified tables should I build on (with grain and owner), and which lookalikes should I avoid?
```

### 2. Confirm the governed definitions of the key fields.

```text
Show the governed definitions of <key fields> so I model them correctly.
```

### 3. Check whether an equivalent already exists.

```text
Does an equivalent table or view already exist that I should reuse instead of rebuilding?
```

## What you'll need

**Required**

- What you're building and its purpose
- Lineage and certification populated for the candidate sources

**Optional, but it helps**

- The metrics or fields it must include, so definitions can be confirmed
- Your target schema or layer, so recommendations fit your stack

## What you get

- The certified source tables to build on (grain, owner, certification), and the lookalikes to avoid
- The governed definitions of the key fields
- Any existing table or view that already covers this, so you reuse instead of rebuild

You start the DDL from trusted sources, at the right grain, with the official definitions, and you don't rebuild what already exists.

**What changed in Atlan:** Nothing is written. It reads sources, lineage, and definitions to inform the build; you write the table or view in your warehouse.

## Follow-ups

**Map the joins**

```text
For those source tables, what join keys and filters do people already use?
```

**Draft the outline**

```text
Draft a column list for the new view with the governed definition next to each field.
```

**Sanity-check the grain**

```text
At <grain>, which source is the driving table and which are lookups?
```

## Cook's note

> The expensive mistake isn't a slow query, it's building on the wrong source or re-deriving a metric that already exists. Five minutes here saves that.

- Match the tool to the work. Run it in whatever AI tool you build in; it reads, so it's safe to run before you write any DDL.
- Automate or chain it. Chain it to your modeling workflow so every new model starts from certified sources and governed definitions.
- It only reads. Nothing is written to Atlan; you build the table or view in your warehouse from the answer.

## Related recipes

- [Reuse before you rebuild](./reuse-before-you-rebuild.md) — Before you write SQL to derive a metric, check whether it already exists — and reuse the governed one.
- [Get build-ready for a new dashboard](./get-build-ready-for-a-new-dashboard.md) — Before you build a dashboard: the trusted source, the confirmed definition, and how the data is really used — as the build recipe.
- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Find every downstream consumer of a changed column or table before merging.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/build-a-new-table-or-view-on-trusted-sources/
