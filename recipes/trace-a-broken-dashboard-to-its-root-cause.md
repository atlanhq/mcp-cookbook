---
name: Trace a broken dashboard to its root cause
slug: trace-a-broken-dashboard-to-its-root-cause
number: 9
summary: Trace lineage upstream from a broken dashboard to find the source of wrong numbers.
job: Change & fix data safely
action: Look up
personas:
- Data/BI Analyst
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- lineage
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/trace-a-broken-dashboard-to-its-root-cause/
related:
- triage-a-data-quality-failure-with-full-context
- see-what-a-sql-change-will-break-before-you-merge
- talk-to-your-data
---

# Trace a broken dashboard to its root cause

Trace lineage upstream from a broken dashboard to find the source of wrong numbers.

| | |
|---|---|
| **Use case** | Change & fix data safely |
| **Action** | Look up |
| **Who it serves** | Data/BI Analyst, Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

The Weekly Sales Dashboard has shown revenue about 30% low since Monday, and the cause is not on the dashboard; it is somewhere in the chain of tables and transforms behind it. You want to walk the lineage back and find where the numbers went wrong, with the owners and any recent notices along the way.

## What to ask for

- The upstream lineage of the dashboard
- Every source table and transformation in the chain
- The owners, recent announcements, and any DQ rule failures along it

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
The Weekly Sales Dashboard is showing revenue figures 30% lower than expected since Monday. Trace its upstream lineage hop by hop and show me the source tables and transformations in the chain along with their owners, any recent announcements, and the DQ rule failures on each.
```

## Steps

### 1. Find the dashboard and confirm its upstream lineage.

```text
The <dashboard> has shown <metric> about <30%> off since <Monday> — find it and confirm it has upstream lineage to walk.
```

### 2. Trace its upstream lineage, one hop at a time.

```text
Walk the upstream source tables and transformations hop by hop toward the source.
```

### 3. Read the owners, recent announcements, and any DQ failures along the chain.

```text
For each node, show the owner, any recent announcements, and its current DQ rule failures or incidents, so I can pinpoint where the numbers break.
```

## What you'll need

**Required**

- The dashboard and the anomaly (Weekly Sales, revenue 30% low since Monday)
- Lineage populated back to the sources

**Optional, but it helps**

- When it was last correct, to bound which upstream changes to suspect
- The metric's known source table, if you want to start mid-chain
- Data Quality Studio (or another data quality connector) enabled on the chain, to surface real DQ rule failures alongside announcements

## What you get

- The dashboard's upstream chain: every source table and transformation
- The owner of each node in the chain
- Any recent announcements and DQ rule failures along the way — the likely first suspects

The search narrows from "the dashboard is wrong" to a short chain with owners and a timeline. Half the time a recent announcement or a DQ rule failure upstream already names the change that broke it.

**What changed in Atlan:** Nothing is written. This recipe only reads lineage, metadata, announcements, and DQ rule failures, so it is safe to run mid-incident against production.

## Follow-ups

**Zero in**

```text
Which nodes in that chain changed or got an announcement since last Friday? Start there.
```

**Get the owners**

```text
For the top suspect tables, resolve each owning group to the specific person or on-call to contact.
```

**Write it up**

```text
Draft a short root-cause note summarizing the chain and the most likely cause for the dashboard's owner.
```

## Cook's note

> Check announcements first. Half the time someone already flagged the upstream change.

- Match the tool to the work. Run it in whatever AI tool is open during the incident; speed matters, and the recipe is read-only. Trace one hop at a time from the dashboard rather than pulling the whole upstream graph at once, and make sure the asset actually has lineage before you start.
- Automate or chain it. Chain it to your alerting: when a dashboard's metric moves beyond a threshold, run the upstream trace and attach it to the alert.
- It only reads. No writes, no risk. Run it against production as many times as you need while you narrow the cause.

## Related recipes

- [Triage a data-quality failure with full context](./triage-a-data-quality-failure-with-full-context.md) — Enrich quality failures with lineage, ownership, and downstream impact for faster triage.
- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Find every downstream consumer of a changed column or table before merging.
- [Talk to your data](./talk-to-your-data.md) — Pair Atlan with your warehouse or SQL-tool MCP to find the right certified data in plain language, then go straight to it.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/trace-a-broken-dashboard-to-its-root-cause/
