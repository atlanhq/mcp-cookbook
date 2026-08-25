---
name: Get build-ready for a new dashboard
slug: get-build-ready-for-a-new-dashboard
number: 4
summary: 'Before you build a dashboard: the trusted source, the confirmed definition, and
  how the data is really used — as the build recipe.'
job: Find & understand data
action: Look up
personas:
- Data/BI Analyst
- AI Builder
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/get-build-ready-for-a-new-dashboard/
related:
- understand-how-a-metric-is-calculated
- reuse-before-you-rebuild
- trace-a-broken-dashboard-to-its-root-cause
---

# Get build-ready for a new dashboard

Before you build a dashboard: the trusted source, the confirmed definition, and how the data is really used — as the build recipe.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/BI Analyst, AI Builder, Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

You've got a request for a product-sales dashboard. Before opening your BI tool, get build-ready: find the certified table to build on (not a lookalike), confirm the metric definition against what's governed, and read how people already query that table so the dashboard matches real usage.

## What to ask for

- The trusted, certified source to build on
- The governed definition — does it match how the team calculates it?
- The joins, filters, and questions the table already answers

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Get me build-ready for the product-sales dashboard — the certified source to build on, the Revenue definition, and how people actually query that table.
```

## Steps

### 1. Find the trusted source.

```text
Find the certified table for <topic> — prefer a mart or gold layer, and steer me off lookalikes.
```

### 2. Confirm the definition.

```text
Pull the governed term for <metric> on that table and tell me if it matches how we calculate it.
```

### 3. Read how the table is used.

```text
Show the popular joins, common filters, and the business questions this table already answers.
```

## What you'll need

**Required**

- The dashboard topic / the metric it's about
- The team's stated calculation, if you have it, to confirm against the governed one

**Optional, but it helps**

- Any cut you know you need (by region, by product), so the filters come back relevant
- Works from a ticket, a Slack ask, or ad hoc

## What you get

- The one certified source to build on — its layer, owner, and certification — with a note to avoid the un-trusted lookalikes
- The governed definition with a verdict: confirmed — matches, or a flagged difference (tax handling, one-time items, gross vs. net)
- The build recipe from SQL Intelligence: popular joins (with the key and when to use), common filters, and the business questions the table already answers

You start building on the certified source with the official number and the questions the data already answers — so the dashboard is right the first time, and a definition mismatch is caught before building, not after.

**What changed in Atlan:** Nothing is written — it stops at build-ready. You build in your BI tool from there.

## Follow-ups

**Map it to tiles**

```text
Turn those business questions into a dashboard layout — which become KPI tiles, which a trend, which a detail table.
```

**Get the cut**

```text
Which filter do I use for a by-region view, and how is it applied?
```

**Avoid the trap**

```text
For the top lookalike, show why it's not the trusted one — uncertified, wrong grain, or stale.
```

## Cook's note

> SQL Intelligence is the hero move — how the table is really queried is the recipe for the dashboard.

- Match the tool to the work. Any AI tool works; it reads and prepares, so it's safe to run for any request.
- Automate or chain it. Run it the moment a dashboard request lands, so every build starts from the certified source and the real usage.
- It only reads. No writes — it stops at build-ready and never builds or changes anything.

## Related recipes

- [Understand how a metric is calculated](./understand-how-a-metric-is-calculated.md) — Get the governed definition of a metric — and where it's documented — without asking a data engineer.
- [Reuse before you rebuild](./reuse-before-you-rebuild.md) — Before you write SQL to derive a metric, check whether it already exists — and reuse the governed one.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/get-build-ready-for-a-new-dashboard/
