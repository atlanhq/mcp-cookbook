---
name: Get the answer, not just the table
slug: get-the-answer-not-just-the-table
number: 26
summary: Every other lookup hands you where to find the data. This one starts from the governed
  definition of a metric, follows it to the certified asset that carries it, and gives you
  the answer itself — calculated the way your business defines it, using Atlan alone.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- AI Builder
effort: Moderate
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/get-the-answer-not-just-the-table/
related:
- talk-to-your-data
- explore-schema-before-writing-sql
- understand-how-a-metric-is-calculated
---

# Get the answer, not just the table

Every other lookup hands you where to find the data. This one starts from the governed definition of a metric, follows it to the certified asset that carries it, and gives you the answer itself — calculated the way your business defines it, using Atlan alone.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, AI Builder |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

An analyst needs the top 3 accounts by revenue, and doesn't want to spin up a BI dashboard or hand-write SQL against a source they're not sure they can trust. The trap isn't finding *a* number — it's that "revenue" means something specific here, and a query that computes it differently produces a figure the business won't stand behind. So the answer gets built up from the governed definition of the metric, down to the certified asset that carries it, and only then queried.

## What to ask for

- The governed definition of the metric and how it's calculated
- The assets that carry it, narrowed to the certified one you should query
- The answer itself, calculated the way the business defines the metric

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Get me the governed definition and calculation of revenue, find the certified asset that carries it, and use that to give me the top 3 accounts by revenue.
```

## Steps

### 1. Get the governed definition of the metric.

```text
Give me the governed definition of <revenue>, including how it's calculated, so I know what the number is supposed to mean.
```

### 2. Find the assets that carry that metric.

```text
Show me the assets linked to <revenue>, so I can see which tables actually hold the data behind that definition.
```

### 3. Narrow to the one you should use.

```text
Of those, show me which are certified, who owns them, and which one I should be querying.
```

### 4. Get the answer from that source.

```text
Using that asset and the governed calculation, give me <the top 3 accounts by revenue>.
```

## What you'll need

**Required**

- **Data Exploration (Insights) enabled in your Atlan tenant** — the final step queries the source through Atlan, so without it the recipe resolves the definition and the asset but can't return the answer
- The metric you're asking about, by the name your business uses for it
- Read access to the certified data through Atlan, with query permission on the connection
- Your assistant connected to the Atlan MCP

**Optional, but it helps**

- A certification or freshness bar for what counts as a trustworthy source
- The time range or grouping you want the answer broken out by

## What you get

- The governed definition of the metric and how it's calculated
- The assets that carry it, narrowed to the certified one you should query, with its owner
- The answer itself, computed the way the business defines the metric

You get a number you can defend, because it was built from the governed definition down to the certified source — not a number that merely ran without erroring against whichever table matched the word.

**What changed in Atlan:** Read-only. This reads the definition, the assets, and the data; it doesn't write anything back to Atlan or the source.

## Follow-ups

**Keep the query**

```text
Show me the exact query you ran, so I can save it or hand it to someone else.
```

**Turn it into a trend**

```text
Compare this quarter against the last four, using the same certified source.
```

**Slice it further**

```text
Break that down by <region or month> using the same asset and calculation.
```

## Cook's note

> Start from the definition, not the table. Searching for a metric by name gets you whatever asset happens to match the word; starting from the governed definition gets you the asset that actually carries it — and a number you can put in front of finance.

- Match the client to the work.** Use a client that shows you the source and the query before it runs, so you can see what you're trusting.
- Automate or chain it.** Once a question is answered against a certified source, save the query and re-run it on a cadence instead of rebuilding it each time.
- Ask what it used.** Have it name the table, columns, and filters behind every answer, so a number you report is always traceable to a governed source.

## Related recipes

- [Talk to your data](./talk-to-your-data.md) — Pair Atlan with your warehouse or SQL-tool MCP: Atlan finds the right certified table and hands over the governed definition, so you query the source correctly — not just quickly.
- [Write SQL that runs on the first try](./explore-schema-before-writing-sql.md) — Pull real column names and types from the source schema first, so the SQL you write runs on the first try instead of guessing at a field name that doesn't exist.
- [Understand how a metric is calculated](./understand-how-a-metric-is-calculated.md) — Get the governed definition of a metric — and where it's documented — without asking a data engineer.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/get-the-answer-not-just-the-table/
