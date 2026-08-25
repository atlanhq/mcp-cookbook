---
name: Triage a data-quality failure with full context
slug: triage-a-data-quality-failure-with-full-context
number: 8
summary: Enrich quality failures with lineage, ownership, and downstream impact for faster
  triage.
job: Change & fix data safely
action: Make changes
personas:
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- data_quality
- lineage
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/triage-a-data-quality-failure-with-full-context/
related:
- warn-downstream-owners-before-a-change-lands
- trace-a-broken-dashboard-to-its-root-cause
- keep-asset-metadata-fresh
---

# Triage a data-quality failure with full context

Enrich quality failures with lineage, ownership, and downstream impact for faster triage.

| | |
|---|---|
| **Use case** | Change & fix data safely |
| **Action** | Make changes |
| **Who it serves** | Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

orders_fact failed a null check on order_id this morning. The raw alert says something broke; it does not say who owns the table or which dashboards break next. Whoever is on call needs that context now, not after twenty minutes of digging.

## What to ask for

- The owners of orders_fact and its DQ rule failures (Data Quality Studio)
- The downstream dashboards it feeds
- A warning announcement on the table with the failure details

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
The orders_fact table failed a null check on order_id this morning. Find its owners and downstream dashboards, then add a warning announcement with the failure details so the team can triage.
```

## Steps

### 1. Pull the failing asset's owners, tags, announcements, and its current DQ rule failures and incidents.

```text
The <table> failed a <null> check on <column> this morning — show its owners, tags, announcements and its current DQ rule failures and incidents.
```

### 2. Trace its downstream consumers.

```text
Trace the downstream dashboards and tables that depend on <table>, so I know what's at risk.
```

### 3. Post a warning announcement with the failure details.

```text
Add a warning announcement to <table> with the failure details so the team can triage.
```

## What you'll need

**Required**

- The failing asset and what failed (orders_fact, null check on order_id)
- Lineage populated, so downstream consumers are real
- Permission to post announcements

**Optional, but it helps**

- The check's run details or a link, to paste into the announcement
- The on-call channel, if you also want a ping and not just the on-asset notice
- Data Quality Studio (or another data quality connector) enabled on the failing asset, to pull its actual DQ rule failures, not just a posted status

## What you get

- The owners of orders_fact, its DQ rule failures from Data Quality Studio, and the downstream dashboards at risk
- A warning announcement on orders_fact carrying the failure details
- A triage-ready picture: what broke, who owns it, what it hits

The alert arrives wrapped in the context that makes it actionable. On-call sees blast radius and ownership in one place, on the asset itself, instead of reconstructing it under pressure.

**What changed in Atlan:** Changed: one warning announcement on the failing table. Left untouched: the data, the check, and every downstream asset, which are surfaced but not edited.

## Follow-ups

**Warn the dependents**

```text
Post a short heads-up announcement on each downstream dashboard that this table failed a check today.
```

**Draft the update**

```text
Write a two-line status update for the on-call channel summarizing the failure and who is affected.
```

**Find the pattern**

```text
Show the current quality rules and any open incidents on this table, so I can see if it's a repeat offender.
```

## Cook's note

> Post the announcement on the failing asset itself. Everyone downstream sees it in context.

- Match the tool to the work. During an incident, run it in whatever AI tool is already open; the value is speed, and the announcement is a small, safe write.
- Automate or chain it. Chain it to your quality tool: on any check failure, fire this recipe so the announcement is posted before a human even looks.
- Ask what it changed. Add "confirm which asset you posted the announcement on." One line, so you know exactly where the notice landed.

## Related recipes

- [Warn downstream owners before a change lands](./warn-downstream-owners-before-a-change-lands.md) — Find every downstream consumer of a changing asset and warn their owners first.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.
- [Keep asset metadata fresh](./keep-asset-metadata-fresh.md) — Catch stale certifications, missing owners, and outdated descriptions early.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/triage-a-data-quality-failure-with-full-context/
