---
name: Reuse before you rebuild
slug: reuse-before-you-rebuild
number: 3
summary: Before you write SQL to derive a metric, check whether it already exists — and reuse
  the governed one.
job: Find & understand data
action: Look up
personas:
- AI Builder
- Data Engineer
effort: Quick
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/reuse-before-you-rebuild/
related:
- understand-how-a-metric-is-calculated
- get-build-ready-for-a-new-dashboard
- trace-a-broken-dashboard-to-its-root-cause
---

# Reuse before you rebuild

Before you write SQL to derive a metric, check whether it already exists — and reuse the governed one.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | AI Builder, Data Engineer |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Someone's about to write SQL to derive MRR for a new exec view. The risk isn't the work; it's ending up with a second, slightly-different definition of a number the company already calculates. Check where it already lives first.

## What to ask for

- Where the metric is already materialized
- The best existing implementation to reuse
- A reuse-or-rebuild verdict

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Does MRR already exist somewhere I can reuse before I build it?
```

## Steps

### 1. Find the metric's governed term.

```text
I'm about to derive <metric> — find its governed term in Atlan first.
```

### 2. Find everywhere it's already materialized.

```text
Show every certified asset linked to that term where <metric> already lives.
```

### 3. Recommend the single best one to reuse.

```text
Give me the one certified asset to reuse, with its owner and location, and a reuse-or-rebuild verdict.
```

## What you'll need

**Required**

- The metric you're about to build (and its governed term, if you know it)

**Optional, but it helps**

- Where the new asset will live, so the recommendation fits your stack
- Works from a ticket, a Slack ask, or ad hoc

## What you get

- Everywhere the metric is already materialized — e.g. MRR across ~30 assets
- The best one to reuse — e.g. a certified warehouse column such as executive_summary.total_monthly_recurring_revenue, plus the BI copies that already report it
- A one-line verdict: reuse the certified column, don't re-derive — one governed definition, not two

A duplicate model you just didn't build. Reuse the governed number instead of minting a second, slightly-different one.

**What changed in Atlan:** Nothing is written — it searches and recommends; you decide what to reuse.

## Follow-ups

**Compare the options**

```text
Between the top two, which is the certified one and which do more teams already use?
```

**Confirm it's official**

```text
Is the column I'd reuse linked to the governed term, so I know it's the official calc?
```

**Get access**

```text
Who owns it and how do I get access to reuse it?
```

## Cook's note

> Reuse the certified implementation. A second definition of the same metric is how two dashboards start disagreeing.

- Match the tool to the work. Any AI tool works; it reads and recommends, so it's safe to run before any build.
- Automate or chain it. Chain it into your modeling workflow: before a new metric model is written, check for an existing governed one.
- It only reads. No writes — pairs naturally with "Understand how a metric is calculated" (confirm the definition, then reuse it).

## Related recipes

- [Understand how a metric is calculated](./understand-how-a-metric-is-calculated.md) — Get the governed definition of a metric — and where it's documented — without asking a data engineer.
- [Get build-ready for a new dashboard](./get-build-ready-for-a-new-dashboard.md) — Before you build a dashboard: the trusted source, the confirmed definition, and how the data is really used — as the build recipe.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/reuse-before-you-rebuild/
