---
name: Talk to your data
slug: talk-to-your-data
number: 17
summary: 'Pair Atlan with your warehouse or SQL-tool MCP: Atlan finds the right certified
  table and hands over the governed definition, so you query the source correctly — not just
  quickly.'
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- AI Builder
effort: Quick
runs_in: any AI tool
requires:
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/talk-to-your-data/
related:
- route-data-requests-to-right-assets
- gamify-your-context
- trace-a-broken-dashboard-to-its-root-cause
---

# Talk to your data

Pair Atlan with your warehouse or SQL-tool MCP: Atlan finds the right certified table and hands over the governed definition, so you query the source correctly — not just quickly.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, AI Builder |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Someone needs revenue by customer for the last two years. They don't know which table to trust or how revenue is actually supposed to be calculated — and getting either wrong produces a number the business won't stand behind. This is a two-MCP move: the Atlan MCP finds the right certified table and, just as importantly, hands over its governed context — the owner, the certification, and the definition and calculation of the metric. A warehouse or SQL-tool MCP (Snowflake, your SQL client, and the like) then runs the query, using that definition so the result matches how the company actually defines revenue.

## What to ask for

- The right certified table for the data you need (say, order and revenue information)
- The governed definition and calculation of the metric (how revenue is actually computed)
- A query against the source that applies that definition, so the number is right

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
I need revenue by customer for the last two years. Find the certified table with the order and revenue data, pull the governed definition and calculation of revenue from Atlan, then query the source using that definition so the number matches how we define it.
```

## Steps

### 1. Find the right certified asset.

```text
Find the certified table with <order/revenue> data, and show its owner and certification.
```

### 2. Pull the governed context — the definition and calculation.

```text
Get the governed definition and calculation of <revenue> from Atlan for that table.
```

### 3. Query the source with that context.

```text
Using that definition, query the table in <Snowflake> to return <revenue by customer for the last two years>.
```

## What you'll need

**Required**

- What you need, in plain language (the metric and any time range)
- Two MCPs connected: the Atlan MCP (to find the asset and pull its governed context — definition, calculation, owner, certification) and a data-access MCP for your warehouse or SQL tool, e.g. Snowflake, to run the query

**Optional, but it helps**

- Your team or domain, to prefer sources you already have access to
- Whether you want only certified assets, or everything that matches

## What you get

- The certified table to use, with its owner and certification
- The governed definition and calculation of the metric, so the query computes it the company's way
- A query run against the source that returns the data, calculated correctly — not just a table name

Atlan supplies the context — the right table and the governed definition — so the query against the source is pointed at the trusted asset and calculated the way the business defines it. You get the number you can stand behind, not just a list of tables.

**What changed in Atlan:** Nothing is written. Atlan reads the asset and its governed context, and the query against the source is read-only — so anyone can run it safely.

## Follow-ups

**Compare the options**

```text
Between the top two tables, which is more current, and which do more teams use?
```

**Get to the data**

```text
For the certified one, who do I ask for access, and is there a sample or data dictionary?
```

**Refine the need**

```text
I actually need this by region. Which of these has a region column?
```

## Cook's note

> Atlan hands you the definition, not just the table — so the query comes back right, not just runnable.

- Match the tool to the work. Use whatever AI tool you already have open; the recipe reads, so there is nothing to set up and nothing to break.
- Automate or chain it. Wire it into a Slack assistant so "where do I find X" questions get answered from Atlan without anyone filing a ticket.
- It only reads. No writes, so ask freely and follow up as many times as you need to find the right source.

## Related recipes

- [Route data requests to right assets](./route-data-requests-to-right-assets.md) — Surface certified, well-documented assets in response to a business request.
- [Gamify your context](./gamify-your-context.md) — Generate per-domain enrichment scorecards to motivate metadata contributions.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/talk-to-your-data/
