---
layout: post
title: "Everything is Agents, agentic-folders approach"
date: 2025-12-10
original_url: https://medium.com/@ori.nachum_22849/everything-is-agents-agentic-folders-approach-31670e6555eb
---

Some time ago, I presented Workbench Development approach, where every task that should happen often is defined by an agent.

Owning team defines, using team uses (Directly, or by an agentic IDE).

This was external — let's talk internal.

## Everything is Agents

Agentic-folders mean you implant AGENT.md in key folders in code instead of putting all documentation in your docs folder.

Hint: you can do that to other systems, like your Google Drive.

First, you place a template file and rule file in your agentic IDE.

Then you request your agentic IDE:

> For each of the following folders, add AGENT.md file with instructions for any agent to understand the folder.
> First, design AGENT-template.md and save to docs/AGENT-template.md
> Then, use it as reference to create any new AGENT.md file.
> Make that template fitting our project.

The goal is to help the model or human to understand context: How to add new code, how to read it, what other files is this folder connected to, any injections and where they are injected, and any other guidelines to help maintain this folder.

The instructions need to be folder specific - anything global is still going to docs folder.

This assumes you want the AGENT.md on key folders you provide.

Find them with Gemini 3 Pro High (Currently) or manually.

Then you request your agentic IDE for documentation cleanup.

> Review all documentation and detect duplicates.
> Any documentation added to an AGENT.md preceeds documentation anywhere else and should be removed from there.
> The goal is less documentation, for higher quality one.
> It is recommended to point AGENT.md from other documentation files

Now the documentation is much cleaner, and there are 'buckets' for extra documentation where the agentic IDE will prefer using for updating documentation.

This puts any documentation in context, so it reduces overall token read, and make sure the agent knows what's going on where, when it visits a folder.

I saw token consumption reduction of ~20% and faster and more accurate success rate, but it needs more testing.

If you liked this — please give me a star on the [autonomous-intelligence repo](https://github.com/OriNachum/autonomous-intelligence)!
