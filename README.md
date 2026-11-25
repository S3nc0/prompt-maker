# Prompt Maker

A Claude skill that turns a rough idea into a ready-to-paste prompt for any AI tool and any kind of project: coding, writing, reports, art, research, study, and multi-agent builds.

You describe what you want. The skill asks only what it needs, picks the right tool and model, and hands back a prompt you can copy straight into another AI.

## What it does

- **Works for any project.** It has separate guidance for coding, writing, reports and academic work, art and visuals (image, video, 3D, pixel art), research, study, system prompts, and multi-agent projects.
- **Checks your stack first.** For coding it confirms the language, framework, platform, and versions before writing anything.
- **Finds the best tool.** It checks a list of known picks, then searches the web for the best current tool, skill, library, or MCP server for the task, and asks before building a prompt around it.
- **Tunes for the model.** It asks which model will receive the prompt and follows that model's official prompting guide.
- **Writes like you.** For writing in your voice it sets a short writing test that matches the piece (a scene for a story, a method paragraph for a paper), analyzes your style, and puts the profile into the prompt.
- **Builds multi-agent packs.** It produces a leader prompt, one brief per worker, a review prompt, and a shared notes file, in the format your orchestration tool expects.
- **Saves tokens.** It assigns each task a right-sized model and writes token-saving rules into the leader prompt.
- **Remembers your defaults.** Your usual stack, models, output language, and writing profiles live in one section, and it asks before applying them.
- **Tests on a budget.** It checks every prompt by reading it as the receiving model would, and test-runs short text prompts once.
- **Fixes existing prompts.** It diagnoses what went wrong with the output before rewriting.

## How it works

1. Work out the project, the tool, and the goal, and ask any questions in one round.
2. Check the model, or the agent team.
3. Find the best tool or MCP server for the job.
4. Collect the ingredients: task, context, inputs, output, constraints, examples, and what "done" means.
5. Write the prompt.
6. Check it, and test it within a budget.

## Install

### Claude Code

Clone this repository into your skills folder, then restart Claude Code:

```bash
git clone https://github.com/S3nc0/prompt-maker ~/.claude/skills/prompt-maker
```

### Claude app

Add `SKILL.md` as a custom skill in your Claude skill settings.

## Use

Ask for a prompt in plain words. For example:

- "Make me a prompt to get an AI to review my lab report."
- "Prompt for a walking knight sprite for my game."
- "I want three agents to build a Discord bot. Make the prompts."
- "This prompt keeps giving generic answers. Fix it."

You get each prompt in its own code block, followed by short notes on what to fill in, what was assumed, and what to adjust if the first result is off.

## Customize

Open `SKILL.md` and edit these two parts:

- **My defaults**: your output language, usual stack, usual models and agents, orchestration tool, and writing profiles.
- **Known picks**: a table mapping a kind of task to the tool you want used for it. It ships with one entry, [Codixel](https://github.com/mankidev/codixel) for pixel art and sprites.

## Notes

- The model line-up in the skill (the Gemini 4 family) is current as of November 2026. The skill is told to confirm line-ups against the maker's own page, since they change.
- Tools the skill recommends are separate projects with their own licences and install steps. The skill tells you what to install and never installs anything itself.
