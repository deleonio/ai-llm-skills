# Contributing

## Adding a new skill

Create a folder under `skills/` whose name matches the `name` field in the frontmatter (lowercase, hyphens instead of spaces). Inside it goes the `SKILL.md`:

```
skills/my-skill/SKILL.md
```

The frontmatter needs two fields:

```yaml
---
name: my-skill
description: What the skill does and when it should be used.
---
```

The `name` doubles as the slash command (`/my-skill`). The `description` triggers the automatic invocation: the agent reads only the description to decide whether to load the skill. It should state both the task and the situation in which the skill applies. The text below is only loaded once the skill is active and can therefore be more detailed.

Additional files (references, scripts, templates) live in the same folder and are referenced from the `SKILL.md` via relative paths.

Then add the new skill to `.claude-plugin/marketplace.json`:

```json
{
  "name": "my-skill",
  "description": "Short description for the plugin list.",
  "source": "./skills/my-skill"
}
```

and to the skill list in the `README.md`.

## Before the pull request

Verify that the skill triggers on its own in a real session. If it doesn't, the cause is almost always the `description`. Only include the skill if it works without credentials, internal systems, or personal data.

By opening a pull request you agree to license your contribution under the [EUPL-1.2](LICENSE) of this repository.
