---
name: See what a SQL change will break before you merge
slug: see-what-a-sql-change-will-break-before-you-merge
number: 6
summary: Find every downstream consumer of a changed column or table before merging.
job: Change & fix data safely
action: Look up
personas:
- AI Builder
- Data Engineer
effort: Quick
runs_in: any AI tool
requires:
- lineage
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/see-what-a-sql-change-will-break-before-you-merge/
related:
- warn-downstream-owners-before-a-change-lands
- trace-a-broken-dashboard-to-its-root-cause
- safely-deprecate-unused-assets
---

# See what a SQL change will break before you merge

Find every downstream consumer of a changed column or table before merging.

| | |
|---|---|
| **Use case** | Change & fix data safely |
| **Action** | Look up |
| **Who it serves** | AI Builder, Data Engineer |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Your PR renames user_id to customer_id in dim_users. The diff looks small, but the real risk is the views, dbt models, and dashboards that read dim_users and never show up in the diff. You want the full blast radius while you are still in review, not after the merge.

## What to ask for

- Every downstream view, table, and dashboard that references the table
- Each one's owner and certification status
- Enough to decide whether the change is safe to merge

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
I'm about to rename the user_id column to customer_id in the dim_users table. Trace the downstream consumers of dim_users — start with the direct ones and expand into the branches that matter — so I can assess the impact before merging.
```

## Steps

### 1. Find the asset you're changing and confirm it has downstream lineage.

```text
I'm renaming <column> to <new name> in <table> — pull <table> and check what depends on it.
```

### 2. Trace its downstream consumers.

```text
Trace the downstream views, tables, and dashboards that read <table> — direct consumers first, then expand into the branches that matter.
```

### 3. Return the impact list with owners and certification.

```text
For each impacted asset, include its owner and certification status so I can decide what to test and who to warn.
```

## What you'll need

**Required**

- The table or column changing in the PR (user_id in dim_users)
- Lineage populated for that asset

**Optional, but it helps**

- Whether to include indirect (multi-hop) consumers or only direct ones
- The certification bar that matters to you, so certified consumers stand out

## What you get

- Every downstream view, table, and dashboard that references dim_users
- The owner and certification status of each
- A checkable impact list to paste into the PR

"I think this is safe" becomes a list you can check off. You see who to warn and what to test before merging, not after a dashboard goes blank.

**What changed in Atlan:** Nothing is written. This recipe only reads lineage and metadata, so it is safe to run against production from inside any review.

## Follow-ups

**Draft the warnings**

```text
For the certified consumers on that list, draft a short heads-up I can send their owners.
```

**Focus the testing**

```text
Which of these consumers are certified or heavily queried, so I test those first?
```

**Widen the change**

```text
I'm also dropping legacy_flag in the same PR. Add its downstream consumers to the impact list.
```

## Cook's note

> Paste this into your PR review. It turns "I think this is safe" into a list you can check off.

- Match the tool to the work. Run it in the AI tool you already review PRs in, so the impact list lands right next to the diff. Ask for the immediate downstream first and expand as needed; a full multi-hop pull can be huge.
- Automate or chain it. Chain it into CI: on a PR that touches a modeled table, post the impact list as a comment automatically.
- It only reads. Nothing is written back, so run it as often as you like, on any branch, without a change window.

## Related recipes

- [Warn downstream owners before a change lands](./warn-downstream-owners-before-a-change-lands.md) — Find every downstream consumer of a changing asset and warn their owners first.
- [Trace a broken dashboard to its root cause](./trace-a-broken-dashboard-to-its-root-cause.md) — Trace lineage upstream from a broken dashboard to find the source of wrong numbers.
- [Safely deprecate unused assets](./safely-deprecate-unused-assets.md) — Verify no active consumers exist, notify owners, then mark assets as deprecated.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/see-what-a-sql-change-will-break-before-you-merge/
