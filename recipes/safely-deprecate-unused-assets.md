---
name: Safely deprecate unused assets
slug: safely-deprecate-unused-assets
number: 10
summary: Verify no active consumers exist, notify owners, then mark assets as deprecated.
job: Retire & migrate
action: Make changes
personas:
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires:
- lineage
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/safely-deprecate-unused-assets/
related:
- triage-assets-for-migration
- warn-downstream-owners-before-a-change-lands
- see-what-a-sql-change-will-break-before-you-merge
---

# Safely deprecate unused assets

Verify no active consumers exist, notify owners, then mark assets as deprecated.

| | |
|---|---|
| **Use case** | Retire & migrate |
| **Action** | Make changes |
| **Who it serves** | Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

You want to retire legacy_orders_v1, an old table you are fairly sure nothing reads anymore. But "fairly sure" is how cleanups become incidents: one forgotten dashboard still pointed at it, and deprecating it breaks a Monday report. Before you touch it, you want proof it is safe, the owners of anything still on it warned, and the countdown posted on the asset itself.

## What to ask for

- What still depends on it — downstream consumers, traced hop by hop, each with its owner
- Usage as a second signal where the asset has it — when it was last queried
- If it's safe: a deprecation announcement, 30-day notice, the table marked deprecated, and the reason recorded

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
I want to deprecate the legacy_orders_v1 table. First check whether anything still depends on it: walk its downstream lineage a hop at a time and give me each consumer with its owner. If usage data is available for the table, also tell me when it was last queried. If it's safe, add a deprecation notice saying it will be removed in 30 days, mark it deprecated, and record the reason — otherwise list the owners to warn first.
```

## Steps

### 1. Trace what still depends on it.

```text
Walk <table>'s downstream lineage one hop at a time and list each downstream consumer with its owner.
```

### 2. Add usage as a second check, where it's available.

```text
If <table> carries usage data, also show when it was last queried; treat it as safe to retire only if there are no live consumers and — where usage exists — no recent reads.
```

### 3. Deprecate it and record why.

```text
Add a deprecation notice (removed in <30 days>), mark <table> deprecated, and set the deprecation reason and date.
```

## What you'll need

**Required**

- The asset to retire (legacy_orders_v1)
- Lineage populated, so "downstream" is real and not empty by accident
- Permission to add announcements and change asset status

**Optional, but it helps**

- The removal window (defaults to 30 days) and the replacement to point people to
- A standard deprecation message to reuse across retirements
- A deprecation custom-metadata field (status, date, reason) if you track retirements there, so the record stays queryable
- Usage/query history is only available on some assets (typically warehouse tables, not BI); where it's missing, ownership and lineage carry the decision

## What you get

- A dependency read: the downstream consumers found tracing outward from legacy_orders_v1, each with its owner and certification — plus, where the table carries usage data, when it was last queried
- A deprecation announcement on the table with the 30-day notice and the replacement
- legacy_orders_v1 set to Deprecated
- A deprecation record in custom metadata (status, date, reason), so the retirement is queryable later, not just a notice on the page

You get a go or no-go picture in one pass. Empty impact list means deprecate with confidence; not empty means you have the exact owners to warn first. The countdown lives on the asset, so no one is surprised on removal day.

**What changed in Atlan:** Changed: the status flag, one announcement, and a deprecation record (status, date, reason) in custom metadata on legacy_orders_v1. Left untouched: the data, and every downstream asset, which are surfaced but never edited; nothing is dropped or moved.

## Follow-ups

**Warn the dependents directly**

```text
For each downstream consumer, draft a one-line migration note pointing to <replacement table> and post it as an announcement on that consumer too.
```

**Batch the family, with a gate**

```text
Do the same for every table in the legacy_orders_* family, but only deprecate the ones with zero downstream consumers; list the rest for me to review.
```

**The pre-delete re-check**

```text
It's been 30 days. Show which deprecated tables still have active consumers, so I know which are not safe to drop.
```

## Cook's note

> Never skip step one. A "dead" table almost always has one dashboard still quietly on it.

- Match the tool to the work. This is a read-then-write chain; run it where you see the impact list before it posts the notice, then let it flip the status. Start with the immediate downstream and expand only if you need to, rather than pulling the whole lineage graph at once.
- Automate or chain it. Point it at a whole schema on a schedule: find tables with no consumers and no queries in 90 days, and draft the deprecation list monthly for approval.
- Ask what it changed. Add "list which assets you changed and which you only read." For anything that writes to Atlan, that line is your audit trail.

## Related recipes

- [Triage assets for migration](./triage-assets-for-migration.md) — Classify every asset by consumer count, ownership, and certification before migrating.
- [Warn downstream owners before a change lands](./warn-downstream-owners-before-a-change-lands.md) — Find every downstream consumer of a changing asset and warn their owners first.
- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Find every downstream consumer of a changed column or table before merging.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/safely-deprecate-unused-assets/
