---
name: Ground AI-written code in your real schema
slug: ground-code-in-real-schema
number: 31
summary: Pull exact column names, types, and certification status for the tables your fix
  touches, before your coding agent writes a line of SQL.
job: Find & understand data
action: Look up
personas:
- AI Builder
- Data Engineer
effort: Quick
runs_in: any AI tool
requires:
- documentation
start_here: false
source_url: https://atlan.com/mcp-cookbook/ground-code-in-real-schema/
related:
- document-sql-with-business-context
- see-what-a-sql-change-will-break-before-you-merge
- explore-schema-before-writing-sql
---

# Ground AI-written code in your real schema

Pull exact column names, types, and certification status for the tables your fix touches, before your coding agent writes a line of SQL.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | AI Builder, Data Engineer |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

A coding agent is about to fix a broken revenue query against `fct_orders`. It has two candidate column names in mind for the discount field and no way to tell which one is real. Guess wrong here and the fix either fails outright or, worse, runs clean against the wrong column and quietly reports the wrong number to finance.

## What to ask for

- The real columns and types on the table, not the ones the agent guessed
- Which of them are certified, and whether a governed definition already covers them
- Confirmation that nothing changed underneath you recently

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Before you touch the query, pull the real columns and types on `fct_orders`, tell me which ones are certified, and flag if any glossary term already defines what 'discount' means on this table.
```

## Steps

### 1. Find the exact table.

```text
Find the <fct_orders> table in the <schema> schema, by description if you're unsure of the exact name.
```

### 2. Pull columns, types, and certification.

```text
Show its columns, data types, and certification status, so I'm coding against what's actually there.
```

### 3. Check for a governed definition.

```text
Check whether <the column — e.g. discount> has a governed glossary definition, so it means the same in my code as it does to the business.
```

### 4. Confirm nothing changed recently.

```text
Show the certification date and any open announcements on <fct_orders> before I commit the fix.
```

## What you'll need

**Required**

- The table name, or a close description of it, and the schema it lives in
- Read access to metadata for that schema

**Optional, but it helps**

- The draft SQL or script you're about to run, so the agent can check it against the real columns directly
- The specific business term you're worried about (e.g. "discount", "revenue")

## What you get

- The real column list, types, and certification status for the table
- The governed definition for any business term you flagged, if one exists
- A go/no-go read on whether your draft SQL references anything that doesn't exist or is deprecated

You now know the fix is being written against what the table actually contains, not a guess, and you know whether the term you're using in your query matches what the business means by it.

**What changed in Atlan:** Read-only. Nothing in Atlan is written or updated; this only pulls context into your coding session.

## Follow-ups

**Cover the whole pipeline**

```text
Do the same check across every table this pipeline touches before I run the full refactor.
```

**Check downstream impact**

```text
Trace what else depends on this table before I change a column.
```

**Recheck before merge**

```text
Re-run this check right before I merge, not just when I started.
```

## Cook's note

> The five minutes this costs you is cheaper than the hour you'll spend debugging a query that ran clean against the wrong column.

- Match the client to the work.** Run this inside whatever coding agent you're already using; you want the context to land in the same session where you're about to write the fix, not in a separate tab.
- Automate or chain it.** Wire this into the start of every coding session touching production tables, or chain it as a pre-commit check on any PR that changes a SQL file referencing a known schema.
- Recheck on long sessions.** If your coding session runs for hours, the schema underneath you can change. Re-pull column and certification status before you actually run the fix, not just when you started writing it.

## Related recipes

- [Document SQL with business context](./document-sql-with-business-context.md) — Generate business-readable descriptions for SQL models from the context already in Atlan.
- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Find every downstream consumer of a changed column or table before merging.
- [Write SQL that runs on the first try](./explore-schema-before-writing-sql.md) — Pull real column names and types from the source schema first, so the SQL you write runs on the first try instead of guessing at a field name that doesn't exist.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/ground-code-in-real-schema/
