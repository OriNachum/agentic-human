---
layout: post
title: "Code as Documentation: The Role of Agent Skills"
date: 2026-02-24
tags: [agentic-ai, developer-experience]
original_url: https://medium.com/@ori.nachum_22849/code-as-documentation-the-role-of-agent-skills-1b223c9e752d
---

For a very long time we compartmentalize concepts. The kitchen, the printer room, the form request. Agent Skills work about the same.

Imagine you enter an office where everything is in a single messy room. Getting bombarded with knowledge doesn't help us. But putting function — printer, coffee machine — in their own rooms, puts order. It instructs us where to find them and when it is relevant.

Do you need a coffee? It's in the kitchen, but the instructions for the brewing machine only open when you press a button. Want to print something? Sure, it's that way — the room has all the instructions you need, or the printer guides you step by step. Need to fill a form? Only after requesting it, you discover the details.

That is how documentation should work. But it doesn't. Documentation fails to bridge a user to the reality of their workspace.

README only gets you so far — too long and you get lost in reading, too short and it's ineffective.

Even if you keep "Documentation as Code", docs folder can be left stale, have errors, and when you execute its instructions, corrections are done on the fly and not always return to the source doc.

## What You Don't Know You Don't Know

When you land on a new folder or code repository with tens or hundreds of files, you may look for a README file and a docs folder to start making sense of it all.

Perhaps I am naive, and you'll just throw everything to NotebookLM, because who has the time to dive? But it's just not helpful when you really do need to dive in, or at least know how to guide your agent.

It's really hard to know what you don't know. Docs could be confusing (Setup AND Configuration??), deep (Each tab, is actually a guide with pages?), and AI may condense too much or skip what you really want to know altogether — RAG is not a solved problem.

## Agent Skills Are the Fix

What if you had pathways in your folder that would describe exactly how to add new articles, or classes? You need a new service? Easy — here is a recipe!

These pathways have a use case — an explanation of when it is relevant — and hold more instructions when you want to use them, little scripts that would do some actions for you, and resources for that script to reference.

Meet: Agent Skills.

A skill is just a folder with a small label file and a toolbox of scripts and references.

The agent generally knows what is possible — only when it needs it, the door is opened and the context is filled with all relevant knowledge.

For a very long time we compartmentalize concepts. The kitchen, the printer room, the form request. Agent Skills work about the same.

## Code as Documentation

Writing agent skills — Code — act as live explanations that are executable, testable, and easily fixable.

They bring you from your question to your answer, and reduce cognitive load — both for you and for your faithful agent.

As they create new content, they reduce tokens by sparing the need to write their output.

Something broke? You can read and fix them — better yet, your agent can! Since they are tied to your code, you can tell exactly when they broke and why.

You will notice it right away, because they are the workflow that makes your workspace tick — Agent Skills are the convenient buttons that do what you would and should do in your workspace.

After all, documentation that is also code can't silently rot. It either works or it doesn't.

Agent skills dictate the things that one would and should do in that repo, thus acting as a guide to that repository.

They let you lock the agent's randomness in the strict flow of code, and keep their context small. That applies to humans too. We work better with small, relevant context than with a 40-page wiki.

When we finally move to an environment full of agents and humans working in tandem, how else would you prepare for that chaos in our workspaces and codebases?

Let me know in the comments what Agent Skills mean for you!
