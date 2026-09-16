---
name: Find the source you can actually trust
slug: find-the-trustworthy-replacement-source
number: 29
summary: When the table you've always been pointed to stops reconciling, find the actual certified
  source instead of guessing at a second bad table.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- AI Builder
- Data Engineer
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- data_quality
- domains
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/find-the-trustworthy-replacement-source/
related:
- triage-assets-for-migration
- safely-deprecate-unused-assets
- reuse-before-you-rebuild
---

# Find the source you can actually trust

When the table you've always been pointed to stops reconciling, find the actual certified source instead of guessing at a second bad table.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, AI Builder, Data Engineer, Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

An analyst has pulled distribution center numbers from `dc_metrics_v1` for months. This week the totals don't reconcile against finance's report, and nobody can say whether the table itself is wrong, stale, or just an old copy that was never cleaned up. Guessing at a second table name gets you a second wrong answer just as easily as a right one.

## What to ask for

- Every candidate source for the concept, found by what it contains rather than by a guessed name
- Certification, owner, and freshness for each candidate
- A source you can defend, or an honest flag that nothing here is certified either

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
I've been told `dc_metrics_v1` is wrong. Find the actual certified source for distribution center data, show me who owns it and when it was last updated, and confirm it isn't itself just a copy of the bad one.
```

## Steps

### 1. Search by concept, scoped to tables.

```text
Find tables (not glossary entries) about <the concept — e.g. distribution center data>, so I see every candidate source, not just the one I suspect is wrong.
```

### 2. Pull certification, owner, and freshness per candidate.

```text
For each candidate, show its certification status, owner, and last-updated date.
```

### 3. Compare against the table you were told is wrong.

```text
Compare the candidates against <dc_metrics_v1> and tell me which is current and actually governed, not just newer-sounding.
```

### 4. Trace upstream to rule out a copy.

```text
Trace the upstream lineage of the strongest candidate to confirm it isn't just a downstream copy of <dc_metrics_v1>.
```

## What you'll need

**Required**

- The concept or domain you need data for
- The table you were originally pointed to and now suspect is wrong

**Optional, but it helps**

- A certification or freshness threshold, if "current" needs a specific cutoff
- The report or number that isn't reconciling, for context on what "right" should look like

## What you get

- A ranked list of candidate source tables with certification, ownership, and lineage evidence attached
- A clear recommendation, or a clear "nothing here is certified either" flag if that's the honest answer

You get a source you can actually point to and defend, backed by who owns it and when it was last touched, instead of a second guess.

**What changed in Atlan:** Read-only. Nothing is updated in Atlan; if the original table should be flagged for cleanup once the replacement is confirmed, that's a separate deprecation step.

## Follow-ups

**Check every suspect table**

```text
Run this same check across every table my team was told is 'the source' before we start the migration.
```

**Close the loop**

```text
Flag the deprecated table for cleanup now that its replacement is confirmed.
```

**Recheck on a cadence**

```text
Re-check this quarterly.
```

## Cook's note

> "Newer" and "certified" aren't the same thing. Don't stop at the first candidate that looks more recently updated; check who actually owns it. And the real source often hides behind a misleading name, ask for tables about the concept, not a table matching a name, so a well-described table with an odd name still surfaces.

- Match the client to the work.** Use a client that shows the full candidate list rather than auto-picking one; you want to see the runner-up sources, not just the top result.
- Automate or chain it.** Batch this across a whole list of suspect tables ahead of a migration, instead of running it one table at a time as each one breaks.
- Recheck before you commit.** Certification status changes. Re-run this right before you switch a pipeline over, not just when you first investigated.

## Related recipes

- [Triage assets for migration](./triage-assets-for-migration.md) — Classify every asset by consumer count, ownership, and certification before migrating.
- [Safely deprecate unused assets](./safely-deprecate-unused-assets.md) — Verify no active consumers exist, notify owners, then mark assets as deprecated.
- [Reuse before you rebuild](./reuse-before-you-rebuild.md) — Before you write SQL to derive a metric, check whether it already exists — and reuse the governed one.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/find-the-trustworthy-replacement-source/
