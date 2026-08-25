---
name: Route data requests to right assets
slug: route-data-requests-to-right-assets
number: 1
summary: Surface certified, well-documented assets in response to a business request.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- Data Governance Lead
effort: Quick
runs_in: any AI tool
requires:
- documentation
start_here: false
source_url: https://atlan.com/mcp-cookbook/route-data-requests-to-right-assets/
related:
- talk-to-your-data
- gamify-your-context
- give-your-dashboards-context
---

# Route data requests to right assets

Surface certified, well-documented assets in response to a business request.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, Data Governance Lead |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

A stakeholder wants to build a monthly churn analysis and asks for "the churn data." What they need is the right certified table with an owner and an explanation, not a raw list of every table with "churn" in the name. You want to read the request as business concepts and return what is ready to use.

## What to ask for

- The request stated as business concepts
- The most relevant certified tables or dashboards
- Who owns each and what it contains

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
A business stakeholder needs data to build a monthly churn analysis. Find the most relevant certified tables or dashboards in Atlan, show who owns them, and explain what each one contains.
```

## Steps

### 1. Search for certified assets that match the request.

```text
A stakeholder needs data for a <monthly churn analysis> — find the most relevant certified tables or dashboards.
```

### 2. Pull ownership and access for the top matches.

```text
For each, show who owns it and how to get access.
```

### 3. Return a ranked shortlist with a plain-English explanation of each.

```text
Rank them by fit and explain what each one contains.
```

## What you'll need

**Required**

- The business request, as concepts (a monthly churn analysis)

**Optional, but it helps**

- Any constraint: certified only, a specific domain, or a freshness bar
- The requester's access, so you can flag what they can already use

## What you get

- A ranked list of certified tables and dashboards that fit the request
- The owner of each (usually a team), and how to get access
- A plain explanation of what each contains

A vague ask returns a short, trustworthy shortlist instead of a raw table dump, so the requester starts from certified data and the "which table?" thread ends before it starts.

**What changed in Atlan:** Nothing is written. This recipe searches and reads metadata to answer the request; nothing in Atlan changes.

## Follow-ups

**Narrow it**

```text
Of these, which single table would you start with for a monthly churn analysis, and why?
```

**Fill the gap**

```text
If nothing certified fully fits, tell me what's missing so I can request or build it.
```

**Hand it off**

```text
Draft a short reply to the stakeholder listing the recommended asset, its owner, and how to get access.
```

## Cook's note

> Point people at certified assets. It's the fastest way to end the "which table?" Slack threads.

- Match the tool to the work. Use any AI tool; the recipe reads and recommends, so it is safe to run for any incoming request.
- Automate or chain it. Put it behind a request form or Slack channel, so every "I need data for X" gets a certified shortlist back automatically.
- It only reads. No writes, so route as many requests through it as you like without touching a single asset.

## Related recipes

- [Talk to your data](./talk-to-your-data.md) — Pair Atlan with your warehouse or SQL-tool MCP to find the right certified data in plain language, then go straight to it.
- [Gamify your context](./gamify-your-context.md) — Generate per-domain enrichment scorecards to motivate metadata contributions.
- [Give your dashboards context](./give-your-dashboards-context.md) — Link BI dashboards to business terms and owners so they show up in search.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/route-data-requests-to-right-assets/
