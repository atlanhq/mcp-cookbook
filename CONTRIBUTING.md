# Contributing

Thanks for wanting to help — here's how changes to the cookbook actually work.

## Recipes aren't edited here

This repo is a published copy of the cookbook at
[atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/), kept in step with it. Everything under
`recipes/`, and `recipes.json`, is produced from the published site.

So a recipe added or changed here would be replaced the next time the copy is refreshed, and it
would never reach the website or the people reading it there. **Pull requests against `recipes/`
or `recipes.json` will be closed.**

That isn't gatekeeping for its own sake. Every recipe is tested against a live Atlan tenant before
it publishes. Prompts that haven't been through that would be untested advice sitting next to
tested advice, with no way for a reader to tell which is which.

## Something wrong with a recipe?

A prompt that no longer works, a broken link, a step that's out of date — we want to know. Raise it
with your Atlan point of contact and name the recipe. Fixes are made on the website and appear here
on the next refresh.

## Using the recipes

You don't need permission. Clone the repo, copy the prompts, adapt them to your own schemas and
assets, build on `recipes.json`. That's what they're for.

If you're using them inside an AI tool, the [`find-a-recipe`](./.claude/skills/find-a-recipe/SKILL.md)
skill will route you to the right one and tell you what it assumes you've already got in place.
