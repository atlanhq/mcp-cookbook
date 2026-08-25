---
name: Know what your domain owns, and whether it's live
slug: navigate-data-products-by-domain
number: 25
summary: Ask what data products exist under a business domain and what actually backs one
  of them, instead of hunting table by table.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- Data Governance Lead
effort: Moderate
runs_in: any AI tool
requires:
- domains
start_here: false
source_url: https://atlan.com/mcp-cookbook/navigate-data-products-by-domain/
related:
- gamify-your-context
- route-data-requests-to-right-assets
- score-assets-for-ai-readiness
---

# Know what your domain owns, and whether it's live

Ask what data products exist under a business domain and what actually backs one of them, instead of hunting table by table.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, Data Governance Lead |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

In Monday standup, the Finance domain lead gets asked how many data products exist under the Opportunity Pipeline product line, and which tables actually feed it. The honest answer today involves opening three different schema browsers and hoping nothing's missing. There's no single place to ask "what do we own, and what's actually behind it."

## What to ask for

- The data products registered under the domain
- The tables and columns that actually back a given product
- Whether those backing assets are still being fed, or have quietly gone stale

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
List the data products registered under the Finance domain, then show me exactly which tables and columns back the Opportunity Pipeline product, and whether that product is actively fed by anything upstream.
```

## Steps

### 1. Find the domain.

```text
Confirm the <domain — e.g. Finance> domain exists and show its details.
```

### 2. List its data products.

```text
List every data product registered under the <domain> domain, so I have the full inventory in front of me.
```

### 3. Pull what backs one product.

```text
For the <product — e.g. Opportunity Pipeline> product, show the underlying tables and columns that back it.
```

### 4. Check it's actively fed.

```text
Show whether <product>'s assets have active upstream lineage, so I know if it's genuinely fed or quietly stale.
```

## What you'll need

**Required**

- The domain name you're asking about
- The specific product name, if you're going deeper than the inventory list

**Optional, but it helps**

- An ownership filter, if you only want products a specific team owns
- A freshness threshold, if staleness is the actual concern

## What you get

- A list of data products registered under the domain
- The concrete tables and columns backing the one product you drilled into
- A lineage read confirming whether that product is actively fed or stale

You walk into standup with the actual inventory and a real answer on freshness, not "I think we have a few things under Finance."

**What changed in Atlan:** Read-only. Nothing is written; this only surfaces what's already registered.

## Follow-ups

**Roll it up**

```text
Roll this up across every domain for a full data mesh coverage report.
```

**Find the gaps**

```text
Which products in this domain have no owner assigned?
```

**Make it recurring**

```text
Re-run this monthly as a standing input to the domain review.
```

## Cook's note

> The domain list answers "what do we own." The lineage check answers "is it actually alive." Don't stop at the first one.

- Match the client to the work.** This reads well in a chat client threaded into a recurring standup channel, since the answer doubles as a status update for the room.
- Automate or chain it.** Schedule this as a recurring pull ahead of your domain review cadence, instead of someone manually compiling it the morning of.
- Recheck before you report it.** Data products get added and deprecated between reviews. Re-pull the inventory right before you present it, not from last month's notes.

## Related recipes

- [Gamify your context](./gamify-your-context.md) — Generate per-domain enrichment scorecards to motivate metadata contributions.
- [Route data requests to right assets](./route-data-requests-to-right-assets.md) — Surface certified, well-documented assets in response to a business request.
- [Score assets for AI readiness](./score-assets-for-ai-readiness.md) — Rate assets on documentation, ownership, and quality before they enter AI pipelines.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/navigate-data-products-by-domain/
