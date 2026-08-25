---
name: Score assets for AI readiness
slug: score-assets-for-ai-readiness
number: 21
summary: Rate assets on documentation, ownership, and quality before they enter AI pipelines.
job: Govern & keep trusted
action: Make changes
personas:
- AI Builder
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- documentation
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/score-assets-for-ai-readiness/
related:
- keep-asset-metadata-fresh
- gamify-your-context
- propagate-pii-tags-to-parent-assets
---

# Score assets for AI readiness

Rate assets on documentation, ownership, and quality before they enter AI pipelines.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Make changes |
| **Who it serves** | AI Builder, Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

The ml_features schema is about to feed an agent, and before it does, each table needs a description, an owner, a certification, and a PII classification. You want to check those criteria across the schema and write a readiness score you can filter and track on.

## What to ask for

- Every table in ml_features
- A check of each for description, owner, certification, and PII status
- An AI Readiness score written to custom metadata

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
For all tables in the ml_features schema, check if they have descriptions, owners, certifications, and PII classification. Score each one for AI readiness and write the score to the AI Readiness custom metadata field.
```

## Steps

### 1. Search for the assets targeted for AI use.

```text
Find all tables in the <ml_features> schema.
```

### 2. Check each for description, owner, certification, and PII status.

```text
Check each for a description, owner, certification, and PII classification.
```

### 3. Write an AI Readiness score to custom metadata.

```text
Score each for AI readiness and write it to the <AI Readiness> custom metadata field.
```

## What you'll need

**Required**

- The assets targeted for AI use (ml_features)
- The rubric: what "ready" means, and how the criteria weight
- An AI Readiness custom metadata field to write to, and permission to write it

**Optional, but it helps**

- A threshold for "ready" versus "needs work," so the score filters cleanly
- Any criteria to add beyond the four (freshness, a passing quality check)

## What you get

- Every ml_features table with its description, owner, certification, and PII status
- An AI Readiness score per table, against your rubric
- The score written to the AI Readiness custom metadata field

"Is this data fit to feed an agent" becomes a field you can filter, not a judgment call per table. The tables that are not ready are visible, with the reason attached.

**What changed in Atlan:** Changed: the AI Readiness custom metadata field on each scored table. Left untouched: descriptions, owners, certifications, and the data itself, which are read to compute the score, not edited.

## Follow-ups

**Show me the gaps**

```text
List the tables that scored "not ready" and, for each, the one thing missing.
```

**Fix the easy ones**

```text
For tables missing only a description, draft one from the columns so I can approve and raise the score.
```

**Track the trend**

```text
Compare this run to last month's scores and show which tables improved and which slipped.
```

## Cook's note

> Agree on what "ready" means with your team first. The score is only as good as the rubric.

- Match the tool to the work. Scoring is close-reading work; use a more capable model so the rubric is applied consistently across the schema.
- Automate or chain it. Schedule it as the gate before data enters a pipeline: score nightly, and let downstream jobs read the readiness field.
- Ask what it changed. Add "list every table you wrote a score to and the score you wrote." That is the run's record.

## Related recipes

- [Keep asset metadata fresh](./keep-asset-metadata-fresh.md) — Catch stale certifications, missing owners, and outdated descriptions early.
- [Gamify your context](./gamify-your-context.md) — Generate per-domain enrichment scorecards to motivate metadata contributions.
- [Propagate PII tags to parent assets](./propagate-pii-tags-to-parent-assets.md) — Roll column-level PII classification up to parent tables and schemas so policies fire.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/score-assets-for-ai-readiness/
