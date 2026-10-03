# ai-llm-skills

Open collection of agent skills for Claude and other LLM agents. A skill is a Markdown file with instructions that the agent loads whenever it matches the task at hand. The format follows the SKILL.md standard and works in Claude Code, the Claude apps (claude.ai, Desktop, Cowork), and via the API.

## Included Skills

### wikipedia-article

A writing coach and opponent in one for creating and improving Wikipedia articles. While drafting, the skill acts as a mentor that enforces Wikipedia's encyclopedic ground rules sentence by sentence: notability gate before writing, neutral point of view, verifiability with real sources, no original research, sober encyclopedic tone, conventional structure. It refuses fabricated citations outright and flags every violating passage on the spot with the violated rule and a rewrite.

When the draft is complete, the role flips: an Advocatus Diaboli dissects the article the way a deletion discussion would — checking every citation, hunting peacock and weasel wording, exposing original research and promotional drift — and reports findings by severity (Blocker, Major, Minor, Polish), each with a concrete revision instruction. The draft loops through review and revision until it earns a *ready* verdict; blockers are never waved through.

Works for any language edition of Wikipedia; also handles biographies of living persons, company and organization articles, and conflict-of-interest situations. German prose additionally follows the [vermenschlichen](https://github.com/LOGIN-TB/claude-skills) rules when that skill is installed (a built-in machine-tell list acts as fallback).

Methods:

```
/wikipedia-article style               capture your personal writing style into STYLE.md
/wikipedia-article assess <topic>      notability gate + source map, before anything is written
/wikipedia-article sources <topic>     find and verify usable sources per claim
/wikipedia-article draft <topic>       write under mentor guard, applying your style profile
/wikipedia-article audit <draft>       the dissection: read-only attack with findings and verdict
/wikipedia-article revise <draft>      apply findings in severity order, tracked to resolved/open
/wikipedia-article polish <draft>      final prose pass: precision, concision, flow — meaning untouched
```

A bare `/wikipedia-article` auto-detects the method from the input.

Your personal writing style lives in a `STYLE.md` in your working directory — captured once via `/wikipedia-article style` from sample texts or a short interview, then applied automatically by `draft`, `revise`, and `polish`. A fillable template ships with the skill ([style-template.md](skills/wikipedia-article/reference/style-template.md)); an installed personal style skill (e.g. `schreibstil`) is imported directly. It shapes voice, rhythm, and terminology, never facts or sourcing: where the profile collides with Wikipedia's ground rules, the rules win. `STYLE.md` is personal and stays out of version control.

→ [`skills/wikipedia-article/SKILL.md`](skills/wikipedia-article/SKILL.md)

Companion skill: [vermenschlichen](https://github.com/LOGIN-TB/claude-skills) – German anti-AI-tell rules, used automatically by this skill when installed. It lives in its own repo but is listed in this marketplace, so a single `/plugin marketplace add` is enough to install both:

```
/plugin install wikipedia-article@ai-llm-skills
/plugin install vermenschlichen@ai-llm-skills
```

## Installation

### Claude Code

Register the repo as a plugin marketplace and install individual skills as plugins:

```
/plugin marketplace add deleonio/ai-llm-skills
/plugin install <skill-name>@ai-llm-skills
```

Fetch updates with `/plugin marketplace update ai-llm-skills`.

### Claude Code, manual

Copy the skill folder directly, either personal or per project:

```bash
git clone https://github.com/deleonio/ai-llm-skills.git
cp -r ai-llm-skills/skills/<skill-name> ~/.claude/skills/
```

`~/.claude/skills/` applies to all projects, while `.claude/skills/` in the project folder applies there only and can be versioned with your team.

### Claude apps (claude.ai, Desktop, Cowork)

Custom skills are uploaded as ZIP files. The folder name inside the archive must match the skill name, otherwise the upload fails.

```bash
cd skills
zip -r <skill-name>.zip <skill-name>
```

Then go to [claude.ai/customize/skills](https://claude.ai/customize/skills), click „+" → „Create skill" → „Upload a skill" and select the ZIP file. Uploaded skills are private to your account. Team and Enterprise organizations distribute them via the organization settings.

### API

Via the [Skills API](https://docs.claude.com/en/api/skills-guide), the skill can be created as a resource and attached to requests.

### Other agents

SKILL.md is an open format based on Markdown with YAML frontmatter. Agents without native skill support can use the text below the frontmatter as a system prompt or custom instruction.

## Repository Layout

```
.claude-plugin/marketplace.json   Marketplace definition for Claude Code
skills/<skill-name>/SKILL.md      one folder per skill, folder name = "name" field
skills/<skill-name>/reference/    optional per-method instruction files
```

Every SKILL.md starts with a frontmatter block containing `name` and `description`. The name doubles as the slash command for invoking the skill directly. The description decides whether the agent loads the skill on its own at the right moment, so it should state both what the skill does and when it applies.

```yaml
---
name: skill-name
description: What the skill does and when it should be used.
---
```

## Contributing

Bugs, additions, and new skills are welcome as issues or pull requests. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

[EUPL-1.2](LICENSE)
