---
name: find-a-recipe
description: >
  Find the right Atlan MCP Cookbook recipe for what someone is trying to do. Reads the
  local recipe index, works out which of the 33 recipes fits their job and their role,
  and hands back the exact prompt to run. Use it whenever someone wants to do something
  with their data through an AI tool and doesn't know which recipe applies, or asks what
  the cookbook can do for them.
  Trigger phrases:
  - "which recipe should I use for [task]"
  - "how do I [do something] with the Atlan MCP"
  - "what can I do with the Atlan MCP as a [role]"
  - "find me a recipe for [problem]"
  - "/find-a-recipe [what you're trying to do]"
---

# Find a recipe

Route someone from *"here's what I'm trying to do"* to the one recipe that does it, and to the
prompt they can paste straight into their AI tool.

## Step 1: read the index, not the recipes

`recipes.json` at the repo root holds every recipe with its facets, summary, and hero prompt.
Read it first. It is enough to route with — do not open all 33 recipe files.

It carries:

- `facets` — the full vocabulary for `job`, `action`, `persona`, `effort`
- `recipes[]` — for each: `slug`, `name`, `summary`, `job`, `action`, `personas[]`, `effort`,
  `hero_prompt`, `step_count`, `path`, `url`, `related[]`

Open the file at `path` only once they've chosen, or when you need the full steps.

## Step 2: work out what they're actually trying to do

Match against **what they've already told you**. Do not open with a questionnaire — most requests
already name the job, and asking for what you were just told is the fastest way to look useless.

The two dimensions that decide the answer:

| Dimension | Values | What it tells you |
|---|---|---|
| `job` | Find & understand data · Make data understandable · Govern & keep trusted · Change & fix data safely · Retire & migrate | The bucket their problem sits in — this does most of the routing |
| `action` | Look up · Make changes | Whether they're reading context or writing it back. Read-only vs. mutating matters to them. |

`persona` (Data Engineer · Data/BI Analyst · AI Builder · Data Governance Lead ·
Data/Business User) is a **ranking signal, never a filter**. This matters more than it sounds:
of the 50 possible job × action × persona combinations, **27 return zero recipes**. Filter on all
three and you will dead-end more than half the time, on a corpus that almost certainly contains
something useful.

`effort` (Quick · Moderate · Involved) is worth mentioning, never worth asking about up front.

**Ask at most one question, and only if the job is genuinely unclear.** Good: *"Are you trying to
understand what's already there, or change something?"* Bad: a four-part intake form.

Ignore `runs_in` as a filter — all 33 recipes read "any AI tool".

### Facets narrow. They do not rank.

`job` + `action` typically leaves ~10 candidates — far too many to hand over, and the facets
carry no signal about which one answers *this* question. So:

1. **Filter** on `job`, and on `action` when you're confident which one they want.
2. **Rank what's left by matching their actual words** against each candidate's `name` and
   `summary`. This is the step that finds the right recipe. Someone saying *"I don't know the
   column names in this schema"* should land on "Write SQL that runs on the first try" — and only
   a semantic read of the summaries gets them there, because nine other recipes share its facets.
3. Use `personas` overlap and `effort` only to break ties between genuinely close candidates.

### When a filter comes back empty, widen — don't apologise

Walk down this ladder until you have candidates:

`job` + `action` + persona → `job` + `action` → `job` alone → the whole index, ranked semantically

Two `job` + `action` pairs are empty in the current corpus no matter the persona — *Find &
understand data / Make changes* and *Make data understandable / Look up*. If you land on either,
drop `action` and keep `job`; the recipe they want is almost always in the same job bucket under
the other action.

## Step 3: offer two or three, not one and not ten

Ranking, in order:

1. **how closely `name` + `summary` answer the question they actually asked** — this decides it
2. `action` matches whether they want to read or write
3. a persona overlap with their role
4. prefer `Quick` over `Involved` when two otherwise tie — a first recipe that works beats a
   thorough one they abandon

For each candidate give:

- the **name**, and one line on why it fits *their* problem — not a restatement of the summary
- the **hero prompt**, verbatim in a code block, so they can paste it now
- `step_count` and `effort`, so they know what they're committing to
- the published URL for the full write-up

Then stop and let them pick. Once they do, read `recipes/<slug>.md` and walk the numbered steps,
handing over each step's prompt as they get to it.

### Handing over a prompt: keep the `<placeholders>` intact

30 of the 33 recipes contain angle-bracket placeholders — `<table>`, `<schema>`, `<metric>`,
`<column>`, `<term>`, and illustrative sample names like `<fct_orders>` or `<cash_ledger>`. They
mark the parts the reader has to replace with their own specifics.

**Reproduce them exactly as written.** Do not rewrite `<table>` as "Insert your table name", "your
table here", or "the table you care about". That's the one thing that makes a prompt *worse*: it
reads as a finished sentence while still being incomplete, so the placeholder stops being visually
obvious and people paste it unchanged. The angle brackets are doing real work — they're a visible
blank the eye catches.

```text
✅  Show me the columns in <table> with their types and any description on record.
❌  Show me the columns in [insert your table name] with their types...
❌  Show me the columns in your table with their types...
```

**Substitute only what you actually know.** If they've already told you the schema is `reporting`
and the table is `fct_orders`, put those in — and say which values you filled, so they can correct
you. Anything you're guessing at stays a placeholder. Never invent a plausible-looking table name;
a wrong-but-real-looking name is worse than a blank, because it might silently run against the
wrong asset.

**Then name what's left to swap.** One line under the prompt:

> Replace `<schema>` with your schema, and `<metric>` with the measure you're checking.

That way they can see the blanks in the prompt *and* know what goes in each one.

## Step 4: close by saying what the recipe assumes

Every recipe in the index carries `requires` — the tenant structures it leans on. Across the
corpus: `owners` (13 recipes), `documentation` (11), `lineage` (8), `glossary` (5), `tags` (5),
`domains` (4), `data_quality` (3). Only 6 of 33 assume nothing at all.

**Use it to set expectations at the end, after they have the recipe.** One line, once:

> Worth knowing: this one works from your business glossary, so it'll only be as good as what's
> defined in there already.

Three rules about that line:

- **It goes last.** They came for the recipe, not a caveat. Never front-load it, never make them
  read a warning before they get the thing they asked for.
- **It's an assumption, not a verdict.** `requires` is derived by pattern-matching the recipe text,
  not verified against anything — so "this works from your glossary" is honest, and "you don't
  have a glossary" would be a claim you can't support.
- **No note when `requires` is empty.** Six recipes need nothing. Say nothing.

**Never withhold a recipe over this, and never quietly swap in a different one.** Offer what they
asked for. A recipe someone can't run today still tells them what's worth building toward, and
they know their own tenant far better than you do. Gating on derived metadata would hide 27 of the
33 recipes from exactly the people who most need to see what's possible.

If they want to know whether their tenant is ready, they'll ask — answer it then.

### The vague opener: start from `start_here`

If someone asks "what can I even do with this" and names no job, lead with the `start_here`
recipes — 6 that read only and assume nothing pre-exists. That's a sensible default ordering for
someone with nothing to go on, not a restriction: ask for something specific and you get it,
prerequisites or not.

## Step 5: the things that actually go wrong

- **They haven't connected the Atlan MCP.** Every recipe assumes it. If their tool can't reach
  Atlan, no prompt here will work. Setup:
  `https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview`
- **Recipes assume the reader supplies the specifics.** See the placeholder rule above — the
  single most common way a hand-off goes wrong is rewriting a `<placeholder>` into prose.
- **`action: Make changes` recipes write to Atlan.** Say so before they run one, and point at the
  recipe's "What changed in Atlan" line. Someone expecting a read-only lookup should not discover
  mid-run that they've updated metadata.
- **Follow-ups exist for a reason.** After a recipe lands, the `Follow-ups` section usually has
  the next thing they'll want. Offer it rather than waiting to be asked.

## Boundaries

- **Only route to recipes in `recipes.json`.** Never invent a recipe, never improvise a prompt
  and present it as one from the cookbook. If a prompt is your own, say so plainly.
- **If nothing fits, say nothing fits.** Forcing the nearest-but-wrong recipe wastes their time
  and teaches them not to trust the cookbook.
- This repo is a **read-only mirror** of atlan.com. Don't edit recipes here or offer to; the
  website is the source of truth and everything under `recipes/` is generated.
- Recipes are tested patterns, not guarantees. Results depend on what's actually documented in
  the reader's own Atlan tenant — a recipe can only surface context that exists.
