---
name: Reach the real owner, not the wrong person
slug: find-the-right-owner-to-contact
number: 32
summary: Trace a failing number back to the asset behind it, then find out who owns that dataset,
  so the problem reaches the team accountable for it instead of a general channel.
job: Govern & keep trusted
action: Look up
personas:
- Data/Business User
- Data Engineer
- Data Governance Lead
effort: Quick
runs_in: any AI tool
requires:
- data_quality
- owners
start_here: false
source_url: https://atlan.com/mcp-cookbook/find-the-right-owner-to-contact/
related:
- route-data-requests-to-right-assets
- warn-downstream-owners-before-a-change-lands
- triage-a-data-quality-failure-with-full-context
---

# Reach the real owner, not the wrong person

Trace a failing number back to the asset behind it, then find out who owns that dataset, so the problem reaches the team accountable for it instead of a general channel.

| | |
|---|---|
| **Use case** | Govern & keep trusted |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data Engineer, Data Governance Lead |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

A revenue dashboard is showing figures that don't reconcile, and the analyst who spotted it has no idea which upstream asset is actually at fault or who to tell. Posting "revenue looks wrong" in a general channel gets a day of guessing and no owner. The fix is to identify the asset behind the number first, then resolve who's accountable for that specific asset — because the right contact depends entirely on which asset turns out to be the problem.

## What to ask for

- The asset the failing number actually comes from
- Its data quality status, including whether the failure is already known
- Who owns that dataset, and the team accountable for it

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Revenue numbers aren't reconciling. Find the asset behind the revenue figures, check its data quality status, and tell me who owns it so I can raise this with the right team.
```

## Steps

### 1. Find the asset behind the number.

```text
Find the certified asset that the <revenue> figures come from, so I know which one is actually behind the number that's wrong.
```

### 2. Check what its data quality status says.

```text
Show me that asset's data quality status and any recent failures or incidents on it, so I know whether the problem is already known.
```

### 3. Resolve who's accountable for it.

```text
Show me the owner of that asset, so I can raise this with the team accountable for it rather than a general channel.
```

## What you'll need

**Required**

- The number, metric, or dashboard that looks wrong

**Optional, but it helps**

- Where you saw it, if the same figure appears in more than one place
- How urgent it is, which changes whether you raise it now or queue it

## What you get

- The asset the failing number actually comes from
- Its data quality status, including whether the failure is already known
- The owner accountable for that asset, so you know who to raise it with

The problem goes to whoever is accountable for the specific asset at fault, with the quality status already attached, instead of a general channel where it waits for someone to guess which table is wrong.

**What changed in Atlan:** Read-only. Nothing is updated in Atlan; this identifies the asset, its status, and its owner.

## Follow-ups

**Look further upstream**

```text
Trace the lineage upstream from that asset to see whether the problem starts further back.
```

**Find ownership gaps**

```text
Check ownership coverage across this domain.
```

**See who else is affected**

```text
Show me everything else that depends on that asset.
```

## Cook's note

> Find the asset before you look for the owner. Ownership is only useful once you know which asset is actually at fault — reaching the owner of the dashboard when the problem is three tables upstream just moves the guessing to someone else's inbox.

- Match the client to the work.** Any client works here; this is a short lookup, not a multi-step reasoning job.
- Automate or chain it.** Wire this into the channel where quality alerts land, so an alert arrives with its asset and owner already resolved.
- Recheck before you escalate.** Ownership and quality status both change. Re-pull them right before you raise it, not from a check you ran days ago — otherwise you escalate a failure that's already been fixed, or route it to someone who's handed the asset on.

## Related recipes

- [Route data requests to right assets](./route-data-requests-to-right-assets.md) — Surface certified, well-documented assets in response to a business request.
- [Warn downstream owners before a change lands](./warn-downstream-owners-before-a-change-lands.md) — Find every downstream consumer of a changing asset and warn their owners first.
- [Triage a data-quality failure with full context](./triage-a-data-quality-failure-with-full-context.md) — Enrich quality failures with lineage, ownership, and downstream impact for faster triage.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/find-the-right-owner-to-contact/
