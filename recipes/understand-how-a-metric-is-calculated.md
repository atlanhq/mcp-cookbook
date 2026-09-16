---
name: Understand how a metric is calculated
slug: understand-how-a-metric-is-calculated
number: 2
summary: Get the governed definition of a metric — and where it's documented — without asking
  a data engineer.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- AI Builder
effort: Quick
runs_in: any AI tool
requires:
- documentation
start_here: false
source_url: https://atlan.com/mcp-cookbook/understand-how-a-metric-is-calculated/
related:
- reuse-before-you-rebuild
- get-build-ready-for-a-new-dashboard
- see-what-a-sql-change-will-break-before-you-merge
---

# Understand how a metric is calculated

Get the governed definition of a metric — and where it's documented — without asking a data engineer.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, AI Builder |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

"How is MRR calculated?" keeps landing on the data team. It's not a task, it's a question — and the answer already lives in a governed glossary term. Anyone can ask Atlan for it directly instead of routing it through an engineer.

## What to ask for

- The governed definition of the metric
- The calculation
- Where it's documented, and who owns it

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
How is MRR calculated here, and where is that documented?
```

## Steps

### 1. Look up the governed term for the metric.

```text
Find the governed glossary term for <metric>.
```

### 2. Return its definition and calculation.

```text
Show the plain-English definition and the exact calculation.
```

### 3. Show who owns it and which certified assets carry it.

```text
Tell me who owns the term and which certified tables or columns use it, so I query the official one.
```

## What you'll need

**Required**

- The metric or term name (an alias is fine — MRR, monthly recurring revenue)

**Optional, but it helps**

- Whether you want the SQL/formula or just the plain-English definition
- No Atlan training needed — ask like you'd ask a coworker who knows
- If the metric is defined in more than one glossary (say a team copy and a company one), ask for the certified, company-level term so you get the canonical number

## What you get

- The governed term — e.g. the VERIFIED "Monthly Recurring Revenue" term, owned by finance: "the normalized amount of subscription revenue the company expects to earn each month from active customer contracts; excludes one-time charges but includes usage not contracted to recur"
- The calculation, and the certified assets that carry the term

The official definition, straight from the source, in one ask. The person who needed it never had to interrupt an engineer.

**What changed in Atlan:** Nothing is written — it reads the governed term and returns it.

## Follow-ups

**Show me the math**

```text
If the term only stores a prose definition, reconstruct the calculation from the linked certified column so I can see the exact math.
```

**Which one's canonical?**

```text
Among the certified assets that carry this term, which is the most-queried one I should treat as canonical?
```

**Is it on the column?**

```text
Is the calculation documented on the specific column I'd query, or only on the term?
```

## Cook's note

> The governed, certified term is the answer — not the first column that happens to be named for the metric.

- Match the tool to the work. Any AI tool works; the recipe reads and returns, nothing to set up.
- Automate or chain it. Put it behind a Slack assistant so "how is X calculated?" is answered from Atlan without a ticket.
- It only reads. No writes — the point is self-serve: whoever asked could have asked Atlan directly.

## Related recipes

- [Reuse before you rebuild](./reuse-before-you-rebuild.md) — Before you write SQL to derive a metric, check whether it already exists — and reuse the governed one.
- [Get build-ready for a new dashboard](./get-build-ready-for-a-new-dashboard.md) — Before you build a dashboard: the trusted source, the confirmed definition, and how the data is really used — as the build recipe.
- [See what a SQL change will break before you merge](./see-what-a-sql-change-will-break-before-you-merge.md) — Find every downstream consumer of a changed column or table before merging.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/understand-how-a-metric-is-calculated/
