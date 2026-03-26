---
layout: post
title: "Assimilai: The Borg Paradigm for Dependency Management"
date: 2026-03-26
tags: [dependency-management, agents, assimilai, security, supply-chain]
toc: true
original_url: https://medium.com/@ori.nachum_22849/assimilai-the-borg-paradigm-for-dependency-management-b89805ebfa43
---

You don't own your dependencies. For years we got used to importing packages in a static way: find what you need, install, and reference it. The tools to manage it have changed, and today we have a strong foundation for importing code. Then came the agentic coders, and **chaos came with them.**

---

![Assimilai](/assets/images/assimilai.jpeg)

## Background

Development speed rocketed, and hallucinated packages were used by hackers to attack vibe-coded systems. The models have improved since and we give them more and more tasks. Even after agents became the main coder in the team, there is still some expectation of them to "do the human work" — that friction hinders agent efficiency.

## Proposal

Here's the next step in making agents the first-citizens in the coding environment, by capitalizing on their strengths, and simplifying their work.

**Assimilai:** instead of using the traditional importing strategy, I let the LLM read the source, and only add the relevant logic where needed.

I have been using that methodology for a while, and a huge weight lifted from that process of debugging and development. Stacktrace is smaller, changes are easier, and logic is clearer.

## Benefits

I traded the cost of code management for agent management — and the latter is far more manageable.

Error logs got smaller, easier for me to read, taking less space and sparing tokens for the agent. Reducing my cognitive load also reduces theirs.

I don't have to think of mass changes — **there are no more breaking changes in my packages.**

Programming language barriers virtually eliminated, and security risk by foreign code was removed drastically. Security and bugs are now my responsibility to mitigate, as I would with any piece of my code. The agent and I can grasp the full picture far better now.

## Agent-First

Let's solidify this concept with the agent's strongest tool: **Agent Skills.**

To help our agents remain consistent and manage that behavior, I provided a CLI: Assimilai both via pip & npm. It is agentic first, augmenting the agent with tools to note which files it assimilated in the code, and how to detect drift from the source.

With it, the agent's behavior remains consistent across packages and target solutions, while making adjustments to make both fit, whether it's a different language, a breaking change, a small piece of logic, or code that merges with existing work.

By using Assimilai directly or in scripts, agents naturally wield it.

## Strategies of Assimilation

Assimilai offers 3 ways to assimilate code:

- **Verbatim** — you just copy the file to your source code, and keep it untouched.
- **Adapted** — somewhat like verbatim, with the freedom to change the file to fit its use.
- **Dissolved** — the file is completely merged into an existing file.

These three strategies give the flexibility needed when assimilating packages.

## Caveats

There are some important caveats to note.

I still use the old way for packages — I respect closed source and usage policy. Also, I track the sources I use in pyproject.toml, so I know which files I pulled at what version. It lets me credit the package source and apply changes only when relevant.

## Final Words

This is a time when major processes change. We automate, we dare, we completely change what was previously taken for granted.

How do you make your environment more agent-friendly? Consider how you make your coding strategies modern, fitting for your agentic first-citizens.

**Don't import, assimilate.**
