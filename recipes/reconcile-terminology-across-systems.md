---
name: Give one concept one trusted definition
slug: reconcile-terminology-across-systems
number: 33
summary: Confirm whether two differently-named fields or terms mean the same thing, then link
  them under one governed definition so the next person searching either name lands in the
  same place.
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
source_url: https://atlan.com/mcp-cookbook/reconcile-terminology-across-systems/
related:
- grow-your-business-glossary
- decode-internal-jargon-against-the-glossary
- enrich-assets-with-your-context
---

# Give one concept one trusted definition

Confirm whether two differently-named fields or terms mean the same thing, then link them under one governed definition so the next person searching either name lands in the same place.

| | |
|---|---|
| **Use case** | Make data understandable |
| **Action** | Make changes |
| **Who it serves** | Data Governance Lead, Data/BI Analyst |
| **Effort** | Moderate |
| **Runs in** | any AI tool |

## The problem

Ops in one region tracks a balance as `cash_ledger`. Finance in another region calls the same balance `payments_settlement`. A new analyst gets asked to reconcile the two and can't tell if they're the same number under two names or genuinely different things. Nobody wants to be the person who merges two different metrics into one report.

## What to ask for

- The existing definition of each term in its own system
- Whether they genuinely describe the same thing or only sound alike
- One governed term both resolve to, with a record of exactly what changed

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
Check whether `cash_ledger` and `payments_settlement` describe the same underlying balance. If they do, link them under one glossary term so anyone searching either name gets the same governed answer.
```

## Steps

### 1. Pull the first term's definition.

```text
Search for <cash_ledger> as written in its own system and pull whatever definition or description already exists.
```

### 2. Pull the second term's definition.

```text
Do the same for <payments_settlement> in its own system.
```

### 3. Compare to confirm they match.

```text
Compare the two definitions and their underlying columns side by side; tell me whether they truly describe the same thing or only sound similar.
```

### 4. Link both under one governed term.

```text
Link both under a single governed glossary term so a search on either <cash_ledger> or <payments_settlement> resolves to one answer, then list exactly what you changed.
```

## What you'll need

**Required**

- Both terms or field names, and the systems or schemas they come from
- Write access to the glossary, for the linking step

**Optional, but it helps**

- Whether the mismatch is a translation issue (different language, same concept) rather than a genuine naming divergence
- A stakeholder from each side who should be looped in before the merge is finalized

## What you get

- A documented alias or synonym relationship linking both terms to one glossary definition
- Or, if they turn out not to match, a written explanation of exactly how they differ

Anyone who searches `cash_ledger` or `payments_settlement` from now on lands on the same governed definition, instead of two people quietly reporting two different numbers under the same name.

**What changed in Atlan:** This writes a new alias link (or an updated term description) into the glossary. It leaves the original two source fields untouched; only the governed definition layer changes.

## Follow-ups

**Look for a third name**

```text
Check if any other system uses yet another name for this same balance.
```

**Audit the whole glossary**

```text
Audit the whole glossary for likely duplicate concepts under different names.
```

**Re-run after a migration**

```text
Re-run this after the next acquisition or system migration.
```

## Cook's note

> The riskiest version of this isn't two names for the same thing, it's two names for two subtly different things that someone merges anyway. Don't skip the comparison step to save time.

- Match the client to the work.** Use a client that shows you the proposed link before it writes it; this is a governance decision, not a lookup, and you want to eyeball it first.
- Automate or chain it.** Run this against a running list of terms flagged as "possibly duplicate" during onboarding or a merger integration, instead of waiting for someone to notice by accident.
- Ask what it changed.** After it runs, ask it to list exactly which term was updated and which alias was added, so you have an audit trail of every reconciliation it made.

## Related recipes

- [Grow your business glossary](./grow-your-business-glossary.md) — Bootstrap glossary terms from how your assets already use business concepts.
- [Decode internal jargon without asking around](./decode-internal-jargon-against-the-glossary.md) — Check whether an internal acronym or jargon term already has a governed definition before you interrupt five people on Slack to ask.
- [Enrich assets with your context](./enrich-assets-with-your-context.md) — Bring context that lives outside Atlan, like a spreadsheet or a Confluence page, onto your assets as owners, tags, and additional metadata.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/reconcile-terminology-across-systems/
