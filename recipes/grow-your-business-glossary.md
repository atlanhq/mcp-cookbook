---
name: Grow your business glossary
slug: grow-your-business-glossary
number: 15
summary: Bootstrap glossary terms from how your assets already use business concepts.
job: Make data understandable
action: Make changes
personas:
- Data Governance Lead
- Data/BI Analyst
effort: Moderate
runs_in: any AI tool
requires:
- glossary
start_here: false
source_url: https://atlan.com/mcp-cookbook/grow-your-business-glossary/
related:
- document-sql-with-business-context
- enrich-assets-with-your-context
- give-your-dashboards-context
---

# Grow your business glossary

Bootstrap glossary terms from how your assets already use business concepts.

| | |
|---|---|
| **Use case** | Make data understandable |
| **Action** | Make changes |
| **Who it serves** | Data Governance Lead, Data/BI Analyst |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

"Customer lifetime value" shows up in a dozen tables, three dashboards, and half your dbt models, spelled LTV in some and CLV in others, and it has no canonical definition anywhere. You want a real term in the glossary, drafted from how the concept is actually used, with the relevant assets linked to it.

## What to ask for

- Every asset that references customer lifetime value or LTV
- A definition drafted from how those assets use it
- A glossary term created and the assets linked to it

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Find all assets that reference customer lifetime value or LTV. Create a glossary term called Customer Lifetime Value with a definition based on how these assets use it, then link them to the term.
```

## Steps

### 1. Search for assets that reference the concept.

```text
Find all assets that reference <concept, e.g. customer lifetime value>.
```

### 2. Draft a definition from how it's used across those assets.

```text
Draft a definition based on how these assets use it.
```

### 3. Create the term and link the relevant assets to it.

```text
Create a glossary term called <name> and link these assets to it.
```

## What you'll need

**Required**

- The business concept to bootstrap (and its aliases: LTV, CLV)
- Glossary creation permission
- A glossary to create the term in

**Optional, but it helps**

- A preferred definition style (one sentence, or definition plus formula)
- Any assets to exclude, such as sandbox or test tables

## What you get

- The set of assets that reference the concept, by name and type
- A draft definition of Customer Lifetime Value, written from that usage
- The glossary term created, with the assets linked to it

You edit a first draft instead of starting from a blank page, and the term ships linked to the assets that actually use it, so the definition is discoverable the moment someone lands on one of them.

**What changed in Atlan:** Changed: a new glossary term, and glossary links on the matched assets. Left untouched: the asset descriptions and the data; only the link is added.

## Follow-ups

**Do the next concept**

```text
Now the same for "active user," and note where the definition looks inconsistent across assets.
```

**Sharpen the definition**

```text
Rewrite the definition to one sentence a new analyst would understand, and add the formula the tables use.
```

**Fill the gaps**

```text
List assets that clearly use this concept but do not name it, so I can decide whether to link them.
```

## Cook's note

> Let Atlan write the first draft of the definition. You edit; you don't start from a blank page.

- Match the tool to the work. Definitions read better from a model built for close reading; use a more capable model, review the draft, then create the term.
- Automate or chain it. Run it as a monthly sweep for undefined high-use concepts, so the glossary grows from real usage instead of a backlog.
- Ask what it changed. Add "list the term you created and every asset you linked." A new term and its links are worth confirming.

## Related recipes

- [Document SQL with business context](./document-sql-with-business-context.md) — Generate business-readable descriptions for SQL models from the context already in Atlan.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Give your dashboards context](./give-your-dashboards-context.md) — Link BI dashboards to business terms and owners so they show up in search.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/grow-your-business-glossary/
