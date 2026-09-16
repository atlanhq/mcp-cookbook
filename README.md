<a href="https://atlan.com/mcp-cookbook/" target="_blank">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="images/atlan-logo-white.svg">
    <img alt="Atlan" src="images/atlan-logo-blue.svg" width="200px">
  </picture>
</a>

# The Atlan MCP Cookbook

> ✨ Browse the published cookbook at **[atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/)**

33 tested recipes for putting your company's context to work through the [Atlan MCP](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview) — from inside whatever AI tool you already build in.

Each recipe is a real workflow someone runs: the problem it solves, the prompts to type, what you need to hand it, and what you get back. They're written to be pasted, not admired.

To run any of them you need the Atlan MCP connected to your AI tool — **[set it up here](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview)**. No recipe works without it.

---

## Quick start

```bash
git clone https://github.com/atlanhq/mcp-cookbook.git
cd mcp-cookbook
claude
```

Then describe the problem, don't name a recipe:

> *"I need to write a query against a schema I don't know"*

The bundled [`find-a-recipe`](./.claude/skills/find-a-recipe/SKILL.md) skill reads the index, works out which recipe fits your job and role, hands you the prompt with its placeholders intact, and tells you what the recipe assumes you've already got in place. To use it anywhere rather than only in this repo:

```bash
cp -r .claude/skills/find-a-recipe ~/.claude/skills/
```

**Prefer to read?** Browse [`recipes/`](./recipes/) — every file is self-contained.
**Building on top?** Parse [`recipes.json`](./recipes.json) — facets, summaries and hero prompts in one file.

## New to the MCP? Start with these

A recipe can only surface context that already exists in your tenant. Most lean on something being in place — a glossary, assigned owners, populated lineage — so running one of those first in a tenant that hasn't got there yet returns an empty answer, and you'd reasonably conclude the whole thing doesn't work.

These six read only and assume nothing pre-exists. They work on day one, in any tenant:

| Recipe | Effort |
|---|---|
| [Reuse before you rebuild](./recipes/reuse-before-you-rebuild.md) | Quick |
| [Profile a field's shape before you build on it](./recipes/profile-a-field-before-you-build-on-it.md) | Quick |
| [Check the master list before you add a new value](./recipes/check-value-against-master-list.md) | Quick |
| [Get the answer, not just the table](./recipes/get-the-answer-not-just-the-table.md) | Moderate |
| [Get build-ready for a new dashboard](./recipes/get-build-ready-for-a-new-dashboard.md) | Moderate |
| [See exactly what a migration would leave behind](./recipes/compare-two-sources-before-a-migration-decision.md) | Moderate |

Every recipe declares what it leans on in `requires:`, and `recipes.json` carries a `start_here` list plus a `prerequisite_index`. Nothing is hidden from you on that basis — a recipe you can't run today still tells you what's worth building toward. The skill just says what a recipe assumes so you're not surprised by a thin answer.

## How recipes are organised

| Use case (`job`) | Recipes |
|---|--:|
| Find & understand data | 13 |
| Govern & keep trusted | 7 |
| Make data understandable | 6 |
| Change & fix data safely | 4 |
| Retire & migrate | 3 |

`action` is either **Look up** (19 recipes, read-only) or **Make changes** (14, writes back to Atlan) — worth checking before you run one. Recipes also carry `personas` (Data Engineer · Data/BI Analyst · AI Builder · Data Governance Lead · Data/Business User) and `effort` (Quick · Moderate · Involved). Most serve several personas, so treat those as a hint, not a gate.

## Two things worth knowing

**Prompts contain `<placeholders>`.** Replace them with your real schema, asset or glossary term. A prompt pasted with `<schema>` still in it won't work.

**A recipe can only surface context that exists.** If an asset isn't documented, no prompt will invent its meaning — which is usually the finding, not a failure.

## Repo layout

```
recipes/                       33 recipes, one markdown file each
recipes.json                   machine index — facets, summaries, hero prompts
.claude/skills/find-a-recipe/  routing skill
images/                        Atlan brand assets
```

## Contributing

This repo is a published copy of the cookbook, kept in step with
[atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/). Recipes are written and reviewed there
first, so **pull requests against `recipes/` or `recipes.json` aren't accepted** — see
[CONTRIBUTING.md](./CONTRIBUTING.md).

## More from Atlan

- [Atlan MCP setup](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/remote-mcp-overview) — connect the MCP to your AI tool
- [Atlan AI documentation](https://docs.atlan.com/product/capabilities/atlan-ai/how-tos/atlan-mcp-overview) — what the MCP can do
- [The published cookbook](https://atlan.com/mcp-cookbook/) — the same recipes, nicer to browse
- [atlan.com](https://atlan.com) — the context layer for AI
