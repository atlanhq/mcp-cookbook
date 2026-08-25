---
name: Give your dashboards context
slug: give-your-dashboards-context
number: 13
summary: Link BI dashboards to business terms and owners so they show up in search.
job: Make data understandable
action: Make changes
personas:
- Data Governance Lead
- Data/BI Analyst
effort: Quick
runs_in: any AI tool
requires:
- glossary
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/give-your-dashboards-context/
related:
- enrich-assets-with-your-context
- grow-your-business-glossary
- route-data-requests-to-right-assets
---

# Give your dashboards context

Link BI dashboards to business terms and owners so they show up in search.

| | |
|---|---|
| **Use case** | Make data understandable |
| **Action** | Make changes |
| **Who it serves** | Data Governance Lead, Data/BI Analyst |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

Your Tableau site has hundreds of dashboards, and the two everyone actually opens, Revenue Overview and Customer Churn, have no owner, no description, and no glossary link. So they never surface in search, and no one can govern them. You want to give them the context that makes them findable and trustworthy.

## What to ask for

- Find the two dashboards in Tableau
- Set the Finance team as owner
- Link them to the Revenue and Churn Rate glossary terms

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Find the Revenue Overview and Customer Churn dashboards in Tableau. Add the Finance team as owner and link them to the Revenue and Churn Rate glossary terms.
```

## Steps

### 1. Search for the dashboards by name or business area.

```text
Find the <dashboard name> dashboards in <BI tool>.
```

### 2. Review the gaps: missing owners, terms, descriptions.

```text
Show which are missing an owner, description, or glossary link.
```

### 3. Add business terms and owners.

```text
Add <team> as owner and link them to the <term> and <term> glossary terms.
```

## What you'll need

**Required**

- The dashboards, by name or business area
- The glossary terms to link (they must already exist)
- Permission to update dashboard metadata

**Optional, but it helps**

- The owning team's naming in Atlan, so the owner resolves cleanly
- A tag scheme for business area, if you group dashboards that way

## What you get

- The matched dashboards with their current gaps listed
- The Finance team set as owner on each
- Glossary links from each dashboard to Revenue and Churn Rate

The dashboards now resolve when someone searches "revenue" or "churn," and they carry an owner and a definition, so a viewer knows what they are looking at and who to ask.

**What changed in Atlan:** Changed: owner and glossary links on the two dashboards. Left untouched: the dashboards themselves in Tableau, and the glossary terms, which are only linked, not edited.

## Follow-ups

**Cover the rest of the workbook**

```text
Do the same for every dashboard in the Finance workbook that is missing an owner.
```

**Add a description too**

```text
For these dashboards, draft a one-line description of what each shows and who uses it, then save it.
```

**Find the orphans**

```text
List every Tableau dashboard in this workbook that still has no owner or description, so I can prioritize the gaps.
```

## Cook's note

> Link the glossary term first. Search picks the dashboard up the moment it's connected.

- Match the tool to the work. This writes to dashboard metadata; run it in an AI tool that shows the plan first, confirm the term links, then let it save.
- Automate or chain it. Chain it after every BI publish: search for dashboards added this week with no owner, and draft the owner and term links for review.
- Ask what it changed. Add "tell me which dashboards you edited and which terms you linked." For linking work, that is the audit trail.

## Related recipes

- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and richer descriptions.
- [Grow your business glossary](./grow-your-business-glossary.md) — Bootstrap glossary terms from how your assets already use business concepts.
- [Route data requests to right assets](./route-data-requests-to-right-assets.md) — Surface certified, well-documented assets in response to a business request.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/give-your-dashboards-context/
