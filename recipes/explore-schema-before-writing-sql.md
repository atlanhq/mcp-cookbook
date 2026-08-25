---
name: Write SQL that runs on the first try
slug: explore-schema-before-writing-sql
number: 23
summary: Pull real column names and types from the source schema first, so the SQL you write
  runs on the first try instead of guessing at a field name that doesn't exist.
job: Find & understand data
action: Look up
personas:
- Data/BI Analyst
- AI Builder
- Data Engineer
effort: Quick
runs_in: any AI tool
requires:
- documentation
start_here: false
source_url: https://atlan.com/mcp-cookbook/explore-schema-before-writing-sql/
related:
- see-what-a-sql-change-will-break-before-you-merge
- ground-code-in-real-schema
- check-value-against-master-list
---

# Write SQL that runs on the first try

Pull real column names and types from the source schema first, so the SQL you write runs on the first try instead of guessing at a field name that doesn't exist.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/BI Analyst, AI Builder, Data Engineer |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

An analyst needs a query against the `reporting` schema listing every customer and their orders, but doesn't know the exact table or column names going in. Someone else needs to know which status codes can actually update a record before writing the `WHERE` clause. Both are one failed query away from a wrong guess at a column name, or worse, a query that runs clean against the wrong field and returns a plausible-looking wrong answer.

## What to ask for

- The tables in the schema that relate to what you need, matched on what they contain rather than a name you're guessing at
- Every column on those tables with its exact name, data type, and any description on record
- A query written against those confirmed names, with any column that doesn't exist flagged before you run it

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Before I write this query, show me the tables and columns in the `reporting` schema that relate to customers and their orders, with their real names and types.
```

## Steps

### 1. Find the tables the question is about.

```text
Find the tables in the <schema> schema that relate to <what you need — e.g. customers and their orders>. Match on a description, not just names I'm guessing at.
```

### 2. Pull their real columns, types, and descriptions.

```text
For those tables, list every column with its exact name, data type, and any description on record, so I write against what's actually there.
```

### 3. Write the query against the confirmed names.

```text
Using only the columns you just confirmed, write the query for <what you're trying to answer>, and flag any column I reference that doesn't exist in the schema you pulled.
```

## What you'll need

**Required**

- The schema or table name, or a description close enough to find it
- What you're trying to answer or build with the query

**Optional, but it helps**

- A first-draft query you already have, so it can check it against the real schema instead of building blind
- Any known naming quirks in the source (e.g. non-English column names, legacy naming conventions)

## What you get

- The confirmed table and column names, types, and descriptions for the schema in question
- A query written against those confirmed names, ready to run

The query runs against real columns on the first attempt, instead of failing on a guessed name or, worse, running clean against the wrong one.

**What changed in Atlan:** Read-only. Nothing in Atlan is written or updated; this only pulls schema context ahead of writing SQL elsewhere.

## Follow-ups

**Check for governed definitions**

```text
Check if any of these columns already have a governed definition before I use them in a report.
```

**Widen it to the whole query**

```text
Do the same check across every table this report joins, not just the first one.
```

**Catch anything being retired**

```text
Flag if any of these columns are deprecated or scheduled for removal.
```

## Cook's note

> The failure mode that costs you time isn't the query that errors out, it's the one that runs clean against a column that means something slightly different than you assumed.

- Match the client to the work. Run this in whatever client you're about to write the SQL in, so the schema context lands in the same session as the query.
- Automate or chain it. Chain this ahead of every ad-hoc query against an unfamiliar schema, not just the first time you touch it. Naming conventions vary enough between schemas that "I checked it last month" isn't the same as checking it now.
- Confirm what it used. This is read-only, so nothing changes — but when you paste the query back in afterward, ask it to confirm every column you reference actually exists in the schema it pulled.

## Related recipes

- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Trace lineage downstream from a SQL change to see what it affects before it lands.
- [Ground AI-written code in your real schema](./ground-code-in-real-schema.md) — Give a coding agent the real column names and types so the code it writes compiles against what's actually there.
- [Check the master list before you add a new value](./check-value-against-master-list.md) — Confirm a value against the governed reference list before introducing a duplicate.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/explore-schema-before-writing-sql/
