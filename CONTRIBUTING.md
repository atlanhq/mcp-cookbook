# Contributing

Thanks for wanting to help. Here's where things stand.

## We aren't taking contributions yet

This repo doesn't accept outside contributions right now: no pull requests and no commits, to
recipes or to anything else. Pull requests opened against it will be closed.

It's a published copy of the cookbook at [atlan.com/mcp-cookbook](https://atlan.com/mcp-cookbook/),
kept in step with it. Everything under `recipes/`, and `recipes.json`, is produced from the
published site, so a change made here would be replaced on the next refresh and would never reach
the website or the people reading it there. Every recipe is also tested against a live Atlan tenant
before it publishes, and a prompt that hasn't been through that would sit next to tested ones with no
way for a reader to tell which is which.

## A submission process is coming soon

We're putting together a way to submit your own recipes and suggestions. Details will be posted
here when it's ready.

## Something wrong with a recipe?

A prompt that no longer works, a broken link, a step that's out of date: we want to know. Raise it
with your Atlan point of contact and name the recipe. Fixes are made on the website and appear here
on the next refresh.

## Using the recipes

You don't need permission. Clone the repo, copy the prompts, adapt them to your own schemas and
assets, build on `recipes.json`. That's what they're for.

If you're using them inside an AI tool, the [`find-a-recipe`](./.claude/skills/find-a-recipe/SKILL.md)
skill will route you to the right one and tell you what it assumes you've already got in place.
