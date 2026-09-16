---
name: See exactly what a migration would leave behind
slug: compare-two-sources-before-a-migration-decision
number: 30
summary: Line up two connections, databases, or schemas and see exactly what matches, what's
  missing, and what only exists on one side, before you commit to a migration or consolidation
  plan.
job: Retire & migrate
action: Look up
personas:
- Data Engineer
effort: Moderate
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/compare-two-sources-before-a-migration-decision/
related:
- find-the-trustworthy-replacement-source
- triage-assets-for-migration
- safely-deprecate-unused-assets
---

# See exactly what a migration would leave behind

Line up two connections, databases, or schemas and see exactly what matches, what's missing, and what only exists on one side, before you commit to a migration or consolidation plan.

| | |
|---|---|
| **Use case** | Retire & migrate |
| **Action** | Look up |
| **Who it serves** | Data Engineer |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

A migration plan says `LEGACY_SALES` is being replaced by `CONFORMED_SALES`, and someone needs to sign off that nothing gets lost in the switch. Eyeballing two schema browsers side by side in separate tabs misses the tables that only exist on one side, the ones that look the same but aren't, and the ones nobody's opened in two years. The decision needs an actual list, not a skim.

## What to ask for

- The full table list on each of the two sources
- Which tables match across both
- Exactly what exists on only one side, so nothing gets silently left behind

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Compare every table in `LEGACY_SALES` against `CONFORMED_SALES`. Tell me which ones match, which exist only in `LEGACY_SALES`, and which exist only in `CONFORMED_SALES`.
```

## Steps

### 1. Pull the first source's tables.

```text
List every table in <LEGACY_SALES>.
```

### 2. Pull the second source's tables.

```text
List every table in <CONFORMED_SALES>.
```

### 3. Match across both lists.

```text
Match the two lists by name and structure; flag exact matches, close-but-not-identical matches, and anything with no counterpart.
```

### 4. List what exists on only one side.

```text
Give me the tables that exist on only one side, split by which source, since those are the migration calls someone has to make.
```

## What you'll need

**Required**

- The two connections, databases, or schemas you're comparing, named exactly as they appear in Atlan

**Optional, but it helps**

- Whether you want column-level comparison within matched tables, or just table-level presence
- A known list of intentional exceptions (tables that are supposed to be one-sided), so those don't show up as false alarms

## What you get

- A matched list: tables present in both sources
- A one-sided list: tables that exist only in one source, split out by which one
- Optionally, a column-level diff for the tables that matched but might not be identical

You get an actual coverage report to sign a migration off on, not a gut check from skimming two browser tabs.

**What changed in Atlan:** Read-only. This produces a comparison; nothing in either source gets modified, moved, or flagged.

## Follow-ups

**Go column-level**

```text
Run this again at the column level for the tables that matched by name.
```

**Check what's still in use**

```text
Flag any one-sided table that still has active downstream consumers.
```

**Recheck before cutover**

```text
Re-run this the week before cutover.
```

## Cook's note

> A name match isn't a content match. Two tables can be called the same thing and hold different data, or be called different things and hold the same data. Don't sign off on the name list alone.

- Match the client to the work.** Use a client that can hold a long output well, this comparison gets wide fast on anything beyond a handful of tables.
- Automate or chain it.** Run this as a recurring check throughout the migration window, not once at the start, so drift between the two sides shows up before cutover instead of during it.
- Ask what it changed.** Even though this is read-only, ask for the diff in a form you can attach to the migration ticket: a clean list of matched, missing, and one-sided tables, dated.

## Related recipes

- [Find the source you can actually trust](./find-the-trustworthy-replacement-source.md) — When the table you've always been pointed to stops reconciling, find the actual certified source instead of guessing at a second bad table.
- [Triage assets for migration](./triage-assets-for-migration.md) — Classify every asset by consumer count, ownership, and certification before migrating.
- [Safely deprecate unused assets](./safely-deprecate-unused-assets.md) — Verify no active consumers exist, notify owners, then mark assets as deprecated.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/compare-two-sources-before-a-migration-decision/
