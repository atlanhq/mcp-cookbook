---
name: Profile a field's shape before you build on it
slug: profile-a-field-before-you-build-on-it
number: 27
summary: Get a quick profile of a field, its type, null rate, distinct count, and range, so
  you know what you're working with before you aggregate or join on it.
job: Find & understand data
action: Look up
personas:
- Data/BI Analyst
- AI Builder
- Data Engineer
effort: Quick
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/profile-a-field-before-you-build-on-it/
related:
- check-value-against-master-list
- explore-schema-before-writing-sql
- triage-a-data-quality-failure-with-full-context
---

# Profile a field's shape before you build on it

Get a quick profile of a field, its type, null rate, distinct count, and range, so you know what you're working with before you aggregate or join on it.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/BI Analyst, AI Builder, Data Engineer |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

An analyst is about to aggregate on a field they've never used, an `amount` or `status` column, and needs a quick profile first: what type it really is, how many nulls, how many distinct values, and its range. Building on a field that's secretly 40% null, stored as text, or dominated by one value is how a report goes wrong before it starts.

## What to ask for

- The field's data type, null rate, distinct count, and range
- Whether its real shape matches what you were about to assume
- Anything about it that makes it risky to build on

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Give me a quick profile of the `amount` field on `<table>`: its data type, null rate, how many distinct values, and its range, before I build on it.
```

## Steps

### 1. Find the field.

```text
Find the <amount> field on <table> and confirm it's the one I mean.
```

### 2. Quick-profile its shape.

```text
Profile it: data type, null count and rate, number of distinct values, and its min/max range.
```

### 3. Flag anything that makes it risky to build on.

```text
Tell me if anything here would break a report: a high null rate, a text type where I expected a number, or one value dominating the field.
```

## What you'll need

**Required**

- The table and field
- Read access to the connected source through Atlan, with query permission

**Optional, but it helps**

- What you're about to build (a sum, an average, a join), so the profile can call out what specifically would break it
- The type or range you expect, so it can flag the gap

## What you get

- The field's real data type, null count and rate, distinct-value count, and min/max range
- A plain read on whether it's safe to build on, with the specific risk called out

You know the shape of the field, not just its name, before you aggregate or join on it, so you don't discover a 40%-null column after the numbers look wrong.

**What changed in Atlan:** Read-only. This profiles the field; nothing in Atlan or the source is written.

## Follow-ups

**Widen the check**

```text
Profile every field this report aggregates on, not just this one.
```

**Compare over time**

```text
Compare this field's null rate to the last time I profiled it.
```

**Find a better field**

```text
If the type isn't what I need, show me the closest field that is.
```

## Cook's note

> A field's name tells you what it's called, not what it holds. A quick profile is five minutes; a wrong aggregate is a rebuilt report.

- Match the client to the work.** Any client works; this is a fast lookup, not a multi-step reasoning job.
- Automate or chain it.** Chain a profile across every field feeding a new dashboard before it ships, instead of profiling only the one that seems risky.
- Recheck on recurring reports.** If a report runs on a schedule, the field underneath it can drift. Re-profile periodically instead of trusting the check from when you first built it.

## Related recipes

- [Check the master list before you add a new value](./check-value-against-master-list.md) — Before adding a new value to a field, pull the existing values so a new entry doesn't duplicate one under a different name and fragment the master list.
- [Write SQL that runs on the first try](./explore-schema-before-writing-sql.md) — Pull real column names and types from the source schema first, so the SQL you write runs on the first try instead of guessing at a field name that doesn't exist.
- [Triage a data-quality failure with full context](./triage-a-data-quality-failure-with-full-context.md) — Enrich quality failures with lineage, ownership, and downstream impact for faster triage.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/profile-a-field-before-you-build-on-it/
