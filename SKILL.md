---
name: "prompt-maker"
description: "Turn a rough idea into a ready-to-paste prompt for any AI tool and any kind of project: coding, writing, reports, art, research, study, and multi-agent builds. Use whenever the user asks to write, make, generate, fix, or improve a prompt, even if they only say 'help me ask an AI to do X'."
---

# Prompt Maker

Turn what the user wants into a prompt they can paste straight into another AI tool and get a good result on the first try. This works for any kind of project. The deliverable is the prompt itself, not advice about prompting.

The core idea: the model receiving the prompt knows nothing about the user, their project, or what "good" looks like. Almost every weak prompt fails because that context stayed in the user's head. Your job is to get it onto the page.

## My defaults

The user's standing choices. Edit this section to change them.

- **Output language**: (not set)
- **Usual stack**: (not set)
- **Usual models and agents**: (not set)
- **Orchestration tool**: (not set)
- **Writing profiles** (one per kind of writing): (none yet)

How to use these:

- Defaults are a starting suggestion, never applied silently. Pick the ones relevant to this request, show them in one line ("Using your usual stack, X and Y. Okay for this project?"), and wait for a yes.
- Judge the fit yourself before offering. If a default does not suit this project (a web stack for a firmware task, a story-writing profile for a lab report), say so and suggest what fits better instead.
- A default that is not set means ask.
- When the user confirms something reusable (a stack, a model, a finished writing profile), offer to save it here by updating this skill.

## Step 1: Work out the project, the tool, and the goal

Three things decide the shape of the prompt:

- **Kind of work**: coding, writing, a report, art, research, study, planning, or something else
- **Tool**: what will receive the prompt? A chat assistant, a coding agent, a team of agents, an image or video generator, or a system prompt for a bot or app
- **Goal**: what should come back, and what will the user do with it?

Infer what you can from the request, attached files, and the defaults. Then ask for what is still missing **in one round**: a single short message with every question you need, not one question per turn. Depending on the work, that round may cover:

- Whether the relevant defaults apply
- The exact model, or whether this is multi-agent work (Step 2)
- The stack, for coding (Coding notes)
- A writing sample, for writing in the user's voice (Writing notes)

Skip any question already answered. For a simple one-off prompt where nothing essential is missing, ask nothing: draft and list what you assumed.

A big project is rarely one prompt. If the request covers several stages (plan, build, review) or several kinds of work, write one prompt per stage and number them in order of use. Each must stand alone, because the receiving model will not see the others.

## Step 2: Check the model, or the agent team

Different models respond to different prompt styles, so a prompt tuned for the wrong one loses quality.

**Single model.** Find out exactly which model will receive the prompt: the name and version, or the model ID. If the user only knows the app they use, work out the model from that. Then look up the official prompting guide from the model's maker for that model and follow it: how it wants structure marked, where instructions go, how it handles reasoning, and for image or video models, its parameters and phrasing. Prefer the maker's own documentation over blog posts. Model line-ups change fast, so do not rely on memory for what is current. Where the official guide disagrees with the general principles in Step 5, the guide wins for that model.

Keep the lookup proportional: one search and one page is usually enough. If the user does not know or does not mind which model, write a model-neutral prompt and say so.

**Several agents.** If the user will run more than one agent, go to the Multi-agent projects notes. That changes the deliverable from one prompt to a pack.

### Current line-ups to use

Line-ups the user has asked for. Confirm against the maker's own model page before relying on the details, because these change.

**Gemini: use the Gemini 4 family** (current as of November 2026). Whenever a prompt or an agent will run on Gemini, pick from these and write their model IDs, not older Gemini 3.x Pro or Flash names:

| Model | Model ID | Use for | In the Gemini app |
|---|---|---|---|
| Carbon | `gemini-4-carbon` | The hardest, longest problems: planning, architecture, deep debugging | Ultra plan only |
| Neon | `gemini-4-neon` | Complex coding, analysis, and research at good speed | Pro and Ultra plans |
| Hydrogen | `gemini-4-hydrogen` | Fast, low-cost everyday work: routine coding, tests, agent subtasks | Every plan, and the only one with a free API tier |

- Argon (`gemini-4-argon`) was the first Gemini 4 model and is now API-only. Prefer the three above unless the user asks for it.
- Check which of these the user's plan or API access includes before assigning one.
- If the user names an older Gemini model, point out the Gemini 4 equivalent (Neon in place of a Pro model, Hydrogen in place of a Flash model) and ask which they want. Keep the older one only if their tool cannot run Gemini 4 yet.
- Look up Google's prompting guide for the specific Gemini 4 model, including its thinking level setting, before writing the prompt.

## Step 3: Find the best tool or MCP for the job

A good prompt aimed at the wrong tool still gives a poor result. Before drafting, work out whether a specialised tool, skill, library, model, or MCP server (a connector that gives an agent access to an app or data source) does this task better than a general approach.

1. **Check the known picks below first.** These are tools the user has already chosen, so use them and say so in one line.
2. **Otherwise search the web** for the current best option for this specific task. Search for the task itself ("sprite animation tool for coding agents", "MCP server for Blender") and prefer the project's own page or repository over listicles.
3. **Open the top candidate's page and confirm** what it does, what it needs installed, whether it is still maintained, its licence, and for an MCP server, what access or credentials it asks for. A tool you have not checked does not go in the prompt.
4. **Ask the user before building around it.** Give the name, a link, one line on why, and what they would need to install or connect. If two options are close, name both and say which you would pick. If they say no, write the prompt for a general approach.
5. **Write the prompt for the chosen tool**: use its real commands, inputs, and workflow as its documentation describes them.

Skip the search when the user has already named the tool, or when the task is simple enough that a general assistant handles it well. If web search is not available, say so, suggest a tool from what you know, and mark it as unverified.

Do not install anything or connect any MCP server as part of this skill. Put the install step in the notes after the prompt. Flag any tool that wants broad access to files or accounts so the user can decide with that in view.

### Known picks

| Task | Tool | Notes |
|---|---|---|
| Pixel art, game sprites, sprite animation | Codixel (https://github.com/mankidev/codixel) | A Claude Code skill. Install by cloning the repo into `~/.claude/skills/codixel`. It works from reference images, so the prompt should name or attach a reference and state the pixel style. The user reviews each stage. Licence: GPL-3.0-or-later. |

When the user approves a tool for a kind of task, offer to add it to this table.

## Step 4: Collect the ingredients

Pull these from the conversation, attached files, and anything the user has said about their project. Leave a clearly marked placeholder for anything unknown rather than inventing it.

- **Task**: the one thing the model should do, stated plainly
- **Context**: who it is for, why it matters, what already exists
- **Inputs**: the material the model will work from (text, code, data, images)
- **Output**: format, length, language, tone, structure
- **Constraints**: what must be kept, what must be avoided, tools or versions involved
- **Examples**: a sample of good output, if the user has one
- **Done means**: how the user will judge whether the result is right

## Step 5: Write the prompt

Principles, with the reason behind each so you can judge when they apply:

- **Say the task first and plainly.** A model handed a wall of background before the request tends to latch onto the wrong part.
- **Explain why, not just what.** "Keep it under 200 words because it goes on a slide" lets the model make sensible trade-offs. A bare rule gets followed rigidly or ignored.
- **Describe what you want instead of what you do not want.** "Write in flowing paragraphs" works better than "no bullet points", because negative instructions name the thing you are trying to avoid.
- **Be specific where it matters and silent where it does not.** Every instruction costs attention and tokens. Cut anything a capable model would do anyway.
- **Separate instructions from material.** Wrap long inputs in labelled tags such as `<draft>` or `<error_log>` so the model can tell what to act on and what to read. Put long material before the final question.
- **Show an example when format matters.** One real example beats a paragraph describing the format. Say it is an illustration so the model does not copy its content.
- **Give a role only when it changes the output.** "Review this as a senior security engineer" sets a standard. "You are a helpful assistant" adds nothing.
- **Leave room to think on hard tasks.** For analysis, planning, or debugging, ask the model to reason through the problem before giving its answer.
- **Write calmly.** Capital letters and repeated warnings make models over-apply a rule. A clear sentence with its reason is enough.
- **Mark variables.** Anything the user will change each time goes in `{{double_braces}}` so the prompt is reusable.

Match length to the task. A one-off question needs a few sentences. An agent brief or system prompt can run to several sections. Do not pad a simple request into a template.

## Notes by kind of work

Use the section that fits. For anything not listed, the ingredients in Step 4 are enough.

### Coding

**Confirm the stack before writing anything.** A coding prompt with the wrong language, framework, or version produces code the user cannot use.

- If the stack is stated, or visible in project files the user shared, use it and say which one you are using.
- If a default stack is set, offer it only if it suits this project, and get a yes.
- Otherwise ask: language, framework, key libraries, target platform (web, desktop, mobile, a specific device), and versions where they matter.
- If the user has not decided, search for what fits the task and their constraints, propose one stack with a one-line reason, and wait for a yes.

Then build the prompt:

- State the goal and the definition of done: tests pass, it builds, it matches a spec.
- Name the confirmed stack and versions, and the files or modules involved.
- Say what must not change (public APIs, file layout, dependencies).
- For a bug, include the exact error, what was expected, what happened, and what has been tried.
- Say how to verify the work and what to do when blocked: stop and ask, or note the assumption and continue.

### Multi-agent projects

When several agents will work on one project, the deliverable is a pack: a leader prompt, a brief for each worker, a review prompt, and a shared notes file.

**1. Confirm the setup** (in the Step 1 question round):

- **Orchestration tool**: which one runs the agents (Orca, for example)? Read its documentation before writing: how a leader and workers are defined, how tasks are handed off, where shared files live, and what format its configuration takes. Write the pack in the format that tool expects.
- **Available agents**: which can the user run? Claude, Gemini, ChatGPT, others, and at which tier or plan. Only assign agents the user has. For Gemini, use the Gemini 4 line-up listed in Step 2.
- **Limits**: any usage caps or budget to stay inside.

**2. Give each task the right-sized model.** Using the strongest model for everything wastes tokens, and using the cheapest for everything wastes time on rework. Look up the user's available models and their current prices rather than assuming, then assign along these lines:

| Kind of task | Model to use |
|---|---|
| Planning, architecture, hard debugging, final review | The strongest model available |
| Building a feature from a clear spec | A mid-tier model |
| Running tests, formatting, renaming, boilerplate, scanning logs | The smallest, cheapest model |
| Reading a whole codebase or long documents | A model with a large context window and low input cost |
| Prose: docs, stories, reports | The model whose writing the user prefers |

For Gemini agents this maps to Carbon for the first row, Neon for building from a spec, and Hydrogen for the routine row and for high-volume subtasks.

Show the assignment as a short table (agent, model, role) and get a yes before writing the pack.

**3. Look for tools and MCP servers** the agents would benefit from (Step 3), and ask before including any.

**4. Write the pack:**

- **Leader prompt.** The leader plans and coordinates and should do little of the work itself. Include:
  - The goal and the definition of done for the whole project
  - The roster: each agent, its model, and its role
  - The task breakdown: order, dependencies, and what can run in parallel
  - Handoff rules: what each worker receives and what it must return
  - The shared notes file and what gets recorded there
  - When to stop and ask the user
  - How the finished work gets verified
- **Worker briefs**, one per agent, each self-contained: role, scope, inputs, definition of done, what not to touch, and the report format.
- **Review prompt** for an agent that did not build the work, checking it against the definition of done.
- **Shared notes file** template: decisions made, interfaces between parts, status, open questions.

**5. Build token efficiency into the leader prompt.** Tell the leader to:

- Hand each worker a small self-contained brief, not the whole conversation
- Pass file paths, not file contents
- Ask workers for short reports: what changed, what was verified, what is open
- Put shared context in the notes file once instead of repeating it in every brief
- Do trivial tasks itself rather than spawning an agent for them
- Cap retries on a failing task (two is a sensible limit), then stop and report
- Not redo or re-read work a worker has already verified

### Writing (stories, essays, papers, emails, posts)

**When the writing should sound like the user, get a sample first.** Adjectives like "natural" or "casual" do not transfer a voice. A real sample does.

People write differently in different kinds of writing, so a profile only applies to the kind it came from. A story profile says nothing about how someone writes a scientific paper. Check the saved profiles for one of the same kind. If there is one, offer it. If not, make a new one.

1. **Get a sample of the same kind.** Existing writing of that kind is best. If there is none, set a short writing test that matches the piece, in the language the final piece will use:

   | Kind of writing | Test (about 150 to 250 words) | Look especially at |
   |---|---|---|
   | Story, fiction | A short scene: two people meet somewhere, with a line or two of dialogue, in the point of view and tense planned for the story | Balance of dialogue and narration, sensory detail, pacing, how close the narration sits to the character, how feelings are shown |
   | Scientific paper, lab report | A paragraph explaining a method or result the user knows well, in the register the paper needs | Active or passive voice, how results and uncertainty are stated, terminology, sentence density, tense for method and for results, how figures are referred to |
   | Essay, opinion | A paragraph arguing a view on a familiar topic | How claims are built and supported, transitions, how strong the stance is |
   | Email, message | A short message to the kind of person who will receive it | Greeting and sign-off, directness, politeness level |
   | Blog or social post | A short post about something recent | Hook, humour, formatting habits, length |

   Ask the user to write it quickly, without polishing and without AI help, because the unpolished version shows their real habits.

2. **Analyse the sample.** Across all kinds, look at sentence length and rhythm, word choice and formality, punctuation and paragraph habits, how they open and close, tone, and quirks worth keeping, including small imperfections that make it sound like them. Add the points from the table for that kind.
3. **Show the user the profile in a few lines** and let them correct it.
4. **Put both in the prompt**: the profile as instructions, and an excerpt of the sample inside `<writing_sample>` tags with a note to match its voice and not reuse its content.
5. **Offer to save the profile** under My defaults, labelled with its kind.

Skip the test when the user has already given a sample of that kind, when they decline, or when the writing is not meant to be in their voice.

Also cover:

- The reader and what they should think, feel, or do afterwards.
- Length, point of view, tense, and language.
- For fiction: the characters, setting, what has happened so far, and what this scene needs to accomplish. Say whether the model should draft, continue, or only give feedback.
- For editing: how heavy a hand to use, from fixing errors only to rewriting freely.

### Reports and academic work

- Give the assignment or brief, the course or audience level, and the required structure or template (for example a LaTeX class or section list).
- Provide the actual data, results, and sources. Tell the model to work only from what is supplied and to mark gaps instead of inventing numbers or citations.
- Specify citation style, units, significant figures, and language.
- Say which part is wanted: outline, a single section, a full draft, or a review of an existing draft.
- If the report should read like the user wrote it, use the writing steps above with the scientific test.
- If the work is graded, ask for feedback or drafts the user will revise, and follow the course's rules on AI use.

### Art and visuals (image, video, 3D, pixel art)

- Check Step 3 first. Specialised tools matter most here: pixel art, sprites, vector logos, 3D models, and video each have tools that beat a general image generator.
- Image and video generators read descriptions, not instructions. Describe the result as if it already exists.
- Cover, roughly in this order: subject, setting, composition and framing, lighting, style or medium, colour palette, mood.
- For video, add the camera movement, what happens over the shot, and its duration.
- For 3D, add the intended use (game asset, render, print), level of detail, and pose.
- For pixel art, add the canvas size, palette limits, the view (side, top-down, isometric), the list of animations and frame counts, and the reference image.
- Include aspect ratio or size if the tool accepts it.
- Describe a style by its qualities (flat colour, thick outlines, soft grain) rather than naming a living artist. Do not ask for a real person's likeness or a copyrighted character, and use only reference images the user owns or is licensed to use.
- Offer two or three variations when the user is exploring a look.

### Research and analysis

- State the question and what decision the answer feeds into.
- Set the scope: time period, region, sources to prefer or exclude.
- Ask for sources to be cited and for uncertain claims to be marked as uncertain.
- Specify the output: a short answer, a comparison table, or a full write-up.

### Study and learning

- Give the subject, the user's current level, and what they are preparing for.
- Say what kind of help is wanted: explanation, worked examples, practice questions, or a quiz.
- Ask the model to check understanding step by step rather than deliver everything at once.

### System prompts (bots, apps, custom assistants)

- Describe the situation the assistant is in, who it talks to, what it should do, and how it should sound.
- Cover the awkward cases: off-topic requests, missing information, and things it should hand off.
- Write it as a briefing to a capable colleague, in prose, rather than a list of rules.

## Step 6: Check it, and test it within a budget

**Read-through (always, costs almost nothing).** Read the prompt as if you were the receiving model with no other context:

- Could you do the task from this alone?
- Is there any instruction you would have to guess the meaning of?
- Does anything contradict anything else?
- Does it use the chosen tool and model the way their own documentation describes?
- Is there a sentence that would not change the output if deleted? Delete it.

**Test run (sometimes).** Running the prompt catches problems a read-through misses, but it costs tokens, so keep it small:

- Test only when the prompt is for a text model and the expected output is short, roughly a page or less.
- For a prompt that would produce something long, test a slice: ask for the outline or the first section only.
- Run at most one test and make at most one round of fixes. If it still looks off after that, tell the user what you saw instead of looping.
- Do not test-run coding agent briefs, multi-agent packs, or image, video, and 3D prompts. Those are too expensive or cannot be run here, so the read-through is the check.
- Skip the test for simple prompts of a few sentences.

Say in one line whether the prompt was tested. If the user asks for more testing or none, do that.

## Output format

Give each prompt in its own fenced code block so it copies cleanly, written in the language the receiving model should work in (the default output language if set and suitable, otherwise the language the user wrote in). When there are several prompts, put a one-line label above each saying what it is for and when to use it.

After the prompts, add only what helps, in a few short lines:

- **Use with**: the model or tool the prompt is written for, with a link and any install step
- **Fill in**: any placeholders the user needs to replace
- **Assumed**: choices you made that they may want to change
- **Tested**: whether it was test-run, and what was fixed
- **To adjust**: one or two things to tweak if the first result is off

Skip any of these that are empty. Do not explain prompt-writing theory unless asked.

## Improving an existing prompt

When the user brings a prompt that is not working:

1. Ask what went wrong with the output, or look at the output if they shared it. The symptom points to the fix: generic results mean missing context, wrong format means the format was never specified or shown, ignored instructions usually mean a conflict or burial under other text. Sometimes the fix is a different tool or model, so revisit Steps 2 and 3 if either looks like a poor fit.
2. Keep what already works. Rewrite only what the diagnosis points to, so the user can see cause and effect.
3. Return the revised prompt in a code block, then two or three lines on what changed and why.

## Examples

**Request**: "make me a prompt to get an AI to review my lab report"

```
Review the lab report below as a teaching assistant grading a second-year engineering lab course would. I want to fix problems before I submit, so focus on what would cost marks.

Check these in order:
1. Whether the conclusions follow from the data shown
2. Errors in calculations, units, or significant figures
3. Missing or weak sections (method detail, error analysis, discussion)
4. Unclear or informal wording

For each problem, quote the sentence or name the figure, say what is wrong, and suggest a fix. Finish with the three changes that would improve the report most. Do not rewrite the report for me.

<report>
{{paste report here}}
</report>
```

**Fill in**: the report text.
**Assumed**: second-year engineering level and a feedback-only review.

**Request**: "prompt for a walking knight sprite for my game"

Known pick: Codixel. Ask for the reference image and canvas size if not given, then:

```
Make a pixel art knight sprite for a side-scrolling game, using the attached reference image for the design.

Canvas: 32x32 pixels per frame, transparent background, side view facing right.
Palette: at most 16 colours, cool steel greys for the armour with one red accent for the plume.
Style: clean 1-pixel dark outline, flat shading with a single highlight, readable silhouette at 1x scale.
Animations: idle (4 frames) and walk cycle (6 frames).

Build the character from the reference first and show me the still sprite before animating. Then rig the parts that move (legs, arms, plume) and show me each animation frame by frame so I can approve it. Export a PNG sprite sheet for each animation plus a GIF preview.

Reference: {{attach reference image}}
```

**Use with**: Codixel in Claude Code (https://github.com/mankidev/codixel). Install by cloning it into `~/.claude/skills/codixel`, then restart Claude Code.
**Fill in**: the reference image.
**Assumed**: 32x32 frames and a 16-colour palette.