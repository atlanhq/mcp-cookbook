---
name: Check the master list before you add a new value
slug: check-value-against-master-list
number: 28
summary: Before adding a new value to a field, pull the existing values so a new entry doesn't
  duplicate one under a different name and fragment the master list.
job: Govern & keep trusted
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- Data Governance Lead
effort: Quick
runs_in: any AI tool
requires: []
start_here: true
source_url: https://atlan.com/mcp-cookbook/check-value-against-master-list/
related:
- profile-a-field-before-you-build-on-it
- reconcile-terminology-across-systems
- grow-your-business-glossary
---

# Check the master list before you add a new value

Before adding a new value to a field, pull the existing values so a new entry doesn't duplicate one under a different name and fragment the master list.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, Data Governance Lead |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Someone's about to add a new category to a field, say a new `product_category` value, but the field already has a governed set of values. If the new one duplicates an existing value under a slightly different name, "Eco" vs "Eco-Friendly" vs "Green", it fragments the master list and quietly breaks every report that groups by it. Before adding, they check what's already there.

## What to ask for

- The current set of distinct values already on the field
- Whether the value you're about to add already exists under another name
- A clear reuse-or-add decision, instead of a silent duplicate

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Before I add `Eco-Friendly` to `product_category`, show me the existing distinct values so I can tell if it already exists under another name.
```

## Steps

### 1. Pull the current value set.

```text
List the existing distinct values in <product_category>, so I can see the master list I'd be adding to.
```

### 2. Check the proposed value against it.

```text
Does <Eco-Friendly> already exist in that list, exactly or as a near-variant like <Eco> or <Green>? Flag the closest matches.
```

### 3. Decide: reuse or add.

```text
Recommend whether to reuse an existing value or add a genuinely new one, and if new, whether <Eco-Friendly> fits the naming pattern of the rest.
```

## What you'll need

**Required**

- The field you're adding a value to
- The value you're proposing to add
- Read access to the connected source through Atlan, with query permission

**Optional, but it helps**

- The naming convention for the field, if one exists, so a new value can be checked against it
- Any governed term or documentation that defines the allowed set

## What you get

- The current distinct values in the field, the effective master list
- The closest existing matches to your proposed value, exact or near-variant
- A reuse-or-add recommendation, with a naming-fit check if it's genuinely new

You add a value that fits the governed set instead of a near-duplicate that fragments it, so reports that group by the field keep reconciling.

**What changed in Atlan:** Read-only in Atlan. It checks the existing values so you can decide; the value itself is added in the source system, not here.

## Follow-ups

**Check the whole load**

```text
Run this check across every field I'm about to add values to in this load, not just one.
```

**Find near-duplicates**

```text
Show me values that already look like near-duplicates of each other, so I can flag the mess that's already there.
```

**Define it properly**

```text
If we add it, draft a one-line definition so the next person knows when to use it.
```

## Cook's note

> The expensive mistake isn't a typo, it's a synonym. "Eco" and "Eco-Friendly" both look fine until a report splits one category into two.

- Match the client to the work.** Use a client that shows the full existing value list, so you're judging against everything, not just the top few.
- Automate or chain it.** Run this ahead of any bulk load that introduces new category values, so variants get caught before they land, not after.
- Ask what it found.** Have it list the near-variants it matched against, so the reuse-or-add call is on the record.

## Related recipes

- [Profile a field's shape before you build on it](./profile-a-field-before-you-build-on-it.md) — Get a quick profile of a field, its type, null rate, distinct count, and range, so you know what you're working with before you aggregate or join on it.
- [Give one concept one trusted definition](./reconcile-terminology-across-systems.md) — Confirm whether two differently-named fields or terms mean the same thing, then link them under one governed definition so the next person searching either name lands in the same place.
- [Grow your business glossary](./grow-your-business-glossary.md) — Bootstrap glossary terms from how your assets already use business concepts.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/check-value-against-master-list/
