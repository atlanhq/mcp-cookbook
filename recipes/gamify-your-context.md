---
name: Gamify your context
slug: gamify-your-context
number: 22
summary: Generate per-domain enrichment scorecards to motivate metadata contributions.
job: Govern & keep trusted
action: Look up
personas:
- Data Governance Lead
effort: Quick
runs_in: any AI tool
requires:
- documentation
- domains
- tags
start_here: false
source_url: https://atlan.com/mcp-cookbook/gamify-your-context/
related:
- keep-asset-metadata-fresh
- enrich-assets-with-your-context
- score-assets-for-ai-readiness
---

# Gamify your context

Generate per-domain enrichment scorecards to motivate metadata contributions.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Look up |
| **Who it serves** | Data Governance Lead |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Metadata quality climbs when a team can see where it stands next to its peers. Right now you have no such view: no one knows whether Marketing's data is better documented than Finance's, so no one competes to improve. You want per-domain scorecards that show the gaps and rank the domains.

## What to ask for

- Assets missing descriptions, tags, or certifications
- The gaps grouped by team or domain
- A ranked report, most complete to least

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Generate a metadata completeness report by data domain. For each domain, show how many assets have descriptions, owners, and certifications versus those that don't. Rank domains from most complete to least complete.
```

## Steps

### 1. Search for assets missing descriptions, tags, or certifications.

```text
Find assets missing descriptions, tags, or certifications.
```

### 2. Summarize the gaps grouped by team or domain.

```text
Group the gaps by data domain.
```

### 3. Generate a ranked report to motivate contributions.

```text
Rank the domains from most complete to least complete.
```

## What you'll need

**Required**

- The scope to score (the whole estate, or a set of domains)
- How domains are defined in your setup (by tag, by owning team, by schema)

**Optional, but it helps**

- Which fields count toward "complete" (description, owner, certification, tags)
- A prior report to compare against, so you can show movement

## What you get

- The count of complete versus incomplete assets, per domain
- The specific gaps each domain carries
- A leaderboard, most complete domain to least

Metadata quality becomes visible and comparable, so teams have a reason to close their gaps. A leaderboard in a channel moves more metadata than a policy memo.

**What changed in Atlan:** Nothing is written. This recipe reads metadata and produces a report; the assets are untouched.

## Follow-ups

**Give a domain its list**

```text
For the bottom domain, list its ten most-queried assets (where usage data exists) that are missing a description, so they know where to start.
```

**Make it shareable**

```text
Format the leaderboard as a short post I can drop in a team channel.
```

**Show the movement**

```text
Compare this to last month's report and highlight the domain that improved most.
```

## Cook's note

> Share the leaderboard in a team channel. Nothing moves metadata like friendly rivalry.

- Match the tool to the work. Any AI tool works; the recipe reads and reports, so there is nothing to review before it runs.
- Automate or chain it. Schedule it monthly and post the leaderboard automatically, so the standings stay live without anyone pulling them.
- It only reads. No writes, so run it as often as you like; pair it with the enrichment recipes to actually close the gaps it surfaces.

## Related recipes

- [Keep asset metadata fresh](./keep-asset-metadata-fresh.md) — Catch stale certifications, missing owners, and outdated descriptions early.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Score assets for AI readiness](./score-assets-for-ai-readiness.md) — Rate assets on documentation, ownership, and quality before they enter AI pipelines.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/gamify-your-context/
