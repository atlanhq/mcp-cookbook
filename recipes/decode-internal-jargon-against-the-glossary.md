---
name: Decode internal jargon without asking around
slug: decode-internal-jargon-against-the-glossary
number: 24
summary: Check whether an internal acronym or jargon term already has a governed definition
  before you interrupt five people on Slack to ask.
job: Find & understand data
action: Look up
personas:
- Data/Business User
- Data/BI Analyst
- AI Builder
effort: Quick
runs_in: any AI tool
requires:
- glossary
start_here: false
source_url: https://atlan.com/mcp-cookbook/decode-internal-jargon-against-the-glossary/
related:
- grow-your-business-glossary
- reconcile-terminology-across-systems
- understand-how-a-metric-is-calculated
---

# Decode internal jargon without asking around

Check whether an internal acronym or jargon term already has a governed definition before you interrupt five people on Slack to ask.

| | |
|---|---|
| **Use case** | Find & understand data |
| **Action** | Look up |
| **Who it serves** | Data/Business User, Data/BI Analyst, AI Builder |
| **Effort** | Quick |
| **Runs in** | any AI tool |

## The problem

A new analyst opens a ticket that references a validation rule called "DQ-17" and a system nickname "falcon", with no explanation attached. The instinct is to ask around on Slack, which means waiting on five people who are each half-sure of the answer. Most of the time, someone already wrote the real definition down; it's just not where you'd think to look.

## What to ask for

- Whether the term already has a governed definition, searched by the literal string and by the concept behind it
- The full definition and the team that owns it
- The assets the term is linked to, so you can see where it's actually applied

## Start here

Paste this into whichever AI tool is connected to the Atlan MCP:

```text
What does 'DQ-17' mean? Check if there's already a governed definition for it before I ask anyone.
```

## Steps

### 1. Search for the term and the concept behind it.

```text
Search the glossary for <DQ-17> — both the exact string as it appears in the ticket and the full-word expansion or business concept it likely stands for — and show every governed definition that could match.
```

### 2. Pull the full definition and its owner.

```text
For the closest match, give me the full definition and the team that owns it, so I get the real answer, not just that something exists.
```

### 3. See where it's actually used.

```text
Show me the assets that term is linked to, so I can see where <DQ-17> is applied in practice, not just how it's defined.
```

## What you'll need

**Required**

- The exact acronym or phrase, copied as written
- Where it appeared (ticket, doc, code comment), for context if the search comes back ambiguous

**Optional, but it helps**

- The team or domain it likely came from, to narrow the search faster

## What you get

- The resolved definition and the team that owns it, if one exists
- The assets the term is linked to, so you can see where it's actually applied
- A clear "not documented yet" signal if it genuinely isn't defined anywhere

You either get the real answer in under a minute, or you get clear confirmation that this is genuinely undocumented and worth flagging, instead of guessing from context.

**What changed in Atlan:** Read-only. Nothing is written; if it turns out to be undocumented, that's a separate follow-up to actually create the term.

## Follow-ups

**Close the gap**

```text
It's undocumented, create the glossary term for it now so the next person doesn't hit this wall.
```

**Do the whole ticket**

```text
Check every acronym in this whole ticket at once, not one at a time.
```

**Make it a standing check**

```text
Run this against the onboarding runbook before the next new hire starts.
```

## Cook's note

> Internal jargon rarely matches its governed name word for word, which is why step 1 asks for the concept as well as the literal string. If both still come back empty, that's a real answer — the term genuinely isn't documented, and that's worth flagging rather than guessing from context.

- Match the client to the work.** Any client works; this is a fast lookup you'll usually run mid-conversation, not a dedicated session.
- Automate or chain it.** Chain this across a whole ticket or runbook in one pass instead of decoding each acronym as you hit it.
- Recheck on old docs.** Definitions get renamed or retired. If the doc you're reading is old, treat a stale match as a prompt to confirm it's still current, not the final answer.

## Related recipes

- [Grow your business glossary](./grow-your-business-glossary.md) — Bootstrap glossary terms from how your assets already use business concepts.
- [Give one concept one trusted definition](./reconcile-terminology-across-systems.md) — Confirm whether two differently-named fields or terms mean the same thing, then link them under one governed definition so the next person searching either name lands in the same place.
- [Understand how a metric is calculated](./understand-how-a-metric-is-calculated.md) — Get the governed definition of a metric — and where it's documented — without asking a data engineer.

---

Set up the Atlan MCP: https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview

Published version of this recipe: https://atlan.com/mcp-cookbook/decode-internal-jargon-against-the-glossary/
